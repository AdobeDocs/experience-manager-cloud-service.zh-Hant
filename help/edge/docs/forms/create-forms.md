---
title: 開始使用 AEM Forms Edge Delivery Service
description: 快速製作完美表單！⚡ AEM Forms Edge Delivery 文件型製作 = 驚人的速度和 SEO 友善表單，讓使用者更滿意且適用於搜尋引擎。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 60%

---


# 在 AEM Forms Edge Delivery Service 上建立表單

身處今日數位時代，任何組織都需要建立對使用者友善的表單。AEM Forms Edge Delivery 讓您可以使用 Word 或 Google Docs 等熟悉的工具來建立表單。

這些表單可直接提交資料至 Microsoft Excel 或 Google Sheets 檔案，讓您能夠使用由 Google Sheets、Microsoft Excel 和 Microsoft Sharepoint 等強大 API 建構的活躍生態系統，以便輕鬆處理提交的資料或啟動現有的業務工作流程。

AEM Forms Edge Delivery提供表單區塊，協助您輕鬆建立表單，以擷取及儲存擷取的資料。 您可以在AEM EDS專案中加入Form區塊以開始建立表單。 讓我們開始吧：


## 先決條件

開始之前，請確定您已完成下列步驟：

* 使用AEM範本設定Edge Delivery Service (EDS) Github專案，並在本機電腦上複製對應的Github存放庫。 另請參閱 [開發人員教學課程](https://www.aem.live/developer/tutorial) 以取得詳細資訊。 在本檔案中，Edge Delivery Service (EDS)專案的本機資料夾稱為 `[EDS Project repository]` .
* 原地複製 [Forms區塊存放庫](https://github.com/adobe/afb) 本機電腦上。 它包含在EDS網頁上轉譯表單的程式碼。 在本檔案中，您的Forms Block存放庫的本機資料夾稱為 `[Forms Block repository]`.
* 確保您有權存取Google工作表或Microsoft SharePoint。 若要將Microsoft SharePoint設定為您的內容來源，請參閱 [如何使用Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint)



## 建立表單

+++ 步驟1：將表單區塊新增至您的邊緣傳遞服務(EDS)專案。

此 `Form block` 包含新增表單至EDS網站的功能。 區塊不包含在使用AEM範本建立的專案中。 若要將 Form 區塊加入您的 Edge Delivery Service 專案中：

1. 導覽至 `[Forms Block repository]/blocks` 資料夾，並複製 `form` 資料夾。

1. 導覽至 `[EDS Project repository]/blocks/` 資料夾並貼上 `form` 資料夾。

1. 存回 `form` 資料夾和基礎檔案新增至GitHub上的邊緣傳遞服務專案。

   表單區塊會新增至GitHub上的EDS專案存放庫。 請確定GitHub建置不會失敗：

   * 如果遇到「無法解析至「&#39;../../scripts/lib-franklin.js&#39;」路徑」錯誤，請開啟 `[EDS Project]/blocks/forms/form.js` 檔案。在匯入語句中，將 `lib-franklin.js` 檔案替換為 `aem.js` 檔案。

   * 如果您遇到任何 linting 錯誤，可隨時忽略這些錯誤。若要繞過 linting 檢查，請開啟 `[EDS Project]\package.json` 檔案並將「lint」指令碼從 `"lint": "npm run lint:js && npm run lint:css"` 更新為 `"lint": "echo 'skipping linting for now'"`。儲存檔案並將其提交到您的 GitHub 專案。

現在您可以建立表單並將其新增至您的網站。

+++

+++ 步驟2：使用Microsoft Excel或Google工作表製作表單。

您可以使用試算表輕鬆建立表單，而不需要複雜的流程。您可以先將列和欄標題新增至試算表中，其中每個列會定義一個表單欄位，每個欄標題會定義對應表單欄位的屬性。

例如，在下面的試算表中，列會定義`contact us`表單的欄位，欄標題會定義對應欄位的屬性。

![聯絡我們試算表](/help/edge/assets/contact-us-form-spreadsheet.png)

若要建立表單：

1. 在 Microsoft SharePoint 或 Google Drive 上，開啟 AEM Edge Delivery 專案資料夾。

1. 在 AEM Edge Delivery 專案目錄下的任意位置，建立 Microsoft Excel 活頁簿或 Google Sheet。例如，在 Google Drive 上的 AEM Edge Delivery 專案目錄中，建立一個名為 `contact-us` 的試算表。

1. 確保該試算表可讓為您專案設定的 AEM 使用者 (例如 `helix@adobe.com`) [](https://www.aem.live/docs/setup-customer-sharepoint) 共用，並且該使用者擁有該試算表的編輯權限。

1. 開啟您所建立的試算表，並將預設試算表的名稱變更為「共用預設」。

   ![將預設試算表重新命名為「共用預設」](/help/edge/assets/rename-sheet-to-shared-default.png)

1. 若要新增表單欄位，請新增列和欄標題至 `shared-default` 試算表中，其中每列會定義一個表單欄位，每個欄標題會定義對應表單欄位的[屬性](/help/edge/docs/forms/eds-form-field-properties)。

   若要快速開始，您可以將[聯絡我們試算表](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link)的內容複製到您的試算表中。

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 預覽和發佈試算表。

   ![使用 AEM Sidekick 預覽和發佈試算表](/help/edge/assets/preview-form.png)

   預覽和發佈時，瀏覽器會開啟新標籤，以 JSON 格式顯示試算表內容。請務必記下即時 URL，因為稍後提交表單時需要用到。

   URL 的格式是：

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

+++

+++ 步驟3：使用Edge Delivery Service (EDS)頁面預覽表單。


到目前為止，您已經將表單區塊新增至EDS專案，並準備好表單的結構。 現在，若要預覽表單：

1. 前往Microsoft SharePoint或Google Drive帳戶，並開啟AEM Edge Delivery專案目錄。

1. 開啟doc檔案以將表單嵌入其中。 例如，開啟索引檔案。 您也可以建立新的doc檔案。

1. 導覽至文件中要新增表單的所需位置。

1. 新增名為 &#39;Form&#39; 的區塊至檔案中，類似於下面顯示的區塊。

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   在第二列中，加入您在前一節中錄製的URL作為超連結。 將預覽URL (.page URL)用於開發或測試目的，或將發佈URL (.live)用於生產。

   >[!IMPORTANT]
   >
   >
   > 請確定URL為超連結，而非以純文字顯示。


1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽頁面。頁面現在會顯示表單。

   例如，這是以[聯絡我們試算表](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link)為主的表單：


   ![EDS Forms 範本](/help/edge/assets/eds-form.png)

   現在，填寫表單並按一下提交按鈕，您會遇到類似於以下內容的錯誤，因為試算表尚未設定為接受資料。

   ![在表單提交時的錯誤](/help/edge/assets/form-error.png)

+++


## 下一步

[準備您的試算表](/help/edge/docs/forms/submit-forms.md) 以在表單提交時開始接受資料。



## 了解更多

* [表單欄位屬性](/help/edge/docs/forms/eds-form-field-properties)
* [建立並預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單來傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈到網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [改變主題和樣式風格](/help/edge/docs/forms/style-theme-forms.md)
