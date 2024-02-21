---
title: AEM Forms Edge Delivery Service快速入門
description: 製作完美的表單，快速！ ⚡ AEM Forms Edge Delivery檔案式撰寫=超快的速度和SEO友善表單，適合更快樂的使用者和搜尋引擎。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: b94bd6cd70af541444fda1d03f502b4588fd879b
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---


# 在AEM Forms Edge Delivery Service上建立表單

在當今的數位時代，建立好用的表單對於任何組織都至關重要。 AEM Forms Edge Delivery可讓您使用熟悉的工具(如Word或Google檔案)建立表單。

這些表單會直接將資料提交至Microsoft Excel或Google Sheets檔案，讓您能夠使用生動的生態系統以及Google Sheets、Microsoft Excel和Microsoft Sharepoint的強大API，輕鬆處理提交的資料或啟動現有的業務工作流程。

## 先決條件

* 您有GitHub帳戶。
* 您可以存取Google工作表或Microsoft SharePoint。
* 您瞭解Git、HTML、CSS和JavaScript的基本概念。
* 您已安裝Node和NPM以進行本機開發。

## 開始之前

* 設定並複製您的邊緣傳遞服務(EDS)專案。 另請參閱 [開發人員教學課程](https://www.aem.live/developer/tutorial) 以取得詳細資訊。
* 原地複製 [Forms區塊存放庫](https://github.com/adobe/afb). 其中包含轉譯表單所需的表單區塊。

![Edge Delivery Forms快速入門](/help/edge/assets/getting-started-with-eds-forms.png)

## 將Form區塊新增至您的Edge Delivery Service (EDS)專案 {#add-forms-block-to-an-eds-project}

AEM Forms Edge Delivery包含表單區塊，可協助您輕鬆建立表單，以擷取及儲存擷取的資料。 若要將表單區塊納入您的Edge Delivery Service專案：

1. 導覽至 `blocks` 位於本機開發環境上Edge Delivery Service (EDS)專案資料夾中的資料夾。


   ```Shell
   cd [EDS Project folder]/blocks
   ```

1. 建立名為的資料夾 `form` 在 `blocks` 目錄。 例如，在目錄下，EDS專案的名稱為 `Portal`，建立名為的資料夾 `form`.

   ```Shell
   mkdir form
   ```


1. 新增 [Forms區塊](https://github.com/adobe/afb/tree/main/blocks/form) 檔案移至&#39;form&#39;資料夾。

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   ```

   **例如，**


   ```shell
   cp -R ../../afb/blocks/form ../../fantastic-computing-machine/blocks 
   ```



1. 將「表單」資料夾和基礎檔案簽入GitHub上的Edge Delivery Service專案。

   ```Shell
   cd ..
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   表單區塊會新增至您的EDS專案。 您現在可以建立表單，並將其新增至您的網站。

   >[!NOTE]
   >
   > * 如果您遇到「無法解析模組&#39;&#39;&#39;../../scripts/lib-franklin.js&#39;&#39;的路徑」錯誤，請開啟 `[EDS Project]/blocks/forms/form.js` 檔案。 在匯入陳述式中，將 `franklin-lib.js` 含下列專案的檔案： `aem.js` 檔案。
   > * 如果您遇到任何絨毛錯誤，請隨時忽略它們。 若要略過內嵌檢查，請開啟 `[EDS Project]\package.json` 檔案並更新「lint」指令碼，從 `"lint": "npm run lint:js && npm run lint:css"` 至 `"lint": "echo 'skipping linting for now'"`. 儲存檔案並將其提交至您的GitHub專案。

## 使用Microsoft Excel或Google工作表建立表單 {#create-a-form-for-an-eds-project}

您可以使用試算表輕鬆建立表單，而不是複雜的程式。 您可以先將列和欄標題新增至試算表，其中每一列定義一個表單欄位，每一欄標題定義對應表單欄位的屬性。

例如，在下列試算表中，列會定義 `contact us` 表單和欄標題定義對應欄位的屬性。

![聯絡我們的試算表](/help/edge/assets/contact-us-form-spreadsheet.png)

若要建立表單：

1. 在Microsoft SharePoint或Google Drive上開啟AEM Edge Delivery專案資料夾。

1. 在AEM Edge Delivery專案目錄下的任何位置，建立Microsoft Excel活頁簿或Google工作表。 例如，建立名為 `contact-us` 在Google Drive上的AEM Edge Delivery專案目錄下。

1. 請確定工作表已與AEM使用者共用(例如 `helix@adobe.com`) [已針對您的專案進行設定](https://www.aem.live/docs/setup-customer-sharepoint) 且使用者擁有工作表的編輯許可權。

1. 開啟您建立的試算表，並將預設工作表的名稱變更為「shared-default」。

   ![將預設工作表重新命名為「shared-default」](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 若要新增表單欄位，請將列和欄標題新增至 `shared-default` 工作表，其中每一列定義一個表單欄位，每一欄標題定義 [屬性](/help/edge/docs/forms/eds-form-field-properties))。

   若要快速開始，您可以複製 [聯絡我們的試算表](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) 至您的試算表。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽和發佈工作表。

   ![使用AEM Sidekick預覽和發佈工作表](/help/edge/assets/preview-form.png)

   預覽和發佈時，瀏覽器會開啟新標籤，以JSON格式顯示工作表內容。 請務必記下即時URL，因為這是之後轉譯表單的必要條件。

   URL 的格式是：

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```



## 使用Edge Delivery Service (EDS)頁面預覽表單 {#add-a-form-to-your-eds-page}

到目前為止，您已為EDS專案啟用表單區塊，並準備好表單的結構。 現在，若要預覽表單：

1. 前往Microsoft SharePoint或Google Drive上的AEM Edge Delivery專案目錄。

1. 建立或開啟doc檔案以託管表單。 例如，開啟索引檔案。

1. 導覽至檔案中您要新增表單的位置。

1. 將名為「Form」的區塊新增至檔案，類似於下方顯示的區塊。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   在第二列中，加入您在上一節中記下的URL作為超連結。 您可以使用預覽URL (.page URL)或發佈URL (.live)。 為生產環境建置或測試表單和發佈URL時，可以使用預覽URL。

   >[!IMPORTANT]
   >
   >
   > 請確定沒有以純文字提及URL。 應將其新增為超連結。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽頁面。 頁面現在會顯示表單。 例如，以下是根據 [聯絡我們的試算表](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link)：


   ![EDS表單範例](/help/edge/assets/eds-form.png)

   現在，填寫表單並按一下提交按鈕，您會遇到類似以下內容的錯誤，因為試算表尚未設定為接受資料。

   ![表單提交時發生錯誤](/help/edge/assets/form-error.png)


   下一步是 [準備您的試算表以接受資料](/help/edge/docs/forms/submit-forms.md).



## 檢視更多

* [表單欄位屬性](/help/edge/docs/forms/eds-form-field-properties)
* [建立及預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單以傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈至網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [變更表單的主題和樣式](/help/edge/docs/forms/style-theme-forms.md)
