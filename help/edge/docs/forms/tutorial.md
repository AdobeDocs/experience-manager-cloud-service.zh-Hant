---
title: 開始使用 AEM Forms 適用的 Edge Delivery Services - 開發人員教學課程
description: 本教學課程可協助您啟動並執行新的 Adob​​e Experience Manager (AEM) Forms 專案。您將在 10 到 20 分鐘內建立好自己的表單。
feature: Edge Delivery Services
exl-id: bb7e93ee-0575-44e1-9c5e-023284c19490
role: Admin, Architect, Developer
source-git-commit: 744f505c8e97b6ca6947b685ddb1eba41b370cfa
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 97%

---

# 快速入門 - 開發人員教學課程

身處今日數位時代，任何組織都需要建立對使用者友善的表單。適用於AEM Forms的Edge Delivery Services可讓您使用熟悉的工具(如Google Docs和Microsoft Office)來建立表單。

這些表單可直接提交資料至 Microsoft Excel 或 Google Sheets 檔案，讓您能夠使用由 Google Sheets、Microsoft Excel 和 Microsoft SharePoint 等強大 API 建構的活躍生態系統，以便輕鬆處理提交的資料或啟動現有的業務工作流程。

AEM Forms 會提供一個區塊 (名為最適化表單區塊)，協助您輕鬆建立表單來擷取和儲存擷取的資料。您可以[建立已預先設定最適化表單區塊的全新 AEM 專案](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) <!--or [add the Adaptive Forms Block to an existing AEM project](#add-adaptive-forms-block-to-your-existing-aem-project)-->。

此 AEM Forms 教學課程將引導您使用新的 Adob&#x200B;&#x200B;e Experience Manager (AEM) Forms 專案建立、預覽和發佈您自己的自訂表單。

## 先決條件

* 您擁有 GitHub 帳戶，並且了解 Git 基本知識。
* 您擁有 Google 或 Microsoft SharePoint 帳戶。
* 您了解 HTML、CSS 和 JavaScript 的基本知識。
* 您已安裝 Node/npm 可進行本機開發。

**請注意！** 本教學課程使用 macOS、Chrome 和 Visual Studio Code。雖然這些步驟可調整以適用於其他設定，但螢幕擷圖和特定 UI 元素可能會根據您選擇的作業系統、瀏覽器和程式碼編輯器而有所不同。


## 建立一個預先設定最適化表單區塊的新 AEM 專案

AEM Forms 範本可協助您很快開始使用預先設定最適化表單區塊的 AEM 專案。這是遵守 AEM 最佳實務進行，且是直接開始建立表單的最快、最簡單的方法。

### 開始使用 AEM Forms 範本的存放庫範本

1. 為您的 AEM 專案建立 GitHub 存放庫。若要建立存放庫：
   1. 前往 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) 。

      ![AEM Forms 範本](/help/edge/assets/aem-forms-boilerplate.png)
   1. 按一下「**使用此範本**」選項，然後選取「 **建立新存放庫**」選項。建立新存放庫畫面會開啟。

      ![使用 AEM Forms 範本建立新存放庫](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. 在建立新存放庫畫面上，選取「**所有者**」，並指定「**存放庫名稱**」 。Adobe 建議將存放庫設定為 「**公開**」。因此，選取「**公開**」選項，然後按一下「**建立存放庫**」。

   ![將存放庫設定為公開](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. 在您的存放庫上安裝 AEM Code Sync GitHub 應用程式。若要安裝：
   1. 前往 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new) 。
   1. 在「安裝 AEM Code Sync」畫面上，選取「**僅選取存放庫**」選項，然後選取您新建立的存放庫。按一下「儲存」。

   ![將存放庫設定為公開](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > 如果您使用GitHub Enterprise搭配IP篩選，您可以將下列IP新增至允許清單： 3.227.118.73

   恭喜！您有一個在  `https://<branch>--<repo>--<owner>.aem.page/` 上執行的新網站。

   * `<branch>`是指 GitHub 存放庫的分支。
   * `<repository>`表示您的 GitHub 存放庫。
   * `<owner>`是指託管 GitHub 存放庫的 GitHub 帳戶使用者名稱。

   例如，如果分支名稱為 `main`，存放庫為 `wefinance`，而所有者為 `wkndforms`，則網站會在 `https://main--wefinance--wkndforms.aem.page` &lt;! 啟動並運作。--(https://main--wefinance--wkndform.aem.page)-->

### 連結您自己的內容來源

<!--Your newly created GitHub repository points to [example content stored in a Google Drive folder](https://drive.google.com/drive/folders/1bvjfi6TqpYA7DvbX6kKc-m7FgHuJ4RUQ). This read-only content provides a great starting point for your forms. Feel free to copy it into your own Google Drive and customize it to fit your needs.

![Sample Content on Google Drive](/help/edge/assets/folder-with-sample-content.png)-->

若要將範例內容複製到您自己的內容資料夾，並將 GitHub 存放庫指向您自己的內容資料夾：

1. 在 Google Drive 或 Microsoft SharePoint 中專為您的 AEM 內容建立一個新資料夾。本文件是使用建立在 Microsoft SharePoint 的資料夾。

1. 與 Adob&#x200B;&#x200B;e Experience Manager 使用者 (forms@adobe.com) 共用該資料夾。

   ![使用「管理存取」選項與 AEM 使用者共用資料夾 - SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![使用「管存」取,選項與 AEM 使用者共用資料夾 - Google Drive](/help/edge/assets/share-google-drive-folder.png)


   確保您已向 Adob&#x200B;&#x200B;e Experience Manager 使用者提供該資料夾的編輯權限。

   ![與 AEM 使用者共用資料夾，提供編輯權限-SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png){width=50%}

   ![與 AEM 使用者共用資料夾，提供編輯權限 - Google Drive](/help/edge/assets/add-aem-user-google-folder.png){width=50%}

1. 將[範例內容](/help/edge/assets/wefinance1.zip)複製到您的資料夾。若要複製：

   1. 解壓縮已下載的資料夾並複製內容。

      ![下載範例內容](/help/edge/assets/download-sample-content.png)

      `nav` 和 `footer` 檔案是定義頁面的基本版面，並且在整個專案中很少有變動。檔案還具有與大多數其他內容檔案不同的特定結構。檢視這些檔案即可了解 AEM 專案中的內容是如何組織。


   1. 將這些檔案上傳到 Microsoft SharePoint 或 Google Drive 資料夾。

      ![Google Drive 上的範例內容](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      確保您將範例內容的`enquiry`工作表複製至 Google Drive 或 Microsoft SharePoint 上的資料夾。 此工作表含有範本表單的結構。

1. 現在您已經設定了內容資料夾，您應該可將資料夾連結到先前使用 AEM Forms 範本在 GitHub 建立的專案。 若要連接：

   1. 前往您先前使用 AEM Forms 範本建立的 GitHub 存放庫。
   1. 開啟 `fstab.yaml` 進行編輯。
   1. 將現有參照更換為您與 AEM 使用者共用的資料夾路徑 (forms@adobe.com)。

      ![Google Drive 上的範例內容](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      如果您使用 Microsoft SharePoint，則資料夾路徑採用下列格式：

      ```HTML
      https://<tenant>.SharePoint.com/sites/<sp-site>/Shared%20Documents/<folder-name>
      ```

      例如，

      ```HTML
      https://adobe.SharePoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      如需更多有關在 Microsoft SharePoint 中管理檔案的資訊，請參閱「[如何使用 Adobe SharePoint](https://www.aem.live/docs/setup-customer-sharepoint)」。


   1. 您更新參照且一切看起來沒問題，就可提交更新的 `fsatb.yaml` 檔案。 如果您遇到任何建置問題，請參閱「[解決 GitHub 建置問題](#troubleshooting-github-build-issues)」。

      ![提交更新的 fsatab.yaml 檔案](/help/edge/assets/commit-updated-fstab-yaml.png)

      這樣即可將您的內容資料夾連結到您的網站。 更新參照後，您最初可能會遇到「404 Not Found」錯誤。 這是因為您的內容還沒過預覽。 下一部分將介紹如何開始製作和預覽內容。



### 預覽和發佈您的內容

完成最後一個步驟之後，您的新內容來源並非空值，但在前進至預覽或上線階段之前，在您的網站上不會看到此內容。 目前，這可能會導致 404 錯誤。

若要預覽未發佈的內容：

1. 安裝名為 [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo) 的 Chrome 擴充功能 。

   ![安裝 AEM SideKick](/help/edge/assets/install-aem-sidekick.png)

   安裝擴充功能至 Chrome 後，記得要釘選以便輕鬆找到。

   ![釘選 AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. 若要設定 Sidekick Chrome 擴充功能，請前往先前共用的 Google Drive 或 Microsoft SharePoint 資料夾，然後按滑鼠右鍵點選瀏覽器工具列中的擴充功能圖示，然後選取「`Add this project`」。

   ![AEM Sidekick - 新增專案](/help/edge/assets/aem-sidekick-add-a-project.png)

   安裝擴充功能並新增專案後，您就可以預覽並發佈 Google Drive 的內容。

1. 選取 Microsoft SharePoint 或 Google Drive 資料夾中的所有文件。 您可以在點選時長按 Ctrl 鍵 (Windows/Linux) 或 Cmd 鍵 (Mac) 以選擇多個文件。

   ![選取所有檔案](/help/edge/assets/select-all-files.png)

1. 按一下釘選至 Chrome 擴充功能列的 AEM Sidekick 圖示。 螢幕上會出現一個工具列。 您可以選擇預覽或發佈您的內容。

   如果您複製`index`、`nav`、`footer`和`enquiry`檔案過來，這些都是有其個別預覽和發佈週期的文件，因此請確保預覽 (和發佈) 所有這些檔案。

   預覽檔案後，新的瀏覽器標籤會顯示這些文件。 若要預覽範例表單，請前往以下 URL：


   ```HTML
   https://<branch>--<repository>--<owner>.aem.live
   ```

   * `<branch>`是指 GitHub 存放庫的分支。
   * `<repository>`表示您的 GitHub 存放庫。
   * `<owner>`是指託管 GitHub 存放庫的 GitHub 帳戶使用者名稱。


   `https://<branch>--<repo>--<owner>.aem.page/enquiry` URL.

   例如，如果您的專案存放庫名為 &quot;wefinance&quot; (位於帳戶所有者 &quot;wkndform&quot; 下面)，並且您使用的是 &quot;main&quot; 分支，表單名稱為 `enquiry`，則 URL 為：`https://main--wefinance--wkndform.aem.live/enquiry`。
&lt;!--(https://main--wefinance--wkndform.aem.live/enquiry).-->

### 建立表單

範例內容包含一個「查詢」工作表，這是「查詢」表單的範本。 工作表的每一列代表一個[表單欄位](/help/edge/docs/forms/form-components.md#available-components)，且欄標題定義[欄位屬性](/help/edge/docs/forms/form-components.md#available-components)。 使用此範例表單，讓您在建立表單上佔有優勢。

![查詢表單](/help/edge/docs/forms/assets/enquiry-form-microsoft-sharepoint.png)

讓我們從更新欄位標籤開始。 開啟「查詢」表進行編輯，將提交按鈕的標籤變更為`Let's Talk`，並使用 AEM Sidekick 預覽和發佈檔案。

![查詢表單](/help/edge/assets/enquiry-form-preview-publish.png)

當您預覽或發佈檔案時，該檔案的 JSON 版本將顯示在新標籤中。 複製預覽 (.aem.page) 或發佈檔案的 (.aem.live) URL。

![表單試算表的 JSON](/help/edge/assets/preview-and-publish-enquiry-form.png)

開啟 `enquiry` 檔案，並將表單區塊中的 URL 更換為上一個步驟中複製的檔案 URL。 確保 URL 是超連結。

![有試算表 URL 的 .json URL 的查詢檔案](/help/edge/assets/enquiry-doc-to-embed-form.png)

使用 AEM Sidekick 預覽和發佈查詢文件。

![有試算表 URL 的 .json URL 的查詢檔案](/help/edge/assets/preview-and-publish-enquiry-document.png)


若要預覽更新後的查詢表單，請往下列 URL：


```HTML
    https://<branch>--<repository>--<owner>.aem.page/enquiry
       
```

提交按鈕的標籤更新為 `Let's Talk`。

![查詢表單](/help/edge/assets/updated-form.png)

&lt;!--(https://main--wefinance--wkndform.aem.live/enquiry)-->

URL：`https://main--wefinance--wkndform.aem.live/enquiry`
&lt;!--(https://main--wefinance--wkndform.aem.live/enquiry)-->


若需要建立和發佈新表單的詳細資訊，請參閱「[建立表單](/help/edge/docs/forms/create-forms.md)」指南。

### 開始開發樣式和功能


若要立即啟動並運作本機 AEM 開發環境：

1. 安裝 AEM CLI：AEM CLI 簡化了開發任務。讓我們使用 npm 進行全域安裝：

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. 複製您的 GitHub 專案：使用以下命令從 GitHub 原地複製您的專案存放庫，更換為 <owner> 存放庫所有者和 <repo> 存放庫名稱：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. 啟動您的本機環境：瀏覽至專案目錄並使用單一命令來啟動本機 AEM 執行個體：

   ```
   cd <repo>
   aem up
   ```

最適化表單區塊 `blocks/form` 資料夾是您設定表單樣式和程式碼的場域！編輯此目錄中的任何 `.css` 或 `.js` 檔案，這些變更會立即反映在您的瀏覽器中。

準備好展示您的創作了嗎？使用 Git 提交並推播您的變更。這將更新可在這些 URL 存取的預覽和生產環境 (將預留位置更換為您的專案詳細資訊)：

預覽：`https://<branch>--<repo>--<owner>.aem.page/`
生產：`https://<branch>--<repo>--<owner>.aem.live/`

恭喜！您已成功設定本機開發環境並部署好您的變更。


<!--
## Add Adaptive Forms Block to your existing AEM project


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

If you have an existing AEM Project, you can integrate the Adaptive Forms Block into your current project to get started on form creation. 

>[!NOTE]
>
>
> This step applies to projects built with the [AEM Boilerplate](https://github.com/adobe/aem-boilerplate). If you created your AEM project using the [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms), you can skip this step.

To Integrate:

1. **Add required files and folders**
   1. Copy and paste the following folders and files from the [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms) into your AEM Project:

      * [form block](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form)  folder
       * [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common)  folder
       * [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components) folder
       * [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) file
       * [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) file

1. **Update component definitions and models files**
    1. Navigate to the `../models/_component-definition.json` file in your AEM Project and update it with the changes from the [_component-definition.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48).
    
    1. Navigate to the `../models/_component-models.json` file in your AEM Project and update it with the changes from the [_component-models.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26)

1. **Add Form Editor in editor script**
    1. Navigate to the `../scripts/editor-support.js` file in your AEM Project and update it with the changes from the [editor-support.js file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js#L105-L106)
1. **Update ESLint configuration file**
    1. Navigate to the `../.eslintignore` file in your AEM Project and add the following line of codes to prevent errors related to the Form Block rule engine:
        ```
            blocks/form/rules/formula/*
            blocks/form/rules/model/*
        ```

1. Commit and push these changes to your AEM Project repository on GitHub.

That's it! The Adaptive Forms Block is now part of your AEM project. You can start creating and adding forms to your AEM pages.
-->

## 疑難排解 GitHub 建置問題

解決潛在問題以確保 GitHub 建置流程順利進行：

* **解決模組路徑錯誤：**
如果遇到「無法解決 &quot;../../scripts/lib-franklin.js&quot; 模組的路徑」錯誤，請瀏覽至 [EDS Project]/blocks/forms/form.js 檔案。透過將 lib-franklin.js 檔案更換為 aem.js 檔案來更新匯入語句。

* **處理 Linting 錯誤：**&#x200B;如果您遇到任何 linting 錯誤，您可以略過不予處理。開啟 [EDS Project]/package.json 檔案並將 &quot;lint&quot; 指令碼從 `"lint": "npm run lint:js && npm run lint:css"` 修改為 `"lint": "echo 'skipping linting for now'"`。儲存檔案並將變更提交至您的 GitHub 專案。


## 另請參閱

{{see-more-forms-eds}}
