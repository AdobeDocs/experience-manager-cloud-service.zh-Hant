---
title: 如何為最適化表單建立表單資料模型(FDM)？
description: 瞭解如何根據表單資料模型(FDM)建立最適化Forms和片段。 產生及編輯 FDM 中資料模型物件的樣本資料。
feature: Adaptive Forms, Form Data Model
role: Admin, User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 5%

---

# 使用表單資料模型(FDM) {#use-form-data-model}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/using-form-data-model.html) |
| AEM as a Cloud Service  | 本文章 |


![資料整合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms]資料整合可讓您使用不同的後端資料來源來建立表單資料模型(FDM)，以便在各種最適化Forms <!--and interactive communications-->工作流程中作為結構描述使用。 它需要設定資料來源，並根據資料來源中可用的資料模型物件和服務來建立表單資料模型(FDM)。 如需詳細資訊，請參閱下列內容：

* [[!DNL Experience Manager Forms]資料整合](data-integration.md)
* [設定資料來源](configure-data-sources.md)
* [建立表單資料模型(FDM)](create-form-data-models.md)
* [使用表單資料模型(FDM)](work-with-form-data-model.md)

表單資料模型(FDM)是JSON架構的擴充功能，可用來執行以下操作：

* [建立最適化Forms和片段](#create-af)
  <!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [使用範例資料預覽](#preview-ic)
* [使用表單資料模型服務](#prefill)
* [將提交的最適化表單資料寫回資料來源](#write-af)
* [使用最適化表單規則叫用服務](#invoke-services)

## 建立Adaptive Forms和片段 {#create-af}

您可以根據表單資料模型(FDM)建立[最適化Forms](creating-adaptive-form.md)和最適化表單片段<!-- [Adaptive Form Fragments](adaptive-form-fragments.md) -->。 執行下列動作，以便在建立最適化表單或最適化表單片段時使用表單資料模型(FDM)：

1. 在[新增屬性]畫面的[表單模型]索引標籤中，選取&#x200B;**[!UICONTROL 從]**&#x200B;選取下拉式清單中的&#x200B;**[!UICONTROL 表單資料模型]**。

   ![create-af-1-1](assets/create-af-1-1.png)

2. 選取以展開&#x200B;**[!UICONTROL 選取表單資料模型]**。 列出所有可用的表單資料模型(FDM)。

   從資料模型中選取。

   ![create-af-2-1](assets/create-af-2-1.png)

3. （**僅最適化表單片段**）您只能根據表單資料模型(FDM)中的一個資料模型物件來建立最適化表單片段。 展開&#x200B;**[!UICONTROL 表單資料模型定義]**&#x200B;下拉式清單。 它會列出指定表單資料模型(FDM)中的所有資料模型物件。 從清單中選取資料模型物件。

   ![create-af-3](assets/create-af-3.png)

   根據表單資料模型(FDM)建立最適化表單或最適化表單片段後，表單資料模型物件會出現在最適化表單產生器中內容瀏覽器的&#x200B;**[!UICONTROL 資料來源]**&#x200B;標籤中。

   >[!NOTE]
   >
   >對於最適化表單片段，只有編寫時選取的資料模型物件及其關聯的資料模型物件會出現在資料來源標籤中。

   ![data-model-objects-tab](assets/data-model-objects-tab.png)

   您可以將資料模型物件拖放至最適化表單或片段來新增表單欄位。 新增的表單欄位會保留中繼資料屬性，並與資料模型物件屬性繫結。 繫結可確保欄位值在表單提交時更新到對應的資料來源中，並在表單轉譯時預先填充。

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

表單資料模型編輯器可讓您為表單資料模型(FDM)中的資料模型物件產生和編輯範例資料。 您可以使用此資料來預覽和測試<!--interactive communications and-->最適化Forms。 您必須先產生範例資料再進行預覽，如[使用表單資料模型](work-with-form-data-model.md#sample)中所述。

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and select **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and select **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

若要預覽含有範例資料的最適化表單，請在作者模式中開啟最適化表單，然後選取&#x200B;**[!UICONTROL 預覽]**。

## 使用表單資料模型服務預填 {#prefill}

[!DNL Experience Manager Forms]提供現成可用的表單資料模型預填服務，您可針對以表單資料模型(FDM)為基礎的最適化Forms <!--and interactive communications-->啟用此服務。 預填服務會查詢最適化表單<!--and interactive communication-->中資料模型物件的資料來源，並在呈現表單或通訊時相應預填資料。

若要啟用最適化表單的表單資料模型預填服務，請開啟「最適化表單容器」屬性，然後從「基本」摺疊式功能表的&#x200B;**[!UICONTROL 預填服務]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 表單資料模型預填服務]**。 然後，儲存屬性。

![預填服務](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## 將提交的最適化表單資料寫入資料來源 {#write-af}

當使用者根據表單資料模型(FDM)提交表單時，您可以設定表單以將資料模型物件的已提交資料寫入其資料來源。 為達成此使用案例，[!DNL Experience Manager Forms]提供[表單資料模型提交動作](configuring-submit-actions.md)，僅可用於以表單資料模型(FDM)為基礎的最適化Forms。 它將資料模型物件的已提交資料寫入其資料來源中。

若要設定表單資料模型提交動作：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 使用表單資料模型提交]**。

   ![動作組態](/help/forms/assets/configure-submit-action-invoke-fdm.png)

1. 指定要提交的&#x200B;**[!UICONTROL 資料模型]**。
1. 按一下&#x200B;**[!UICONTROL 完成]**

在提交表單時，會將已設定資料模型物件的資料寫入各自的資料來源。 此外，您可以使用表單資料模型(FDM)和記錄檔案(DoR)將表單附件提交至資料來源。 如需表單資料模型(FDM)的相關資訊，請參閱[[!DNL AEM Forms] 資料整合](data-integration.md)。

<!--![data-submission](assets/data-submission.png)-->

>[!NOTE]
>
> AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)文章中進一步瞭解這些選項。

您也可以使用二進位資料模型物件屬性，將表單附件提交至資料來源。 執行下列動作，將附件提交至JDBC資料來源：

1. 將包含二進位屬性的資料模型物件新增至表單資料模型(FDM)。
1. 在最適化表單中，將&#x200B;**[!UICONTROL 檔案附件]**&#x200B;元件從「元件」瀏覽器拖放至最適化表單。
1. 選取「 」以選取新增的元件，並選取「![settings_icon](assets/configure-icon.svg)」以開啟元件的「屬性」瀏覽器。
1. 在「繫結參考」欄位中，選取![foldersearch_18](assets/folder-search-icon.svg)，並導覽以選取您在表單資料模型(FDM)中新增的二進位屬性。 視需要設定其他屬性。

   選取![check-button](assets/save_icon.svg)以儲存屬性。 附件欄位現在已繫結至表單資料模型(FDM)的二進位屬性。

1. 在最適化表單容器屬性的提交區段中，啟用&#x200B;**[!UICONTROL 提交表單附件]**。 它會在表單提交時，將二進位屬性欄位中的附件提交至資料來源。

## 使用規則在Adaptive Forms中叫用服務 {#invoke-services}

在基於表單資料模型(FDM)的最適化表單中，您可以[建立規則](rule-editor.md)以叫用表單資料模型(FDM)中設定的服務。 規則中的&#x200B;**[!UICONTROL 叫用服務]**&#x200B;作業會列出表單資料模型(FDM)中的所有可用服務，並讓您選取服務的輸入和輸出欄位。 您也可以使用&#x200B;**[!UICONTROL 設定值]**&#x200B;規則型別來叫用表單資料模型服務，並將欄位值設定為服務傳回的輸出。

例如，下列規則會叫用以Employee Id作為輸入的get服務，而傳回的值會填入表單中對應的Dependent Id、Last Name、First Name和Gender欄位。

![叫用服務](assets/invoke-service.png)

此外，您可以使用`guidelib.dataIntegrationUtils.executeOperation` API在規則編輯器的程式碼編輯器中撰寫JavaScript。<!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->

### 使用自訂函式叫用表單資料模型(FDM) {#invoke-form-data-model-using-custom-functions}

您可以使用自訂函式[，從規則編輯器](/help/forms/rule-editor.md#custom-functions-in-rule-editor-custom-functions)叫用表單資料模型。 若要叫用表單資料模型(FDM)，請將表單資料模型新增至允許清單。 若要將表單資料模型新增至允許清單：

1. 前往`https://server:host/system/console/configMgr`的Experience Manager Web主控台。
1. 尋找&#x200B;**[!UICONTROL 用於服務引動的最適化表單層級白名單 — 組態處理站]**。
1. 按一下![加號圖示](/help/forms/assets/Smock_Add_18_N.svg)圖示以新增組態。
1. 新增&#x200B;**[!UICONTROL 內容路徑模式]**&#x200B;以指定最適化Forms的位置。  預設值為`/content/forms/af/(.*)`，其中包含所有最適化Forms。 您也可以指定特定最適化表單的路徑。
1. 新增&#x200B;**[!UICONTROL 表單資料模型路徑模式]**&#x200B;以指定表單資料模型(FDM)的位置。 預設值為`/content/dams/formsanddocuments-fdm/(.*)`，其中包含所有表單資料模型(FDM)。 您也可以指定特定表單資料模型(FDM)的路徑。
1. 儲存設定。

新增的組態會儲存在&#x200B;**[!UICONTROL 用於服務引動的最適化表單資料模型最適化表單層級白名單中 — 組態處理站]**&#x200B;選項。

>[!VIDEO](https://video.tv.adobe.com/v/3423977/adaptive-forms-custom-function-rule-editor)

>[!NOTE]
>
> 若要透過AEM原型專案使用自訂函式，從規則編輯器叫用表單資料模型(FDM)：
>
>1. [建立組態檔](https://github.com/adobe/aem-core-forms-components/blob/master/it/config/src/main/content/jcr_root/apps/system/config/com.adobe.aemds.guide.factory.impl.AdaptiveFormFDMConfigurationFactoryImpl~core-components-it.cfg.json)。
>1. 設定getContentPathPattern和getFormDataModelPathPattern的屬性。
>1. 部署專案。

## 相關文章

{{af-submit-action}}

