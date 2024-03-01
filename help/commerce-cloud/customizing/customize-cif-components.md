---
title: 自定義 CIF 核心元件
description: 瞭解如何自定義 AEM CIF 核心元件。 該教學課程涵蓋了如何安全地擴展 CIF 核心元件以滿足特定于業務的要求。 瞭解如何擴展 GraphQL 查詢以返回自定義屬性並在 CIF 核心元件中顯示新屬性。
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 4933fc37-5890-47f5-aa09-425c999f0c91
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 0%

---

# 自定義 AEM CIF 核心元件 {#customize-cif-components}

[CIF Venia 專案](https://github.com/adobe/aem-cif-guides-venia)是使用 [CIF 核心元件](https://github.com/adobe/aem-core-cif-components)的參考代碼庫。在此教學課程中，您將進一步擴展 [產品 Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) 元件以顯示來自 Adobe Systems Commerce 的自定義屬性。 您還將了解有關 AEM 和 Adobe Systems Commerce 之間的 GraphQL 集成以及 CIF 核心元件提供的擴展鉤子的更多資訊。

>[!TIP]
>
> [在開始您自己的商務實施時，請使用 AEM 專案原型](https://github.com/adobe/aem-project-archetype)。

## 您將構建什麼

Venia 品牌最近開始使用可持續材料製造一些產品，該企業按讚展示&#x200B;****&#x200B;環保徽章作為產品預告片的一部分。Adobe Systems Commerce 中會創建一個新的自定義屬性，以指示產品是否使用了 **環保** 材料。 此自定義屬性作為 GraphQL 查詢的一部分添加，並顯示在指定產品的產品預告片上。

![環保徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 先決條件 {#prerequisites}

完成此教學課程需要當地開發環境。 此環境包括已配置並連接到Adobe Systems商務執行個體的正在運行的執行個體AEM。 查看使用 AEM 作為 Cloud Service SDK](../develop.md) 設置本地開發的要求[和步驟。要完全追隨教學課程，您需要權限在Adobe Systems Commerce中為產品](https://docs.magento.com/user-guide/catalog/product-attributes-add.html)添加[屬性。

您還需要 GraphQL IDE（如 [GraphiQL](https://github.com/graphql/graphiql) 或 瀏覽器 擴展）來運行代碼示例和教程。 如果安裝 瀏覽器 擴充功能，請確認它可以設定請求標頭。 在Google鉻黃 上， _Altair GraphQL Client_ 是一個可以完成這項工作的擴展。

## 原地複製維尼亞專案 {#clone-venia-project}

[原地複製 Venia 專案](https://github.com/adobe/aem-cif-guides-venia)，然後覆蓋預設樣式。

>[!NOTE]
>
> **免費使用現有專案** （基於包含 CIF 的 AEM 專案原型）並跳過此部分。

1. 執行以下 git 命令，以便克隆專案：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 將專案建立並部署為本機執行個體AEM：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 添加必要的 OSGi 配置，以便將AEM 執行個體連接到 Adobe Systems Commerce 執行個體，或將配置添加到創建的專案。

1. 此時，您應該具有連接到Adobe Systems商務執行個體的店面的工作版本。 導航到 `US` > `Home` 頁面位置： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您應該看到店面當前使用的是 Venia 主題。 展開店面的主功能表，您應該會看到各種類別，表明與 Adobe Systems Commerce 的連接正在工作。

   ![配置了 Venia 主題的店面](../assets/customize-cif-components/venia-store-configured.png)

## 作者產品預告片 {#author-product-teaser}

產品 Teaser 元件將延伸至此教學課程。 第一步，將產品 Teaser 執行個體添加到主页頁面以了解基線功能。

1. 導航到網站的首 **頁頁面** ： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 插入新專案 **產品Teaser** 元件放入頁面上的主版面容器中。

   ![插入產品預告片](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展開側面板（如果尚未切換），然後將資產查找器下拉式清單切換為 **產品**。 此清單應显示已連接商務執行個體的可用產品清單Adobe Systems。 選擇一個產品並將其 **拖放** 到頁面上的產品 **Teaser** 元件上。

   ![拖曳產品 Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 請注意，您還可以通過使用對話框（按兩下 _扳手_ 圖示）配置元件來配置顯示的產品。

4. 現在，您應該會看到產品 Teaser 正在顯示產品。 產品的「名稱」和產品的「價格」是顯示的預設屬性。

   ![產品Teaser — 預設樣式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Adobe Commerce中新增自訂屬性 {#add-custom-attribute}

AEM中顯示的產品和產品數據存儲在 Adobe Systems Commerce 中。 下一個使用“Adobe Systems商務”UI將“環保&#x200B;**”属性**&#x200B;添加為產品屬性集的一部分。

>[!TIP]
>
> 您的產品屬性集中已有自定義 **的「是/否** 」屬性？ 感覺免費使用它並跳過本節。

1. Log on to your Adobe Commerce instance.
1. 瀏覽至 **目錄** > **產品**.
1. 更新搜尋篩選器，以便您找到 **可設定的產品** 用於上一個練習中新增至Teaser元件時。 在編輯模式中開啟產品。

   ![搜尋Valeria產品](../assets/customize-cif-components/search-valeria-product.png)

1. 在產品檢視中，按一下 **新增屬性** > **建立新屬性**.
1. **使用以下值填寫新屬性**&#x200B;表單（保留其他值的預設設定）

   | 欄位集 | 欄位標籤 | 值 |
   | ----------------------------- | ------------------ | ---------------- |
   | 屬性屬性 | 属性加標籤 | **環保** |
   | 屬性屬性 | 目錄輸入類型 | **是/否** |
   | 進階屬性屬性 | 屬性Code | **eco_friendly** |

   ![新屬性形式](../assets/customize-cif-components/attribute-new-form.png)

   完成後儲存&#x200B;**按下**&#x200B;屬性。

1. 滾動到產品底部，然後展開 **屬性** 標題。 您應該看到新的 **環保** 欄位。 將切換開關切換為 **是**。

   ![切換切換為「是」](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   ****&#x200B;儲存對產品的更改。

   >[!TIP]
   >
   > 有關管理 [產品屬性的更多詳細資訊，請參閱Adobe Systems商務用戶 指南](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)。

1. 導航到 **「系統** > **工具** > **緩存管理**」。 由於對數據綱要進行了更新，因此您必須使 Adobe Systems Commerce 中的某些緩存類型失效。
1. 核選設定&#x200B;**旁邊的**&#x200B;方塊，並提交重新整理&#x200B;**的快取類型**

   ![重新整理設定快取類型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > 有關「快取管理」的 [更多詳情，請參閱 Adobe Systems Commerce 用戶 指南](https://docs.magento.com/user-guide/system/cache-management.html)。

## 使用 GraphQL IDE 驗證屬性 {#use-graphql-ide}

在進入AEM代碼之前，使用 GraphQL IDE 探索 [GraphQL 概述](https://devdocs.magento.com/guides/v2.4/graphql/) 很有用。 Adobe Systems Commerce 與 AEM 的集成主要通過一系列 GraphQL 查詢完成。 瞭解和修改 GraphQL 查詢是擴展 CIF 核心元件的關鍵方法之一。

下一個，請使用 GraphQL IDE `eco_friendly` 驗證該屬性是否已添加到產品屬性集中。 此教學課程中的屏幕截圖使用 _Altair GraphQL Client_ Google 鉻黃 擴展。

1. 開啟 GraphQL IDE 並在 IDE 或擴充功能的URL欄中輸入URL `http://<commerce-server>/graphql` 。
2. 新增下列[產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 上一練習中使用的產品SKU **的位置`YOUR_SKU`**：

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

3. 執行查詢，應按讚得到如下回應：

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

   ![圖QL 回應範例](../assets/customize-cif-components/sample-graphql-query.png)

   「是」的值&#x200B;**是** 1 **的**&#x200B;整數。當您使用 Java™ 編寫 GraphQL 查詢時，此值非常有用。

   >[!TIP]
   >
   > 在此處](https://devdocs.magento.com/guides/v2.4/graphql/index.html)閱讀有關Adobe Systems Commerce GraphQL 的[更詳細文檔。

## 更新產品 Teaser 的 Sling 模型 {#updating-sling-model-product-teaser}

下一個，透過實施 Sling 模型來延長「產品 Teaser」的商業邏輯。 [Sling 模型](https://sling.apache.org/documentation/bundles/models.html) 是註解驅動的“POJO”（普通的舊 Java™ 物件），用於實施 商業邏輯元件所需的內容。 Sling 模型與 HTL 腳本一起使用，作為元件的一部分。 請 [遵循 Sling 模型的委派模式，以便擴展現有產品 Teaser 模型](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 的各個部分。

Sling 模型以 Java™ 形式實現，可以在生成專案的核心模組中找到&#x200B;****。

使用您選擇的](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) IDE 匯入 [Venia 專案。使用的螢幕截圖來自 [Visual Studio Code IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 在 IDE 中，在核心&#x200B;**模組下**&#x200B;導航到： `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`。

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是擴充 CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 介面的 Java™ 介面。

   已新增 `isShowBadge()` 一個名為在產品被視為「新」時顯示徽章的新方法。

1. 新增 `isEcoFriendly()` 至介面：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   引入此新方法是為了封裝邏輯以指示產品的屬性 `eco_friendly` 是否設置為 **“是** ”或 **“否**”。

1. 下一個，檢查 `MyProductTeaserImpl.java` .`core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`

   [Sling 模型的委派模式允許`MyProductTeaserImpl`通過以下`sling:resourceSuperType`屬性引用`ProductTeaser`模型](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   對於您不想覆寫或變更的方法，您可以傳回 `ProductTeaser` 會傳回。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   This method minimizes the amount of Java™ code that an implementation must write.

1. CIF核心元件 `AbstractProductRetriever` 提供的額外擴展點之一是AEM提供對特定產品屬性的訪問。 Inspect方法：`initModel()`

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to initialize the productRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   `@PostConstruct`註解可確保在初始化 Sling 模型時調用此方法。

   請注意，產品GraphQL查詢已使用 `extendProductQueryWith` 擷取其他專案的方法 `created_at` 屬性。 此屬性稍後會用作 `isShowBadge()` 方法。

1. 更新GraphQL查詢以包含 `eco_friendly` 部分查詢中的屬性：

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   將新增至 `extendProductQueryWith` 方法是一種強大的方式，可確保模型的其餘部分都可以使用其他產品屬性。 它也會將執行的查詢數減到最少。

   在上述程式碼中，`addCustomSimpleField` 用於擷取 `eco_friendly` 屬性。 This attribute illustrates how you can query for any custom attributes that are part of the Adobe Commerce schema.

   >[!NOTE]
   >
   > 該方法`createdAt()`已作為產品介面](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)的一部分[實施。大多數常見的綱要 屬性都已實現，因此僅將 用於 `addCustomSimpleField` 真正的自定義屬性。

1. 新增記錄器，以便偵錯 Java™ 程序代碼：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 下一個，實施方法：`isEcoFriendly()`

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

   在上面的方法中，用於 `productRetriever` 獲取產品， `getAsInteger()` 該方法用於獲取屬性的值 `eco_friendly` 。 根據您之前運行的 GraphQL 查詢，您知道屬性設置為“**是”時的`eco_friendly`預期值實際上是 1** 的&#x200B;****&#x200B;整數。

   現在 Sling 模型已更新，元件標記必須更新，以實際顯示基於 Sling 模型的環保&#x200B;**指示器**。

## 自訂產品 Teaser 的標記 {#customize-markup-product-teaser}

AEM元件的常見擴展是修改元件生成的標記。 此編輯是通過覆蓋 [元件用於呈現其標記的 HTL 腳本](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 來完成的。 HTML 範本語言 （HTL） 是一種輕量級範本語言，AEM元件使用它來根據創作的內容動態呈現標記，從而允許重用元件。 例如，產品 Teaser 可以反覆使用以顯示不同的產品。

在這種情況下，您希望在Teaser頂部呈現一個橫幅，以根據自定義屬性指示產品是「環保的」。 自定義元件標記](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup)的設計[模式是所有AEM元件的標準模式，而不僅僅是AEM CIF核心元件的標準模式。

>[!NOTE]
>
> 如果使用 CIF 產品和類別選取器自定義元件，按讚此產品 Teaser 或 CIF 頁面元件，請確保為元件對話框包含所需的 `cif.shell.picker` clientlib。 有關詳細信息，請參閱 [CIF 產品的用法類別選擇器](use-cif-pickers.md) 。

1. 在 IDE 中，導航並展開模組，然後將資料夾階層展開 `ui.apps` 為： `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` ，然後檢查 `.content.xml` 檔。

   ![產品預告片 ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   上述元件定義針對您專案中的產品 Teaser 元件。 請注意屬性 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`。 此屬性是創建 [代理元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components)的示例。 您不必從AEM CIF 核心元件複製和粘貼產品預告片 HTL 腳本，而是使用 `sling:resourceSuperType` 繼承所有功能。

1. 打開檔 `productteaser.html`。 此檔案是來自 CIF 產品 Teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) 的[檔案副本`productteaser.html`。

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

   請注意，物件的 `MyProductTeaser` Sling 模型已使用並指派給 `product` 變數。

1. 修改以便 `productteaser.html` 可以呼叫 `isEcoFriendly` 在上一練習中實現的方法：

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

   在 HTL 中呼叫 Sling 模型方法時，會刪除方法的 and `is` 部分，`get`並將第一個字母變為小寫。所以`isShowBadge()`成為和`isEcoFriendly`成為`.ecoFriendly``.showBadge`.根據返回的 `.isEcoFriendly()` 布林值，確定是否 `<span>Eco Friendly</span>` 顯示 。

   `data-sly-test`有關 HTL 塊語句的更多資訊，[請參閱此處](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html)。

1. 從命令行終端使用 Maven 技能儲存更改並部署更新以AEM：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 開啟新瀏覽器視窗並導覽至 AEM 和 **OSGi 控制台** >狀態&#x200B;**>****Sling 模型**： [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Search， `MyProductTeaserImpl` 您應該會看到如下所示按讚行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   這一行表示 Sling 模型已正確部署並映射到正確的元件。

1. 重新整理添加到&#x200B;**已添加產品預告片的 http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 的 Venia Home 頁面**[。

   ![顯示環保資訊](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果產品的屬性設置為`eco_friendly`**是**，您應該會在頁面上看到“環保”文字。嘗試切換到其他產品以查看行為變化。

1. 下一個打開AEM `error.log` 以查看添加的日誌語句。 位於 `error.log` `<AEM SDK Install Location>/crx-quickstart/logs/error.log`。

   Search AEM 日誌以查看 Sling 模型中新增的日誌語句：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > 如果Teaser中使用的產品沒有該 `eco_friendly` 屬性作為其屬性集的一部分，則還可能會看到一些堆疊跟蹤。

## 為環保徽章添加樣式 {#add-styles}

此時，何時顯示 **環保** 徽章的邏輯正在工作，但是純文本可以使用某些樣式。 下一個向模組添加圖標和样式 `ui.frontend` 以完成實施。

1. [下載 eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) 檔案。此檔用作 **環保** 徽章。
1. 返回到 IDE 並導航到該 `ui.frontend` 資料夾。
1. 將 `eco_friendly.svg` 檔案 `ui.frontend/src/main/resources/images` 新增到資料夾：

   ![添加了環保 SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 在中`ui.frontend/src/main/styles/commerce/_productteaser.scss`開啟檔案`productteaser.scss`。
1. 在類別中新增 `.productteaser` 以下 Sass 規則：

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
   > 簽出 [設定CIF核心元件的樣式](./style-cif-component.md) 以取得有關前端工作流程的更多詳細資訊。

1. 從命令行終端使用 Maven 技能儲存更改並部署更新以AEM：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 重新整理添加到&#x200B;**已添加產品預告片的 http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 的 Venia Home 頁面**[。

   ![環保徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 祝賀 {#congratulations}

您自定義了您的第一個 AEM CIF 元件！ 在此處](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)下載完成的解決方案[檔案。

## 額外挑戰 {#bonus-challenge}

檢閱的功能 **新增** 已在產品Teaser中實施的徽章。 嘗試為作者添加一個額外的複選框，以控制&#x200B;****&#x200B;何時顯示環保徽章。更新位於的 `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`元件對話框。

![新徽章實施挑戰](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他資源 {#additional-resources}

- [AEM原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)
- [自定義 CIF 核心元件AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/customize-cif-components.html)
- [自訂核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [快速入門AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
- [CIF產品和類別器的使用](use-cif-pickers.md)
