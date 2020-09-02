---
title: 自訂CIF核心元件
description: 瞭解如何自訂AEM CIF核心元件。 本教學課程涵蓋如何安全地擴充CIF核心元件，以符合商業特定需求。 瞭解如何擴充GraphQL查詢以傳回自訂屬性，並在CIF核心元件中顯示新屬性。
sub-product: 商務
topics: development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
kt: 4279
thumbnail: 4279-customize-cif.jpg
translation-type: tm+mt
source-git-commit: 34b4dc697d3fb8c3f81e16ee3cab5d768e42b99c
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 0%

---


# 自訂AEM CIF核心元件 {#customize-cif-components}

CIF Venia Project [(](https://github.com/adobe/aem-cif-guides-venia) CIF Venia Project [)是使用](https://github.com/adobe/aem-core-cif-components)CIF Core Components的參考代碼庫。 在本教學課程中，您將進一步擴充 [Product Teaser元件](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) ，以顯示Magento的自訂屬性。 您也將進一步瞭解AEM和Magento之間的GraphQL整合，以及CIF核心元件提供的擴充勾點。

>[!TIP]
>
> 啟動您 [自己的商務實作時，請使用AEM Project原型](https://github.com/adobe/aem-project-archetype) 。

## 您將建立的

Venia品牌最近開始使用可持續材料製造某些產品，而企業希望在產品摘要中顯示 **Eco Friend** badge。 Magento中將會建立新的自訂屬性，以指出產品是否使用 **Eco友好** 物料。 然後，此自訂屬性會新增為GraphQL查詢的一部分，並顯示在指定產品的產品摘要中。

![環保徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 必備條件 {#prerequisites}

完成本教學課程時，需要有本機開發環境。 這包括已設定並連線至Magento例項的AEM執行個體。 檢閱使用AEM做為雲 [端服務SDK設定本機開發的需求和步驟](../develop.md)。 要完全遵循本教學課程，您需要權限才能在Magento中 [將「屬性](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) 」新增至「產品」。

您還需要GraphQL IDE(如 [GraphQL](https://github.com/graphql/graphiql) )或瀏覽器擴充功能來運行代碼示例和教程。 如果您安裝瀏覽器擴充功能，請確定它能夠設定請求標題。 在Google Chrome上， [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) 是可執行工作的擴充功能。

## 複製Venia專案 {#clone-venia-project}

我們將仿製 [Venia Project](https://github.com/adobe/aem-cif-guides-venia) ，然後覆寫預設樣式。

>[!NOTE]
>
> **您可以隨意使用現有的專案** （根據包含CIF的AEM Project Archetype），並略過本節。

1. 執行下列git命令以複製專案：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 建立專案並部署至AEM的本機例項：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 新增必要的OSGi設定，將您的AEM例項連接至Magento例項，或將設定新增至新建立的專案。

1. 此時，您應該有連接到Magento實例的店面的工作版本。 導覽至 `US` >頁 `Home` 面： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   您應該會看到，店面目前使用的是Venia主題。 展開店面的「Main Menu（主菜單）」時，您應該會看到各種類別，指出Magento連線正在運作。

   ![使用Venia Theme配置的店面](../assets/customize-cif-components/venia-store-configured.png)

## 製作產品摘要 {#author-product-teaser}

本教學課程將擴充產品摘要元件。 首先，將「產品摘要」的新例項新增至首頁，以瞭解基準功能。

1. 導覽至 **網站的首頁** : [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 將新的產 **** 品摘要元件插入頁面的主版面容器。

   ![插入產品摘要](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展開「側面板」（如果尚未切換），並將資產搜尋器下拉式清單切換至「產 **品」**。 這應該會顯示已連接Magento實例的可用產品清單。 選取產品 **並拖放** ，到頁面 **上的Product Teaser** 元件上。

   ![拖放產品摘要](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 請注意，您也可以使用對話方塊（按一下扳手圖示）設定元件，以設 *定顯示* 的產品。

4. 您現在應該會看到產品摘要正在顯示產品。 產品名稱和產品價格是顯示的預設屬性。

   ![產品摘要——預設樣式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Magento中新增自訂屬性 {#add-custom-attribute}

AEM中顯示的產品和產品資料會儲存在Magento中。 接著，使用Magento UI新增 **Eco Friendly** 屬性，作為產品屬性集的一部分。

>[!TIP]
>
> 已有自訂 **「是／否** 」屬性做為產品屬性集的一部分？ 您可隨意使用，並略過本節。

1. 登入您的Magento實例。
1. 導覽至「 **目錄** >產 **品」**。
1. 更新搜尋篩選器，以尋找在上 **** 一練習中新增至Teaser元件時使用的「可設定產品」。 在編輯模式中開啟產品。

   ![搜尋Valeria產品](../assets/customize-cif-components/search-valeria-product.png)

1. 在產品檢視中，按一下「 **新增屬性** > **建立新屬性」**。
1. 使用下列值 **填寫「新增屬性** 」表單（保留其他值的預設設定）

   | 欄位集 | 欄位標籤 | 值 |
   |-----------|-------------|---------|
   | 屬性屬性 | 屬性標籤 | **環保** |
   | 屬性屬性 | 目錄輸入類型 | **是／否** |
   | 進階屬性屬性 | 屬性代碼 | **eco_friendly** |

   ![新屬性表單](../assets/customize-cif-components/attribute-new-form.png)

   完成 **時，按一下** 「儲存屬性」。

1. 捲動至產品底部，並展開「屬 **性** 」標題。 您應該會看到新的 **Eco Friendly欄位** 。 將切換切換為 **是**。

   ![切換為yes](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **儲存** 對產品的變更。

   >[!TIP]
   >
   > 有關管理產品屬 [性的更多詳細資訊，請參閱Magento使用手冊](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)。

1. 導覽至「 **系統** >工具 **>快** 取管理 ****」。 由於對資料模式進行了更新，因此我們需要使Magento中的某些快取類型失效。
1. 選中「配置」旁邊的 **框** ，並提交快取類型以刷新 **。**

   ![刷新配置快取類型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > 有關「快取管 [理」的詳細資訊，請參閱Magento使用手冊](https://docs.magento.com/user-guide/system/cache-management.html)。

## 使用GraphQL IDE驗證屬性 {#use-graphql-ide}

在跳至AEM程式碼之前，使用GraphQL IDE來探 [索Magento GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) 非常實用。 與AEM的Magento整合主要是透過一連串的GraphQL查詢完成。 瞭解和修改GraphQL查詢是擴展CIF核心元件的關鍵方法之一。

接下來，使用GraphQL IDE驗證屬性 `eco_friendly` 是否已添加到產品屬性集。 本教學課程中的螢幕擷取畫面是使 [用Altair GraphQL用戶端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)。

1. 開啟GraphQL IDE，並在IDE或擴展 `http://<magento-server>/graphql` 名的URL欄中輸入URL。
2. 新增下 [列產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) ，其中 `YOUR_SKU` 是上一練習中使 **用之產品的SKU** :

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

3. 執行查詢，您應得到如下響應：

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

   ![GraphQL響應示例](../assets/customize-cif-components/sample-graphql-query.png)

   請注意，「是」 **的值** 是1的整 **數**。 當我們使用Java編寫GraphQL查詢時，這將非常有用。

   >[!TIP]
   >
   > 有關 [Magento GraphQL的更詳細文檔可在此處找到](https://devdocs.magento.com/guides/v2.4/graphql/index.html)。

## 更新Product Teaser的Sling Model {#updating-sling-model-product-teaser}

接下來，我們將透過實作Sling Model來擴充Product Teaser的商業邏輯。 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)，是註解導向的&quot;POJOs&quot;(Plain Old Java Objects)，可實作元件所需的任何商業邏輯。 Sling Models會與HTL指令碼搭配使用，做為元件的一部分。 我們將遵循Sling Models [的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) ，以便我們只擴充現有產品摘要模型的部分。

Sling Models是以Java形式實作，可在產生的專 **案的** core模組中找到。

使 [用您選擇的IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) ，匯入Venia專案。 使用的螢幕擷取畫面來自 [Visual Studio程式碼IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 在IDE中，導航至核心模 **塊下** ，以： `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是可擴充CIF產品摘要介面的Java [介面](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 。

   已經新增了命名為的新方 `isShowBadge()` 法，以在產品被視為「新」時顯示徽章。

1. 將新方法添 `isEcoFriendly()` 加到介面：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   這是我們將引入的一種新方法，用來封裝邏輯，以指出產品的屬性 `eco_friendly` 是設為 **Yes** 或 **No**。

1. 接下來，檢查 `MyProductTeaserImpl.java` 位置 `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`。

   Sling Models [的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) , `MyProductTeaserImpl` 可讓您透過屬 `ProductTeaser` 性參考 `sling:resourceSuperType` 模型：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   對於我們不想覆寫或變更的所有方法，我們只要傳回傳回的值即可 `ProductTeaser` 。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   這可將實作所需的Java程式碼量減到最小。

1. AEM CIF核心元件提供的額外擴充點之一，就是 `AbstractProductRetriever` 提供特定產品屬性的存取。 檢查方 `initModel()` 法：

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

   注 `@PostConstruct` 釋可確保在Sling Model初始化時，會立即呼叫此方法。

   請注意，產品GraphQL查詢已使用檢索附加屬 `extendProductQueryWith` 性的方法進行擴 `created_at` 展。 此屬性稍後會用作方法的一 `isShowBadge()` 部分。

1. 更新GraphQL查詢，將屬 `eco_friendly` 性包含在部分查詢中：

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

   添加到該方 `extendProductQueryWith` 法是確保模型其餘部分可以使用附加產品屬性的有力方法。 它還將執行的查詢數減到最小。

   在上述代碼中`addCustomSimpleField` ，將用於檢索屬 `eco_friendly` 性。 這說明了如何查詢屬於Magento架構一部分的任何自定義屬性。

   >[!NOTE]
   >
   > 實際 `createdAt()` 上，該方法已作為產品介面的一 [部分實現](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)。 大部分常見的架構屬性都已實作，因此只使用真正 `addCustomSimpleField` 的自訂屬性。

1. 新增記錄器以協助除錯Java程式碼：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 接著，實作方 `isEcoFriendly()` 法：

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

   在上述方法中， `productRetriever` 用於讀取產品，並 `getAsInteger()` 用於獲取屬性的值 `eco_friendly` 。 根據我們先前運行的GraphQL查詢，我們知道當屬性設 `eco_friendly` 置為&quot;**Yes**&quot;時，預期值實際上是 **1的整數**。

   現在Sling Model已更新，Component標籤需要更新，才能實際顯示以Sling Model為基礎的 **Eco Friendly** 指示符。

## 自訂產品摘要的標籤 {#customize-markup-product-teaser}

AEM元件的常見擴充功能是修改元件產生的標籤。 這是透過覆寫元件用 [來轉換其標籤的HTL](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html) 指令碼來完成的。 HTML範本語言(HTL)是輕量型範本語言，AEM元件會使用它來根據撰寫的內容動態轉換標籤，讓元件可重複使用。 例如，「產品摘要」可重複使用，以顯示不同的產品。

在我們的案例中，我們想要在摘要上方呈現橫幅，以指出產品是以自訂屬性為基礎的「環保」。 自訂元件標 [記的設計模式](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) ，實際上是所有AEM元件（而不只是AEM CIF核心元件）的標準。

1. 在IDE中，導航並展開模 `ui.apps` 塊，然後將資料夾層次展開為： `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` 並檢查檔 `.content.xml` 案。

   ![產品摘要ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   以上是我們專案中產品摘要元件的元件定義。 請注意屬性 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`。 這是建立 [Proxy元件的示例](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)。 我們不需從AEM CIF核心元件複製和貼上所有產品摘要HTL指令碼，而是可 `sling:resourceSuperType` 以使用繼承所有功能。

1. 開啟檔案 `productteaser.html`。 這是來自 `productteaser.html`[CIF Product Teaser的檔案副本](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
       data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
       data-sly-use.actionsTpl="actions.html"
       data-sly-test.isConfigured="${properties.selection}"
       data-sly-test.hasProduct="${product.url}">
   ```

   請注意，Sling Model for `MyProductTeaser` 已使用並指派給變 `product` 數。

1. 修 `productteaser.html` 改以調用前一練 `isEcoFriendly` 習中實現的方法：

   ```html
   ...
   <div data-sly-test="${isConfigured && hasProduct}" class="item__root" data-cmp-is="productteaser" data-virtual="${product.virtualProduct}">
       <div data-sly-test="${product.showBadge}" class="item__badge">
           <span>${properties.text || 'New'}</span>
       </div>
       <!--/* Insert call to Eco Friendly here */-->
       <div data-sly-test="${product.ecoFriendly}" class="item__eco">
           <span>Eco Friendly</span>
       </div>
   ...
   ```

   在HTL中呼叫Sling Model方法時， `get` 會捨 `is` 棄該方法的和部分，並將第一個字母小寫。 所以 `isShowBadge()` 它變 `.showBadge` 得 `isEcoFriendly` 越來越 `.ecoFriendly`好 根據從返回的布爾值確 `.isEcoFriendly()` 定是否顯 `<span>Eco Friendly</span>` 示。

   有關其他 `data-sly-test` HTL區塊陳 [述式的詳細資訊，請參閱這裡](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test)。

1. 使用您的Maven技能，從命令列終端機儲存變更並部署更新至AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 開啟新的瀏覽器視窗並導覽至AEM和 **OSGi主控台** > **狀態** > **Sling Models**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜尋時， `MyProductTeaserImpl` 您應會看到如下所示的行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   這表示Sling Model已正確部署並對應至正確的元件。

1. 重新整理 **至Venia首頁**[](http://localhost:4502/editor.html/content/venia/us/en.html) http://localhost:4502/editor.html/content/venia/us/en.html，其中已新增產品摘要。

   ![顯示Eco友好消息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果產品的屬 `eco_friendly` 性設為「 **是**」，您應該會在頁面上看到「Eco Friendly」文字。 嘗試切換至不同的產品，以檢視行為變更。

1. 接著開啟AEM以 `error.log` 查看我們新增的log陳述式。 位 `error.log` 於 `<AEM SDK Install Location>/crx-quickstart/logs/error.log`。

   搜尋AEM記錄檔，以查看Sling Model中新增的log陳述式：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > 如果摘要中使用的產品沒有屬性作為屬性集的一部分，您也 `eco_friendly` 會看到一些堆棧跟蹤。

## 新增Eco Friendly徽章的樣式 {#add-styles}

此時，顯示 **Eco Friendly** badge的邏輯正在運作，但純文字可能會使用某些樣式。 接著，將圖示和樣式新增至模 `ui.frontend` 組以完成實作。

1. 下載 [eco_friendly.svg檔案](../assets/customize-cif-components/eco_friendly.svg) 。 此徽章將用作環保 **徽章** 。
1. 返回IDE並導航到該文 `ui.frontend` 件夾。
1. 將檔案 `eco_friendly.svg` 添加到檔案 `ui.frontend/src/main/resources/images` 夾：

   ![新增環保SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 在中開啟 `productteaser.scss` 檔案 `ui.frontend/src/main/styles/commerce/_productteaser.scss`。
1. 在類內添加以下Sass規 `.productteaser` 則：

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
   > 如需前 [端工作流程的詳細資訊](./style-cif-component.md) ，請參閱Styling CIF Core Components。

1. 使用您的Maven技能，從命令列終端機儲存變更並部署更新至AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 重新整理 **至Venia首頁**[](http://localhost:4502/editor.html/content/venia/us/en.html) http://localhost:4502/editor.html/content/venia/us/en.html，其中已新增產品摘要。

   ![環保徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 恭喜 {#congratulations}

您剛自訂了第一個AEM CIF元件！ 請在這裡下 [載完成的解決方案檔案](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)。

## 獎金挑戰 {#bonus-challenge}

檢閱「產品摘 **要** 」中已實作的新標章功能。 嘗試新增其他核取方塊，讓作者控制何時應顯 **示Eco Friendly** badge。 您需要在中更新元件對話框 `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`。

![全新徽章實作挑戰](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他資源 {#additional-resources}

* [AEM Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)
* [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)
* [自訂AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [自訂核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
* [AEM Sites快速入門](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)