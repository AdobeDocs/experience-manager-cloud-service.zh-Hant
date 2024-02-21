---
title: AEM Forms Edge Delivery Service快速入門
description: 製作完美的表單，快速！ ⚡ AEM Forms Edge Delivery檔案式撰寫=超快的速度和SEO友善表單，適合更快樂的使用者和搜尋引擎。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f37a99cd5cbfb745cb591e3be2a46a5f52139cb2
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---


# 在AEM Forms Edge Delivery Service上建立表單

在當今的數位時代，建立好用的表單對於任何組織都至關重要。 AEM Forms Edge Delivery可讓您使用熟悉的工具(如Word或Google檔案)建立表單。

這些表單會直接將資料提交至Microsoft Excel或Google Sheets檔案，讓您能夠使用生動的生態系統以及Google Sheets、Microsoft Excel和Microsoft Sharepoint的強大API，輕鬆處理提交的資料或啟動現有的業務工作流程。

## 先決條件

* 您有Github帳戶。
* 您可以存取Google工作表或Microsoft SharePoint。
* 您瞭解Git、HTML、CSS和JavaScript的基本概念。
* 您已安裝Node和NPM以進行本機開發。

## 開始之前

* 設定並複製Edge Delivery Service (EDS)專案。 另請參閱 [開發人員教學課程](https://www.aem.live/developer/tutorial) 以取得詳細資訊。
* 原地複製 [Forms區塊存放庫](https://github.com/adobe/afb). 其中包含轉譯表單所需的表單區塊。

![Edge Delivery Forms快速入門](/help/edge/assets/getting-started-with-eds-forms.png)

## 將Form區塊新增至您的Edge Delivery Service (EDS)專案 {#add-forms-block-to-an-eds-project}

AEM Forms Edge Delivery包含表單區塊，可協助您輕鬆建立表單，以擷取及儲存擷取的資料。 若要將表單區塊納入您的Edge Delivery Service專案：

1. 導覽至本機開發環境上的Edge Delivery Service (EDS)專案資料夾。


   ```Shell
   cd [EDS Project folder]
   ```

1. 建立名為的資料夾 `form` 在EDS專案目錄下。 例如，在目錄下，EDS專案的名稱為 `Portal`，建立名為的資料夾 `form`.

   ```Shell
   mkdir form
   ```


1. 新增 [Forms區塊](https://github.com/adobe/afb/tree/main/blocks/form) 檔案移至&#39;form&#39;資料夾。

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   
   For example
   
   cp -R Documents/afb/blocks/form Documents/portal/blocks/
   ```

1. 將「表單」資料夾和基礎檔案簽入GitHub上的Edge Delivery Service專案。

   ```Shell
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   您現在已準備好呈現EDS表單。

   >[!NOTE]
   >
   > * 如果您的提取請求/eds專案建置失敗，且您遇到與匯入 `franklin-lib.js` 檔案中，更新匯入陳述式以參照 `aem.js` 檔案而非 `franklin-lib.js` 檔案。
   > * 如果您遇到任何絨毛錯誤，請隨時忽略它們。 若要略過Lint檢查，請導覽至package.json檔案，然後從更新「Lint」指令碼 `"lint": "npm run lint:js && npm run lint:css"` 至 `"lint": "echo 'skipping linting for now'"`. 然後，將變更提交到package.json檔案。

## 使用Microsoft Excel或Google工作表建立表單 {#create-a-form-for-an-eds-project}

允許網站開發人員建立表單，並選擇從網站訪客那裡收集哪些資訊可能會有所幫助。 作者可以使用試算表輕鬆設定表單，而不是複雜的程式。 他們需要新增正確的欄標題，然後使用表單區塊在網站上輕鬆顯示。 若要建立表單：

1. 在Microsoft SharePoint或Google Drive的AEM Edge Delivery專案目錄下，隨處建立Microsoft Excel活頁簿或Google工作表。

1. 確定AEM使用者(例如 `helix@adobe.com`)擁有工作表的編輯許可權。

1. 開啟您已建立的活頁簿，並將預設工作表的名稱變更為「shared-default」。

   ![將預設工作表重新命名為「shared-default」](/help/edge/assets/rename-sheet-to-helix-default.png)

1. 複製 [聯絡我們的試算表](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) 至您自己的試算表。

   ![聯絡我們的試算表](/help/edge/assets/contact-us-form-spreadsheet.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽和發佈工作表。

   預覽和發佈時，瀏覽器會開啟新標籤，以JSON格式顯示工作表內容。 請務必記下即時URL，因為這是之後轉譯表單的必要條件。

   URL 的格式是：

   ```shell
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

## 使用Edge Delivery Service (EDS)頁面預覽表單 {#add-a-form-to-your-eds-page}

到目前為止，您已為EDS專案啟用表單區塊，並準備好表單的結構。 現在，若要將表單加入EDS頁面並轉譯：

1. 前往Microsoft SharePoint或Google Drive上的AEM Edge Delivery專案目錄。

1. 若要將表單新增至頁面，請開啟對應的doc檔案。 例如，開啟索引檔案。

1. 導覽至檔案中您要新增表單的位置。

1. 將名為「Form」的區塊新增至檔案，類似於下方顯示的區塊。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   在第二列中，加入您在上一節中記下的URL作為超連結。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽和發佈頁面。 表單已轉譯。

   例如，以下是根據 [聯絡我們的試算表](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link)：


   ![聯絡我們（EDS表單）](/help/edge/assets/eds-form.png)

   表單區塊會轉譯表單，但尚未準備好接受資料。 按一下提交按鈕時，您會遇到類似下列的錯誤：

   ![表單提交時發生錯誤](/help/edge/assets/form-error.png)

   [準備您的工作表以接受資料](/help/edge/docs/forms/submit-forms.md). 您可以在準備接受資料後，將資料提交至工作表。


## 檢視更多

* [建立及預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單以傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈至網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [變更表單的主題和樣式](/help/edge/docs/forms/style-theme-forms.md)