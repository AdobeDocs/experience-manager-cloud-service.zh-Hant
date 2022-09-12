---
title: 如何使用表單資料模型？
description: 了解如何根據表單資料模型建立最適化Forms和最適化表單片段。 在表單資料模型中為資料模型物件產生和編輯範例資料，以深入挖掘。 您可以使用此資料來預覽和測試適用性Forms。
feature: Form Data Model
role: User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# 使用表單資料模型 {#use-form-data-model}

![data-integration](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 資料整合可讓您使用不同的後端資料來源來建立表單資料模型，以便用作各種適用性Forms中的結構 <!--and interactive communications--> 工作流程。 它需要配置資料源，並根據資料源中可用的資料模型對象和服務建立表單資料模型。 如需詳細資訊，請參閱下列內容：

* [[!DNL Experience Manager Forms] 資料整合](data-integration.md)
* [設定資料來源](configure-data-sources.md)
* [建立表單資料模型](create-form-data-models.md)
* [使用表單資料模型](work-with-form-data-model.md)

表單資料模型是JSON結構的擴充功能，可用於：

* [建立最適化Forms和片段](#create-af)

<!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [使用範例資料預覽](#preview-ic)
* [使用表單資料模型服務](#prefill)
* [將提交的最適化表單資料寫入資料來源](#write-af)
* [使用適用性表單規則叫用服務](#invoke-services)

## 建立最適化Forms和片段 {#create-af}

您可以建立 [適用性Forms](creating-adaptive-form.md) 和最適化表單片段 <!-- [Adaptive Form Fragments](adaptive-form-fragments.md) --> 根據表單資料模型。 建立最適化表單或最適化表單片段時，請執行下列動作以使用表單資料模型：

1. 在「添加屬性」螢幕上的「表單模型」頁簽中，選擇 **[!UICONTROL 表單資料模型]** 在 **[!UICONTROL 從]** 下拉式清單。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 點選以展開 **[!UICONTROL 選擇表單資料模型]**. 會列出所有可用的表單資料模型。

   從資料模型中選取。

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**僅限適用性表單片段**)您可以僅根據表單資料模型中的一個資料模型物件來建立最適化表單片段。 展開 **[!UICONTROL 表單資料模型定義]** 下拉式清單。 它列出指定表單資料模型中的所有資料模型對象。 從清單中選取資料模型物件。

   ![create-af-3](assets/create-af-3.png)

   建立基於表單資料模型的最適化表單或最適化表單片段後，表單資料模型物件會出現在 **[!UICONTROL 資料來源]** （適用性表單編輯器中的內容瀏覽器）頁簽。

   >[!NOTE]
   >
   >對於適用性表單片段，只有在製作時選取的資料模型物件及其相關的資料模型物件會顯示在「資料來源」索引標籤中。

   ![data-model-objects-tab](assets/data-model-objects-tab.png)

   您可以將資料模型物件拖放至最適化表單或片段，以新增表單欄位。 新增的表單欄位會保留中繼資料屬性，並與資料模型物件屬性系結。 系結可確保表單提交時欄位值會在對應的資料來源中更新，並在表單轉譯時預填。

<!-- ## Create interactive communications {#create-ic}

You can create an interactive communication based on a Form Data Model that you can use to prefill interactive communication with data from configured data sources. In addition, the building blocks of an interactive communication, such as text, list, and condition document fragments can be based on a form data model.

You can choose a Form Data Model when creating an interactive communication or a document fragment. The following image shows the General tab of the Create Interactive Communication dialog.

![create-ic](assets/create-ic.png)

General tab of Create Interactive Communication dialog

For more information, see:

[Create an interactive communication](create-interactive-communication.md)

[Text in Interactive Communications](texts-interactive-communications.md)

[Conditions in Interactive Communications](conditions-interactive-communications.md)

[List fragments](lists.md) -->

## 使用範例資料預覽 {#preview-ic}

表單資料模型編輯器可讓您為表單資料模型中的資料模型物件產生和編輯範例資料。 您可以使用此資料來預覽和測試 <!--interactive communications and--> 適應性Forms。 您必須先產生範例資料，才能依照 [使用表單資料模型](work-with-form-data-model.md#sample).

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and tap **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and tap **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

若要預覽包含範例資料的適用性表單，請以製作模式開啟適用性表單，然後點選 **[!UICONTROL 預覽]**.

## 使用表單資料模型服務預填 {#prefill}

[!DNL Experience Manager Forms] 提供現成可用的表單資料模型預填服務，供您啟用適用性Forms <!--and interactive communications--> 根據表單資料模型。 預填服務會查詢適用性表單中資料模型物件的資料來源 <!--and interactive communication--> 並因此在呈現表單或通訊時預填資料。

若要啟用最適化表單的表單資料模型預填服務，請開啟「最適化表單容器」屬性並選取 **[!UICONTROL 表單資料模型預填服務]** 從 **[!UICONTROL 預填服務]** 「基本」設定追蹤器中的下拉式清單。 然後，儲存屬性。

![預填服務](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## 將提交的適用性表單資料寫入資料來源 {#write-af}

當使用者根據表單資料模型提交表單時，您可以設定表單以將資料模型物件的已提交資料寫入其資料來源。 要實現此使用案例， [!DNL Experience Manager Forms] 提供 [表單資料模型提交動作](configuring-submit-actions.md)，現成可用，僅適用於以表單資料模型為基礎的適用性Forms。 它會將資料模型物件的已提交資料寫入其資料來源中。

若要設定「表單資料模型提交動作」，請開啟「適用性表單容器」屬性並選取 **[!UICONTROL 使用表單資料模型提交]** 從「提交」設定追蹤器下的「提交動作」下拉式清單。 然後，瀏覽並選取資料模型物件， **[!UICONTROL 要提交的資料模型對象的名稱]** 下拉式清單。 儲存屬性。

在表單提交時，將配置的資料模型對象的資料寫入相應的資料源。

<!--![data-submission](assets/data-submission.png)-->

您也可以使用二進位資料模型物件屬性，將表單附件提交至資料來源。 執行以下操作將附件提交到JDBC資料源：

1. 將包含二進位屬性的資料模型物件新增至表單資料模型。
1. 在適用性表單中，拖放 **[!UICONTROL 檔案附件]** 元件（從「元件」瀏覽器）到最適化表單。
1. 點選以選取新增的元件，然後點選 ![settings_icon](assets/configure-icon.svg) 開啟元件的「屬性」瀏覽器。
1. 在「系結參考」欄位中，點選 ![foldersearch_18](assets/folder-search-icon.svg) 並導覽至選取您在表單資料模型中新增的二進位屬性。 視需要設定其他屬性。

   點選 ![check-button](assets/save_icon.svg) 以儲存屬性。 附件欄位現在已綁定到表單資料模型的二進位屬性。

1. 在適用性表單容器屬性的「提交」區段中，啟用 **[!UICONTROL 提交表單附件]**. 它會在提交表單時將二進位屬性欄位中的附件提交給資料來源。

## 使用規則叫用適用性Forms中的服務 {#invoke-services}

在以表單資料模型為基礎的適用性表單中，您可以 [建立規則](rule-editor.md) 調用在表單資料模型中配置的服務。 此 **[!UICONTROL 調用服務]** 規則中的操作會列出「表單資料模型」中的所有可用服務，並允許您為服務選擇輸入和輸出欄位。 您也可以使用 **[!UICONTROL 設定值]** 規則類型，以叫用表單資料模型服務，並將欄位的值設定為服務傳回的輸出。

例如，以下規則調用以員工ID作為輸入的獲取服務，並且返回的值將填充到窗體中相應的「從屬ID」、「姓氏」、「名字」和「性別」欄位中。

![調用服務](assets/invoke-service.png)

此外，您也可以使用 `guidelib.dataIntegrationUtils.executeOperation` 在規則編輯器的程式碼編輯器中撰寫JavaScript的API。 <!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->
