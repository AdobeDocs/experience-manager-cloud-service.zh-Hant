---
title: 如何建立自適應表單？
description: '瞭解如何使用 [!DNL Experience Manager Forms]。 自適應Forms是可以簡化資訊收集和處理的響應性HTML5表。 更深入地瞭解如何基於表單資料模型和XML或JSON架構建立自適應表單。 '
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: b29d11550ee8b7671059a1f04de37c7b79658a60
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# 建立最適化表單 {#creating-an-adaptive-form}


自適應Forms允許您建立具有吸引力、響應性、動態性和適應性的表單。 AEM Forms提供了業務用戶友好嚮導，可快速編寫AdaptiveForms。 該嚮導具有快速頁籤導航功能，可輕鬆選擇預配置的模板、樣式、欄位和提交選項以建立自適應表單。

<!-- 

You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form: 

-->

![用於建立自適應表單的嚮導](/help/release-notes/assets/wizard.png)

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

您需要使用以下命令建立「自適應表單」：

* 自適應表單模板：模板提供基本結構並定義自適應表單的外觀（佈局和樣式）。 它具有預格式化的元件，包含某些屬性和內容結構。 它還提供了定義主題和提交操作的選項。 該主題定義外觀和感覺並提交操作定義在提交自適應表單時要採取的操作。 例如，將收集的資料發送到資料源。 你可以 [建立新模板](template-editor.md) 或導入現有模板。 您還可以部署 [最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.test%3A%20是%20基於Java的%20整合%20test。) 的下界。
* 自適應表單主題：主題包含元件和面板的樣式詳細資訊。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 應用主題時，指定的樣式會反映在相應的元件上。 你可以 [建立新主題](themes.md)。 [導入現有主題](import-export-forms-templates.md#uploading-a-theme)，或下載並導入 [示例主題](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:2779f80e-16ba-4cd1-a96f-8e2b53f3be25)。 您還可以部署 [最新原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.test%3A%20是%20基於Java的%20整合%20test。) 的下界。
* 將用戶添加到 [!DNL forms-users] 為他們提供建立自適應表單的權限。 有關特定用戶組的表單的詳細清單，請參見 [組和權限](forms-groups-privileges-tasks.md)。

## 建立最適化表單 {#strong-create-an-adaptive-form-strong}

按照以下步驟建立「自適應表單」。

1. 訪問 [!DNL Experience Manager Forms] 作者實例。 它可以是雲實例或本地開發實例。

1. 在Experience Manager登錄頁上輸入憑據。

   登錄後，在左上角，點擊 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。

1. 點擊 **[!UICONTROL 建立]**  > **[!UICONTROL 自適應Forms]**。 將開啟嚮導。
1. 在「源」頁籤中，選擇模板：
   * 選擇模板時，將自動選擇模板中指定的主題和提交操作，並啟用「建立」按鈕。 您可以轉到「樣式」或「提交」頁籤，以選擇其他主題或「提交」操作。
   * 如果所選模板未指定主題，則「建立」按鈕仍處於禁用狀態。 您可以轉到「樣式」頁籤以手動選擇主題。
1. 在「樣式」頁籤中，選擇一個主題：
   * 當所選模板指定主題時，將在嚮導中自動選擇主題。 可以從「樣式」頁籤中選擇不同的主題。
   * 如果所選模板未指定主題，則可以使用「樣式」頁籤選擇主題。 選擇主題後，將啟用「建立」按鈕。
1. （可選）在「資料」頁籤中，選擇一個資料模型：
   * 表單資料模型：A [窗體資料模型](data-integration.md) 允許您將不同資料源中的實體和服務整合到自適應表單。 如果要建立的自適應表單涉及從多個資料源讀取和寫入資料，請選擇「表單資料模型」。
   * JSON架構：JSON架構表示組織中後端系統生成或使用資料的結構。 可以將模式與自適應表單相關聯，並使用其元素將動態內容添加到自適應表單。 創作自適應Forms時，模式的元素可用於內容瀏覽器的「資料模型對象」頁籤中，並且所有欄位也添加到新建立的自適應表單中。
1. 在提交標籤中，選擇提交操作：
   * 選擇模板時，將自動選擇在模板中指定的提交操作。 您可以從「提交」標籤中選擇其他「提交」操作。 「提交」標籤顯示所有可用的提交操作。
   * 如果所選模板未指定提交操作，則可以使用「提交」頁籤選擇提交操作

1. （可選）在「傳遞」頁籤中，可以為自適應表單指定發佈或取消發佈日期。

1. 按一下「建立」。 將顯示一個對話框，用於指定標題、名稱和位置以保存自適應表單：

   * **[!UICONTROL 標題：]** 指定窗體的顯示名稱。 標題可幫助您在 [!DNL Experience Manager Forms] 用戶介面。
   * **[!UICONTROL 名稱：]** 指定窗體的名稱。 在儲存庫中建立具有指定名稱的節點。 開始鍵入標題時，將自動生成名稱欄位的值。 您可以更改建議的值。 名稱欄位只能包含字母數字字元、連字元和下划線。 所有無效輸入都用連字元替換。
   * **[!UICONTROL 路徑：]** 指定自適應表單的保存位置。 您可以直接在 `/content/dam/formsanddocuments` 或建立資料夾，如 `/content/dam/formsanddocuments/adaptiveforms` 的子菜單。 確保在路徑中使用資料夾之前先建立該資料夾。 「路徑」欄位不會自動建立資料夾。

1. 點擊 **[!UICONTROL 建立]**。 將建立一個自適應表單，並在自適應Forms編輯器中開啟。 編輯器顯示模板中的可用內容。 它還顯示邊欄，以根據需要定制新建立的表單。

   根據「自適應表單」的類型，在關聯的 <!--XFA form template, XML schema or --> JSON架構或表單資料模型顯示在 **[!UICONTROL 資料模型對象]** 頁籤 **[!UICONTROL 內容瀏覽器]** 欄。 也可以拖放這些元素來構建自適應表單。

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

## 編輯自適應表單的表單模型屬性 {#edit-form-model}

您可以更改自適應表單（基於JSON或表單資料模型）的表單模型。 不能從一個窗體模型更改為另一個窗體模型。

1. 選擇「自適應表單」並點擊 **屬性** 表徵圖
1. 開啟 **[!UICONTROL 窗體模型]** ，然後執行以下操作之一。

   * 如果「自適應表單」沒有表單模型，則可以選擇另一個表單模型，並相應地選擇 <!-- a form template, --> XML或JSON架構或表單資料模型。
   * 如果「自適應表單」基於表單模型，則可以選擇其他 <!-- form template, --> XML或JSON架構，或同一表單模型的表單資料模型。

1. 點擊 **[!UICONTROL 保存]** 的子菜單。
