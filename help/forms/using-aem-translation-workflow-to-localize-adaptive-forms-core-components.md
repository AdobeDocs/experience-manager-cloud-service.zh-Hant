---
title: 如何翻譯以核心元件為基礎的最適化表單？
description: 瞭解如何在AEM Forms中建立表單資料模型(FDM)、使用範例資料和服務測試模型，以及為模型設定各種選項。
feature: Adaptive Forms, Core Components
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 4%

---

# 使用機器翻譯或人工翻譯來翻譯以核心元件為基礎的最適化表單 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表單可協助您跨地理區域提供更廣泛的受眾。 Adobe Experience Manager翻譯工作流程可協助您將Adaptive Forms及其記錄檔案本地化。 您可以使用&#x200B;**機器翻譯**&#x200B;或&#x200B;**人力翻譯人員**&#x200B;將最適化表單當地語系化。

## 使用機器翻譯翻譯翻譯最適化表單和記錄檔案 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即以最適化表單和[記錄檔案](/help/forms/generate-document-of-record-core-components.md)翻譯您的內容。 AEM Forms as a Cloud Service已預先設定為使用機器翻譯適用的Microsoft Translator試用版。 執行以下步驟來啟用最適化Forms和記錄檔案的機器翻譯：

1. 在AEM Forms UI上，選取表單，然後選取&#x200B;**[!UICONTROL 新增字典]**&#x200B;選項。
1. 在[新增字典至翻譯專案]畫面中，針對&#x200B;**[!UICONTROL 專案]**&#x200B;選項

   * 若要建立翻譯專案，請選取&#x200B;**[!UICONTROL 建立新翻譯專案]**&#x200B;選項，並在&#x200B;**專案標題**&#x200B;欄位中指定標題。 例如 `Government Reference Site - German locale.`
   * 若要在現有翻譯專案中新增字典，請選取&#x200B;**[!UICONTROL 新增至現有翻譯專案]**&#x200B;選項，並選取&#x200B;**[!UICONTROL 現有翻譯專案]**。
