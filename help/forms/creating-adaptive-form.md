---
title: 表單產生器：使用基礎元件建立表單
description: 瞭解如何使用AEM Forms的表單產生器，以建立具有基礎元件的調適型表單。 非常適合表單建立者維護現有表單或使用舊版整合。
keywords: 表單產生器， foundation元件，建立表單，表單建立器，調適型表單，建立表單， AEM forms，表單製作器
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 62%

---

# 表單產生器：使用基礎元件建立表單 {#creating-an-adaptive-form}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html) |
| AEM as a Cloud Service  | 本文章 |


>[!NOTE]
>
> Adobe建議針對[建立新的Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)或[將Adaptive Forms新增至AEM Sites頁面](/help/forms/creating-adaptive-form-core-components.md)，使用現代且可擴充的資料擷取[核心元件](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文說明使用基礎元件製作最適化Forms的舊方法。

AEM Forms的表單產生器可讓您建立吸引人、回應式、動態且最適化的表單。 無論您是維護現有基礎表單的表單建立者，還是需要快速建立包含已建立元件的表單，AEM Forms都能提供使用者易用的精靈。 精靈具有快速索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項。

開始之前，請先了解您可以使用的表單元件類型：

* [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)是標準化的資料擷取元件。 這些元件提供自訂功能、縮短開發時間，並降低數位註冊體驗的維護成本。 開發人員可以輕鬆地自訂這些元件和設計其樣式。Adobe建議使用這些現代且可擴展的元件來開發最適化Forms。

* [最適化Forms Foundation元件](creating-adaptive-form.md)是傳統（舊）資料擷取元件。 您可以繼續使用這些元件來編輯以現有基礎元件為主的最適化表單。如果您要建立新表單，Adobe建議使用[最適化Forms核心元件](creating-adaptive-form-core-components.md)來建立最適化Forms。



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
   XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate the schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available for use in the Data Model Objects tab of the Content browser when authoring Adaptive Forms.

* **Using none or without a form model**
   Adaptive Forms created with this option do not use any form model. The data XML generated from such forms has flat structure with fields and corresponding values. -->

## 必要條件

您必須符合以下條件才能建立最適化表單：

* **權限**：將您的使用者新增到 [!DNL forms-users]，以便為他們提供建立最適化表單的權限。如需表單特定使用者群組的詳細清單，請參閱[群組與許可權](forms-groups-privileges-tasks.md)。

* **最適化表單主題**：主題包含元件和面板的樣式詳細資料。樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。套用主題時，指定的樣式會反映在對應的元件上。您可以[建立主題](themes.md)或[匯入現有主題](import-export-forms-templates.md#uploading-a-theme)。 您也可以針對一些範例主題部署[最新的原型版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project)。

* **最適化表單範本**：此範本會提供基本結構並定義最適化表單的外觀 (版面和樣式)。其中具有包含特定屬性和內容結構的預先格式化元件。它也會提供定義主題和提交動作的選項。主題會定義外觀，而提交動作會定義提交最適化表單時要採取的動作。例如，將所收集的資料傳送到資料來源。雲端服務支援兩種類型的範本：

   * **可編輯的範本**：您可以[建立](template-editor.md)或[匯入現有的可編輯的範本](migrate-to-forms-as-a-cloud-service.md)。 您也可以部署[最新的原型版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=zh-Hant#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20Java-based%20integration%20tests.)以取得一些可編輯範本範例。

   * **靜態範本**：這些是舊範本，建議僅用於從 Adobe Managed Services (AMS) 和內部部署 AEM Forms 安裝 (AEM 6.5 Forms 或更早版本) 移轉的客戶。這些範本可讓您繼續使用對靜態範本的現有投資。建立最適化表單時，請使用可編輯的範本。



## 建立最適化表單（基礎元件） {#create-an-adaptive-form-foundation-components}

1. 存取 [!DNL Experience Manager Forms] 作者執行個體；可以是 Cloud 執行個體或本機開發執行個體。

1. 在 Experience Manager 登入頁面上輸入您的認證。

   登入後，在左上角選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。

1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 自適應表單]**」。此時會開啟精靈。
1. 在「來源」標籤中，選取一個範本：

   * 選取可編輯範本時，系統會自動選取範本中指定的主題和提交動作，且「**[!UICONTROL 建立]**」按鈕已啟用。您可以前往「**[!UICONTROL 樣式]**」或「**[!UICONTROL 提交]**」標籤，選取不同的主題或提交動作。如果選取的可編輯範本並未指定主題，則「建立」按鈕將維持停用狀態。您可以前往「**[!UICONTROL 樣式]**」標籤以手動選取主題。

     >[!NOTE]
     >
     > 您也可以使用最適化表單編輯器建立「[!UICONTROL 記錄文件]」範本。如需更多資訊，請參閱[最適化表單編輯器中的記錄文件支援](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)。

   * 選取靜態範本時，無法使用資料、樣式、提交、傳遞和預覽選項。建立最適化表單時，請使用可編輯的範本。

1. 在「**[!UICONTROL 樣式]**」標籤中，選取一個主題：

   * 所選取的範本指定主題時，就會在精靈中自動選取該主題。您也可以從「樣式」標籤中選擇不同的主題。
   * 如果選取的範本未指定主題，您可以使用「樣式」標籤選擇主題。只有在選取主題之後，「**[!UICONTROL 建立]**」按鈕才會啟用。

1. (選用) 在「**[!UICONTROL 資料]**」標籤中，選取一個資料模型：

   * **表單資料模型**：[表單資料模型](data-integration.md)可讓您將來自分散資料來源的實體和服務整合到最適化表單。如果您要建立的最適化表單涉及從多個資料來源擷取及寫入資料，請選擇表單資料模型(FDM)。

   * **JSON 結構描述**：[JSON 結構描述](adaptive-form-json-schema-form-model.md)代表組織內後端系統產生或使用之資料的結構。您可以將結構描述與最適化表單建立關聯，並使用其元素將動態內容新增到最適化表單。編寫Adaptive Forms時，可在內容瀏覽器的「資料模型物件」索引標籤中使用結構描述的元素，所有欄位也會新增到已建立的Adaptive Form。

   系統預設會選取資料模型的所有欄位。建立最適化表單時，所有選取的資料模型欄位都會轉換成對應的最適化表單元件。精靈會為您提供核取方塊，以便您只選取要在最適化表單中包含哪些欄位。

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. 在「**[!UICONTROL 提交]**」標籤中，選取提交動作：

   * 您選取範本後，系統會自動選取範本中指定的提交動作。您可以從「提交」標籤選取不同的提交動作。「**[!UICONTROL 提交]**」標籤會顯示所有可用的提交動作。

   * 所選取的範本未指定提交動作時，您可以使用「**[!UICONTROL 提交]**」標籤選取提交動作

1. (選用) 在「傳遞」標籤中，您可以為最適化表單指定發佈或取消發佈日期。

1. 選擇 **[!UICONTROL 建立]**。此時會顯示一個對話框，以指定標題、名稱和儲存最適化表單的位置：

   * **[!UICONTROL 標題：]**&#x200B;指定表單的顯示名稱。標題有助於在 [!DNL Experience Manager Forms] 使用者介面中識別表單。
   * **[!UICONTROL 名稱：]**&#x200B;指定表單的名稱。存放庫中會建立具有指定名稱的節點。您開始輸入標題時，就會自動產生名稱欄位的值。您可以變更建議的值。名稱欄位只能包含字母數字字元、連字號和底線。所有無效的輸入都會以連字號取代。
   * **[!UICONTROL 路徑：]**&#x200B;指定最適化表單的儲存位置。您可以將最適化表單直接儲存在 `/content/dam/formsanddocuments`，或建立一個資料夾 (例如 `/content/dam/formsanddocuments/adaptiveforms`) 以儲存最適化表單。要使用路徑中的資料夾之前，請務必先建立該資料夾。「**[!UICONTROL 路徑：]**」欄位不會自動建立資料夾。

1. 選擇 **[!UICONTROL 建立]**。此時已建立最適化表單，並在最適化表單編輯器中開啟。編輯器會顯示範本中可用的內容，它也會顯示側邊欄，以根據需求自訂建立的表單。

   根據最適化表單的型別，相關<!--XFA form template, XML schema or --> JSON結構描述或表單資料模型(FDM)中存在的表單元素會顯示在側邊欄中&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;的&#x200B;**[!UICONTROL 資料模型物件]**&#x200B;索引標籤中。 您也可以拖放這些元素以建置自己的最適化表單。

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Select to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Build an adaptive form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, select on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Select **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and select Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
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

您可以變更最適化表單 (JSON 型或表單資料模型) 的表單模型。您無法從一種表單模型變更為另一種表單模型。

1. 選取最適化表單並選取&#x200B;**屬性**&#x200B;圖示。
1. 開啟「**[!UICONTROL 表單模型]**」標籤，並執行以下其中一項操作。

   * 如果最適化表單沒有表單模型，您可以選擇其他表單模型，並相應地選擇<!-- a form template, --> XML或JSON結構描述或表單資料模型(FDM)。
   * 如果最適化表單是以表單模型為基礎，您可以為相同表單模型選擇其他<!-- form template, --> XML或JSON結構描述，或表單資料模型(FDM)。

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存屬性。

您也可以從最適化表單產生器或最適化表單範本產生器修改表單模型屬性。

1. 選取「**[!UICONTROL 最適化表單容器 (根)]**」元件。
1. 按一下 ![設定圖示](/help/forms/assets/configure-icon.svg) 圖示以開啟最適化表單容器的「**[!UICONTROL 屬性]**」。
1. 選取「**[!UICONTROL 資料模型]**」標籤，並執行以下其中一項操作：

   * 如果最適化表單沒有表單模型，您可以選擇表單模型，並相應地選擇<!-- a form template, --> XML或JSON結構描述或表單資料模型(FDM)。
   * 如果最適化表單是以表單模型為主，則無法變更表單模型。您可以為適用的相同表單模型選擇其他<!-- form template, --> XML或JSON結構描述，或表單資料模型(FDM)。
1. 選取![儲存](/help/forms/assets/check-button.png)以儲存屬性。

![FDM-Schema-Support](/help/forms/assets/fdmsupport.png)

>[!NOTE]
>
> 您也可以將自適應表單另存為範本。 如需更多資訊，請參閱[使用最適化表單建立範本](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template)。

## 如何重新命名AEM最適化表單？ {#rename-an-AEM-Adaptive-Form}

若要重新命名最適化表單，請執行下列步驟：

1. 在您的AEM Forms使用者介面中選取最適化表單。
1. 按一下位於上方邊欄上的&#x200B;**屬性**。
1. 變更&#x200B;**標題**&#x200B;標籤中的表單名稱，如下圖所示。
1. 按一下「**儲存並關閉**」。

![重新命名AEM最適化表單](/help/forms/assets/change-af-name.png)

## 另請參閱 {#see-also}

{{see-also}}
