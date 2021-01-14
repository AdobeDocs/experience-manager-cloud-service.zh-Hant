---
title: 內容片段模型
description: 內容片段模型可用來建立包含結構化內容的內容片段。
translation-type: tm+mt
source-git-commit: da8fcf1288482d406657876b5d4c00b413461b21
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 9%

---


# 內容片段模型 {#content-fragment-models}

>[!CAUTION]
>
>內容片段傳送的AEM GraphQL API可應要求提供。
>
>請連絡[Adobe支援](https://experienceleague.adobe.com/?lang=en&amp;support-solution=General#support)以啟用AEM雲端服務方案的API。

內容片段模型定義[內容片段](/help/assets/content-fragments/content-fragments.md)的內容結構。

若要使用內容片段模型，請：

1. [為您的例項啟用內容片段模型功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [建立](#creating-a-content-fragment-model)，並設 [定內容](#defining-your-content-fragment-model)片段模型
1. [啟用您的內容片段](#enabling-disabling-a-content-fragment-model) 模型，以便在建立內容片段時使用

## 建立內容片段模型{#creating-a-content-fragment-model}

1. 導覽至&#x200B;**工具**、**資產**，然後開啟&#x200B;**內容片段模型**。
1. 導覽至適合您[configuration](/help/assets/content-fragments/content-fragments-configuration-browser.md)的資料夾。
1. 使用&#x200B;**Create**&#x200B;開啟嚮導。

   >[!CAUTION]
   >
   >如果[未啟用內容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，則&#x200B;**Create**&#x200B;選項將不可用。

1. 指定「模 **型標題」**。您也可以視需要新增&#x200B;**Tags**&#x200B;和&#x200B;**Description**。

   ![標題和說明](assets/cfm-models-02.png)

1. 使用&#x200B;**Create**&#x200B;來儲存空的模型。 一條消息將指示操作成功，您可以選擇&#x200B;**Open**&#x200B;立即編輯模型，或選擇&#x200B;**Done**&#x200B;返回控制台。

## 定義內容片段模型{#defining-your-content-fragment-model}

所述內容片段模型使用選擇&#x200B;**[資料類型](#data-types)**&#x200B;有效地定義所生成的內容片段的結構。 使用模型編輯器，您可以新增資料類型的例項，然後設定它們以建立必要欄位：

>[!CAUTION]
>
>編輯現有的內容片段模型可能會影響相依片段。

1. 導覽至&#x200B;**工具**、**資產**，然後開啟&#x200B;**內容片段模型**。

1. 導覽至包含內容片段模型的檔案夾。
1. 開啟&#x200B;**Edit**&#x200B;所需的型號；使用快速動作，或從工具列中選取模型和動作。

   開啟模型編輯器後，會顯示：

   * 左：欄位已定義
   * 右：資 **料類型** ，可用於建立欄位( **和屬性** ，以供建立欄位後使用)

   >[!NOTE]
   >
   >當欄位為「必 **要**」時，左側窗格中指出的「標籤 **」將會標示為字元(** *****)。

1. **要添加欄位**

   * 將必要的資料類型拖曳至欄位的必要位置。

   * 將欄位添加到模型後，右側面板將顯示可為該特定資料類型定義的&#x200B;**屬性**。 您可以在這裡定義該欄位的必要項目。
許多屬性都不言而喻，如需詳細資訊，請參閱[Properties](#properties)。

1. **刪除欄位**

   選取必要欄位，然後按一下／點選垃圾桶圖示。 系統會要求您確認動作。

1. 新增所有必填欄位，並視需要定義相關屬性。

1. 選擇&#x200B;**保存**&#x200B;以保存定義。

<!--
## Defining your Content Fragment Model {#defining-your-content-fragment-model}

The content fragment model effectively defines the structure of the resulting content fragments using a selection of **[Data Types](#data-types)**. Using the model editor you can add instances of the data types, then configure them to create the required fields:

>[!CAUTION]
>
>Editing an existing content fragment model can impact dependent fragments.

1. Navigate to **Tools**, **Assets**, then open **Content Fragment Models**.

1. Navigate to the folder holding your content fragment model.
1. Open the required model for **Edit**; use either the quick action, or select the model and then the action from the toolbar.

   Once open the model editor shows:

    * left: fields already defined
    * right: **Data Types** available for creating fields (and **Properties** for use once fields have been created)

   >[!NOTE]
   >
   >When a field as **Required**, the **Label** indicated in the left pane will be marked with an asterix (**&#42;**).

   ![properties](assets/cfm-models-03.png)

1. **To Add a Field**

    * Drag a required data type to the required location for a field:

      ![data type to field](assets/cfm-models-04.png)

    * Once a field has been added to the model, the right panel will show the **Properties** that can be defined for that particular data type. Here you can define what is required for that field. 
      Many properties are self-explanatory, for additional details see [Properties](#properties).
      For example:

      ![field properties](assets/cfm-models-05.png)

1. **To Remove a Field**

   Select the required field, then click/tap the trash-can icon. You will be asked to confirm the action.

   ![remove](assets/cfm-models-06.png)

1. Add all required fields, and define the related properties, as required. For example:

   ![save](assets/cfm-models-07.png)

1. Select **Save** to persist the definition.
-->

## 資料類型 {#data-types}

可以選擇資料類型來定義模型：

* **單行文字**
   * 在一行文字中新增一或多個欄位；最大長度可以定義
* **多行文字**
   * 文字區域可以是Rich Text、Plain Text或Markdown
* **數量**
   * 添加一個或多個數字欄位
* **布林值 (Boolean)**
   * 新增布林核取方塊
* **日期時間**
   * 新增日期和／或時間
* **列舉**
   * 新增一組核取方塊、選項按鈕或下拉式欄位
* **標記**
   * 允許片段作者存取和選取標籤區域
* **內容參考資料**
   * 參考任何類型的其他內容；可用於[建立巢狀內容](#using-references-to-form-nested-content)

<!--
* **Fragment Reference**
  * References other content fragments; can be used to [create nested content](#using-references-to-form-nested-content)
  * The data type can be configured to allow fragment authors to:
    * Edit the referenced fragment directly.
    * Create a new content fragment, based on the appropriate model  
* **JSON Object**
  * Allows the content fragment author to enter JSON syntax into the corresponding elements of a fragment. 
    * To allow AEM to store direct JSON that you have copy/pasted from another service.
    * The JSON will be passed through, and output as JSON in GraphQL.
    * Includes JSON syntax-highlighting, auto-complete and error-highlighting in the content fragment editor.
-->

## 屬性 {#properties}

許多屬性都不言自明，對於某些屬性，其他詳細資訊如下：

* **演算**
方式用於實現／演算片段中欄位的各種選項。這通常可讓您定義作者將看到欄位的單一執行個體，或允許建立多個執行個體。

* **欄位**
標籤輸入 
**欄位** 標籤會自動產 **生屬性名稱**，然後視需要手動更新。

* **ValidationBasic**
驗證可由Required屬性等機 **** 制使用。有些資料類型有附加驗證欄位。 如需詳細資訊，請參閱[Validation](#validation)。

* 對於「多行」 **資料類型** ，可將「預設類型 **** 」定義為：

   * **RTF**
   * **Markdown**
   * **純文字**

   如果未指定，則此欄位將使用預設值&#x200B;**Rich Text**。

   在內容 **片段模型中變更「預設類型** 」，只會在編輯器中開啟並儲存該片段後，對現有、相關的內容片段生效。

<!--
* **Translatable**
  Checking the "Translatable" checkbox on a field in CF model editor will

  * Ensure the field's property name is added in translation config, context `/content/dam/<tenant>`, if not already present. 
  * For GraphQL: set a `<translatable>` property on the Content Fragment field to `yes`, to allow GraphQL query filter for JSON output with only translatable content.

* See **[Fragment Reference (Nested Fragments)](#fragment-reference-nested-fragments)** for more details about that specific data type and its properties.
-->

## 驗證{#validation}

現在，各種資料類型都可能定義驗證需求，以便在產生的片段中輸入內容：

* **單行文字**
   * 比較預先定義的規則運算式。
* **數量**
   * 檢查特定值。

<!--
* **Content Reference**
  * Test for specific types of content.
  * Only images within a predefined range of width and height (in pixels) can be referenced. 
  * Only assets of specified file size or smaller can be referenced. 
  * Only predefined file types can be referenced.
  * No more than the predefined number of assets can be referenced. 
  * No more than the predefined number of fragments can be referenced.
* **Fragment Reference**
  * Test for a specific content fragment model.
-->

<!--
## Using References to form Nested Content {#using-references-to-form-nested-content}

Content Fragments can form nested content, using either of the following data types:

* **[Content Reference](#content-reference)**
  * Provides a simple reference to other content; of any type.
  * Can be configured for a one or multiple references (in the resulting fragment).

* **[Fragment Reference](#fragment-reference-nested-fragments)** (Nested Fragments)
  * References other fragments, dependent on the specific models specified.
  * Allows you to include/retrieve structured data.
    >[!NOTE]
    >
    >This method is of particular interest in conjunction with [Headless Content Delivery using Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
  * Can be configured for one or multiple references (in the resulting fragment)..

>[!NOTE]
>
>AEM has a recurrence protection for:
>
>* Content References
>  This prevents the user from adding a reference to the current fragment. This may lead to an empty Fragment Reference picker dialog.
>
>* Fragment References in GraphQL 
>  If you create a deep query that returns multiple Content Fragments referenced by each another, it will return null at first occurence.

### Content Reference {#content-reference}

The Content Reference allows you to render content from another source; for example, image or content fragment.

In addition to standard properties you can specify:

* The **Root Path** for any referenced content.
* The content types that can be referenced.
* Limitations for file sizes.
* Image restraints.
-->

<!-- Check screenshot - might need update

   ![Content Reference](assets/cfm-content-reference.png)
-->

<!--
### Fragment Reference (Nested Fragments) {#fragment-reference-nested-fragments}

The Fragment Reference references one, or more, content fragments. This feature of particular interest when retrieving content for use in your app, as it allows you to retrieve structured data with multiple layers.

For example:

* A model defining details for an employee; these include:
  * A reference to the model that defines the employer (company)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
>
>This is of particular interest in conjunction with [Headless Content Delivery using Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

In addition to standard properties you can define:

* **Render As**:

  * **multifield** - the fragment author can create multiple, individual, references

  * **fragmentreference** - allows the fragment author to select a single reference to a fragment

* **Model Type**
  Multiple models can be selected. When authoring the Content Fragment any referenced fragments must have been created using these models.

* **Root Path**
  This specifies a root path for any fragments referenced.

* **Allow Fragment Creation**

  This will allow the fragment author to create a new fragment based on the appropriate model.
-->

<!--
  * **fragmentreferencecomposite** - allows the fragment author to build a composite, by selecting multiple fragments
-->

<!-- Check screenshot - might need update

   ![Fragment Reference](assets/cfm-fragment-reference.png)
-->

<!--
>[!NOTE]
>
>A recurrence protection mechanism is in place. It prohibits the user from selecting the current Content Fragment in the Fragment Reference. This may lead to an empty Fragment Reference picker dialog.
>
>There is also a recurrence protection for Fragment References in GraphQL. If you create a deep query across two Content Fragments that reference each other, it will return null.
-->

## 啟用或停用內容片段模型{#enabling-disabling-a-content-fragment-model}

若要完全控制內容片段模型的使用，他們可以設定狀態。

### 啟用內容片段模型{#enabling-a-content-fragment-model}

建立模型後，必須加以啟用，以便：

* 可供在建立新的內容片段時選取。
* 可從內容片段模型中參考。
* 適用於GraphQL;因此，將生成模式。

若要啟用標幟為下列任一項的模型：

* **草稿** :mew（從未啟用）。
* **停用** :已特別禁用。

您可以使用&#x200B;**Enable**&#x200B;選項，其中一個選項為：

* 當選取了所需的「模型」(Model)時，頂部工具欄。
* 相應的快速操作（將滑鼠移到所需的模型上）。

![啟用繪製或禁用的模型](assets/cfm-status-enable.png)

### 禁用內容片段模型{#disabling-a-content-fragment-model}

也可以禁用模型，以便：

* 此模型不再做為建立&#x200B;*new*&#x200B;內容片段的基礎。
* 但是：
   * GraphQL架構會持續產生且仍可查詢（以避免影響JSON API）。
   * 任何基於模型的內容片段仍可從GraphQL端點查詢和返回。
* 模型不能再被引用，但現有參照保持不變，仍可查詢並從GraphQL端點返回。

要禁用標籤為&#x200B;**Enabled**&#x200B;的模型，請使用&#x200B;**Disable**&#x200B;選項，其中一個選項為：

* 當選取了所需的「模型」(Model)時，頂部工具欄。
* 相應的快速操作（將滑鼠移到所需的模型上）。

![禁用啟用的模型](assets/cfm-status-disable.png)

## 刪除內容片段模型{#deleting-a-content-fragment-model}

>[!CAUTION]
刪除內容片段模型可能會影響相依片段。

要刪除內容片段模型：

1. 導覽至&#x200B;**工具**、**資產**，然後開啟&#x200B;**內容片段模型**。

1. 導覽至包含內容片段模型的檔案夾。
1. 從工具欄中選擇型號，然後選擇&#x200B;**Delete**。

   >[!NOTE]
   如果模型被參照，則會發出警告。 採取適當行動。

## 發佈內容片段模型{#publishing-a-content-fragment-model}

內容片段模型必須在發佈任何相依內容片段時／之前發佈。

若要發佈內容片段模型：

1. 導覽至&#x200B;**工具**、**資產**，然後開啟&#x200B;**內容片段模型**。

1. 導覽至包含內容片段模型的檔案夾。
1. 從工具列中選擇您的型號，然後按&#x200B;**Publish**。
發佈狀態將在控制台中指示。

   >[!NOTE]
   如果您發佈模型尚未發佈的內容片段，則選擇清單會指出此點，而模型將會隨片段一起發佈。

## 取消發佈內容片段模型{#unpublishing-a-content-fragment-model}

如果內容片段模型未被任何片段參照，則可以解除發佈這些模型。

若要解除發佈內容片段模型：

1. 導覽至&#x200B;**工具**、**資產**，然後開啟&#x200B;**內容片段模型**。

1. 導覽至包含內容片段模型的檔案夾。
1. 從工具列中選取您的模型，然後按&#x200B;**Unpublish**。
發佈狀態將在控制台中指示。
