---
title: 在通用編輯器中開始使用 AEM Forms 適用的 Edge Delivery Services - 開發人員教學課程
description: 本教學課程可協助您啟動並執行新的 Adobe Experience Manager Forms (AEM) 專案。在十至二十分鐘內，您便會在通用編輯器中建立自己的 Edge Delivery Services 表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 0e7375adb146c370a189127838d736290d1860ad
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 使用通用編輯器 (WYSIWYG) 開始使用 AEM Forms 適用的 Edge Delivery Services

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| 通用編輯器型製作 | 本文章 |
| 文件型製作 | [按一下這裡](/help/edge/docs/forms/tutorial.md) |


<span class="preview">您可以透過搶先體驗方案使用這項功能。若要請求存取權，請使用您的官方地址傳送電子郵件至 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，郵件內容需包含您的 GitHub 組織名稱和存放庫名稱。例如，若存放庫 URL 為 https://github.com/adobe/abc,，則組織名稱為 adobe，存放庫名稱為 abc。</span>

身處現今的數位時代，所有組織均需要建立簡單易用的表單。Edge Delivery Services 表單是使用通用編輯器所建立，提供 WYSIWYG (所見即所得) 功能。它提供現代、直覺易用的介面，能提高表單製作的效率。

AEM Forms 會提供一個稱為「最適化表單區塊」的區塊，協助您輕鬆建立 Edge Delivery Services 表單來擷取和儲存資料。您可以[建立使用最適化表單區塊預先設定的新 AEM 專案](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，或[將最適化表單區塊新增至現有 AEM 專案](#add-adaptive-forms-block-to-your-existing-aem-project)。

![Github 存放庫工作流程](/help/edge/assets/repo-workflow.png){width=auto}

此教學課程將指導您使用通用編輯器的所見即所得製作功能，在新的或現有的 Adobe Experience Manager Site 專案中，建立、預覽和發佈您自己的表單。

## 先決條件

* 您擁有 GitHub 帳戶，並且了解 Git 基本知識。
* 您了解 HTML、CSS 和 JavaScript 的基本知識。
* 您已安裝 Node/npm 可進行本機開發。

## 建立一個預先設定最適化表單區塊的新 AEM 專案

AEM Forms 範本可協助您很快開始使用預先設定最適化表單區塊的 AEM 專案。這是遵守 AEM 最佳做法最快、最簡單的方式，而且直接開始建立表單。

### 開始使用 AEM Forms 範本的存放庫範本

1. 為您的 AEM 專案建立 GitHub 存放庫。若要建立存放庫：
   1. 前往 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) 。

      ![AEM Forms 範本](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. 按一下「**使用此範本**」選項，然後選取「**建立新存放庫**」選項。

      ![使用 AEM Forms 範本建立新存放庫](/help/edge/docs/forms/assets/use-eds-form-template.png)

      接著開啟「**建立新存放庫**」畫面。

   1. 在「**建立新存放庫**」畫面，選取&#x200B;**所有者**，並指定「**存放庫名稱**」。Adobe 建議將存放庫設定為「**公開**」。因此，選取「**公開**」選項，然後按一下「**建立存放庫**」。

      ![將存放庫設定為公開](/help/edge/docs/forms/assets/name-eds-repo.png)

1. 在您的存放庫上安裝 AEM Code Sync GitHub 應用程式。若要安裝：
   1. 前往 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new) 。
   1. 在「**安裝 AEM Code Sync**」畫面，選取「**僅選取存放庫**」選項，然後選取新建立的存放庫。按一下「**儲存**」。

   ![將存放庫設定為公開](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. 現在將您使用 AEM Forms 範本建立的 GitHub 存放庫連結至您的 AEM 專案製作環境。若要連接：

   1. 前往您先前使用 AEM Forms 範本建立的 GitHub 存放庫。
   1. 在根資料夾中新增&#x200B;**fstab.yaml**&#x200B;檔案。

      ![開啟 fstab.yaml 檔案](/help/edge/docs/forms/assets/open-fstab.png)

   1. 將專案的掛接點新增至&#x200B;**fstab.yaml**&#x200B;檔案。 新增AEM as a Cloud Service編寫執行個體的URL。

      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![編輯 fstab.yaml 檔案](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. 在新增參考且一切看起來正常之後，提交&#x200B;**fstab.yaml**&#x200B;檔案。

      ![認可變更](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      如果您遇到任何建置問題，請參閱「[解決 GitHub 建置問題](#troubleshooting-github-build-issues)」。

### 建立新 AEM 專案

現在您有 GitHub 專案，您可以繼續在 AEM as a Cloud Service 製作執行個體建立並發佈 AEM 專案。

1. 若要建立新 AEM 專案：

   1. 登入 AEM as a Cloud Service 製作執行個體，並選取「**網站**」。

      ![選取網站](/help/edge/assets/select-sites.png)

   1. 按一下「**建立** > **來自範本的網站**」。

      ![建立網站](/help/edge/docs/forms/assets/create-sites.png)

   1. 選取 Edge Delivery Services 網站範本並按一下「**下一步**」。

      ![選取網站範本](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * 如果在您的製作執行個體無法使用 Edge Delivery Services 網站範本，請按一下「匯入」按鈕以上傳範本。
      > * 您可以從 [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases) 下載 Edge Delivery Services 網站範本。

   1. 輸入下列詳細資訊以建立新的 AEM 專案：
      * **網站標題** - 為網站新增描述性標題。
      * **網站標題** - 使用您在上一個步驟定義的 `site-name`。
      * **GitHub URL** - 使用您在上一個步驟中建立的 GitHub 專案 URL。

      ![建立 AEM Site](/help/edge/docs/forms/assets/create-aem-site.png)

   1. 接著顯示「**建立網站**」對話框，按一下「**確定**」。

      ![按一下確定](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      只需幾分鐘，您的新 AEM 專案即建立完成。

   1. 在 Sites 主控台瀏覽至您新建立的 AEM 專案，然後按一下「**編輯**」。在此案例中，`index.html` 頁面用於插圖。

      ![編輯 AEM Site](/help/edge/docs/forms/assets/edit-site.png)

      在通用編輯器中以新索引標籤開啟 AEM 專案，啟用 WYSIWYG 製作。您現在可以編輯您的 AEM 專案。

      ![在通用編輯器中開啟網站](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. 發佈您建立的 AEM 專案

   完成 AEM 專案編輯後發佈。若要發佈：

   1. 在 Sites 主控台，選取所有 AEM 專案頁面，然後按一下「**快速發佈**」。

      ![發佈 AEM Sites 專案](/help/edge/docs/forms/assets/publish-sites.png)

   1. 接著顯示「**快速發佈**」確認對話框，按一下「**發佈**」以開始發佈流程。

      ![快速發佈確認對話框](/help/edge/docs/forms/assets/quick-publish.png)

      或者，您可以直接從通用編輯器使用者介面發佈 AEM 專案頁面。

      ![快速發佈確認對話框](/help/edge/docs/forms/assets/qui.png)

   恭喜！您有一個在  `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/` 上執行的新網站。

   * `<branch>`是指 GitHub 存放庫的分支。
   * `<repository>`表示您的 GitHub 存放庫。
   * `<owner>`是指託管 GitHub 存放庫的 GitHub 帳戶使用者名稱。
   * `<site-name>` 是指您建立的網站名稱。

   例如，如果分支名稱為 `main`，存放庫為 `edsforms`，而所有者為 `wkndforms`，且 `site-name` 為 `eds-forms`，則網站將會在 `https://main--edsforms--wkndforms.aem.page/content/eds-forms/` 啟動並運作

   >[!NOTE]
   >
   > * 若要檢視 AEM 專案的 `index.html` 頁面，請使用下列 URL：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * 若要檢視 AEM 專案的 `index page` 其他頁面，請使用下列 URL：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

現在您可以開始[建立表單並將其新增至 AEM 專案](#add-edge-delivery-services-forms-to-aem-project)。

## 將最適化表單區塊新增至您現有的 AEM 專案

如果擁有現有的 AEM 專案，您可以將自適應表單區塊整合至目前專案中，並開始建立表單。

>[!NOTE]
>
>
> 此步驟適用於使用 [ AEM 範本 XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk) 建置的專案。如果您使用 [AEM Forms 範本](https://github.com/adobe-rnd/aem-boilerplate-forms)建立 AEM 專案，即可省略此步驟。

若要整合：

1. 導覽至本機系統上的 AEM 專案存放庫資料夾。

1. 從 [AEM Forms 範本](https://github.com/adobe-rnd/aem-boilerplate-forms)複製下列資料夾和檔案，並貼到您的 AEM 專案中：

   * [表單區塊](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form)資料夾
   * [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) 檔案
   * [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) 檔案
1. 導覽至 AEM 專案中的 `/scripts/editor-support.js` 檔案，並使用 [AEM Forms 範本中 editor-support.js 檔案](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)來更新檔案
1. 導覽至 AEM 專案中的 `/models/_section.json`，並將「form」和「embed-adaptive-form」附加至 `filters` 物件的元件陣列：

   ```
       "filters": [
       {
     "id": "section",
     "components": [
       .
       .
       .
       "form",
       "embed-adaptive-form"
     ]
    }]
   ```

1. (選用) 導覽至 AEM 專案中的 `/.eslintignore`，並新增下列數行程式碼：

   ```
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

1. (選用) 導覽至 AEM 專案中的 `/.eslintrc.js`，並在 `rules` 物件中新增下列數行程式碼：

   ```
   'xwalk/max-cells': ['error', {
     '*': 4, // default limit for all models
     form: 15,
     wizard: 12,
     'form-button': 7,
     'checkbox-group': 20,
     checkbox: 19,
     'date-input': 21,
     'drop-down': 19,
     email: 22,
     'file-input': 20,
     'form-fragment': 15,
     'form-image': 7,
     'multiline-input': 23,
     'number-input': 22,
     panel: 17,
     'radio-group': 20,
     'form-reset-button': 7,
     'form-submit-button': 7,
     'telephone-input': 20,
     'text-input': 23,
     accordion: 14,
     modal: 11,
     rating: 18,
     password: 20,
     tnc: 12,
   }],
   'xwalk/no-orphan-collapsible-fields': 'off', // Disable until enhancement is done for Forms properties
   ```

1. 開啟終端機並執行下列命令：

   ```
   npm i
   npm run build:json
   ```

   >[!NOTE]
   >
   > 將變更推送至 GitHub 上的 AEM 專案存放庫之前，請確保位於 AEM 專案根目錄層級的 `component-definition.json`、`component-models.json`，以及 `component-filters.json` 檔案已使用表單相關物件進行更新。

1. 認可和推播這些變更至 GitHub 的 AEM 專案存放庫。

   <!--
    1. **Update ESLint configuration file**
    2. Navigate to the `../.eslintignore` file in your AEM Project and add the following line of codes to prevent errors related to the Form Block rule engine:
        
            blocks/form/rules/formula/*
            blocks/form/rules/model/*
       * [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common)  folder
       * [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components) folder
    
     3. **Update component definitions and models files**
       1. Navigate to the `../models/_component-definition.json` file in your AEM Project and update it with the changes from the [_component-definition.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48).
    
    3. Navigate to the `../models/_component-models.json` file in your AEM Project and update it with the changes from the [_component-models.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26) -->

就是這樣！最適化表單區塊現在是您 AEM 專案的一部分。您可以[開始建立並新增表單至 AEM 專案](#add-edge-delivery-services-forms-to-aem-site-project)。

## 使用 WYSIWYG 製作表單

您可以在通用編輯器中開啟 AEM 專案進行 WYSIWYG 製作，您可以編輯專案並新增最適化表單區段，以在 AEM 專案頁面上包含 Edge Delivery Services 表單。

1. 新增最適化表單區段至您的 AEM 專案頁面。若要新增：
   1. 在 Sites 主控台中瀏覽至您的 AEM 專案，選取要編輯的網站頁面，然後按一下「**編輯**」。AEM 專案頁面隨即會在通用編輯器中開啟，以進行編輯。
在此案例中，`index.html` 頁面用於插圖。
   1. 開啟內容樹並瀏覽至您想要新增最適化表單區段的區段。
   1. 按一下「**[!UICONTROL 新增]**」圖示，然後從元件清單選取「**[!UICONTROL 最適化表單]**」元件。

   ![內容樹](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   最適化表單區段已新增。您現在可以開始新增表單元件至 AEM 專案頁面。

1. 新增表單元件至所新增的最適化表單區段。若要新增表單元件：
   1. 瀏覽至內容樹中已新增的最適化表單區段。

      ![已新增最適化表單區塊](/help/edge/docs/forms/assets/adative-form-block.png)


   1. 按一下「**[!UICONTROL 新增]**」圖示，然後從&#x200B;**最適化表單元件**&#x200B;清單新增所需元件。

      ![新增元件](/help/edge/docs/forms/assets/add-component.png)

      您也可以拖放所需的最適化表單元件，因為通用編輯器提供直覺易用的拖放功能。

   1. 選取已新增的最適化表單元件並使用 **[!UICONTROL 屬性]** 來更新其屬性。

      ![開啟屬性](/help/edge/docs/forms/assets/component-properties.png)

   1. 預覽表單。
下列螢幕擷圖顯示使用 WYSIWYG 製作在 AEM 專案中製作的表單：

      ![新增表單](/help/edge/docs/forms/assets/added-form-aem-sites.png)

      一旦對預覽滿意，使用者即可繼續進行頁面的發佈。

      >[!NOTE]
      >
      > 進行變更後再次發佈 AEM 專案頁面很重要；否則，更新無法在瀏覽器中顯示。

1. 重新發佈 AEM 專案頁面。

   1. 新增表單後，按一下「**發佈**」來再次發佈 AEM 專案頁面。

      ![發佈表單](/help/edge/docs/forms/assets/publish-form.png)

   1. 在畫面顯示「**發佈**」確認對話框，按一下「**發佈**」以開始發佈。

      ![發佈表單 1](/help/edge/docs/forms/assets/publish-form1.png)

      按一下「**發佈**」按鈕後，會顯示 `Publish started successfully` 訊息。

      ![發佈表單 2](/help/edge/docs/forms/assets/publish-form2.png)

   您現在可以在下列 URL 中檢視已新增 Edge Delivery Services 表單的 AEM 專案頁面：
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`。

   例如，如果分支名稱為 `main`，存放庫為 `edsforms`，而所有者為 `wkndforms`，且網站名稱為 `eds-forms`，此 URL 將為：
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![索引頁面](/help/edge/docs/forms/assets/publish-index-page.png)

您可以透過編輯最適化表單區塊中的 `.css` 和 `.js` 檔案，設定 Edge Delivery Services 表單的外觀樣式，並[設定本機 AEM 開發環境](#set-up-local-aem-development-environment) 以立即在瀏覽器中檢視變更。

>[!NOTE]
>
> 您也可以[在通用編輯器中製作獨立表單，並將其發佈至 Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md)。

## 設定本機 AEM 開發環境

您可以設定本機 AEM 開發環境，用於在本機開發自訂樣式和元件。若要啟動並運作本機 AEM 開發環境：

1. **安裝 AEM CLI**：AEM CLI 簡化開發任務。讓我們使用 npm 進行全域安裝：

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **原地複製您的 GitHub 專案**：使用下列命令從 GitHub 原地複製您的 AEM 專案存放庫，取代為 &lt;owner> 存放庫所有者和 &lt;repo> 存放庫名稱：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **啟動您的本機環境**：瀏覽至您的專案目錄並使用單一命令啟動本機 AEM 執行個體：

   ```
   cd <repo>
   aem up
   ```

您可以在最適化表單區塊 `blocks/form` 資料夾中進行本機變更，以設定表單的樣式和編碼！編輯此目錄中的 `.css` 或 `.js` 檔案，您可以看見瀏覽器立即反映那些變更。

完成變更後，使用 Git 命令來認可和推播。這樣會更新可在下列 URL 存取的預覽和生產環境 (使用您的專案詳細資訊取代預留位置)：

預覽：`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`

生產：`https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## 疑難排解 GitHub 建置問題

解決潛在問題以確保 GitHub 建置流程順利進行：

* **處理 Linting 錯誤：**&#x200B;如果您遇到任何 linting 錯誤，您可以略過不予處理。開啟 [EDS Project]/package.json 檔案並將 &quot;lint&quot; 指令碼從 `"lint": "npm run lint:js && npm run lint:css"` 修改為 `"lint": "echo 'skipping linting for now'"`。儲存檔案並將變更提交至您的 GitHub 專案。

* **解析模組路徑錯誤：**
如果遇到錯誤「無法解析模組路徑 &#39;/scripts/lib-franklin.js&#39;」，請導覽至 [EDS Project]/blocks/forms/form.js 檔案。將 lib-franklin.js 檔案更換為 aem.js 檔案來更新匯入語句。

## 另請參閱

{{universal-editor-see-also}}
