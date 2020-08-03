---
title: 自訂CIF核心元件
description: 自訂CIF核心元件
translation-type: tm+mt
source-git-commit: dd6973085ae34dd6ea7296c36d0a14f699440269
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---


# 自訂AEM CIF核心元件 {#customize-cif-components}

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) （核心元件）提供一套標準的商務元件集，可用來加速整合Adobe Experience Manager(AEM)和Magento解決方案的專案。 這些元件可立即生產使用，並可 [輕鬆使用CSS建立樣式](style-cif-component.md)。 許多實作也希望擴充這些元件，以符合業務特定需求。

在本教學課程中，我們將大致檢視AEM CIF核心元件和AEM提供的幾個不同擴充點。 我們將擴充「產品摘要」元件的功 [能](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) ，以加入轉換「新」橫幅的功能。 內容作者將能夠切換此橫幅，並判斷該橫幅的顯示時間。 產品的「年齡」將根據Magento目錄中產品的建立日期。 當產品已經過一定的天數時，「新」橫幅應會自動消失。

![新橫幅已擴充](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## 必備條件 {#prerequisites}

需要下列工具和技術：

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) （3.3.9或更新版本）
* [AEM Cloud SKD含CIF附加元件](../develop.md)
* 與CIF核心元件相容的Magento

建議在繼續本教學課程之前先檢閱下列內容：

* [AEM雲端服務商務整合框架簡介](/help/commerce-cloud/overview.md)
* [樣式AEM CIF核心元件——教學課程](style-cif-component.md)

## Starter Project

