---
title: 為 AEM Forms Edge Delivery Services Form 進行翻譯和本地化
description: 為 AEM Forms Edge Delivery Services Form 進行翻譯和本地化
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 6%

---


# 為 AEM Forms Edge Delivery Services Form 進行翻譯和本地化

在Edge Delivery Services中，表單翻譯涉及將表單內容從一種語言轉換為另一種語言，並專注於準確性、清晰度和一致性。 翻譯或本地化的表單可讓不同地理位置的受眾觸及更廣的範圍，進而提升使用者體驗，並促進不同語言偏好間的更佳溝通。


在文章結束時，您將學習：

* [在Google Drive中翻譯表單](#translate-form-google-drive)
* [在SharePoint網站中翻譯表單](#translate-form-sharepoint)

## 在Google Drive中翻譯表單 {#translate-form-google-drive}

此 `GOOGLETRANSLATE` Google工作表的功能透過點選內建翻譯工具來翻譯表單，直接在Google工作表中將文字從一種語言變更為另一種語言。 若要在Google Drive中翻譯表單：

1. 前往Google Drive上的AEM專案資料夾，並開啟Google工作表。
2. 重新命名現有頁面(`shared-default`)至 `shared-en`.
3. 新增名為的工作表 `shared-default`. 此 `shared-default` 工作表包含特定語言本地化內容。
4. 在中新增當地語系化內容 `shared-default` 工作表使用 `GOOGLETRANSLATE` 函式。
您可以使用公式來轉譯儲存格D2的內容，從 `shared-en` 將工作表改成法文 `shared-default` 工作表。 以下是使用的公式：
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![查詢翻譯試算表](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. 預覽和發佈工作表，使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

您可參閱 [試算表](/help/forms/assets/enquirytranslate.xlsx) 包含「 」的表單定義 `enquiry` 表單已從英文翻譯成法文。

![查詢已翻譯表單](/help/forms/assets/translate-form-french.png)

請參閱下列URL，您可在其中檢視表單及其法文翻譯：https://main--portal--wkndforms.hlx.live/enquirytranslate

## 在SharePoint網站中翻譯表單{#translate-form-sharepoint}

若要在Microsoft® SharePoint網站上翻譯表單，您需要使用任何翻譯服務手動變更欄位標籤。 若要在SharePoint網站中翻譯表單：

1. 前往Microsoft® SharePoint上的AEM專案資料夾，並開啟試算表。
2. 重新命名現有頁面(`shared-default`)至 `shared-en`.
3. 新增名為的工作表 `shared-default`. 此 `shared-default` 工作表包含特定語言本地化內容。
4. 在中新增當地語系化內容 `shared-default` 手動工作表。

   ![查詢翻譯試算表](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. 預覽和發佈工作表，使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

請參閱 [試算表](/help/forms/assets/enquirytranslate-sp.xlsx) 包含「 」的表單定義 `enquiry` 表單已從英文翻譯成法文。

![查詢已翻譯表單](/help/forms/assets/translate-form-french.png)

請參閱下列URL，您可在其中檢視表單及其法文翻譯：https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## 已知問題 {#known-issues}

* 表單的標籤會轉譯為中指定的當地語系化語言 `shared-default` 工作表，但錯誤訊息會以瀏覽器的預設語言顯示。

  ![錯誤訊息](/help/forms/assets/translate-error-message.png)

* 當您開啟行事曆時，行事曆下拉式清單會以瀏覽器的預設語言顯示。

  ![錯誤訊息](/help/forms/assets/translate-calender-display.png)


## 常見問題 {#faq}

**Q**：如何在表單中以指定的當地語系化語言輸入內容？

**A**：若要以特定當地語系化語言輸入文字，請調整裝置上的鍵盤設定。 如需操作說明，請參閱下列連結：

* [設定您的Mac以使用其他語言進行輸入](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [設定Windows以使用其他語言輸入](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
* [設定Android或iPhone/iPad以使用其他語言輸入](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**Q**：如何擷取使用於的語言環境清單 `GOOGLETRANSLATE` 函式？

**A**：您可以參閱 [Google的官方檔案](https://cloud.google.com/translate/docs/languages) 以取得GOOGLE TRANSLATE中使用的地區設定完整清單。

## 另請參閱

{{see-more-forms-eds}}

