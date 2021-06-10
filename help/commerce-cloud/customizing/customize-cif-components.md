---
title: 自訂CIF核心元件
description: 了解如何自訂AEM CIF核心元件。 本教學課程說明如何安全地擴充CIF核心元件，以符合業務特定需求。 了解如何延伸GraphQL查詢，以傳回自訂屬性，並在CIF核心元件中顯示新屬性。
sub-product: 商務
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: 商務整合架構
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 4933fc37-5890-47f5-aa09-425c999f0c91
source-git-commit: 73822fb3b74472d48a3db59267ed133fc1a40ad6
workflow-type: tm+mt
source-wordcount: '2582'
ht-degree: 1%

---

# 自訂AEM CIF核心元件{#customize-cif-components}

[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)是使用[CIF核心元件](https://github.com/adobe/aem-core-cif-components)的參考代碼基。 在本教學課程中，您將進一步擴充[Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser)元件，以顯示來自Magento的自訂屬性。 您也將進一步了解AEM與Magento之間的GraphQL整合，以及CIF核心元件提供的擴充功能鈎點。

>[!TIP]
>
> 開始您自己的商務實作時，請使用[AEM專案原型](https://github.com/adobe/aem-project-archetype)。

## 您要建置的

Venia品牌最近開始使用可持續材料生產某些產品，而企業想要在產品預告中顯示&#x200B;**Eco Friendly**&#x200B;徽章。 將在Magento中建立新的自定義屬性，以指明產品是否使用&#x200B;**Eco friendly**&#x200B;材料。 然後，此自訂屬性將會新增為GraphQL查詢的一部分，並顯示在指定產品的產品預告上。

![Eco友好徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 必備條件 {#prerequisites}

完成本教學課程需要本機開發環境。 這包括已設定並連線至AEM執行個體的執行中執行個體。 檢閱[使用AEM作為Cloud ServiceSDK](../develop.md)設定本機開發的需求和步驟。 若要完整遵循本教學課程，您需要權限，才能將[屬性新增至Magento中的Product](https://docs.magento.com/user-guide/catalog/product-attributes-add.html)。

您還需要GraphQL IDE（如[GraphiQL](https://github.com/graphql/graphiql)）或瀏覽器擴展，才能運行代碼示例和教程。 如果您安裝瀏覽器擴充功能，請確定它能設定要求標題。 在Google Chrome上，[Altair GraphQL用戶端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)是可執行此作業的擴充功能。

## 克隆Venia項目{#clone-venia-project}

我們將複製[Venia Project](https://github.com/adobe/aem-cif-guides-venia)，然後覆寫預設樣式。

>[!NOTE]
>
> **歡迎使用現有專案** (根據包含CIF的AEM專案原型)，並略過本節。

1. 執行下列git命令以複製專案：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 建立專案並部署至AEM的本機執行個體：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 新增必要的OSGi設定，將您的AEM例項連線至Magento例項，或將設定新增至新建立的專案。

1. 此時，您應該有連接至Magento例項的店面工作版本。 導覽至`US` > `Home`頁面，網址為：[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您應該會看到店面目前使用Venia主題。 展開店面的「主菜單」時，您應該會看到各種類別，表明連接Magento正在工作。

   ![Venia主題配置的店面](../assets/customize-cif-components/venia-store-configured.png)

## 製作產品預告{#author-product-teaser}

本教學課程將擴充產品預告元件。 首先，將產品預告的新例項新增至首頁，以了解基線功能。

1. 導覽至網站的&#x200B;**首頁**:[http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 將新的&#x200B;**產品預告**&#x200B;元件插入頁面的主版面容器中。

   ![插入Product Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展開「側面板」（如果尚未切換），然後將資產尋找器下拉式清單切換為&#x200B;**Products**。 這應會顯示連線Magento例項的可用產品清單。 選取產品，並將&#x200B;**拖放**&#x200B;它拖放至頁面上的&#x200B;**Product Teaser**&#x200B;元件。

   ![拖放產品預告](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 請注意，您也可以使用對話方塊設定元件，以設定顯示的產品（按一下&#x200B;_扳手_&#x200B;圖示）。

4. 您現在應該會看到產品預告顯示。 產品名稱和產品價格是顯示的預設屬性。

   ![Product Teaser — 預設樣式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Magento{#add-custom-attribute}中新增自訂屬性

AEM中顯示的產品和產品資料會儲存在Magento中。 接下來，使用MagentoUI，在產品屬性集中為&#x200B;**Eco Friendly**&#x200B;添加新屬性。

>[!TIP]
>
> 已有自訂&#x200B;**Yes/No**&#x200B;屬性作為產品屬性集的一部分？ 歡迎使用，並略過本節。

1. 登入您的Magento例項。
1. 導覽至&#x200B;**Catalog** > **Products**。
1. 更新搜尋篩選器，以尋找在上一個練習中新增至Teaser元件時所使用的&#x200B;**可設定產品**。 在編輯模式中開啟產品。

   ![搜尋有效產品](../assets/customize-cif-components/search-valeria-product.png)

1. 在產品檢視中，按一下「新增屬性&#x200B;**>**&#x200B;建立新屬性&#x200B;**」。**
1. 使用下列值填寫&#x200B;**新屬性**&#x200B;表單（保留其他值的預設設定）

   | 欄位集 | 欄位標籤 | 值 |
   | ----------------------------- | ------------------ | ---------------- |
   | 屬性屬性 | 屬性標籤 | **生態友好** |
   | 屬性屬性 | 目錄輸入類型 | **是/否** |
   | 進階屬性 | 屬性代碼 | **eco_friendly** |

   ![新屬性表單](../assets/customize-cif-components/attribute-new-form.png)

   完成後，按一下&#x200B;**儲存屬性**。

1. 捲動至產品底部，然後展開&#x200B;**Attributes**&#x200B;標題。 您應該會看到新的&#x200B;**Eco Friendly**&#x200B;欄位。 將切換為&#x200B;**Yes**。

   ![切換為「是」](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **** 儲存對產品的變更。

   >[!TIP]
   >
   > 有關管理[產品屬性的更多詳細資訊，請參閱Magento使用手冊](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)。

1. 導航至&#x200B;**System** > **Tools** > **Cache Management**。 由於資料架構已更新，因此我們需要使Magento中的某些快取類型失效。
1. 勾選&#x200B;**Configuration**&#x200B;旁的方塊，並提交&#x200B;**Refresh**&#x200B;的快取類型

   ![刷新配置快取類型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > 有關[快取管理的更多詳細資訊，請參閱Magento使用手冊](https://docs.magento.com/user-guide/system/cache-management.html)。

## 使用GraphQL IDE驗證屬性{#use-graphql-ide}

跳入AEM程式碼之前，請先使用GraphQL IDE探索[MagentoGraphQL](https://devdocs.magento.com/guides/v2.4/graphql/)。 與AEM的Magento整合主要是透過一系列GraphQL查詢完成。 了解和修改GraphQL查詢是擴充CIF核心元件的關鍵方式之一。

接下來，使用GraphQL IDE驗證`eco_friendly`屬性已添加到產品屬性集中。 本教程中的螢幕截圖是使用[Altair GraphQL客戶端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)。

1. 開啟GraphQL IDE，然後在IDE或擴展的URL欄中輸入URL `http://<magento-server>/graphql`。
2. 新增下列[產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html)，其中`YOUR_SKU`是上次練習中所用產品的&#x200B;**SKU**:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. 執行查詢，您應得到如下的回應：

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![範例GraphQL回應](../assets/customize-cif-components/sample-graphql-query.png)

   請注意，值&#x200B;**Yes**&#x200B;是整數&#x200B;**1**。 以Java編寫GraphQL查詢時，此功能會相當實用。

   >[!TIP]
   >
   > 有關[MagentoGraphQL的更詳細文檔，請在此處](https://devdocs.magento.com/guides/v2.4/graphql/index.html)找到。

## 更新Product Teaser {#updating-sling-model-product-teaser}的Sling模型

接下來，我們將實作Sling模型，以擴充Product Teaser的商業邏輯。 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)是註解導向的「POJO」（純舊Java物件），可實作元件所需的任何商業邏輯。Sling模型與HTL指令碼搭配使用，是元件的一部分。 我們將遵循Sling模型](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)的[委派模式，以便只擴充部分現有產品預告模型。

Sling模型以Java方式實作，可在產生專案的&#x200B;**core**&#x200B;模組中找到。

使用您選擇的IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide)導入Venia項目。 [使用的螢幕截圖來自[Visual Studio代碼IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 在IDE中，導覽至&#x200B;**core**&#x200B;模組下方：`core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`。

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是可擴充CIF ProductTeaser介面的 [](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) Java介面。

   已新增名為`isShowBadge()`的新方法，如果產品被視為「新」，則會顯示徽章。

1. 將新方法`isEcoFriendly()`添加到介面：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   這是我們將引入的新方法，用於封裝邏輯，以指示產品的`eco_friendly`屬性是否設定為&#x200B;**Yes**&#x200B;或&#x200B;**No**。

1. 接下來，在`core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`檢查`MyProductTeaserImpl.java`。

   Sling模型](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)的[委派模式允許`MyProductTeaserImpl`透過`sling:resourceSuperType`屬性參考`ProductTeaser`模型：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   對於我們不想覆寫或變更的所有方法，我們只需傳回`ProductTeaser`傳回的值即可。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   這可將實施需要寫入的Java程式碼量降至最低。

1. AEM CIF核心元件提供的額外擴充點之一，是可存取特定產品屬性的`AbstractProductRetriever`。 Inspect `initModel()`方法：

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   `@PostConstruct`附註可確保Sling模型初始化後立即呼叫此方法。

   請注意，已使用`extendProductQueryWith`方法擴展產品GraphQL查詢，以檢索其他`created_at`屬性。 此屬性後來作為`isShowBadge()`方法的一部分使用。

1. 更新GraphQL查詢，將`eco_friendly`屬性包含在部分查詢中：

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   向`extendProductQueryWith`方法添加是一種功能強大的方法，可確保模型的其餘部分可以使用其他產品屬性。 它也會將執行的查詢數量降至最低。

   在上述程式碼中，`addCustomSimpleField`用於擷取`eco_friendly`屬性。 這說明如何查詢屬於Magento結構的任何自訂屬性。

   >[!NOTE]
   >
   > `createdAt()`方法實際上已作為[產品介面](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)的一部分實施。 最常找到的結構屬性大多已實作，因此，請僅使用`addCustomSimpleField`作為真正的自訂屬性。

1. 新增記錄器以協助偵錯Java程式碼：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 接下來，實作`isEcoFriendly()`方法：

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   在上述方法中，使用`productRetriever`來擷取產品，使用`getAsInteger()`方法來取得`eco_friendly`屬性的值。 根據我們先前執行的GraphQL查詢，我們知道當`eco_friendly`屬性設為&quot;**Yes**&quot;時，預期值實際上為&#x200B;**1**&#x200B;的整數。

   現在Sling模型已更新，需要更新元件標籤，才能根據Sling模型實際顯示&#x200B;**Eco Friendly**&#x200B;的指標。

## 自定義產品預告{#customize-markup-product-teaser}的標籤

AEM元件的常見擴充功能是修改元件產生的標籤。 若要這麼做，請覆寫元件用來呈現其標籤的[ HTL指令碼](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hant)。 HTML範本語言(HTL)是一種精簡的範本語言，AEM元件可用來根據製作的內容動態轉譯標籤，以允許重複使用元件。 例如，產品預告可反複重複使用，以顯示不同的產品。

在此情況下，我們想在預告頂端呈現橫幅，以根據自訂屬性指出產品為「生態友好」。 [自訂元件標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup)的設計模式實際上是所有AEM元件的標準，而不只是AEM CIF核心元件。

>[!NOTE]
>
> 如果您使用CIF產品和類別選擇器（例如此產品預告）或CIF頁面元件來自訂元件，請務必在元件對話方塊中加入所需的`cif.shell.picker` clientlib。 如需詳細資訊，請參閱[CIF產品與類別選擇器使用](use-cif-pickers.md) 。

1. 在IDE中，導航並展開`ui.apps`模組，然後展開資料夾層次結構以：`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser`並檢查`.content.xml`檔案。

   ![Product Teaser ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   以上是專案中產品預告元件的元件定義。 請注意屬性`sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`。 這是建立[代理元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components)的示例。 我們不必從AEM CIF核心元件複製並貼上所有Product Teaser HTL指令碼，而是可使用`sling:resourceSuperType`繼承所有功能。

1. 開啟檔案`productteaser.html`。 這是[CIF產品預告](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)中`productteaser.html`檔案的副本

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   請注意，`MyProductTeaser`的Sling模型已使用，並指派給`product`變數。

1. 修改`productteaser.html`以呼叫前一個練習中實作的`isEcoFriendly`方法：

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   在HTL中呼叫Sling Model方法時，方法的`get`和`is`部分會遭到捨棄，而第一個字母會變成小寫。 因此，`isShowBadge()`變成`.showBadge`，而`isEcoFriendly`變成`.ecoFriendly`。 根據從`.isEcoFriendly()`返回的布林值確定是否顯示`<span>Eco Friendly</span>`。

   如需`data-sly-test`和其他[ HTL區塊陳述式的詳細資訊，請參閱此處](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/block-statements.html#test)。

1. 使用Maven技能，從命令列終端儲存變更並將更新部署至AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 開啟新的瀏覽器視窗，並導覽至AEM和&#x200B;**OSGi主控台** > **Status** > **Sling模型**:[http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜尋`MyProductTeaserImpl`，您應該會看到如下所示的一行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   這表示Sling模型已正確部署並對應至正確的元件。

1. 在[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)重新整理至已新增產品預告的&#x200B;**Venia首頁**。

   ![顯示「生態友好」消息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果產品的`eco_friendly`屬性設定為&#x200B;**Yes**，您應該會在頁面上看到「Eco Friendly」文字。 嘗試切換至不同的產品，以查看行為變更。

1. 接下來開啟AEM `error.log` ，查看我們新增的記錄陳述式。 `error.log`位於`<AEM SDK Install Location>/crx-quickstart/logs/error.log`。

   搜尋AEM記錄檔，以查看Sling模型中新增的記錄陳述式：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > 如果預告中使用的產品在其屬性集中沒有`eco_friendly`屬性，您也可能會看到一些堆棧跟蹤。

## 添加生態友好徽章的樣式{#add-styles}

此時，**Eco Friendly**&#x200B;徽章顯示時機的邏輯正在運作，但純文字可能會使用某些樣式。 接下來，在`ui.frontend`模組中新增圖示和樣式以完成實作。

1. 下載[eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg)檔案。 這將用作&#x200B;**Eco Friendly**&#x200B;徽章。
1. 返回IDE並導航到`ui.frontend`資料夾。
1. 將`eco_friendly.svg`檔案添加到`ui.frontend/src/main/resources/images`資料夾：

   ![已添加Eco Friendly SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 在`ui.frontend/src/main/styles/commerce/_productteaser.scss`開啟檔案`productteaser.scss`。
1. 在`.productteaser`類別內新增下列Sass規則：

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > 如需前端工作流程的詳細資訊，請參閱[樣式CIF核心元件](./style-cif-component.md) 。

1. 使用Maven技能，從命令列終端儲存變更並將更新部署至AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 在[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)重新整理至已新增產品預告的&#x200B;**Venia首頁**。

   ![Eco友好徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 恭喜 {#congratulations}

您剛自訂了第一個AEM CIF元件！ 在此處](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)下載已完成的解決方案檔案。[

## 獎金挑戰{#bonus-challenge}

檢閱已在產品預告中實作的&#x200B;**New**&#x200B;徽章的功能。 請嘗試新增其他核取方塊，讓作者控制何時應顯示&#x200B;**Eco Friendly**&#x200B;徽章。 您需要在`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`更新元件對話方塊。

![新徽章實作挑戰](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他資源 {#additional-resources}

- [AEM原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)
- [自訂AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [自訂核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [開始使用AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
- [CIF產品和類別選擇器的使用](use-cif-pickers.md)
