---
title: 使用AEM翻譯工作流本地化自適應Forms和記錄文檔
seo-title: Using AEM translation workflow to localize Adaptive Forms and Document of Record
description: 學習使用翻AEM譯工作流來本地化自適應Forms和記錄文檔。
seo-description: Learn to use AEM translation workflows to localize Adaptive Forms and Document of Record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# 使用AEM翻譯工作流本地化自適應Forms和記錄文檔 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表單可幫助您為不同地區的更多受眾提供服務。 Adobe Experience Manager翻譯工作流程幫助您本地化AdaptiveForms及其記錄文檔。 您可以使用 **機器翻譯** 或 **人類翻譯** 的上界。

本文介紹了在Adaptive AEM Forms和文檔記錄下使用翻譯工作流的過程。

## 使用機器翻譯來定位記錄的自適應表單和文檔 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即以「自適應表單」和「記錄文檔」的形式翻譯您的內容。 [!DNL AEM Forms] 已預配置為使用的試用版 [!DNL Microsoft Translator] 機器翻譯。 執行以下步驟以啟用自適應Forms和記錄文檔的機器翻譯：

1. 在 [!DNL AEM Forms] UI，選擇一個表單，然後點擊 **添加詞典** 的雙曲餘切值。
1. 在 **將詞典添加到翻譯項目** ，選擇 **新建翻譯項目** 或 **添加到現有翻譯項目** 的雙曲餘切值。
1. 在 **項目標題** 的子菜單。 例如， `Government Reference Site - German locale.`
1. 在 **目標語言** 欄位，指定區域設定(例如， `German(de)`)，然後按一下 **完成**。 可以指定多個區域設定。 表單將翻譯為在 **目標語言** 的子菜單。
1. 在「添加的字典」對話框中，按一下 **開啟項目**。 在「項目」螢幕中，開啟新建立的項目。
1. 按一下 **橢圓** 在 **翻譯摘要** 平鋪。 將開啟「翻譯摘要」螢幕。
1. 按一下 **編輯** 表徵圖 **翻譯摘要** 的上界。 開啟 **翻譯** ，然後在 **翻譯方法** 的上界。 選擇相應的 **翻譯提供程式** 和 **雲配置**。 按一下 **完成** 表徵圖。
1. 在 **翻譯作業** 平鋪，按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 表徵圖，然後按一下 **開始**。 磁貼的狀態將更改為「草稿」。 完成翻譯後，狀態將更改為 **準備審閱**。 幾分鐘後刷新頁面並驗證狀態。
1. 狀態更改為 **準備審閱** 的 **翻譯作業** 平鋪，在瀏覽器窗口中開啟窗體。 將顯示表單的本地化版本。

   >[!NOTE]
   >
   >* 在瀏覽器窗口中開啟表單的本地化版本之前，請確保將瀏覽器的區域設定設定為與表單的區域設定匹配。 例如，如果表單被翻譯為德語(de)語言，則將瀏覽器的區域設定設定為德語(de)。
   >* 自適應表單元件不支援從右到左(RTL)語言。 例如，希伯來語。


   與「自適應表單」一起，自動生成的「記錄文檔」也會本地化。

   有關「記錄文檔」設定和配置的詳細資訊，請參閱：

[記錄範本文件配置](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[記錄設定的文檔](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定義記錄文檔的品牌資訊](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 並確保瀏覽器區域設定設定為與使用機器語言本地化自適應表單的語言相同的語言。 瀏覽器區域設定有助於在記錄文檔中本地化品牌資訊。
1. 要查看已本地化的記錄文檔，請點擊生成預覽。 「記錄文檔」(Document of Record)PDF在瀏覽器的新頁籤中生成並開啟。

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that will be displayed to the end users and placeholders for the corresponding localized text.

Perform the following steps to localize a form and its Document of Record using Human Translators:

1. [Connect AEM with your translation service provider](/help/sites-administering/tc-tic.md) and [create translation integration framework configurations](/help/sites-administering/tc-tic.md).

1. [Associate the pages of your language master](/help/sites-administering/tc-tic.md) with the translation service and framework configurations.

1. [Identify the type of content](/help/sites-administering/tc-rules.md) to translate.

1. [Prepare the content for translation](/help/sites-administering/tc-prep.md) by authoring the language master and creating the root pages of language copies.

1. [Create translation projects](/help/sites-administering/tc-manage.md) to gather the content to translate and to prepare the translation process.

1. Use the translation projects to [manage the content translation process](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Adaptive Form components do not support right to left (RTL) languages. For example, Hebrew.
> -->

