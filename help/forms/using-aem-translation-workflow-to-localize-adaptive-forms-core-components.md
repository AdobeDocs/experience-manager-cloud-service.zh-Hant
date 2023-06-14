---
title: 翻譯以核心元件為基礎的最適化表單
description: 使用機器翻譯或人工翻譯來翻譯以核心元件為基礎的最適化表單
feature: Adaptive Forms
source-git-commit: a33b380570210a32f4a4a1f26c9a2fe37c885bb1
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 4%

---

# 使用機器翻譯或人工翻譯來翻譯以核心元件為基礎的最適化表單 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表單可協助您跨地理區域提供更廣泛的受眾。 Adobe Experience Manager翻譯工作流程可協助您將Adaptive Forms及其記錄檔案本地化。 您可以使用 **機器翻譯** 或 **人工翻譯** 將最適化表單本地化。

## 使用機器翻譯翻譯翻譯最適化表單和記錄檔案 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即以最適化表單翻譯您的內容，並且 [記錄檔案](/help/forms/generate-document-of-record-core-components.md). AEM Formsas a Cloud Service已預先設定為使用Microsoft Translator的試用版進行機器翻譯。 執行以下步驟來啟用最適化Forms和記錄檔案的機器翻譯：

1. 在AEM Forms UI上，選取表單，然後點選 **[!UICONTROL 新增字典]** 選項。
1. 在「新增字典至翻譯專案」畫面中，針對 **[!UICONTROL 專案]** option

   * 若要建立翻譯專案，請選取 **[!UICONTROL 建立新的翻譯專案]** 選項和 **專案標題** 欄位中，指定標題。 例如 `Government Reference Site - German locale.`
   * 若要在現有翻譯專案中新增字典，請選取 **[!UICONTROL 新增至現有翻譯專案]** 選項並選取 **[!UICONTROL 現有翻譯專案]**.
1. 在 **目標語言** 欄位，指定地區設定(例如， `German(de)`)。 您可以指定多個地區設定。 表單已轉譯為 **目標語言** 欄位。 按一下&#x200B;**「完成」**。
1. 在「新增的字典」對話方塊中，按一下 **開啟專案**.
1. 在「專案」畫面中，按一下新建立的專案。 例如，按一下 **政府參考網站 — 德文地區設定** 圖磚。
1. 於 **翻譯工作** 圖磚，按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 圖示，然後按一下 **開始**. 圖磚的狀態會變更為「草稿」。 翻譯完成後，狀態會變更為 **已核准**. 幾分鐘後重新整理頁面並驗證狀態。

   ![開始翻譯](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. 在狀態變更為 **已核准** 於 **翻譯工作** 圖磚，按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 圖示，然後按一下 **完成**.

1. 若要預覽當地語系化表單，請在AEM Forms UI上選取當地語系化表單。 按一下 **[!UICONTROL 預覽]** >**[!UICONTROL 以HTML預覽]**. 新增後重新開啟表單 `afAcceptLang=<locale code>` 至表單的URL。 例如，新增 `afAcceptLang=de`以開啟德文版的表單。


   >[!NOTE]
   >
   >* 在瀏覽器視窗中開啟表單的當地語系化版本之前，請確定瀏覽器的地區設定已設定為符合表單的地區設定。 例如，如果表單已翻譯成德文(de)語言，則將瀏覽器的地區設定設為德文(de)。
   >* 最適化表單元件不支援由右至左(RTL)語言。 例如，希伯來文。

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, tap Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## 使用人工翻譯將最適化表單及其記錄檔案本地化 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人工翻譯中，內容會傳送給翻譯提供者，並由專業翻譯人員進行翻譯。 完成後，翻譯後的內容將傳回並匯入到 AEM 中。如果您的翻譯提供商與 AEM 相整合，內容會在 AEM 和翻譯提供商之間自動傳送。

對於翻譯，包含XLIFF格式檔案的字典會與專業譯者共用。 字典中包含每個地區設定的個別XLIFF檔案。 每個XLIFF檔案都包含顯示給一般使用者的文字，以及對應本地化文字的預留位置。

執行以下步驟，使用人工翻譯將表單及其記錄檔案本地化：

1. 在AEM Forms UI上，選取表單，然後點選 **[!UICONTROL 新增字典]** 選項。
1. 在「新增字典至翻譯專案」畫面中，針對 **[!UICONTROL 專案]** option

   * 若要建立翻譯專案，請選取 **[!UICONTROL 建立新的翻譯專案]** 選項和 **專案標題** 欄位中，指定標題。 例如 `Government Reference Site - German locale.`
   * 若要在現有翻譯專案中新增字典，請選取 **[!UICONTROL 新增至現有翻譯專案]** 選項並選取 **[!UICONTROL 現有翻譯專案]**.
1. 在 **目標語言** 欄位，指定地區設定(例如， `German(de)`)。 您可以指定多個地區設定。 表單已轉譯為 **目標語言** 欄位。 按一下&#x200B;**「完成」**。
1. 在「新增的字典」對話方塊中，按一下 **開啟專案**.
1. 在「專案」畫面中，按一下新建立的專案。 例如，按一下 **政府參考網站 — 德文地區設定** 圖磚。
1. 在底部 **摘要** 圖磚，按一下 **橢圓**. 翻譯專案屬性畫面隨即開啟。
1. 開啟 **[!UICONTROL 進階]** 索引標籤在頂端 **翻譯專案屬性** 畫面。 對於 **[!UICONTROL 翻譯欄位]**，選取 **[!UICONTROL 人工翻譯]**. 按一下 **儲存並關閉** 在熒幕上方。
1. 於 **翻譯工作** 圖磚，按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 圖示，然後按一下 **匯出**. 在「匯出」對話方塊中，按一下「下載匯出的檔案」選項。 它會下載.zip檔案。
   ![](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. 解壓縮下載的.zip檔案。 解壓縮的資料夾有兩個檔案：
   * translation_export_summary.xml
   * [form-fields-file].xml.
1. 開啟 [form-fields-file].xml進行編輯。 新增表單欄位的本地化字串和訊息。 儲存並關閉檔案。
1. 將translation_export_summary.xml和 [form-fields-file].xml.
1. 於 **翻譯工作** 圖磚，按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 圖示，然後按一下 **匯入**. 選取包含 [form-fields-file].xml. 表單欄位的本地化字串和訊息。

   ![](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. 若要預覽當地語系化表單，請在AEM Forms UI上選取當地語系化表單。 按一下 **[!UICONTROL 預覽]** >**[!UICONTROL 以HTML預覽]**. 新增後重新開啟表單 `afAcceptLang=<locale code>` 至表單的URL。 例如，新增 `afAcceptLang=de`以開啟德文版的表單。