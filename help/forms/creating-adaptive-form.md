---
title: 如何建立最適化表單？
description: '了解如何使用 [!DNL Experience Manager Forms]. 適用性Forms是回應式HTML5表單，可簡化資訊收集和處理。 進一步了解如何根據表單資料模型和XML或JSON結構建立最適化表單。 '
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: bcd9f3cfe6c22a6db51a9e6f96576bb8cdde7d0c
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# 建立最適化表單 {#creating-an-adaptive-form}


適用性Forms可讓您建立吸引人、回應式、動態且最適化的表單。 AEM Forms提供商務使用者易記精靈，可快速撰寫最適化Forms。 精靈提供快速的索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項，以建立最適化表單。

<!-- 

You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form: 

-->

![建立最適化表單的精靈](/help/release-notes/assets/wizard.png)

<!-- 

Adaptive Forms allow you to create forms that are engaging, responsive, dynamic, and adaptive. [!DNL AEM Forms] provides an intuitive wizard and out-of-the-box components to create Adaptive Forms. You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form:

* **Using a form data model**
  [Data integration](data-integration.md) lets you integrate entities and services from disparate data sources in to a Form Data Model that you can use to create Adaptive Forms. Choose Form Data Model if the Adaptive Form you are creating involves fetching and write data from and to multiple data source.

  <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. 

* **Using an XML Schema Definition (XSD) or a JSON Schema**
   XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate the schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema will be available for use in the Data Model Objects tab of the Content browser when authoring Adaptive Forms.

* **Using none or without a form model**
   Adaptive Forms created with this option don’t use any form model. The data XML generated from such forms has flat structure with fields and corresponding values. -->

## 先決條件

您需要下列項目才能建立最適化表單：

* **最適化表單範本**:範本提供基本結構並定義最適化表單的外觀（配置和樣式）。 它具有包含特定屬性和內容結構的預格式化元件。 它還提供定義主題和提交動作的選項。 主題定義外觀和風格，並定義提交動作，以便在提交最適化表單時採取動作。 例如，將收集的資料傳送至資料來源。 雲端服務支援兩種範本：

   * **可編輯的範本**:您可以 [建立新](template-editor.md) 或 [匯入現有的可編輯範本](migrate-to-forms-as-a-cloud-service.md). 您也可以部署 [最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20基於Java的%20integration%20tests。) 以取得一些可編輯的範本範例。
   * **靜態範本**:這些是舊版範本，僅建議從Adobe Managed Services(AMS)和內部部署AEM Forms安裝(AEM 6.5 Forms或更舊版本)移轉的客戶使用。 這些功能可讓您繼續運用現有靜態範本投資。 建立新的適用性表單時，建議使用可編輯的範本。

