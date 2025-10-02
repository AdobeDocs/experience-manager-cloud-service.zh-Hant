---
title: 內容片段模型(Assets — 內容片段)
description: 瞭解內容片段模型如何作為AEM中Headless內容的基礎，讓您建立具有結構化內容的內容片段。
exl-id: fd706c74-4cc1-426d-ab56-d1d1b521154b
feature: Content Fragments, GraphQL API
role: User, Admin, Architect
solution: Experience Manager Sites
source-git-commit: 8c9c51c349317250ddf7ef07e1b545860fd18351
workflow-type: tm+mt
source-wordcount: '3588'
ht-degree: 7%

---

# 內容片段模型 {#content-fragment-models}

AEM中的內容片段模型定義您[內容片段](/help/assets/content-fragments/content-fragments.md)的內容結構，可作為您Headless內容的基礎。

若要使用內容片段模式，您可以：

1. [為您的執行個體啟用內容片段模型功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [建立](#creating-a-content-fragment-model)，並[設定您的內容片段模型](#defining-your-content-fragment-model)
1. [啟用您的內容片段模型](#enabling-disabling-a-content-fragment-model)，以便在建立內容片段時使用
1. [藉由設定](#allowing-content-fragment-models-assets-folder)原則&#x200B;**，在必要的Assets資料夾**&#x200B;上允許您的內容片段模型。

>[!NOTE]
>
>內容片段是 Sites 的一項功能，但儲存為&#x200B;**資產**。
>
>內容片段和內容片段模型現在主要透過&#x200B;**[內容片段](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**&#x200B;主控台進行管理，不過內容片段仍可從&#x200B;**Assets**&#x200B;主控台進行管理，而內容片段模型可從&#x200B;**工具**&#x200B;主控台進行管理。 本節涵蓋&#x200B;**Assets**&#x200B;和&#x200B;**Tools**&#x200B;主控台中的管理。

>[!NOTE]
>
>如果模型是使用[新模型編輯器](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)建立的，您應該永遠使用該編輯器來建立模型。
>
>如果您隨後使用此（原始）模型編輯器開啟模型，您會看到以下訊息：
>
>* 「此模型已設定自訂UI結構描述。 此UI中顯示的欄位順序可能與UI結構描述不相符。 若要檢視與UI結構描述對齊的欄位，您必須切換到新的內容片段編輯器。」

## 建立內容片段模型 {#creating-a-content-fragment-model}

1. 導覽至&#x200B;**工具**、**一般**，然後開啟&#x200B;**內容片段模型**。
1. 導覽至適合您[組態或子組態](/help/assets/content-fragments/content-fragments-configuration-browser.md)的資料夾。
1. 使用&#x200B;**建立**&#x200B;開啟精靈。

   >[!CAUTION]
   >
   >如果[尚未啟用使用內容片段模型](/help/assets/content-fragments/content-fragments-configuration-browser.md)，則&#x200B;**建立**&#x200B;選項將無法使用。

1. 指定&#x200B;**模型標題**。
您也可以定義各種屬性；例如，新增**標籤**、**描述**，並選取&#x200B;**啟用模型**&#x200B;以[啟用模型](#enabling-disabling-a-content-fragment-model) （如有必要）。

   >[!NOTE]
   >
   >如需&#x200B;**預設預覽URL模式**&#x200B;的詳細資訊，請參閱[內容片段模式 — 屬性](#content-fragment-model-properties)。

   ![標題和說明](assets/cfm-models-02.png)

1. 使用&#x200B;**建立**&#x200B;儲存空的模型。 訊息會指出動作是否成功，您可以選取&#x200B;**開啟**&#x200B;立即編輯模型，或選取&#x200B;**完成**&#x200B;返回主控台。

## 定義內容片段模型 {#defining-your-content-fragment-model}

內容片段模型有效定義結果內容片段的結構，方法是使用&#x200B;**[資料型別](#data-types)**&#x200B;的選項。 使用模型編輯器，您可以新增資料型別的例項，然後將其設定以建立必填欄位：

>[!CAUTION]
>
>編輯現有的內容片段模型可能會影響相依片段。

1. 導覽至&#x200B;**工具**、**一般**，然後開啟&#x200B;**內容片段模型**。

1. 導覽至容納您的內容片段模式的資料夾。
1. 開啟&#x200B;**編輯**&#x200B;所需的模型；使用快速動作，或選取模型，然後從工具列選取動作。

   開啟模型編輯器後，會顯示：

   * 左：欄位已定義
   * 右：資 **料類型** ，可用於建立欄位( **和屬性** ，以供建立欄位後使用)
   * top：嘗試[新編輯器](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)的選項

   >[!NOTE]
   >
   >當欄位為&#x200B;**必要**&#x200B;時，左窗格中指示的&#x200B;**標籤**&#x200B;會標示為字元(**&#42;**)。

![屬性](assets/cfm-models-03.png)

1. **新增欄位**

   * 將欄位所需的資料型別拖曳到所需位置：

     ![資料型別至欄位](assets/cfm-models-04.png)

   * 將欄位新增到模型後，右側面板將顯示可以為該特定資料型別定義的&#x200B;**屬性**。 您可以在此處定義該欄位的必要條件。

      * 許多屬性不言自明，如需詳細資訊，請參閱[屬性](#properties)。
      * 輸入&#x200B;**欄位標籤**&#x200B;將會自動完成&#x200B;**屬性名稱** （如果空白），而且之後可以手動更新。

        >[!CAUTION]
        >
        >手動更新資料型別的屬性&#x200B;**屬性名稱**&#x200B;時，請注意，名稱必須僅包含A-Z、a-z、0-9和下劃線「_」作為特殊字元。
        >
        >如果在舊版AEM中建立的模型包含非法字元，請移除或更新這些字元。

     例如：

     ![欄位屬性](assets/cfm-models-05.png)

1. **移除欄位**

   選取必填欄位，然後選取垃圾桶圖示。 系統會要求您確認動作。

   ![移除](assets/cfm-models-06.png)

1. 新增所有必要欄位，並視需要定義相關屬性。 例如：

   ![儲存](assets/cfm-models-07.png)

1. 選取&#x200B;**儲存**&#x200B;以保留定義。

## 資料類型 {#data-types}

定義模型時可選用多種資料型別：

* **單行文字**
   * 為單行文字新增欄位；可以定義最大長度
   * 欄位可設定為允許片段作者建立欄位的新執行個體

* **多行文字**
   * 可能是RTF、純文字或Markdown的文字區域
   * 欄位可設定為允許片段作者建立欄位的新執行個體

  >[!NOTE]
  >
  >文字區域是否為RTF、純文字或Markdown，是由屬性&#x200B;**預設型別**&#x200B;在模型中定義。
  >
  >此格式無法從[內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)變更，只能從模型變更。

* **數字**
   * 新增數值欄位
   * 欄位可設定為允許片段作者建立欄位的新執行個體

* **布林值**
   * 新增布林值核取方塊

* **日期和時間**
   * 新增日期和/或時間欄位

* **分項清單**
   * 新增一組核取方塊、選項按鈕或下拉式清單欄位
      * 您可以指定片段作者可用的選項

* **標籤**
   * 允許片段作者存取及選取標籤區域

* **片段參考**
   * 參考其他內容片段；可用於[建立巢狀內容](#using-references-to-form-nested-content)
   * 可以設定此資料類型以允許片段作者：
      * 直接編輯參考的片段。
      * 根據適當的模式建立新的內容片段
      * 建立欄位的新執行個體
   * 參考指定參考資源的路徑；例如`/content/dam/path/to/resource`

* **片段參考 (UUID)**
   * 參考其他內容片段；可用於[建立巢狀內容](#using-references-to-form-nested-content)
   * 可以設定此資料類型以允許片段作者：
      * 直接編輯參考的片段。
      * 根據適當的模式建立新的內容片段
      * 建立欄位的新執行個體
   * 在編輯器中，參考會指定所參考資源的路徑；在內部，參考被視為參考資源的通用唯識別碼 (UUID)。
      * 您不需要知道UUID；在片段編輯器中，您可以瀏覽到所需的片段

  >[!NOTE]
  >
  >UUID是存放庫專屬的。 如果您使用[內容複製工具](/help/implementing/developing/tools/content-copy.md)來複製內容片段，將會在目標環境中重新計算UUID。

* **內容參考**
   * 參考任何型別的其他內容；可用於[建立巢狀內容](#using-references-to-form-nested-content)
   * 如果參照了影像，您可以選擇顯示縮圖
   * 欄位可設定為允許片段作者建立欄位的新執行個體
   * 參考指定參考資源的路徑；例如`/content/dam/path/to/resource`

* **內容參考 (UUID)**
   * 參考任何型別的其他內容；可用於[建立巢狀內容](#using-references-to-form-nested-content)
   * 如果參照了影像，您可以選擇顯示縮圖
   * 欄位可設定為允許片段作者建立欄位的新執行個體
   * 在編輯器中，參考會指定所參考資源的路徑；在內部，參考被視為參考資源的通用唯識別碼 (UUID)。
      * 您不需要知道UUID；在片段編輯器中，您可以瀏覽到所需的資產資源

  >[!NOTE]
  >
  >UUID是存放庫專屬的。 如果您使用[內容複製工具](/help/implementing/developing/tools/content-copy.md)來複製內容片段，將會在目標環境中重新計算UUID。

* **JSON物件**
   * 允許內容片段作者在片段的對應元素中輸入JSON語法。
      * 允許AEM儲存您從其他服務複製/貼上的直接JSON。
      * JSON會傳遞，並在GraphQL中輸出為JSON。
      * 在內容片段編輯器中包括JSON語法醒目提示、自動完成和錯誤醒目提示。

* **索引標籤預留位置**
   * 允許引進索引標籤，以在編輯內容片段內容時使用。
      * 這些在模型編輯器中顯示為分隔線，分隔內容資料型別清單的區段。 每個例項代表新索引標籤的開始。
      * 在片段編輯器中，每個例項都會顯示為一個索引標籤。

     >[!NOTE]
     >
     >此資料型別僅用於格式設定，AEM GraphQL結構描述會忽略此資料型別。

## 屬性 {#properties}

許多屬性的含義一目瞭然，對於某些屬性，其他詳細資訊如下：

* **屬性名稱**

  手動更新資料型別的此屬性時，請注意，名稱&#x200B;**必須**&#x200B;僅包含&#x200B;*A-Z、a-z、0-9和下劃線「_」作為特殊字元。*

  >[!CAUTION]
  >
  >如果在舊版AEM中建立的模型包含非法字元，請移除或更新這些字元。

* **呈現為**
在片段中實現/轉譯欄位的各種選項。 通常，此屬性可讓您定義作者是否看到欄位的單一例項，或允許建立多個例項。 使用**多個欄位**&#x200B;時，您可以定義專案的最小和最大數量 — 如需詳細資訊，請參閱[驗證](#validation)。

* **欄位標籤**
輸入**欄位標籤**&#x200B;將會自動產生&#x200B;**屬性名稱**，然後可視需要手動更新。

* **驗證**
基本驗證可由機制使用，例如**Required**&#x200B;屬性。 有些資料型別有額外的驗證欄位。 如需詳細資訊，請參閱[驗證](#validation)。

* 對於「多行」 **資料類型** ，可將「預設類型 **** 」定義為：

   * **RTF 文字**
   * **Markdown**
   * **純文字**

  如果未指定，此欄位會使用預設值&#x200B;**RTF**。

  在內容 **片段模型中變更「預設類型** 」，只會在編輯器中開啟並儲存該片段後，對現有、相關的內容片段生效。

* **唯一**
從目前模型建立的所有內容片段內容（適用於特定欄位）必須是唯一的。

  這是為了確保內容作者無法重複已新增至相同模型其他片段中的內容。

  例如，內容片段模型中名為&#x200B;**的**&#x200B;單行文字`Country`欄位在兩個相依的內容片段中不能有值`Japan`。 嘗試第二個執行個體時會發出警告。

  >[!NOTE]
  >
  >確保每個語言根的唯一性。

  >[!NOTE]
  >
  >變數可以有與相同片段變數相同的&#x200B;*唯一*&#x200B;值，但與其他片段變數中使用的值不同。

  >[!CAUTION]
  >
  >如果您想使用MSM （這會建立內容片段的復本），則應該從個別內容片段模式中使用的任何資料型別中移除任何&#x200B;**唯一**&#x200B;限制。

* 如需特定資料型別及其屬性的詳細資訊，請參閱&#x200B;**[內容參考](#content-reference)**。

* 如需特定資料型別及其屬性的詳細資訊，請參閱&#x200B;**[片段參考（巢狀片段）](#fragment-reference-nested-fragments)**。

* **可翻譯**

  核取內容片段模型編輯器中欄位上的&#x200B;**可翻譯**&#x200B;核取方塊將：

   * 確認欄位的屬性名稱已新增至翻譯組態，內容`/content/dam/<sites-configuration>` （如果尚未存在）。
   * 對於GraphQL：將內容片段欄位上的`<translatable>`屬性設定為`yes`，以允許GraphQL查詢篩選僅包含可翻譯內容的JSON輸出。

## 驗證 {#validation}

各種資料型別現在包含定義在結果片段中輸入內容時適用的驗證需求的可能性：

* **單行文字**
   * 與預先定義的規則運算式比較。
* **數字**
   * 檢查特定值。
* **內容參考**
   * 測試特定型別的內容。
   * 只能參考指定檔案大小或更小的資產。
   * 只能參考預先定義的寬度和/或高度範圍（以畫素為單位）內的影像。
* **片段參考**
   * 測試特定內容片段模型。
* **最小專案數** / **最大專案數**

  已定義為&#x200B;**多個欄位** （以&#x200B;**Render As**&#x200B;設定）的欄位具有選項：

   * **最小專案數**
   * **最大專案數**

  這些功能已經過驗證：

   * 已在[原始內容片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)中驗證最大值。
   * 兩者皆已在[內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)中驗證。

## 使用參照來形成巢狀內容 {#using-references-to-form-nested-content}

內容片段可使用下列任一種資料型別來形成巢狀內容：

* [內容參考](#content-reference)
   * 提供其他內容的簡單參照；任何型別。
   * 由資料型別提供：
      * **內容參考** — 以路徑為基礎
      * **內容參考(UUID)** — 以UUID為基礎
   * 可以為一個或多個參考（在產生的片段中）設定。

* [片段參考](#fragment-reference-nested-fragments) （巢狀片段）
   * 根據指定的特定模型，參考其他片段。
   * 由資料型別提供：
      * **片段參考** — 以路徑為基礎
      * **片段參考(UUID)** — 以UUID為基礎
   * 可讓您包含/擷取結構化資料。

     >[!NOTE]
     >
     >當您透過GraphQL[使用內容片段的](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)Headless內容傳遞時，此方法特別令人感興趣。

   * 可以為一個或多個參考（在產生的片段中）設定。

>[!NOTE]
>
>請參閱[升級您的UUID參考內容片段](/help/headless/graphql-api/uuid-reference-upgrade.md)，以取得有關內容/片段參考和內容/片段參考(UUID)以及升級為UUID型資料型別的進一步資訊。

>[!NOTE]
>
>AEM對下列專案提供週期性保護：
>
>* 內容參考
>  >  這可防止使用者新增對目前片段的引用。 這可能會導致空的片段參考選擇器對話方塊。
>
>* GraphQL中的片段參考
>  >  如果您建立深層查詢，且該查詢傳回多個互相參照的內容片段，則該查詢在第一次出現時會傳回null。

### 內容參考 {#content-reference}

**內容參考**&#x200B;和&#x200B;**內容參考(UUID)**&#x200B;資料型別可讓您轉譯來自其他來源的內容；例如，影像、頁面或體驗片段。

除了標準屬性之外，您還可以指定：

* 任何參考內容的&#x200B;**根路徑**
* 可參考的內容型別
* 檔案大小限制
* 如果參照影像：
   * 顯示縮圖
   * 影像高度和寬度的限制

![內容參考](assets/cfm-content-reference.png)

### 片段參考（巢狀片段） {#fragment-reference-nested-fragments}

**片段參考**&#x200B;和&#x200B;**片段參考(UUID)**&#x200B;資料型別可以參考一或多個內容片段。 此功能可讓您擷取多個圖層的結構化資料，在擷取應用程式中使用的內容時特別感興趣。

例如：

* 定義員工詳細資訊的模型；這些包括：
   * 定義僱主（公司）的模型參考

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
>這與[搭配GraphQL](/help/assets/content-fragments/content-fragments-graphql.md)使用內容片段的Headless內容傳遞特別相關。

除了標準屬性之外，您還可以定義：

* **呈現為**：

   * **multifield** — 片段作者可以建立多個個別參考

   * **fragmentreference** — 允許片段作者選取片段的單一參考

* **模型型別**
可選取多個模型。 製作內容片段時，必須使用這些模型建立任何參照的片段。

* **根路徑**
這會指定所參考之任何片段的根路徑。

* **允許建立片段**

  如此可讓片段作者根據適當的模型建立片段。

   * **fragmentreferencecomposite** — 允許片段作者藉由選取多個片段來建置複合

  ![片段參考](assets/cfm-fragment-reference.png)

>[!NOTE]
>
>已建立重複保護機制。 它禁止使用者在片段參考中選取目前的內容片段。 這可能會導致空的片段參考選擇器對話方塊。
>
>GraphQL中也有片段參考的週期性保護。 如果您在兩個相互參照的內容片段間建立深層查詢，則會傳回null。

## 內容片段模型 — 屬性 {#content-fragment-model-properties}

您可以編輯內容片段模型的&#x200B;**屬性**：

* **基本**
   * **模型標題**
   * **標籤**
   * **說明**
   * **上傳影像**
   * **預設預覽URL模式**

     >[!NOTE]
     >
     >此僅供&#x200B;*新*&#x200B;內容片段編輯器使用。 如需進一步資訊，請參閱[內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-fragment-model-properties)。


## 啟用或停用內容片段模型 {#enabling-disabling-a-content-fragment-model}

為了完全控制內容片段模型的使用，它們有一個您可以設定的狀態。

### 啟用內容片段模型 {#enabling-a-content-fragment-model}

建立模型時，必須啟用該模型，以便：

* 可在建立內容片段時選擇。
* 可在內容片段模型中參考。
* 可供GraphQL使用，因此會產生結構描述。

若要啟用被標示為下列其中一項的模型：

* **草稿** ： mew （從未啟用）。
* **已停用** ：已特別停用。

您可從下列任一位置使用&#x200B;**啟用**&#x200B;選項：

* 當選取所需的「模型」時，頂部工具列。
* 對應的「快速動作」(Quick Action) （將滑鼠移到所需模型上）。

![啟用草稿或已停用的模型](assets/cfm-status-enable.png)

### 停用內容片段模型 {#disabling-a-content-fragment-model}

也可以停用模型，以便：

* 此模型無法再用來建立&#x200B;*新的*&#x200B;內容片段。
* 但是：
   * GraphQL結構描述會持續產生，且仍可查詢（以避免影響JSON API）。
   * 您仍可以從GraphQL端點查詢及傳回任何以模型為基礎的內容片段。
* 該模型無法再參考，但現有參考將保持不變，並且仍可以從GraphQL端點查詢和返回。

若要停用標示為&#x200B;**已啟用**&#x200B;的模型，您可以使用下列任一專案中的&#x200B;**停用**&#x200B;選項：

* 當選取所需的「模型」時，頂部工具列。
* 對應的「快速動作」(Quick Action) （將滑鼠移到所需模型上）。

![停用啟用的模型](assets/cfm-status-disable.png)

## 允許資產資料夾中的內容片段模型 {#allowing-content-fragment-models-assets-folder}

若要實作內容控管，您可以在Assets資料夾上設定&#x200B;**原則**，以控制允許在該資料夾中建立片段的內容片段模型。

>[!NOTE]
>
>此機制類似於[允許在頁面的進階屬性中，為頁面及其子頁面設定頁面範本](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author)。

若要為&#x200B;**允許的內容片段模型**&#x200B;設定&#x200B;**原則**：

1. 瀏覽並開啟必要的Assets資料夾的&#x200B;**屬性**。

1. 開啟&#x200B;**原則**&#x200B;標籤，您可以在其中設定：

   * **繼承自`<folder>`**

     建立新的子資料夾時，會自動繼承原則；如果子資料夾需要允許與父資料夾不同的模型，則可以重新設定原則（並中斷繼承）。

   * **允許的內容片段模型（依路徑**）

     可允許多個模型。

   * **允許的內容片段模型（依標籤）**

     可允許多個模型。

   ![內容片段模型原則](assets/cfm-model-policy-assets-folder.png)

1. **儲存**&#x200B;任何變更。

允許用於資料夾的內容片段模型的解析如下：

* **允許的內容片段模型**&#x200B;的&#x200B;**原則**。
* 如果空白，請嘗試使用繼承規則來決定原則。
* 如果繼承鏈結未傳遞結果，請檢視該資料夾的&#x200B;**雲端服務**&#x200B;設定（也請先直接再透過繼承）。
* 如果以上所有內容均未提供任何結果，則該資料夾不允許使用模型。

## 刪除內容片段模型 {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>刪除內容片段模型可能會影響相依片段。

若要刪除內容片段模型：

1. 導覽至&#x200B;**工具**、**一般**，然後開啟&#x200B;**內容片段模型**。

1. 導覽至容納您的內容片段模式的資料夾。
1. 選取您的模型，然後從工具列&#x200B;**刪除**。

   >[!NOTE]
   >
   >如果參照模型，則會發出警告。 採取適當行動。

## 發佈內容片段模型 {#publishing-a-content-fragment-model}

內容片段模型需要在任何相關內容片段發佈時/之前發佈。

若要發佈內容片段模型：

1. 導覽至&#x200B;**工具**、**一般**，然後開啟&#x200B;**內容片段模型**。

1. 導覽至容納您的內容片段模式的資料夾。
1. 選取您的模型，然後從工具列選取&#x200B;**發佈**。
主控台會指出發佈狀態。

   >[!NOTE]
   >
   >如果您發佈的內容片段尚未發佈模型，選擇清單會指出這一點，模型會與片段一起發佈。

## 取消發佈內容片段模型 {#unpublishing-a-content-fragment-model}

如果內容片段模型未由任何片段引用，則可取消發佈這些模型。

若要取消發佈內容片段模型：

1. 導覽至&#x200B;**工具**、**一般**，然後開啟&#x200B;**內容片段模型**。

1. 導覽至容納您的內容片段模式的資料夾。
1. 選取您的模型，然後從工具列&#x200B;**取消發佈**。
主控台會指出發佈狀態。

如果您嘗試取消發佈一個或多個片段目前使用的模型，則會出現錯誤警告，通知您：

取消發佈使用中的模型時出現![內容片段模型錯誤訊息](assets/cfm-model-unpublish-error.png)

此訊息建議您檢查[參考](/help/sites-cloud/authoring/basic-handling.md#references)面板以進一步調查：

![參考中的內容片段模型](assets/cfm-model-references.png)

## 鎖定的 (已發佈的) 內容片段模型 {#locked-published-content-fragment-models}

此功能為已發佈的內容片段模型提供控管。

### 挑戰 {#the-challenge}

* 內容片段模型決定AEM中GraphQL查詢的結構描述。

   * AEM GraphQL結構描述會在建立內容片段模型後立即建立，且可同時存在於製作和發佈環境中。

   * 發佈上的結構描述最為關鍵，因為它們為JSON格式的內容片段內容的即時傳送奠定了基礎。

* 修改內容片段模型或編輯內容片段模型時，可能會出現問題。 這表示結構描述變更，進而可能影響現有的GraphQL查詢。

* 將新欄位新增到內容片段模式通常不應有任何有害影響。 但是，修改現有資料欄位（例如，其名稱）或刪除欄位定義時，將會在請求這些欄位時中斷現有GraphQL查詢。

### 需求 {#the-requirements}

* 讓使用者瞭解在編輯已用於即時內容傳送的模型時的風險，換言之，就是已發佈的模型。

* 此外，也可避免非預期的變更。

如果修改後的模型重新發佈，這兩種情況都可能中斷查詢。

### 解決方案 {#the-solution}

為了解決這些問題，內容片段模型在發佈後立即在作者上&#x200B;*鎖定*&#x200B;為唯讀模式。 這表示為&#x200B;**已鎖定**：

鎖定內容片段模型![的](assets/cfm-model-locked.png)卡片

當模型為&#x200B;**鎖定** （在「唯讀」模式中）時，您可以檢視模型的內容和結構，但無法進行編輯。

您可以從主控台或模型編輯器管理&#x200B;**已鎖定的**&#x200B;模型：

* 主控台

  從主控台，您可以使用工具列中的&#x200B;**解除鎖定**&#x200B;和&#x200B;**鎖定**&#x200B;動作來管理唯讀模式：

  ![鎖定的內容片段模型的工具列](assets/cfm-model-locked.png)

   * 您可以&#x200B;**解鎖**&#x200B;模型以啟用編輯。

     如果您選取&#x200B;**解除鎖定**，會顯示警告，而且您必須確認&#x200B;**解除鎖定**動作：
     解鎖內容片段模型![時出現](assets/cfm-model-unlock-message.png)訊息

     然後您可以開啟模型以進行編輯。

   * 您之後也可以&#x200B;**鎖定**&#x200B;模型。
   * 重新發佈模型會立即將其置於&#x200B;**鎖定** （唯讀）模式。

* 模型編輯器

   * 當您開啟已鎖定的模型時，系統會警告您，並顯示三個動作： **取消**、**檢視唯讀**、**編輯**：

     檢視鎖定的內容片段模型時出現![訊息](assets/cfm-model-editor-lock-message.png)

   * 如果您選取&#x200B;**檢視唯讀**，您可以檢視模型的內容和結構：

     ![檢視唯讀 — 鎖定的內容片段模型](assets/cfm-model-editor-locked-view-only.png)

   * 如果您選取&#x200B;**編輯**，您可以編輯並儲存您的更新：

     ![編輯 — 鎖定的內容片段模型](assets/cfm-model-editor-locked-edit.png)

     >[!NOTE]
     >
     >頂端可能仍會顯示警告，但此時模型已由現有內容片段使用。

   * **取消**&#x200B;將返回主控台。
