---
title: 為 AEM Forms 適用的 Edge Delivery Services 進行翻譯和本地化
description: 為 AEM Forms 適用的 Edge Delivery Services 進行翻譯和本地化
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 100%

---


# 為 AEM Forms 適用的 Edge Delivery Services 進行翻譯和本地化

在 Edge Delivery Services 中，表單翻譯是將表單內容從一種語言轉換為另一種語言，且著重準確性、清晰度和一致性。翻譯或本地化表單可在不同地理位置贏得範圍更廣泛的客群，因此可增強使用者體驗並促進不同語言偏好之間更有效溝通。


閱讀完本文章後，您將學會：

- [翻譯 Google Drive 內的表單](#translate-form-google-drive)
- [翻譯 SharePoint 網站內的表單](#translate-form-sharepoint)

## 翻譯 Google Drive 內的表單 {#translate-form-google-drive}

Google 工作表的 `GOOGLETRANSLATE` 功能可利用內建翻譯工具來翻譯表單，直接在 Google 工作表中將文字從一種語言變更為另一種語言。若要翻譯 Google Drive 內的表單：

1. 前往 Google Drive 上的 AEM 專案資料夾並開啟 Google 工作表。
2. 將現有工作表 (`shared-default`) 重新命名為 `shared-en`。
3. 新增一個名為 `shared-default` 的工作表.`shared-default` 表單包含要本地化為特定語言的內容。
4. 使用 `GOOGLETRANSLATE` 功能在 `shared-default` 工作表中新增本地化內容。
您可以使用公式將 `shared-en` 工作表中儲存格 D2 內容翻譯為在 `shared-default` 工作表中的法文。這是要使用的公式：
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![查詢翻譯的試算表](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

您可以參考包含從英文翻譯成法文的 `enquiry` 表單內表單定義的[試算表](/help/forms/assets/enquirytranslate.xlsx)。

![查詢翻譯的表單](/help/forms/assets/translate-form-french.png)

請參閱下面的 URL，您可以在其中查看表單及其法語翻譯：
https://main--portal--wkndforms.hlx.live/enquirytranslate

## 翻譯 SharePoint 網站內的表單{#translate-form-sharepoint}

若要翻譯 Microsoft® SharePoint 網站上的表單，您需要使用任何翻譯服務手動變更欄位標籤。若要翻譯 SharePoint 網站內的表單：

1. 前往 Microsoft® SharePoint 上的 AEM 專案資料夾並開啟試算表。
2. 將現有工作表 (`shared-default`) 重新命名為 `shared-en`。
3. 新增一個名為 `shared-default` 的工作表.`shared-default` 表單包含要本地化為特定語言的內容。
4. 手動在 `shared-default` 工作表中新增本地化內容。

   ![查詢翻譯的試算表](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

參考包含從英文翻譯成法文的 `enquiry` 表單內表單定義的[試算表](/help/forms/assets/enquirytranslate-sp.xlsx)。

![查詢翻譯的表單](/help/forms/assets/translate-form-french.png)

請參閱下面的 URL，您可以在其中查看表單及其法語翻譯：
https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## 已知問題 {#known-issues}

- 表單標籤會翻譯為 `shared-default` 工作表中指定的本地化語言，但錯誤訊息會以瀏覽器的預設語言顯示。

  ![錯誤訊息](/help/forms/assets/translate-error-message.png)

- 當您開啟行事曆時，行事曆下拉式選單將以瀏覽器的預設語言顯示。

  ![錯誤訊息](/help/forms/assets/translate-calender-display.png)


## 常見問題 {#faq}

**問**：如何在表單中以指定的本地化語言輸入內容？

**答**：若要以特定本地化語言輸入文字，請調整裝置上的鍵盤設定。有關如何操作的說明，請參閱以下連結：

- [設定 Mac 以接受另一種語言的輸入](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
- [設定 Windows 以接受另一種語言的輸入](https://support.microsoft.com/zh-hant/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:文字=選取%20%20開始%20%3E%20設定%20%3E%20時間，然後%20您%2C%20要%20選取%20選項)
- [設定您的 Android 或 iPhone/iPad 以接受其他語言的輸入](https://support.google.com/gboard/answer/7068494?hl=en&co=GENIE.Platform%3DAndroid)


**問**：如何擷取 `GOOGLETRANSLATE` 功能中使用的地區設定清單？

**答**：您可以參考 [Google 正式文件](https://cloud.google.com/translate/docs/languages)，取得 GOOGLETRANSLATE 所用地區設定的完整清單。