我們提供了一個入門專案，可與本教學課程搭配使用。 該項目是使用 [CIF項目原型的](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) v0.7.0生成的。 在啟動新專案時，請一律使用 [最新版](https://github.com/adobe/aem-cif-project-archetype/releases/latest) 「原型」，這被視為最佳實務。

1. 將起始專案 [**acme-store.zip下載&#x200B;**](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip)到您的案頭。

1. 解 **壓縮acme-store.zip** ，您應該會看到下列檔案夾結構：

   ```plain
   /acme-store
      /ui.content
      /ui.apps
      /samplecontent
      /core
      /all
      + pom.xml
      + README.md
   ```

1. 開啟新的終端視窗，並建立專案並部署至AEM的本機執行個體；

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. 新增必要的OSGi設定，將您的AEM例項連接至Magento例項，或將設定新增至新建立的專案。

1. 此時，您應該有連接到Magento實例的店面的工作版本。 導覽至 `US` >頁 `Home` 面： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   您應該會看到，店面目前使用的是Venia主題。 展開店面的「Main Menu（主菜單）」時，您應該會看到各種類別，指出Magento連線正在運作。

   ![使用Venia Theme設定的店面](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## 製作產品摘要 {#author-product-teaser}

我們將在本教學課程中擴充「產品摘要元件」。 首先，我們將在首頁新增產品摘要的例項，以瞭解基準功能。

1. 導覽至 **網站的首頁** : [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. 將新的產 **** 品摘要元件插入頁面的主版面容器。

   ![插入產品摘要](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. 展開「側面板」（如果尚未切換），並將資產搜尋器下拉式清單切換至「產 **品」**。 這應該會顯示已連接Magento實例的可用產品清單。 選取產品 **並拖放** ，到頁面 **上的Product Teaser** 元件上。

   ![拖放產品摘要](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > 請注意，您也可以使用對話方塊（按一下扳手圖示）設定元件，以設 *定顯示* 的產品。

1. 您現在應該會看到產品摘要正在顯示產品。 產品名稱和產品價格是顯示的預設屬性。

   ![產品摘要——預設樣式](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## 自訂產品摘要的標籤 {#customize-markup-product-teaser}

AEM元件的常見擴充功能是修改元件產生的標籤。 這是透過覆寫元件用 [來轉換其標籤的HTL](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html) 指令碼來完成的。 HTML範本語言(HTL)是輕量型範本語言，AEM元件會使用它來根據撰寫的內容動態轉換標籤，讓元件可重複使用。 例如，「產品摘要」可重複使用，以顯示不同的產品。

在我們的案例中，我們想要在摘要上方呈現橫幅，以指出產品是「新」的，而且最近已新增至目錄。 自訂元件標 [記的設計模式](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) ，實際上是所有AEM元件（而不只是AEM CIF核心元件）的標準。

使用您選擇的IDE來開 [啟在教學課程開始時下載](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) 的入門專案。

1. 導覽並展開 **ui.apps模組** ，並展開資料夾階層至： `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` 並檢查檔 `.content.xml` 案。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   以上是我們專案中產品摘要元件的元件定義。 請注意屬性 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`。 這是建立 [Proxy元件的示例](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)。 我們不需從AEM CIF核心元件複製和貼上所有產品摘要HTL指令碼，而是可 `sling:resourceSuperType` 以使用繼承所有功能。

1. 在AEM中開啟新瀏覽器並導 [覽至CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) 。 展開樹以查看以下 `productteaser` 元件： `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![CRXDE Lite產品摘要](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   這是Product Teaser元件的完整元件定義。

1. 切換回IDE和Acme Store專案。 建立名為下方的新 `productteaser.html` 檔案 `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`。

1. 從 `productteaser.html` CRXDE-Lite [複製內容，並貼入新建立檔案的Acme-Store專](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)`productteaser.html` 案。

   ![產品摘要html覆寫](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. 在Acme-Store專案中，修改 `productteaser.html` 檔案並插入新div，此div代表產品影像標籤上方的標章：

   ```html
   ...
   <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
       <!-- Add Badge -->
       <div class="item__badge">
           <span>New</span>
       </div>
       <!-- end add badge -->
       <a class="item__images" href=${product.url}>
           <img class="item__image" width="100%" height="100%"
                   src="${product.image}" alt="${product.image}"/>
       </a>
       <a class="item__name" href=${product.url}><span>${product.name}</span></a>
       <div class="item__price">
           <span> ${product.formattedPrice} </span>
       </div>
       <sly data-sly-call="${actionsTpl.actions @ product=product}"></sly>
   </div>
   ```

1. 使用您的技巧或使用IDE的功能，將更新的程式碼部署至AEM [的本機例項](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. 在瀏覽器中，返回AEM [中商店前端的首頁](http://localhost:4502/editor.html/content/acme/us/en.html) 。 重新整理後，您應會看到「新」橫幅出現在元件的右上角。

   ![新橫幅已擴充](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   目前，橫幅何時顯示並不包含邏輯。 在接下來的幾場演習中，我們將糾正這一點。

   > 請注意，轉換橫幅的CSS是做為起始專案的一部分提供，可在以下網址找到： `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. 如需詳細資訊，請結帳 [「樣式CIF核心元件」教學課程](style-cif-component.md)。

## 自訂產品摘要的對話方塊 {#customize-dialog-product-teaser}

接下來，我們將自訂「產品摘要」元件的對話方塊，讓「作者」決定產品被視為「新」的日期範圍，以及是否應顯示橫幅。 我們將自訂「產 [品摘要](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) 」(Product Teaser)對話方塊，做為Acme Store專案的一部分。

1. 在您選擇的IDE中開啟Acme Store專案，然後導覽至 `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`。

1. 在資料夾 `productteaser` 下方，新增名為的新資料夾 `_cq_dialog`。 將新檔案添加到名為的 `_cq_dialog` 資料夾中 `.content.xml`。 您現在應該有下列檔案結構：

   ```plain
   ../acme
       /components
           /commerce
               /productteaser
                  /_cq_dialog
                     + .content.xml
                  /_cq_template
                  + .content.xml
                  + productteaser.html
   ```

1. 使用 `_cq_dialog/.content.xml` 下列XML更新：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
       xmlns:cq="http://www.day.com/jcr/cq/1.0" 
       xmlns:jcr="http://www.jcp.org/jcr/1.0" 
       xmlns:nt="http://www.jcp.org/jcr/nt/1.0" 
       jcr:primaryType="nt:unstructured" 
       jcr:title="My Product Teaser" 
       sling:resourceType="cq/gui/components/authoring/dialog" 
       trackingFeature="cif-core-components:productteaser:v1">
       <content jcr:primaryType="nt:unstructured" 
           sling:resourceType="granite/ui/components/coral/foundation/container">
           <items jcr:primaryType="nt:unstructured">
               <tabs jcr:primaryType="nt:unstructured" 
                   sling:resourceType="granite/ui/components/coral/foundation/tabs" 
                   maximized="{Boolean}true">
                   <items jcr:primaryType="nt:unstructured">
                       <badge jcr:primaryType="nt:unstructured" 
                           jcr:title="Badge" 
                           sling:resourceType="granite/ui/components/coral/foundation/container" 
                           margin="{Boolean}true">
                           <items jcr:primaryType="nt:unstructured">
                               <columns jcr:primaryType="nt:unstructured" 
                                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns" 
                                   margin="{Boolean}true">
                                   <items jcr:primaryType="nt:unstructured">
                                       <column jcr:primaryType="nt:unstructured" 
                                           sling:resourceType="granite/ui/components/coral/foundation/container">
                                           <items jcr:primaryType="nt:unstructured">
                                               <badge jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/checkbox" 
                                                   text="Display 'New' badge" 
                                                   value="true" 
                                                   uncheckedValue="false" 
                                                   name="./badge" />
                                               <age jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield" 
                                                   fieldDescription="The maximum age in days the 'new' badge should be shown" 
                                                   fieldLabel="Max Product Age" 
                                                   name="./age"
                                                   min="{Long}0" 
                                                   value="10" />
                                               <ageTypeHint jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/foundation/form/hidden" 
                                                   ignoreData="{Boolean}true" 
                                                   name="./age@TypeHint" 
                                                   value="Long" />
                                           </items>
                                       </column>
                                   </items>
                               </columns>
                           </items>
                       </badge>
                   </items>
               </tabs>
           </items>
       </content>
   </jcr:root>
   ```

   在上方，我們新增了2個欄位，作為新標籤和單一隱藏欄位的一部分。

   1. 顯示「新增」徽章的核取方塊
   2. 用於定義最大產品年齡的數字欄位
   3. 隱藏欄位，以確保「最大產品年齡」儲存為長(如需詳細資 [訊，請參閱@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) )

   定義為proxy元件一部分的對話方塊會繼承所有現有的對話方塊欄位，其功能稱為 [Sling Resource Merger](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/sling-resource-merger.html)。 因此，我們不必重新定義屬於產品摘要一部分的現有欄位。

1. 更 `productteaser.html` 新並 `data-sly-test` 新增徽 `<div>` 章。 如果使用者已勾選「true」，則此測試將可讓您輕鬆決定轉譯徽章。

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. 使用IDE的功能或運用您的技巧，將更新的程式碼部署至AEM的本機例項：

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. 返回「產品摘要」元件，然後按一下 *扳手圖* 示以開啟「對話方塊」。 您現在應該會看到一個標籤，標 **示為Badge** ，並附加兩個欄位。 更新這些欄位會將值保留至AEM。 您應該可以使用核取方塊來開啟／關閉徽章：

   ![切換徽章](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   這可讓作者控制徽章出現的時間。 不過，當產品在一天中達到某個年齡時，根據「最大產品年齡」的項目，徽章會自動消失，這是 **最理想的選擇**。 為此，我們需要實作一些後端邏輯。

## 更新產品摘要的Sling Model {#updating-sling-model-product-teaser}

接下來，我們將透過實作Sling Model來擴充Product Teaser的商業邏輯。 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)，是註解導向的&quot;POJOs&quot;(Plain Old Java Objects)，可實作元件所需的任何商業邏輯。 Sling Models會與HTL指令碼搭配使用，做為元件的一部分。 我們將遵循Sling Models [的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) ，以便我們只擴充現有產品摘要模型的部分。

Sling Models是以Java形式實作，可在產生的專 **案的** core模組中找到。

1. 在您選擇的IDE中開啟Acme Store專案，並在核心模組下導 **覽** ，以： `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java是我們預先建立的Java介面** ，可擴充CIF **ProductTeaser介面** 。

1. 接著，開啟位 **於** : `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` 是介面的實現類 `MyProductTeaser`。

   使用Sling [Models的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) ，我們可以透過 `ProductTeaser` 屬性來參考 `sling:resourceSuperType` 類別：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   對於我們不想覆寫或變更的所有方法，我們只要傳回傳回的值即 `ProductTeaser` 可：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. AEM CIF Core Components提供的額外擴充點之一，就是 `AbstractProductRetriever` 讓我們存取特定產品屬性。 添加以下方法以初始化 `AbstractProductRetriever` 該方 `init()` 法：

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
   
       }
   ...
   ```

1. 讓您修改格式化價格並覆寫中的邏輯，以測試這些變更 `getFormattedPrice()`。 進行下列更新，以便我們根據德文地區設定價格格式。 （或者選擇不同的國家！）

   ```java
           import java.util.Locale;
           import java.text.NumberFormat;
            ...
   
               @Override
                   public String getFormattedPrice() 
                   {
                   //return productTeaser.getFormattedPrice();
                   NumberFormat germanCurrencyFormat = NumberFormat.getCurrencyInstance(Locale.GERMANY);
                   Double price =  productRetriever.fetchProduct().getPrice().getRegularPrice().getAmount().getValue();
                       if(price != null) 
                       {
                           return germanCurrencyFormat.format(price);
                       }
                   return null;
                   }
   ```

   請注意，物 `productRetriever` 件如何透過方法讓 `ProductInterface` 我們存取物 `fetchProduct()` 件。 您可在此處查看所有 [可用方法](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)。

   > 注意*將地區設定修改為德文，只是查看覆寫的有趣範例。 實際上，ProductTeaser會使 [用頁面的地區設定來決定格式](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173)。

1. 接下來，我們需要更新 **ui.apps模組中的** productteaser.html **** ，以參考我們新的Sling Model，網址為： `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
       ...
   ```

   將更改保存到 `productteaser.html`。

1. 將程式碼庫部署至AEM的本機例項。 由於變更了ui.apps **和核心模組** , **** 所以請從根目錄建立和部署專案：

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. 開啟瀏覽器並導覽至： [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). 此主控台顯示系統中註冊的所有Sling Models。 請連按兩下，以確保MyTeaserModelImpl已部署且已正確映射。 您應該能夠看到類似的內容：

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. 最後，導覽至您製作「產品摘要」元件的位置，您現在應該看到以德國貨幣格式計價的價格：

   ![價格格式已更新](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## 實作isShowBadge邏輯 {#implement-isshowbadge}

既然我們有機會嘗試覆寫Sling Model方法，請讓實作何時顯示「新」徽章的邏輯。

1. 返回IDE並開啟 **MyProductTeaser.java** 檔案，網址為： `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. 將新方法添 `isShowBadge()` 加到介面：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   這是我們將引入的一種新方法，來封裝是否顯示徽章的邏輯。

1. 接下來，請在 **重新開啟MyProductTeaserImpl.java**`core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`。

1. 「新」標章的顯示時間邏輯將根據「產品」的 `created_at` 屬性而定。 為了能夠訪問該屬性，我們需要擴展ProductTeaser執 **行的GraphQL** 查詢。 我們可以在 `init()` MyProductTeaserImpl.java中更新方 **法來執行此**&#x200B;操作：

   ```java
   //MyProductTeaserImpl.java
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           // Pass your custom partial query to the ProductRetriever. This class will
           // automatically take care of executing your query as soon
           // as you try to access any product property.
           productRetriever.extendProductQueryWith(p ->
               p.addCustomSimpleField("created_at")
           );
       }
   }
   ```

   添加到該方 `extendProductQueryWith` 法是確保模型其餘部分可以使用附加產品屬性的有力方法。 它還將執行的查詢數減到最小。

   >[!NOTE]
   >在上述程式碼中，我們使用`addCustomSimpleField` ，擷取屬 `created_at` 性。 這說明了如何查詢屬於Magento架構一部分的任何自定義屬性。
   >
   > 不過， `created_at` 該屬性實際上已實作為「產品介面」的一部分實作 [](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) ，較佳的做法是重複使用如下方法： `productRetriever.extendProductQueryWith(p -> p.createdAt());`. 大部分常見的架構屬性都已實作，因此只使用真正 `addCustomSimpleField` 的自訂屬性。

1. 接下來，我們將實現該 `isShowBadge()` 方法：

   ```java
   import java.time.format.DateTimeFormatter;
   import java.util.Locale;
   import java.time.temporal.ChronoUnit;
   
   ...
   
   @Override
   public Boolean isShowBadge() {
        final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
   
        //Look at the checkbox from the dialog to see if we should even attempt to show the badge
        final boolean showBadge = properties.get("badge", false);
        if (showBadge) {
   
            //Look at the numberfield set from the dialog to determine the max "age" in days to compare too
            final int maxAgeProp = properties.get("age", 0);
   
           String createdAtString;
           try {
               //Grab the created_at property from the product
               //Here we show the example of retrieving the attribute as if it was a custom attribute
               // an alternative that would work is productRetriever.fetchProduct().getCreatedAt()
               createdAtString = productRetriever.fetchProduct().getAsString("created_at");
               log.info("***CREATED_AT**** " + createdAtString);
           } catch (SchemaViolationError e) {
               //it is possible that a schema error could be thrown if the attribute is not part of the schema
               log.error("Error determining to showBadge" , e);
               return false;
           }
   
            // Custom code to calc the date difference of the product creation
            // compared to today
           final LocalDate createdAt = LocalDate.parse(createdAtString, formatter);
            if (createdAt != null) {
   
                final long ageInDays = ChronoUnit.DAYS.between(createdAt, LocalDate.now());
                if (ageInDays < maxAgeProp) {
                    return true;
                }
            }
        }
        return false;
    }
   ```

   在上述方法中，我們首先檢查作者是否已使用核取方塊啟用徽章功能。 接著，我們讀取在對話方塊中設 `age` 定的屬性值，並代表產品在橫幅消失前應使用的天數上限。 最後，我們根據日期計算產品的 `created_at` 年齡。 如果比較兩個值後，我們會傳 `true` 回來顯示徽章，在所 `false` 有其他情況下。

1. 最後，需要對指令碼再添加一 `productteaser.html` 個，才能調用該方 `isShowBadge()` 法。 在中開啟檔案 `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`。 進行下列更新：

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. 將程式碼庫部署至AEM的本機例項。 由於變更了ui.apps **和核心模組** , **** 所以請從根目錄建立和部署專案：

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. 返回AEM和ProductTeaser元件，並嘗試使用不同的數字來顯示產品的最大年齡。 視產品的年齡而定，您可能需要輸入一些非常大的數字才能顯示徽章。

   ![最大產品年齡999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. 最後，搜尋AEM記錄檔，以查看上述步驟5中輸入的log陳述式。 這應該會列印來自Magento `created_at` 的屬性值。 您可以開啟檔案以檢視AEM的記 `error.log` 錄檔。 此檔案位於已安 `crx-quickstart/logs/error.log` 裝AEM jar的下方。 您可以預期看到如下行項目：

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   現在您可以驗證我們實作的邏輯是否正確！

### 恭喜 {#congratulations}

您剛自訂了第一個AEM CIF元件！ 請在此處下 [載完成的解決方案套件](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip)。

## 其他資源 {#additional-resources}

* [AEM Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)
* [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)
* [自訂AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [自訂核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
