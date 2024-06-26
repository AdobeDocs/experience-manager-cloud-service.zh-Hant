---
title: 樣式Adobe Experience Manager CIF核心元件
description: 瞭解如何設定Adobe Experience Manager (AEM) CIF核心元件的樣式。 本教學課程涵蓋如何使用使用者端資料庫或clientlibs來針對AEM Commerce實作部署及管理CSS和JavaScript。 本教學課程也涵蓋ui.frontend模組和webpack專案如何整合至端對端建置流程。
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
exl-id: 521c1bb8-7326-4ee8-aba3-f386727e2b34
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '2342'
ht-degree: 0%

---

# 建立AEM CIF核心元件的樣式 {#style-aem-cif-core-components}

此 [CIF Venia專案](https://github.com/adobe/aem-cif-guides-venia) 是用於的參考程式碼基底 [CIF Core Components](https://github.com/adobe/aem-core-cif-components). 在本教學課程中，您需檢查Venia參考專案，瞭解AEM CIF核心元件所使用的CSS和JavaScript如何進行組織整理。 您也可以使用CSS建立樣式，以更新 **產品Teaser** 元件。

>[!TIP]
>
> 使用 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 當您開始自己的commerce實作時。

## 您將建置的內容

在本教學課程中，將針對類似卡片的Product Teaser元件實作新樣式。 在本教學課程中吸取的課程可套用至其他CIF核心元件。

![您將建置的內容](../assets/style-cif-component/what-you-will-build.png)

## 先決條件 {#prerequisites}

本機開發環境是完成本教學課程的必要條件。 此環境包含設定並連線至Adobe Commerce執行個體的AEM執行個體。 檢閱的需求和步驟 [使用AEMas a Cloud ServiceSDK設定本機開發](../develop.md).

## 原地複製Venia專案 {#clone-venia-project}

您即將複製 [Venia專案](https://github.com/adobe/aem-cif-guides-venia)，然後覆寫預設樣式。

>[!NOTE]
>
> **您可以隨意使用現有的專案** (根據包含CIF的AEM專案原型)並略過本節。

1. 執行下列git命令，以便複製專案：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 建立專案並將其部署到AEM的本機執行個體：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 新增必要的OSGi設定，以便將AEM執行個體連線至Adobe Commerce執行個體，或將設定新增至已建立的專案。

1. 此時，您應該有已連線至Adobe Commerce執行個體的有效店面版本。 導覽至 `US` > `Home` 頁面位置： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   您應該會看到店面目前使用Venia佈景主題。 展開店面的「主要」功能表，應該會看到各種類別，表示與Adobe Commerce的連線正常運作。

   ![使用Venia佈景主題設定的店面](../assets/style-cif-component/venia-store-configured.png)

## 使用者端程式庫和ui.frontend模組 {#introduction-to-client-libraries}

在AEM中，負責轉譯店面主題/樣式的CSS和JavaScript是由 [使用者端資料庫](/help/implementing/developing/introduction/clientlibs.md) 或「clientlibs」的簡稱。 使用者端程式庫提供的機制，可在專案程式碼中整理CSS和JavaScript，然後傳送至頁面。

可透過新增和覆寫這些使用者端資料庫所管理的CSS，將品牌特定樣式套用至AEM CIF核心元件。 瞭解使用者端程式庫如何建構並包含在頁面上至關重要。

此 [ui.frontend](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 是專用的 [webpack](https://webpack.js.org/) 專案以管理專案的所有前端資產。 此網頁套件可讓前端開發人員使用各種語言和技術，例如 [TypeScript](https://www.typescriptlang.org/)， [Sas](https://sass-lang.com/)，以及更多功能。

此 `ui.frontend` 模組也是Maven模組，並使用NPM模組與較大的專案整合。 [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator). 在建置期間， `aem-clientlib-generator` 將編譯後的CSS和JavaScript檔案複製到的 `ui.apps` 模組。

![ui.frontend至ui.apps架構](../assets/style-cif-component/ui-frontend-architecture.png)

*編譯的CSS和JavaScript會從 `ui.frontend` 將模組移入 `ui.apps` 在Maven建置期間作為使用者端程式庫的模組*

## 更新Teaser樣式 {#ui-frontend-module}

接下來，對Teaser樣式進行小幅變更，以瞭解 `ui.frontend` 模組和使用者端程式庫都可運作。 使用 [您選擇的IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) 匯入Venia專案。 使用的熒幕擷取畫面來自 [Visual Studio Code IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. 導覽並展開 **ui.frontend** 模組，並將資料夾階層展開至： `ui.frontend/src/main/styles/commerce`：

   ![ui.frontend商務資料夾](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   請注意，有多個Ass (`.scss`)個檔案時，才會追蹤退出連結。 這些檔案是每個Commerce元件的Commerce專屬樣式。

1. 開啟檔案 `_productteaser.scss`.

1. 更新 `.item__image` 並修改框線規則：

   ```scss
   .item__image {
       border: #ea00ff 8px solid; /* <-- modify this rule */
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

   上述規則應為產品Teaser元件新增粗粉紅色邊框。

1. 開啟新的終端機視窗並導覽至 `ui.frontend` 資料夾：

   ```shell
   $ cd <project-location>/aem-cif-guides-venia/ui.frontend
   ```

1. 執行下列Maven命令：

   ```shell
   $ mvn clean install
   ...
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time:  29.497 s
   [INFO] Finished at: 2020-08-25T14:30:44-07:00
   [INFO] ------------------------------------------------------------------------
   ```

   Inspect終端機輸出。 請注意，Maven命令會執行數個NPM指令碼，包括 `npm run build`. 此 `npm run build` 命令定義於 `package.json` 檔案並編譯webpack專案，然後觸發使用者端程式庫產生。

1. Inspect檔案 `ui.frontend/dist/clientlib-site/site.css`：

   ![已編譯的網站CSS](../assets/style-cif-component/comiled-site-css.png)

   此檔案是專案中所有Sass檔案的編譯及縮製版本。

   >[!NOTE]
   >
   > 原始檔控制會忽略這類檔案，因為它們應該在建置期間產生。

1. Inspect檔案 `ui.frontend/clientlib.config.js`.

   ```js
   /* clientlib.config.js*/
   ...
   // Config for `aem-clientlib-generator`
   module.exports = {
       context: BUILD_DIR,
       clientLibRoot: CLIENTLIB_DIR,
       libs: [
           {
               ...libsBaseConfig,
               name: 'clientlib-site',
               categories: ['venia.site'],
               dependencies: ['venia.dependencies', 'aem-core-cif-react-components'],
               assets: {
   ...
   ```

   此設定檔適用於 [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator) 和會決定編譯的CSS和JavaScript轉換為AEM使用者端程式庫的位置和方式。

1. 在 `ui.apps` 模組，檢查檔案： `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`：

   ![ui.apps中已編譯的網站CSS](../assets/style-cif-component/comiled-css-ui-apps.png)

   此檔案為 `site.css` 已複製到 `ui.apps` 專案。 它現在是名為的使用者端資料庫的一部分 `clientlib-site` 具有類別 `venia.site`. 一旦檔案成為 `ui.apps` 模組；可部署至AEM。

   >[!NOTE]
   >
   > 原始檔控制也會忽略這類檔案，因為它們應該在建置期間產生。

1. 接下來，檢查專案產生的其他使用者端程式庫：

   ![其他使用者端資料庫](../assets/style-cif-component/other-clientlibs.png)

   這些使用者端程式庫並非由管理 `ui.frontend` 模組。 這些使用者端資料庫會包含Adobe所提供的CSS和JavaScript相依性。 這些使用者端資料庫的定義位於 `.content.xml` 每個資料夾下方的檔案。

   **clientlib-base**  — 空白的使用者端程式庫，僅從內嵌必要的相依性 [AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant). 類別為 `venia.base`.

   **clientlib-cif**  — 空白的使用者端程式庫，僅從內嵌必要的相依性 [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components). 類別為 `venia.cif`.

   **clientlib-grid**  — 包含可啟用AEM回應式格線功能的CSS。 使用AEM格線可啟用 [版面模式](/help/sites-cloud/authoring/page-editor/responsive-layout.md) AEM並賦予內容作者重新調整元件大小的能力。 類別為 `venia.grid` 並內嵌於 `venia.base` 資料庫。

1. Inspect檔案 `customheaderlibs.html` 和 `customfooterlibs.html` 下 `ui.apps/src/main/content/jcr_root/apps/venia/components/page`：

   ![自訂頁首與頁尾指令碼](../assets/style-cif-component/custom-header-footer-script.png)

   這些指令碼包括 **venia.base** 和 **venia.cif** 資料庫作為所有頁面的一部分。

   >[!NOTE]
   >
   > 只有基底程式庫會在頁面指令碼中「以硬式編碼」。 `venia.site` 不會包含在這些檔案中，而是包含在頁面範本中，以擁有更大的彈性。 稍後會檢查此程式。

1. 從終端機，建置並部署整個專案到AEM的本機執行個體：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## 編寫產品Teaser {#author-product-teaser}

現在已部署程式碼更新，請使用AEM編寫工具將Product Teaser元件的執行個體新增到網站的首頁。 這麼做可讓我們檢視更新的樣式。

1. 開啟新的瀏覽器索引標籤，並導覽至 **首頁** 網站的： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. 在中展開資產尋找器（側欄） **編輯** 模式。 切換資產篩選器至 **產品**.

   ![展開「資產尋找器」並依產品篩選](../assets/style-cif-component/drag-drop-product-page.png)

1. 將新產品拖放至主配置容器的首頁：

   ![粉紅色邊框的產品Teaser](../assets/style-cif-component/pink-border-product-teaser.png)

   您應該會看到，根據先前建立的CSS規則變更，產品Teaser現在有亮粉紅色邊框。

## 驗證頁面上的使用者端程式庫 {#verify-client-libraries}

接下來，驗證頁面上是否包含使用者端程式庫。

1. 導覽至 **首頁** 網站的： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. 選取 **頁面資訊** 功能表並按一下 **以發佈的形式檢視**：

   ![以發佈的形式檢視](../assets/style-cif-component/view-as-published.png)

   此頁面會開啟，但不載入任何AEM作者JavaScript，如發佈網站中所示。 請注意，url具有查詢引數 `?wcmmode=disabled` 已附加。 開發CSS和JavaScript時，最好使用此引數來簡化頁面，而無需AEM作者提供任何內容。

1. 檢視頁面來源，您應該能夠識別已包含數個使用者端程式庫：

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-site.min.css" type="text/css">
   </head>
   ...
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-base.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/common.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-cif.min.js"></script>
   </body>
   </html>
   ```

   使用者端程式庫在傳送至頁面時會加上前置詞 `/etc.clientlibs` 並透過 [proxy](/help/implementing/developing/introduction/clientlibs.md) 以避免在中公開任何敏感內容 `/apps` 或 `/libs`.

   通知 `venia/clientlibs/clientlib-site.min.css` 和 `venia/clientlibs/clientlib-site.min.js`. 這些檔案是衍生自下列專案的已編譯CSS和JavaScript檔案： `ui.frontend` 模組。

## 頁面範本包含使用者端資料庫 {#client-library-inclusion-pagetemplates}

包含使用者端程式庫有數個選項。 接下來，檢查產生的專案如何包含 `clientlib-site` 程式庫，透過 [頁面範本](/help/implementing/developing/components/templates.md).

1. 導覽至 **首頁** 在AEM編輯器中的網站： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. 選取 **頁面資訊** 功能表並按一下 **編輯範本**：

   ![編輯範本](../assets/style-cif-component/edit-template.png)

   此 **登陸頁面** 範本開啟後， **首頁** 頁面根據。

   >[!NOTE]
   >
   > 若要從AEM開始畫面檢視所有可用的範本，請導覽至 **工具** > **一般** > **範本**.

1. 在左上角，選取 **頁面資訊** 圖示並按一下 **頁面原則**.

   ![頁面原則功能表專案](../assets/style-cif-component/page-policy-menu.png)

1. 「頁面原則」會針對登入頁面範本開啟：

   ![頁面原則 — 登陸頁面](../assets/style-cif-component/page-policy-properties.png)

   在右側，您可以看到使用者端程式庫的清單 **類別** 包含在所有使用此範本的頁面上的資訊。

   * `venia.dependencies`  — 提供符合下列條件的任何廠商程式庫： `venia.site` 取決於。
   * `venia.site`  — 的類別 `clientlib-site` 該 `ui.frontend` 模組會產生。

   請注意，其他範本使用相同的原則， **內容頁面**， **登陸頁面**、等等。 透過重複使用相同原則，可確保在所有頁面上包含相同的使用者端程式庫。

   使用範本和頁面原則來管理使用者端資料庫之包含專案的優點在於，您可以根據範本變更原則。 例如，您可能在同一個AEM執行個體中管理兩個不同的品牌。 每個品牌都有其獨特風格或 *主題* 但基礎程式庫和程式碼相同。 另一個範例，如果您有一個大型使用者端程式庫，您只想讓它出現在某些頁面上，您可以為該範本制定唯一的頁面原則。

## 本機Webpack開發 {#local-webpack-development}

在上一個練習中，更新了 `ui.frontend` 模組，然後在執行Maven組建後，將變更部署到AEM。 接下來，您會考慮使用webpack-dev-server來快速開發前端樣式。

webpack-dev-server可代理來自AEM本機例項的影像和部分CSS/JavaScript，但可讓開發人員修改中的樣式和JavaScript `ui.frontend` 模組。

1. 在瀏覽器中導覽至 **首頁** 頁面和 **以發佈的形式檢視**： [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled).

1. 檢視頁面來源和 **複製** 頁面的原始HTML。

1. 返回您選擇的IDE，位於 `ui.frontend` 模組開啟檔案： `ui.frontend/src/main/static/index.html`

   ![靜態HTML檔案](../assets/style-cif-component/static-index-html.png)

1. 覆寫的內容 `index.html` 和 **貼上** 上一步中複製的HTML。

1. 尋找的「包含」 `clientlib-site.min.css`， `clientlib-site.min.js`、和 **移除** 它們。

   ```html
   <head>
       <!-- remove this link -->
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       ...
   </head>
   <body>
       ...
        <!-- remove this link -->
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
   </body>
   ```

   這些「include」會移除，因為它們代表產生的CSS和JavaScript編譯版本。 `ui.frontend` 模組。 將其他使用者端程式庫保留為即將從執行中的AEM例項代理的程式庫。

1. 開啟新的終端機視窗並瀏覽至 `ui.frontend` 資料夾。 執行命令 `npm start`：

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   此命令會啟動webpack-dev-server [http://localhost:8080/](http://localhost:8080/)

   >[!CAUTION]
   >
   > 如果您收到Sass相關錯誤，請停止伺服器並執行命令 `npm rebuild node-sass` 並重複上述步驟。 如果您有其他版本的 `npm` 和 `node` 比專案中指定的還多 `aem-cif-guides-venia/pom.xml`.

1. 導覽至 [http://localhost:8080/](http://localhost:8080/) 在與登入的AEM例項具有相同瀏覽器的新標籤中。 您應該會透過webpack-dev-server看到Venia首頁：

   ![連線埠80上的Webpack開發伺服器](../assets/style-cif-component/webpack-dev-server-port80.png)

   讓webpack-dev-server保持執行。 它將在下一個練習中使用。

## 實作產品Teaser的卡片樣式 {#update-css-product-teaser}

接下來，修改中的Sass檔案 `ui.frontend` 模組，實作產品Teaser的卡片樣式。 webpack-dev-server用於快速檢視變更。

返回IDE和生成的專案。

1. 在 **ui.frontend** 模組，重新開啟檔案 `_productteaser.scss` 在 `ui.frontend/src/main/styles/commerce/_productteaser.scss`.

1. 對產品Teaser邊框進行下列變更：

   ```diff
       .item__image {
   -       border: #ea00ff 8px solid;
   +       border-bottom: 1px solid #c0c0c0;
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

   儲存變更，webpack-dev-server應該會使用新樣式自動重新整理。

1. 在「產品Teaser」中新增投影並包含圓角。

   ```scss
    .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

1. 更新產品名稱以顯示於Teaser底部，並修改文字顏色。

   ```css
   .item__name {
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

1. 更新產品的價格，使其也出現在Teaser底部，並修改文字顏色。

   ```css
   .price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   
       ...
   ```

1. 更新底部的媒體查詢，以便在小於的畫面中棧疊名稱和價格 **992畫素**.

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

   您現在應該會看到卡片樣式反映在webpack-dev-server中：

   ![Webpack開發伺服器Teaser變更](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   不過，這些變更尚未部署至AEM。 您可以下載 [在此填入解決方案檔案](../assets/style-cif-component/_productteaser.scss).

1. 從命令列終端機，使用您的Maven技能將更新部署到AEM：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >還有其他的 [IDE設定和工具](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) 可將專案檔案直接同步至本機AEM執行個體，而不需執行完整的Maven建置。

## 檢視更新的產品Teaser {#view-updated-product-teaser}

將專案的程式碼部署到AEM後，您現在應該能夠檢視產品Teaser的變更。

1. 返回瀏覽器並重新整理首頁： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html). 您應該會看到已套用的更新產品Teaser樣式。

   ![已更新產品Teaser樣式](../assets/style-cif-component/product-teaser-new-style.png)

1. 新增其他產品Teaser以進行實驗。 使用「版面模式」來變更元件的寬度和位移，以在一列中顯示多個Teaser。

   ![多個產品預告](../assets/style-cif-component/multiple-teasers-final.png)

## 疑難排解 {#troubleshooting}

您可在中驗證 [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) 更新的CSS檔案已部署： [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

部署新的CSS檔案或JavaScript檔案（或兩者）時，請務必確保瀏覽器不會提供過時的檔案。 您可以清除瀏覽器快取或啟動新的瀏覽器工作階段，藉此消除此潛在問題。

AEM也會嘗試快取使用者端程式庫以提高效能。 在程式碼部署後，偶爾會提供舊檔案。 AEM您可以使用 [重新建置使用者端資料庫工具](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *如果您懷疑AEM已快取舊版的使用者端程式庫，建議使用讓快取失效的方法。 重建程式庫效率低下且耗時。*

## 恭喜 {#congratulations}

您已完成第一個AEM CIF核心元件的樣式，而且使用的是Webpack開發伺服器！

## 額外挑戰 {#bonus-challenge}

使用 [AEM樣式系統](/help/sites-cloud/authoring/page-editor/style-system.md) 以建立可由內容作者開啟或關閉的兩種樣式。 [使用樣式系統進行開發](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/style-system.html) 包括有關如何完成此工作的詳細步驟和資訊。

![額外挑戰 — 樣式系統](../assets/style-cif-component/bonus-challenge.png)

## 其他資源 {#additional-resources}

* [AEM專案原型](https://github.com/adobe/aem-project-archetype)
* [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)
* [設定本機AEM開發環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [用戶端資源庫](/help/implementing/developing/introduction/clientlibs.md)
* [AEM Sites快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
* [使用樣式系統進行開發](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/style-system.html)