* **最適化表單主題**:主題包含元件和面板的樣式詳細資料。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 應用主題時，指定的樣式會反映在相應的元件上。 您可以 [建立新主題](themes.md) 或 [導入現有主題](import-export-forms-templates.md#uploading-a-theme). 您也可以部署 [最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project) 樣主題。

* **權限**:將使用者新增至 [!DNL forms-users] 提供建立最適化表單的權限。 如需特定使用者群組的表單詳細清單，請參閱 [群組和權限](forms-groups-privileges-tasks.md).

1. 存取 [!DNL Experience Manager Forms] 製作例項。 可以是雲端例項或本機開發例項。

1. 在Experience Manager登入頁面上輸入您的憑證。

   登入後，在左上角，點選 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.

1. 點選 **[!UICONTROL 建立]**  > **[!UICONTROL 適用性Forms]**. 精靈隨即開啟。
1. 在源頁簽中，選擇模板：

   * 選取可編輯的範本時，會自動選取範本中指定的主題和提交動作，並 **[!UICONTROL 建立]** 按鈕。 您可以前往 **[!UICONTROL 樣式]** 或 **[!UICONTROL 提交]** 頁簽，以選擇不同的主題或提交操作。 如果所選的可編輯模板未指定主題，則建立按鈕將保持禁用狀態。 您可以前往 **[!UICONTROL 樣式]** 頁簽，手動選擇主題。
   * 選取靜態範本時，資料、樣式、提交、傳送和預覽選項無法使用。 建立新的適用性表單時，建議使用可編輯的範本。

1. 在樣式標籤中，選擇主題：
   * 當所選模板指定主題時，該主題將在嚮導中自動選中。 您也可以從「樣式」索引標籤中選擇不同的主題。
   * 如果所選模板未指定主題，則可以使用「樣式」頁簽選擇主題。 此 **[!UICONTROL 建立]** 按鈕僅在選取主題後啟用。
1. （可選）在「資料」索引標籤中，選取資料模型：
   * **表單資料模型**:A [表單資料模型](data-integration.md) 可讓您將不同資料來源的實體和服務整合至最適化表單。 如果您建立的適用性表單涉及從多個資料來源擷取資料並將其寫入多個資料來源，請選擇「表單資料模型」。
   * **JSON結構**: [JSON結構](adaptive-form-json-schema-form-model.md) 代表組織內後端系統產生或使用資料的結構。 您可以將結構與適用性表單建立關聯，並使用其元素將動態內容新增至適用性表單。 製作適用性Forms時，結構的元素可用於內容瀏覽器的「資料模型物件」索引標籤，所有欄位也會新增至新建立的適用性表單。

   預設情況下，會選取資料模型的所有欄位。 建立適用性表單時，所有選取的資料模型欄位都會轉換為對應的適用性表單元件。 精靈提供您的核取方塊，以僅選取應包含在適用性表單中的欄位。

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. 在「提交」頁簽中，選擇提交操作：

   * 選取範本時，會自動選取範本中指定的提交動作。 您可以從「提交」頁簽中選擇不同的提交操作。 此 **[!UICONTROL 提交]** 標籤顯示所有可用的提交操作。

   * 當選取的範本未指定提交動作時，您可以使用 **[!UICONTROL 提交]** 頁簽以選擇提交操作

1. （選用）在「傳送」索引標籤中，您可以指定最適化表單的發佈或取消發佈日期。

1. 點選 **[!UICONTROL 建立]**. 此時會出現一個對話方塊，用於指定標題、名稱和儲存最適化表單的位置：

   * **[!UICONTROL 標題]** 指定表單的顯示名稱。 標題可協助您識別 [!DNL Experience Manager Forms] 使用者介面。
   * **[!UICONTROL 名稱：]** 指定表單的名稱。 在儲存庫中建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。
   * **[!UICONTROL 路徑：]** 指定最適化表單的儲存位置。 您可以直接在 `/content/dam/formsanddocuments` 或建立資料夾，例如 `/content/dam/formsanddocuments/adaptiveforms` 以儲存最適化表單。 在路徑中使用資料夾之前，請確定已建立該資料夾。 此 **[!UICONTROL 路徑：]** 欄位不會自動建立資料夾。

1. 點選 **[!UICONTROL 建立]**. 適用性表單會建立並在適用性Forms編輯器中開啟。 編輯器會顯示範本中的可用內容。 它也會顯示邊欄，以根據需求自訂新建立的表單。

   根據最適化表單的類型，關聯 <!--XFA form template, XML schema or --> JSON結構描述或表單資料模型會顯示在 **[!UICONTROL 資料模型物件]** 的 **[!UICONTROL 內容瀏覽器]** 欄。 您也可以拖放這些元素來建立最適化表單。

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Tap to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Create an Adaptive Form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, tap on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Tap **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and tap Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
    * **[!UICONTROL Search in repository]** - Select this option to select from the list of schema definition files available in the repository. Select the XML or JSON schema file as form model. The selected schema is associated with the form by reference and is accessible for use in other Adaptive Forms.

      Ensure that the JSON schema filename ends with **.schema.json**. For example: mySchema.schema.json

   ![Selecting XML or JSON schema](assets/upload-schema.png)
**Figure:** *Selecting XML or JSON schema*

1. (For XML schema only) After you select or upload an XML Schema, specify a root element of the selected XSD file to map with the Adaptive Form.

   ![Selecting XSD root element](assets/xsd-root-element.png)
**Figure:** *Selecting XSD root element*

>[!NOTE]
>
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model). -->

## 編輯最適化表單的表單模型屬性 {#edit-form-model}

您可以變更最適化表單的表單模型（以JSON為基礎或表單資料模型）。 不能將一個表單模型更改為另一個表單模型。

1. 選取「適用性表單」，然後點選 **屬性** 表徵圖。
1. 開啟 **[!UICONTROL 表單模型]** 標籤，然後執行下列任一操作。

   * 如果適用性表單沒有表單模型，則可以選擇其他表單模型並相應地選擇 <!-- a form template, --> XML或JSON結構，或表單資料模型。
   * 如果適用性表單是以表單模型為基礎，您可以選擇其他表單 <!-- form template, --> XML或JSON結構，或相同表單模型的表單資料模型。

1. 點選 **[!UICONTROL 儲存]** 以儲存屬性。