1. 在&#x200B;**目標語言**&#x200B;欄位中，指定地區設定（例如，`German(de)`）。 您可以指定多個地區設定。 表單已轉譯為&#x200B;**目標語言**&#x200B;欄位中指定的所有地區設定。 按一下&#x200B;**「完成」**。
1. 在[新增的字典]對話方塊中，按一下[**開啟專案**]。
1. 在「專案」畫面中，按一下已建立的專案。 例如，按一下&#x200B;**政府參考網站 — 德文地區設定**&#x200B;圖磚。
1. 在&#x200B;**翻譯工作**&#x200B;圖磚上，按一下![aem62forms_downarrow](assets/aem62forms_downarrow.png)圖示，然後按一下&#x200B;**開始**。 圖磚的狀態會變更為「草稿」。 翻譯完成後，狀態會變更為&#x200B;**已核准**。 幾分鐘後重新整理頁面並驗證狀態。

   ![開始翻譯](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. 在&#x200B;**翻譯工作**&#x200B;圖磚上的狀態變更為&#x200B;**已核准**&#x200B;後，按一下![aem62forms_downarrow](assets/aem62forms_downarrow.png)圖示，然後按一下&#x200B;**完成**。

1. 若要預覽本地化表單，請在AEM Forms UI上選取本地化表單。 按一下&#x200B;**[!UICONTROL 預覽]** >**[!UICONTROL 預覽為HTML]**。 將`afAcceptLang=<locale code>`新增至表單的URL後，重新開啟表單。 例如，新增`afAcceptLang=de`以開啟德文版的表單。


   >[!NOTE]
   >
   >* 在瀏覽器視窗中開啟本地化的表單版本之前，請確定瀏覽器的地區設定已設定為符合表單的地區設定。 例如，如果表單被翻譯成德文(de)語言，則將瀏覽器的地區設定設為德文(de)。
   >* 最適化表單元件不支援由右至左(RTL)語言。 例如，希伯來文。

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, select Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## 使用人工翻譯將最適化表單及其記錄檔案當地語系化 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人工翻譯中，內容會傳送給翻譯提供者，並由專業翻譯人員進行翻譯。 完成後，翻譯後的內容將傳回並匯入到 AEM 中。如果您的翻譯提供商與 AEM 相整合，內容會在 AEM 和翻譯提供商之間自動傳送。

翻譯時，會與專業譯者共用包含XLIFF格式檔案的字典。 字典包括每個地區設定的個別XLIFF檔案。 每個XLIFF檔案都包含顯示給一般使用者的文字，以及對應本地化文字的預留位置。

執行以下步驟，使用人工翻譯將表單及其記錄檔案本地化：

1. 在AEM Forms UI上，選取表單，然後選取&#x200B;**[!UICONTROL 新增字典]**&#x200B;選項。
1. 在[新增字典至翻譯專案]畫面中，針對&#x200B;**[!UICONTROL 專案]**&#x200B;選項

   * 若要建立翻譯專案，請選取&#x200B;**[!UICONTROL 建立新翻譯專案]**&#x200B;選項，並在&#x200B;**專案標題**&#x200B;欄位中指定標題。 例如 `Government Reference Site - German locale.`
   * 若要在現有翻譯專案中新增字典，請選取&#x200B;**[!UICONTROL 新增至現有翻譯專案]**&#x200B;選項，並選取&#x200B;**[!UICONTROL 現有翻譯專案]**。
1. 在&#x200B;**目標語言**&#x200B;欄位中，指定地區設定（例如，`German(de)`）。 您可以指定多個地區設定。 表單已轉譯為&#x200B;**目標語言**&#x200B;欄位中指定的所有地區設定。 按一下&#x200B;**「完成」**。
1. 在[新增的字典]對話方塊中，按一下[**開啟專案**]。
1. 在「專案」畫面中，按一下已建立的專案。 例如，按一下&#x200B;**政府參考網站 — 德文地區設定**&#x200B;圖磚。
1. 在&#x200B;**摘要**&#x200B;圖磚底部，按一下&#x200B;**省略符號**。 翻譯專案屬性畫面隨即開啟。
1. 開啟&#x200B;**翻譯專案屬性**&#x200B;畫面頂端的&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。 針對&#x200B;**[!UICONTROL 翻譯欄位]**，選取&#x200B;**[!UICONTROL 人工翻譯]**。 按一下熒幕上方的&#x200B;**儲存並關閉**。
1. 在&#x200B;**翻譯工作**&#x200B;圖磚上，按一下![aem62forms_downarrow](assets/aem62forms_downarrow.png)圖示，然後按一下&#x200B;**匯出**。 在「匯出」對話方塊中，按一下「下載匯出的檔案」選項。 它會下載.zip檔案。
   ![匯出翻譯檔案](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. 解壓縮下載的.zip檔案。 擷取的資料夾有兩個檔案：
   * translation_export_summary.xml
   * [form-fields-file].xml。
1. 開啟[form-fields-file].xml進行編輯。 為表單欄位新增當地語系化的字串和訊息。 儲存並關閉檔案。
1. 將translation_export_summary.xml和[form-fields-file].xml壓縮檔案。
1. 在&#x200B;**翻譯工作**&#x200B;圖磚上，按一下![aem62forms_downarrow](assets/aem62forms_downarrow.png)圖示，然後按一下&#x200B;**匯入**。 選取包含[form-fields-file].xml的封存。 表單欄位有當地語系化的字串和訊息。

   ![匯入翻譯檔案](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. 若要預覽本地化表單，請在AEM Forms UI上選取本地化表單。 按一下&#x200B;**[!UICONTROL 預覽]** >**[!UICONTROL 預覽為HTML]**。 將`afAcceptLang=<locale code>`新增至表單的URL後，重新開啟表單。 例如，新增`afAcceptLang=de`以開啟德文版的表單。

## 另請參閱 {#see-also}

{{see-also}}