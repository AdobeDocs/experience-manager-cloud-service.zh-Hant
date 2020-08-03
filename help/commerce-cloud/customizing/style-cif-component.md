---
title: 樣式AEM CIF核心元件
description: 樣式AEM CIF核心元件
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 0%

---


# 樣式AEM CIF核心元件 {#style-aem-cif-core-components}

[CIF專案原型](https://github.com/adobe/aem-cif-project-archetype) ，會建立最小的Adobe Experience Manager(AEM)CIF專案，做為使用 [AEM CIF核心元件之客戶專案的起點](https://github.com/adobe/aem-core-cif-components)。 預設樣式（稱為Venia品牌）最初會套用至網站。 在本教學課程中，您將檢視由原型產生的新AEM CIF專案，並瞭解AEM CIF核心元件所使用的CSS和JavaScript的組織方式。 您也可以使用CSS建立新樣式，以取代「產品摘要」元件的預設樣式。

![您將建立的](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> 類似卡片的產品摘要元件將會建置新樣式。

## 必備條件 {#prerequisites}

需要下列工具和技術：

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 或 [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) （僅限AEM 6.5+）
* [Apache Maven](https://maven.apache.org/) （3.3.9或更新版本）
* Adobe Experience Manager（本機實例）
   * [AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/introduction/technical-requirements.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/sp-release-notes.html)
* 執行與原 [型相容的版本](https://github.com/adobe/aem-cif-project-archetype#requirements)

## 產生專案 {#generate-project}

我們將使用 [CIF Project原型產生新的AEM CIF專案](https://github.com/adobe/aem-cif-project-archetype) ，然後覆寫預設樣式。

**您可以使用現有專案** （根據CIF專案原型）並略過本節。

1. 在GitHub上查看最新版本，確定CIF項目原 [型的最新版本](https://github.com/adobe/aem-cif-project-archetype/releases/latest)。 在下個步驟中，請 `x.y.z` 以最新版本取代。

1. 運行以下Maven命令，以批處理模式生成 [新項目](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html)。

   ```terminal
   mvn archetype:generate -B \
       -DarchetypeGroupId="com.adobe.commerce.cif" \
       -DarchetypeArtifactId="cif-project-archetype" \
       -DarchetypeVersion=x.y.z \
       -DgroupId="com.acme.cif" \
       -DartifactId="acme-store" \
       -Dversion=0.0.1-SNAPSHOT \
       -Dpackage="com.acme.cif" \
       -DappsFolderName="acme" \
       -DartifactName="Acme Store" \
       -DcontentFolderName="acme" \
       -DpackageGroup="acme" \
       -DsiteName="Acme Store" \
       -DoptionAemVersion=6.5.0 \
       -DoptionIncludeExamples=y \
       -DoptionEmbedConnector=y
   ```

1. 建立專案並部署至AEM的本機例項：

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. 新增必要的OSGi設定，將您的AEM例項連接至Magento例項，或將設定新增至新建立的專案。

1. 此時，您應該有連接到Magento實例的店面的工作版本。 導覽至 `US` >頁 `Home` 面： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   您應該會看到，店面目前使用的是Venia主題。 展開店面的「Main Menu（主菜單）」時，您應該會看到各種類別，指出Magento連線正在運作。

   ![使用Venia Theme設定的店面](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## 客戶端庫簡介 {#introduction-to-client-libraries}

負責轉譯店面主題／樣式的CSS和JavaScript，由 [Client資料庫或clientlibs在AEM中管理](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html) 。 用戶端程式庫提供一種機制，可在專案程式碼中組織CSS和Javascript，然後傳送至頁面。

我們可將品牌特定樣式套用至AEM CIF核心元件的方式是新增並覆寫這些用戶端程式庫所管理的CSS。 瞭解用戶端程式庫的結構化及包含在頁面上，是十分重要的。

### 項目客戶端庫 {#project-client-libraries}

接下來，我們將檢查原型自動生成的客戶端庫。 使用您選擇的IDE來匯 [入上一個練習中產生的專案](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)。

1. 導覽並展開 **ui.apps模組** ，並展開檔案夾階層至： `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`:

   ![ui.apps clientlibs](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   下面有兩個資料夾，即 **clientlib-base** 和 **theme**。

1. **clientlib-base** —— 此為空的用戶端程式庫，只會內嵌 [AEM核心元件的必要相依性](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)。

   ![Clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   以下是clientlib-base的XML **定義** ( `.content.xml` 檔案):

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` 是此客戶端庫的類別。 把一個類別當成標籤。 這將用於在頁面上包含或內嵌程式庫。

   請注意 `embed` 屬性和其他clientlib類別的陣列。 這些類別中的每一個都代表一個用戶端程式庫。 例如，包 `core.wcm.components.accordion.v1` 含Accordion元件運作所 [需的javascript](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/accordion.html) 。

   使用和屬 `embed` 性 `categories` ，您可以管理並包含不同專案的用戶端程式庫。

   `allowProxy=true` 確保用戶端程式庫CSS和JavaScript會從前置詞的路徑提供： `/etc.clientlibs`. 這可確保受保護的應用程 `/apps` 式碼不受一般使用者的保護，但網站運作所需的CSS和JavaScript可以匿名提供。 如需allowProxy屬性的 [詳細資訊，請參閱這裡](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)。

1. **theme** —— 此為用戶端資料庫，包含CIF專案的開始主題和CSS。 此用戶端程式庫是依每個實作來自訂的，從一些現有的樣式開始，可讓元件開始運作。

   ![主題clientlibrary](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   以下是主題的XML定 **義**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` 是此用戶端程式庫的類別，而這是該用戶端程式庫將如何包含在頁面中。

1. 在主 **題用戶端** ，您應會在下列位置看到名 **** 為css.txt的檔案： `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`:

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   css. **txt** (和 **js.txt**)可當成資訊清單，決定個別檔案在最終CSS檔案中的加入順序。 訂購對CSS和JavaScript都很重要，而且能建立多個檔案，以便更好地管理程式碼，也是件好事。 透過 **css.txt檔案** ，您可以看到檔案是由套用樣式的元件所組織。

1. 檢查主題／元件下 **方的CSS檔案** ，以瞭解ootb元件樣式。 我們將在教學課程的稍後部份更新這些檔案。

### 包含基本頁元件的客戶端庫包含

接下來，我們將使用 [HTL](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#using-htl) 和Page元件檢查用戶端程式庫在頁面上的包含方式。

1. 在 **ui.apps模組中** ，導覽至下列元件 `page` 定義： `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. 此 **頁面元件** （由原型產生）是用於呈現專案中所有頁面的入口點。

1. 如果檢查頁 **面元件** (`page/.content.xml`)的定義 `sling:resourceSuperType` ，您會注意到指向的 `core/cif/components/structure/page/v1/page`屬性。 這表示我們專案的(Acme)頁面 **元件** ，將繼承 [](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page) CIF Core Page元件的所有功能，並可讓我們管理較少的程式碼。

1. 在頁面 **元件下** ，您會找到兩個檔案： **customheaderlibs.html** 和 **customfooterlibs.html**。

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs.html** 是HTL指令碼，將呈現在頁首。 這是覆寫和新增專案特定邏輯的常用指令碼。 在本例中，我們使用它將客戶端庫包含在類別中 `acme.wcm.base`。 遵循網頁開發的最佳實務，我們只會將CSS加入頁面的標題中。

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfooterlibs.html** 是HTL指令碼，會在頁面底部，緊接在結束標籤之 `</body>` 前呈現。 再次使用類別 `acme.wcm.base` ，但這次只會載入用戶端程式庫的JavaScript。

修改頁面元件的HTL **指令碼** , `acme.wcm.base` 是如何納入所有頁面的。 那麼呢 `acme.theme`? 在下個練習中，我們將查看包含客戶端庫的另一個選項。

### 包含頁面範本的用戶端程式庫 {#client-library-inclusion-pagetemplates}

如何包含用戶端程式庫有幾個選項。 接下來，我們將透過頁面範本檢查產生的專案如何包含主題用戶端 [程式庫](https://docs.adobe.com/content/help/en/experience-manager-65/developing/platform/templates/page-templates-editable.html)。

開啟新瀏覽器並登入您在本教學課程開始時部署專案的AEM例項。

1. 從「AEM開始」畫面導覽至「工 **具** >一 **般** >范 **本」**。

   ![範本導覽](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. 導覽至 **Acme Store Configuration** 檔案夾。 選取鉛 **筆圖示** ，以開啟「類 *別頁面範本」* 。

   ![類別頁面範本卡](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. 在左上角，選取「頁面資訊」圖 **示並按一下** 「頁 **面原則」**。

   ![頁面原則功能表項目](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. 這將開啟目錄頁模板的頁策略：

   ![頁面策略——目錄頁](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   在右側，您可以看到將包含在使用此範本 **的所有頁面** ，的客戶程式庫類別的清單。

   * **wcm.foundation.components.page.responsive** —— 提供作者啟用回應式版面 [控制所需](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/siteandpage/responsive-layout.html) 的CSS。
   * **acme.theme** —— 這是原型自動產生的起始主題。 依預設，此樣式與範例Venia展示商店相似。 但是，如同您從名稱中所看到的，此項目實作將加以自訂。 *這是我們將在下一節中修改的內容！*
   * **core.cif.components.react** —— 這是編譯的用戶端程式庫，包含數個用於動態功能（例如購物車）的React元件。 如需詳 [細資訊，請參閱此處](https://github.com/adobe/aem-core-cif-components/tree/master/react-components)。

   請注意，其他範本使用相 **同的原則**、 **內容頁面**、著陸頁面等…… 透過重新使用相同的原則，我們可以確保所有頁面上都包含相同的用戶端程式庫。

   使用「範本」和「頁面」原則管理包含用戶端程式庫的好處是，您可以依範本變更原則。 例如，您可能是在同一個AEM實例中管理兩個不同的品牌。 每個品牌都有其獨特的風格或 *主題* ，但基本資料庫和程式碼會相同。 另一個範例是，如果您有較大的用戶端程式庫，而您只想要顯示在特定頁面上，則可針對該範本建立唯一的頁面原則。 另一項優勢

### 驗證頁面上的客戶端庫 {#verify-client-libraries}

目前，我們已檢視如何搭配 **customheaderlibs.html** 和 **customfooterlibs.html** 指令碼使用HTL來包含用戶端程式庫，以及如何使用範本的頁面原則來包含其他用戶端程式庫。 接下來，我們將驗證網站上是否包含用戶端程式庫。

1. 從「AEM開始」畫面導覽至「 **Sites** > **Acme Store** > **United States** >英文」, **** 並開啟頁面進行編輯： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. 選取「頁 **面資訊** 」功能表，然後按 **一下「檢視為已發佈**:

   ![以已發佈狀態檢視](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   如此會開啟頁面，而未載入任何AEM作者javascript，因為它會顯示在發佈的網站上。 請注意，URL已附加查詢 `?wcmmode=disabled` 參數。 在開發CSS和Javascript時，最好使用此參數來簡化頁面，而不需AEM作者提供任何資訊。

1. 檢視頁面來源，您應該能夠識別包含下列用戶端程式庫： **acme.wcm.base**、 **wcm.foundation.components.page.responsive**、 **acme.theme**、 **core.cif.components.react**

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/clientlib-base.css" type="text/css">
       <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/theme.css" type="text/css">
   </head>
   ...
   
       <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/react-components.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/acme/clientlibs/clientlib-base.js"></script>
   </body>
   </html>
   ```

## 設定產品摘要樣式 {#style-product-teaser}

既然我們瞭解原型產生的用戶端程式庫結構，就可以開始自訂AEM CIF核心元件。 我們將修改「產品摘要」元件的樣式，讓它看起來更像「卡片」。

### 製作產品摘要 {#author-product-teaser}

首先，我們將使用AEM製作工具，將新的「產品摘要」元件例項新增至網站首頁。

1. 開啟新的瀏覽器標籤，並導覽至 **網站的首頁** : [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. 將新的產 **** 品摘要元件插入頁面的主版面容器。

   ![插入產品摘要](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. 展開「側面板」（如果尚未切換），並將資產搜尋器下拉式清單切換至「產 **品」**。 這應該會顯示已連接Magento實例的可用產品清單。 選取產品 **並拖放** ，到頁面 **上的Product Teaser** 元件上。

   ![拖放產品摘要](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > 請注意，您也可以使用對話方塊（按一下扳手圖示）設定元件，以設 *定顯示* 的產品。

1. 您現在應該會看到產品摘要正在顯示產品。 產品名稱和產品價格是顯示的預設屬性。

   ![產品摘要——預設樣式](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### 更新產品摘要的CSS {#update-css-product-teaser}

接下來，我們將修改主題用 **戶端程式庫中的** CSS，以便為「產品摘要」建置類似卡片的樣式。

返回到IDE和生成的項目。

1. 在 **ui.apps模組中** ，導覽至資料夾： `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. 這是定義「產品摘要」所有樣式的地方。

1. 開啟檔 **案teaser.css** ，並更新對應的CSS規則(或下載解決 [方案teaser.css檔案](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) ，然後取代)。

   新增下垂式陰影並將圓角加入「產品摘要」中。

   ```css
    .productteaser .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .productteaser .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

   在「產品摘要」中變更影像的邊框。

   ```css
   .productteaser .item__image {
       border-bottom: 1px solid #c0c0c0;
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
    }
   ```

   更新產品名稱以顯示在摘要底部，並修改文字顏色。

   ```css
   .productteaser .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

   更新產品價格，以便也顯示在摘要底部，並修改文字顏色。

   ```css
   .productteaser .item__price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   }
   ```

   更新底部的媒體查詢，將名稱和價格堆疊在小於992像素的螢幕上。

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   將變更儲存 **為Teaser.css**。 您可以在此處下 [載解決方案Teaser.css檔案](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css)。

1. 使用您的Maven技能，從命令列 **** 終端機將ui.apps模組的更新部署至AEM:

   ```shell
           $ cd acme-store/ui.apps/
           $ mvn -PautoInstallPackage clean install
           ...
           saving approx 0 nodes...
           Package imported.
           Package installed in 61ms.
           [INFO] ------------------------------------------------------------------------
           [INFO] BUILD SUCCESS
           [INFO] ------------------------------------------------------------------------
           [INFO] Total time:  6.903 s
           [INFO] Finished at: 2020-02-06T13:21:36-08:00
            [INFO] ------------------------------------------------------------------------
   ```

   >[!NOTE]
   >還有其他 [IDE設定和工具](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) ，可直接將專案檔案同步至本機AEM例項，而不需執行完整的Maven組建。

### 檢視更新的產品摘要 {#view-updated-product-teaser}

在專案的程式碼已部署至AEM後，我們現在應該可以看到產品摘要的變更。

1. 返回瀏覽器並重新整理首頁： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html). 您應該會看到已套用更新的產品摘要樣式。

   ![更新的產品摘要樣式](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. 加入額外的產品預告來嘗試。 使用「版面模式」變更元件的寬度和偏移，以一列顯示多個預告。

   ![多種產品預告](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >每個產品摘要都包含相同的樣式。

### 疑難排解 {#troubleshooting}

您可以在 [CRXDE-Lite中確認](http://localhost:4502/crx/de/index.jsp) ，已部署更新的CSS檔案： [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

部署新的CSS和／或JavaScript檔案時，請務必確保瀏覽器不提供舊檔。 您可以清除瀏覽器快取或啟動新的瀏覽器工作階段，以消除這種情況。

AEM也會嘗試快取用戶端程式庫以取得效能。 有時，在程式碼部署後，會提供舊版檔案。 您可以使用「重建用戶端程式庫」工具手動使AEM的用戶端程 [式庫快取失效](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)。 *如果您懷疑AEM已快取舊版用戶端程式庫，則偏好使用「使快取無效」方法。 重建庫效率低下，耗時。*

### 恭喜 {#congratulations}

您剛剛設計了您的第一個AEM CIF核心元件！

### 獎金挑戰 {#bonus-challenge}

使用 [AEM Style系統](https://docs.adobe.com/content/help/en/experience-manager-65/developing/components/style-system.html) ，建立兩種樣式，供內容作者開啟／關閉。 [使用Style System進行開發](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) ，包括詳細步驟和資訊，說明如何完成此作業。

![獎金挑戰——樣式系統](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## 其他資源 {#additional-resources}

* [AEM CIF原型](https://github.com/adobe/aem-cif-project-archetype)

* [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)

* [設定本機AEM開發環境](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [用戶端資源庫](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html)
* [AEM Sites快速入門](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [用體制發展](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
