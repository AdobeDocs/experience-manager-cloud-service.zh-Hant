---
title: 內容片段模型
description: 內容片段模型可用來建立包含結構化內容的內容片段。
translation-type: tm+mt
source-git-commit: 243b7509661cbb9da670bdc15b68378db43b423a
workflow-type: tm+mt
source-wordcount: '2177'
ht-degree: 7%

---


# 內容片段模型 {#content-fragment-models}

內容片段模型定義[內容片段](/help/assets/content-fragments/content-fragments.md)的內容結構。

若要使用內容片段模型，請：

1. [為您的例項啟用內容片段模型功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [建立](#creating-a-content-fragment-model)，並設 [定內容](#defining-your-content-fragment-model)片段模型
1. [啟用您的內容片段](#enabling-disabling-a-content-fragment-model) 模型，以便在建立內容片段時使用
1. [透過設定原則，允許您在所需資產資料夾上](#allowing-content-fragment-models-assets-folder) 的內容片段 **模型**。

## 建立內容片段模型{#creating-a-content-fragment-model}

1. 導覽至&#x200B;**工具**、**資產**，然後開啟&#x200B;**內容片段模型**。
1. 導覽至適合您[configuration](/help/assets/content-fragments/content-fragments-configuration-browser.md)的資料夾。
1. 使用&#x200B;**Create**&#x200B;開啟嚮導。

   >[!CAUTION]
   >
   >如果[未啟用內容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，則&#x200B;**Create**&#x200B;選項將不可用。

1. 指定「模 **型標題」**。您也可以新增&#x200B;**Tags**、**Description**，並視需要選擇&#x200B;**Enable model**&#x200B;至[enable the model](#enabling-disabling-a-content-fragment-model)。

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

   ![屬性](assets/cfm-models-03.png)

1. **要添加欄位**

   * 將必要的資料類型拖曳至欄位的必要位置：

      ![資料類型至欄位](assets/cfm-models-04.png)

   * 將欄位添加到模型後，右側面板將顯示可為該特定資料類型定義的&#x200B;**屬性**。 您可以在這裡定義該欄位的必要項目。

      * 許多屬性都不言而喻，如需詳細資訊，請參閱[Properties](#properties)。
      * 鍵入&#x200B;**欄位標籤**&#x200B;將自動完成&#x200B;**屬性名稱** —— 如果為空，然後可以手動更新。

      例如：

      ![欄位屬性](assets/cfm-models-05.png)


1. **刪除欄位**

   選取必要欄位，然後按一下／點選垃圾桶圖示。 系統會要求您確認動作。

   ![移除](assets/cfm-models-06.png)

1. 新增所有必填欄位，並視需要定義相關屬性。 例如：

   ![儲存](assets/cfm-models-07.png)

1. 選擇&#x200B;**保存**&#x200B;以保存定義。

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
* **片段引用**
   * 參考其他內容片段；可用於[建立巢狀內容](#using-references-to-form-nested-content)
   * 可以配置資料類型以允許片段作者：
      * 直接編輯參考的片段。
      * 根據適當的模型建立新的內容片段
* **JSON 物件**
   * 允許內容片段作者在片段的對應元素中輸入JSON語法。
      * 若要AEM允許儲存您已從其他服務複製／貼上的直接JSON。
      * JSON將會傳遞，並在GraphQL中輸出為JSON。
      * 在內容片段編輯器中包含JSON語法反白顯示、自動完成和錯誤反白顯示。

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

* **UniqueContent（適用於特定欄位）在從目前模型建立的所有內容片段中必須是唯一的。**


   這可確保內容作者無法重複已新增至相同模型其他片段的內容。

   例如，在「內容片段模型」中名為「`Country`」的「單行文字&#x200B;**」欄位，在兩個相依的內容片段中不能有值「`Japan`」。**&#x200B;當嘗試第二個例項時，會發出警告。

   >[!NOTE]
   確保每個語言根的獨特性。

   >[!NOTE]
   變數的值可以與相同片段的變數相同&#x200B;*唯一*，但與其他片段的變數不同。

* **可**
翻譯在CF模型編輯器中選中欄位上的「可翻譯」複選框

   * 確保欄位的屬性名稱已添加到翻譯配置`/content/dam/<tenant>`中（如果尚未出現）。
   * 對於GraphQL:將「內容片段」欄位上的`<translatable>`屬性設為`yes`，以允許GraphQL查詢篩選器只針對可轉譯內容進行JSON輸出。

* 有關該特定資料類型及其屬性的詳細資訊，請參閱&#x200B;**[片段參考（嵌套片段）](#fragment-reference-nested-fragments)**。

## 驗證{#validation}

現在，各種資料類型都可能定義驗證需求，以便在產生的片段中輸入內容：

* **單行文字**
   * 比較預先定義的規則運算式。
* **數量**
   * 檢查特定值。
* **內容參考資料**
   * 測試特定類型的內容。
   * 只能參考指定檔案大小或較小的資產。
   * 只能參考預先定義的寬度和／或高度範圍（以像素為單位）內的影像。
* **片段引用**
   * 測試特定內容片段模型。

<!--
  * Only predefined file types can be referenced.
  * No more than the predefined number of assets can be referenced. 
  * No more than the predefined number of fragments can be referenced.
-->

## 使用參照來建立巢狀內容{#using-references-to-form-nested-content}

「內容片段」可使用下列任一種資料類型，來建立巢狀內容：

* **[內容參考資料](#content-reference)**
   * 提供其他內容的簡單參考；任何類型。
   * 可針對一或多個參照（在產生的片段中）進行設定。

* **[片段參考](#fragment-reference-nested-fragments)** （巢狀片段）
   * 參照其他片段，取決於指定的特定模型。
   * 允許您包括／檢索結構化資料。

      >[!NOTE]
      此方法與[使用內容片段搭配GraphQL](/help/assets/content-fragments/content-fragments-graphql.md)的無頭內容傳送特別有趣。
   * 可針對一個或多個引用（在產生的片段中）進行配置。

>[!NOTE]
對AEM以下項目提供定期保護：
* 內容參考
這可防止用戶向當前片段添加引用。 這可能會導致空白的「片段參考」選擇器對話框。

* GraphQL中的片段參考
如果您建立可傳回彼此參考之多個內容片段的深層查詢，它會在首次出現時傳回null。


### 內容參考資料 {#content-reference}

「內容參考」可讓您從其他來源轉換內容；例如，影像或內容片段。

除了標準屬性外，您還可以指定：

* 任何參考內容的&#x200B;**根路徑**。
* 可參考的內容類型。
* 檔案大小的限制。
* 影像限制。
   <!-- Check screenshot - might need update -->
   ![內容參考資料](assets/cfm-content-reference.png)

### 片段參考（巢狀片段）{#fragment-reference-nested-fragments}

「片段參考」會參照一或多個內容片段。 擷取內容以用於應用程式時，這項功能尤其受關注，因為它可讓您擷取含有多個圖層的結構化資料。

例如：

* 為員工定義詳細資訊的模型；這些包括：
   * 對定義雇主（公司）的模式的參考

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
這與[使用內容片段搭配GraphQL](/help/assets/content-fragments/content-fragments-graphql.md)進行無頭內容傳送特別有趣。

除了標準屬性外，您還可以定義：

* **呈現為**:

   * **multifield**  —— 片段作者可以建立多個個別的參考

   * **fragmentreference**  —— 允許片段作者選擇片段的單一參考

* **模型類**
型可選取多個模型。編寫「內容片段」時，必須已使用這些模型建立任何參考片段。

* **根路**
徑這可指定所引用任何片段的根路徑。

* **允許建立片段**

   這可讓片段作者根據適當的模型建立新片段。

   * **fragmenterferenccompresition** -允許片段作者選取多個片段來建立合成

   <!-- Check screenshot - might need update -->
   ![片段引用](assets/cfm-fragment-reference.png)

>[!NOTE]
已建立週期保護機制。 它禁止使用者在片段參考中選取目前的內容片段。 這可能會導致空白的「片段參考」選擇器對話框。
GraphQL中還對片段引用提供定期保護。 如果您在兩個相互參照的內容片段間建立深度查詢，則會傳回null。

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

## 允許資產資料夾{#allowing-content-fragment-models-assets-folder}上的內容片段模型

若要實作內容控管，您可以在「資產」檔案夾上設定&#x200B;**Policies**，以控制在該檔案夾中允許建立「片段」的「內容片段模型」。

>[!NOTE]
此機制類似於在頁面的進階屬性中允許頁面範本](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author)及其子項的[。

要為&#x200B;**允許的內容片段模型**&#x200B;配置&#x200B;**策略**:

1. 導覽並開啟所需Assets資料夾的&#x200B;**Properties**。

1. 開啟&#x200B;**Policies**&#x200B;頁籤，您可以在其中配置：

   * **繼承自`<folder>`**

      建立新子資料夾時，策略會自動繼承；如果子資料夾需要允許與父資料夾不同的模型，則可以重新配置策略（並中斷繼承）。

   * **允許的內容片段模型 (依路徑)**

      允許使用多種型號。

   * **允許的內容片段模型（依標籤）**

      允許使用多種型號。
   ![內容片段模型原則](assets/cfm-model-policy-assets-folder.png)

1. **保** 存任何更改。

資料夾允許的內容片段模型解析如下：
* ****&#x200B;允許的內容片段模型&#x200B;**的Policys**。
* 如果為空，請嘗試使用繼承規則確定策略。
* 如果繼承鏈未傳遞結果，則查看該資料夾的&#x200B;**Cloud Services**&#x200B;配置（也首先直接，然後通過繼承）。
* 如果上述項目均未提供任何結果，則該資料夾不允許使用模型。

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

## 內容片段模型——屬性{#content-fragment-model-properties}

您可以編輯內容片段模型的&#x200B;**屬性**:

* **基本**
   * **模型標題**
   * **標記**
   * **說明**
   * **上傳影像**

<!--
* **GraphQL**
  
  >[!CAUTION]
  >
  >These properties are only required for [development purposes](/help/assets/content-fragments/graphql-api-content-fragments.md#schema-generation).
  >
  >Updating these properties can impact dependent applications.

  * **API Name**
  * **Single Query Field Name**
  * **Multiple Query Field Name**
-->
