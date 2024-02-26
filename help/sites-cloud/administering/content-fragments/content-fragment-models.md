---
title: 內容片段模型
description: 瞭解內容片段模型如何作為您在AEM中內容片段的基礎，讓您建立結構化內容，以用於Headless傳送或頁面編寫。
feature: Content Fragments
role: User, Developer, Architect
exl-id: 8ab5b15f-cefc-45bf-a388-928e8cc8c603
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '3125'
ht-degree: 3%

---

# 內容片段模型 {#content-fragment-models}

Adobe Experience Manager (AEM)中的內容片段模型as a Cloud Service定義 [內容片段](/help/sites-cloud/administering/content-fragments/overview.md). 這些片段隨後可用於頁面製作，或用作Headless內容的基礎。

若要使用內容片段模式，您可以：

1. [為您的執行個體啟用內容片段模型功能](/help/sites-cloud/administering/content-fragments/setup.md)
1. [建立](#creating-a-content-fragment-model)、和 [設定](#defining-your-content-fragment-model)，您的內容片段模型
1. [啟用您的內容片段模型](#enabling-disabling-a-content-fragment-model) 以便在建立內容片段時使用
1. [在所需的Assets資料夾上允許您的內容片段模型](#allowing-content-fragment-models-assets-folder) 透過設定 **原則**.

## 建立內容片段模型 {#creating-a-content-fragment-model}

1. 瀏覽至 **工具**， **一般**，然後開啟 **內容片段模型**.
1. 導覽至適合您的檔案夾 [設定，或子設定](/help/sites-cloud/administering/content-fragments/setup.md).
1. 使用 **建立** 以開啟精靈。

   >[!CAUTION]
   >
   >如果 [未啟用內容片段模型](/help/sites-cloud/administering/content-fragments/setup.md)，則 **建立** 選項將無法使用。

1. 指定 **模型標題**.
您也可以定義各種屬性；例如，新增 **標籤**， a **說明**，選取 **啟用模型** 至 [啟用模型](#enabling-disabling-a-content-fragment-model) 若有需要，並定義
   **預設預覽URL模式**.

   >[!NOTE]
   >
   >另請參閱 [內容片段模型 — 屬性](#content-fragment-model-properties) 以取得完整詳細資訊。

   ![標題和說明](assets/cf-cfmodels-create.png)

1. 使用 **建立** 以儲存空白模型。 訊息會指出動作是否成功，您可以選取 **開啟** 立即編輯模型，或 **完成** 以返回主控台。

### 內容片段模型 — 屬性 {#content-fragment-model-properties}

這些屬性是在您建立模型時定義的，稍後可透過進行編輯 **屬性** 內容片段模式的選項：

* **基本**
   * **模型標題**
   * **標籤**
   * **說明**
   * **啟用模型**
   * **預設預覽URL模式**
內容片段編輯器可讓作者 **預覽** 外部前端應用程式中的內容。 一旦 **預覽服務** 已設定，請為前端應用程式新增URL。

     預覽URL應遵循此模式：
    `https://<preview_url>?param=${expression}`

     可用的運算式包括：

      * `${contentFragment.path}`
      * `${contentFragment.model.path}`
      * `${contentFragment.model.name}`
      * `${contentFragment.variation}`
      * `${contentFragment.id}`

   * **上傳影像**

<!-- CHECK: currently under FT -->
<!--
* **GraphQL**
  Define names relevant for GraphQL.
  Changing the GraphQL API Name, or Query field names will impact client applications.
  * **API Name**
    Represents the GraphQL type and query field names in the GraphQL schema.
  * **Single Query Field Name**
    Represents the GraphQL single query field name in the GraphQL schema.
  * **Multiple Query Field Name**
    Represents the GraphQL multiple query field name in the GraphQL schema.
-->

## 定義內容片段模型 {#defining-your-content-fragment-model}

內容片段模式透過以下選項，有效地定義了結果內容片段的結構 **[資料型別](#data-types)**. 使用模型編輯器，您可以新增資料型別的例項，然後將其設定以建立必填欄位：

>[!CAUTION]
>
>編輯現有內容片段已使用的模型可能會影響這些相依片段。

1. 瀏覽至 **工具**， **一般**，然後開啟 **內容片段模型**.

1. 導覽至容納您的內容片段模式的資料夾。
1. 開啟所需的模型 **編輯**；使用快速動作或選取模型，然後從工具列選取動作。

   開啟模型編輯器後，會顯示：

   * 左：欄位已定義
   * 右：資 **料類型** ，可用於建立欄位( **和屬性** ，以供建立欄位後使用)

   >[!NOTE]
   >
   >當欄位定義為 **必填**，則 **標籤** 左窗格中標示為星號(**&#42;**)。

![屬性](assets/cf-cfmodels-empty-model.png)

1. **新增欄位**

   * 將欄位所需的資料型別拖曳到所需位置：

     ![拖曳資料型別以建立欄位](assets/cf-cfmodels-create-field.png)

   * 將欄位新增到模型後，右側面板會顯示 **屬性** 可針對該特定資料型別定義的屬性。 您可以在此處定義該欄位的必要條件。

      * 許多屬性的含義一目瞭然，如需更多詳細資訊，請參閱 [屬性](#properties).
      * 輸入 **欄位標籤** 自動完成 **屬性名稱**   — 如果為空白，則可在之後手動更新。

        >[!CAUTION]
        >
        手動更新屬性時 **屬性名稱** 對於資料型別，名稱必須包含 *僅限* A-Z、a-z、0-9和下劃線「_」作為特殊字元。
        >
        如果在舊版AEM中建立的模型包含非法字元，請移除或更新這些字元。

     例如：

     ![欄位屬性](assets/cf-cfmodels-field-properties.png)

1. **移除欄位**

   選取必填欄位，然後選取垃圾桶圖示。 系統會要求您確認動作。

   ![移除](assets/cf-cfmodels-remove-icon.png)

1. 新增所有必要欄位，並視需要定義相關屬性。 例如：

   ![儲存](assets/cf-cfmodels-save.png)

1. 選取 **儲存** 以保留定義。

## 資料類型 {#data-types}

定義模型時可選用多種資料型別：

* **單行文字**
   * 新增一行或多行文字的欄位；可以定義最大長度
* **多行文字**
   * 可能是RTF、純文字或Markdown的文字區域

  >[!NOTE]
  >
  文字區域是RTF、純文字還是Markdown，由屬性在模型中定義 **預設型別**.
  >
  此格式無法從 [內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)，但僅從模型中進行。

* **數字**
   * 新增一或多個數值欄位
* **布林值**
   * 新增布林值核取方塊
* **日期和時間**
   * 新增日期和/或時間
* **分項清單**
   * 新增一組核取方塊、選項按鈕或下拉式清單欄位
* **標籤**
   * 允許片段作者存取及選取標籤區域
* **內容參考**
   * 參考任何型別的其他內容；可用於 [建立巢狀內容](#using-references-to-form-nested-content)
   * 如果參照了影像，您可以選擇顯示縮圖
* **片段引用**
   * 參考其他內容片段；可用於 [建立巢狀內容](#using-references-to-form-nested-content)
   * 可以設定此資料類型以允許片段作者：
      * 直接編輯參考的片段。
      * 根據適當的模式建立新的內容片段
* **json物件**
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
     此資料型別僅用於格式設定，AEM GraphQL結構描述會忽略此資料型別。

## 屬性 {#properties}

許多屬性的含義一目瞭然，對於某些屬性，其他詳細資訊如下：

* **屬性名稱**

  手動更新資料型別的此屬性時，名稱 **必須** contain *僅限* A-Z、a-z、0-9和下劃線「_」作為特殊字元。

  >[!CAUTION]
  >
  如果在舊版AEM中建立的模型包含非法字元，請移除或更新這些字元。

* **呈現為**

  在片段中實現/轉譯欄位的各種選項。 這通常可讓您定義作者將看到欄位的單一例項，還是允許建立多個例項。 時間 **多個欄位** 用於定義專案的最小和最大數量 — 請參閱 [驗證](#validation) 以取得更多詳細資料。

* **欄位標籤**
輸入 **欄位標籤** 自動產生 **屬性名稱**，然後可視需要手動更新。

* **驗證**
基本驗證可由以下機制提供 **必填** 屬性。 有些資料型別有額外的驗證欄位。 另請參閱 [驗證](#validation) 以取得更多詳細資料。

* 對於「多行」 **資料類型** ，可將「預設類型 **** 」定義為：

   * **RTF文字**
   * **Markdown**
   * **純文字**

  若未指定，則預設值 **RTF文字** 用於此欄位。

  變更 **預設型別** 在內容片段模型中，只有在編輯器中開啟並儲存該片段後，該片段才會對現有、相關的內容片段生效。

* **獨特**
從目前模型建立的所有內容片段內容（適用於特定欄位）必須是唯一的。

  這是為了確保內容作者無法重複已新增至相同模型其他片段中的內容。

  例如， **單行文字** 已呼叫的欄位 `Country` 在內容片段模型中不能有 `Japan` 於兩個相依內容片段中。 嘗試第二個執行個體時會發出警告。

  >[!NOTE]
  >
  確保每個語言根的唯一性。

  >[!NOTE]
  >
  變數可能具有相同的 *獨特* 值做為相同片段的變數，但與其他片段變數中使用的值不同。

* 另請參閱 **[內容參考](#content-reference)** 以取得該特定資料型別及其屬性的詳細資訊。

* 另請參閱 **[片段參考（巢狀片段）](#fragment-reference-nested-fragments)** 以取得該特定資料型別及其屬性的詳細資訊。

* **可翻譯**

  檢查 **可翻譯** 內容片段模型編輯器中的欄位上的核取方塊將：

   * 確保欄位的屬性名稱已新增到翻譯設定、上下文 `/content/dam/<sites-configuration>`，如果尚未存在。
   * 對於GraphQL：設定 `<translatable>` 「 」內容片段欄位上的屬性 `yes`，以允許GraphQL查詢篩選僅含有可翻譯內容的JSON輸出。

## 驗證  {#validation}

各種資料型別現在包含定義在結果片段中輸入內容時適用的驗證需求的可能性：

* **單行文字**
   * 與預先定義的規則運算式比較。
* **數字**
   * 檢查特定值。
* **內容參考**
   * 測試特定型別的內容。
   * 只能參考指定檔案大小或更小的資產。
   * 只能參考預先定義的寬度和/或高度範圍（以畫素為單位）內的影像。
* **片段引用**
   * 測試特定內容片段模型。
* **專案最小數量** / **專案最大數量**

  已定義為 **多個欄位** (設定為 **呈現為**)擁有下列選項：

   * **專案最小數量**
   * **專案最大數量**

  這些將在中驗證 [內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md).

## 使用參照來形成巢狀內容 {#using-references-to-form-nested-content}

內容片段可使用下列任一種資料型別來形成巢狀內容：

* **[內容參考](#content-reference)**
   * 提供其他內容的簡單參照；任何型別。
   * 可以為一個或多個參考（在產生的片段中）設定。

* **[片段引用](#fragment-reference-nested-fragments)** （巢狀片段）
   * 根據指定的特定模型，參考其他片段。
   * 可讓您包含/擷取結構化資料。
     >[!NOTE]
     >
     當您使用時，此方法特別有趣 [搭配GraphQL使用內容片段的Headless內容傳送](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
   * 可以為一個或多個參考（在產生的片段中）設定。

>[!NOTE]
>
AEM針對下列專案提供週期性保護：
>
* 內容參考這可防止使用者新增對目前片段的參考，並可能導致空白的片段參考選擇器對話方塊。
>
* GraphQL中的片段參考如果您建立深層查詢，並傳回互相參考的多個內容片段，則在第一次出現時就會傳回null。

### 內容參考 {#content-reference}

內容參考可讓您轉譯來自其他來源的內容；例如，影像、頁面或體驗片段。

除了標準屬性之外，您還可以指定：

* 此 **根路徑**，會指定儲存任何參考內容的位置
  >[!NOTE]
  >
  如果您想在使用內容片段編輯器時直接在此欄位上傳和參考影像，則必須使用此選項。
  >
  另請參閱 [參考影像](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images) 以取得更多詳細資料。

* 可參考的內容型別
  >[!NOTE]
  >
  這些必須包括 **影像** 如果您想在使用內容片段編輯器時直接在此欄位上傳和參考影像。
  >
  另請參閱 [參考影像](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images) 以取得更多詳細資料。

* 檔案大小限制
* 如果參照影像：
   * 顯示縮圖
   * 影像高度和寬度的限制

![內容參考](assets/cf-cfmodels-content-reference.png)

### 片段參考（巢狀片段） {#fragment-reference-nested-fragments}

片段參考會參考一或多個內容片段。 此功能可讓您擷取多個圖層的結構化資料，在擷取應用程式中使用的內容時特別感興趣。

例如：

* 定義員工詳細資訊的模型；包括：
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
片段參考對以下專案特別感興趣 [搭配GraphQL使用內容片段的Headless內容傳送](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).

除了標準屬性之外，您還可以定義：

* **呈現為**：

   * **多欄位**  — 片段作者可以建立多個個別參考

   * **片段參考**  — 允許片段作者選取片段的單一參照

* **模型型別**
可選取多個模型。 將參照新增至內容片段時，任何參照的片段都必須使用這些模型建立。

* **根路徑**
這會指定所參考之任何片段的根路徑。

* **允許建立片段**

  如此可讓片段作者根據適當的模型建立片段。

   * **片段參考複合**  — 允許片段作者藉由選取多個片段來建置複合

  ![片段引用](assets/cf-cfmodels-fragment-reference.png)

>[!NOTE]
>
已建立重複保護機制。 它禁止使用者在片段參考中選取目前的內容片段，並可能導致空白的片段參考選擇器對話方塊。
>
GraphQL中也有片段參考的週期性保護。 如果您在兩個互相參照的內容片段間建立深層查詢，則會傳回null。

## 啟用或停用內容片段模型 {#enabling-disabling-a-content-fragment-model}

您可以 **啟用** 或 **停用** 您的內容片段模型，以完整控制其使用。

### 啟用內容片段模型 {#enabling-a-content-fragment-model}

建立模型後，必須將其啟用，以便：

* 可在建立內容片段時選擇。
* 可在內容片段模型中參考。
* 可供GraphQL使用，因此會產生結構描述。

若要啟用被標示為下列其中一項的模型：

* **草稿** ：新增（從未啟用）。
* **已停用** ：已特別停用。

您使用 **啟用** 選項來自：

* 當選取所需的「模型」時，頂部工具列。
* 對應的「快速動作」(Quick Action) （將滑鼠移到所需模型上）。

![啟用草稿或已停用的模型](assets/cf-cfmodels-status-enable.png)

### 停用內容片段模型 {#disabling-a-content-fragment-model}

也可以停用模型，以便：

* 模型無法再用來作為建立基礎 *新* 內容片段。
* 但是：
   * GraphQL結構描述會持續產生，且仍可查詢（以避免影響JSON API）。
   * 您仍可以從GraphQL端點查詢及傳回任何以模型為基礎的內容片段。
* 該模型無法再參考，但現有參考將保持不變，並且仍可以從GraphQL端點查詢和返回。

若要停用標示為 **已啟用**，您會使用 **停用** 選項來自：

* 當選取所需的「模型」時，頂部工具列。
* 對應的「快速動作」(Quick Action) （將滑鼠移到所需模型上）。

![停用啟用的模型](assets/cf-cfmodels-status-disable.png)

## 允許資產資料夾中的內容片段模型 {#allowing-content-fragment-models-assets-folder}

若要實作內容控管，您可以設定 **原則** ，以控制在該資料夾中允許建立片段的內容片段模型。

>[!NOTE]
>
其機制類似於 [允許頁面範本](/help/sites-cloud/authoring/sites-console/templates.md#allowing-a-template-author) 頁面及其子頁面（在頁面的進階屬性中）。

若要設定 **原則** 的 **允許的內容片段模型**：

1. 導覽並開啟 **屬性** ，作為所需的Assets資料夾。

1. 開啟 **原則** 標籤，您可在其中設定：

   * **繼承自`<folder>`**

     建立新的子資料夾時，會自動繼承原則；如果子資料夾需要允許與父資料夾不同的模型，則可以重新設定原則（並中斷繼承）。

   * **允許的內容片段模型（依路徑）**

     可允許多個模型。

   * **允許的內容片段模型（依標籤）**

     可允許多個模型。

   ![內容片段模型原則](assets/cf-cfmodels-policy-assets-folder.png)

1. **儲存** 任何變更。

允許用於資料夾的內容片段模型的解析如下：
* 此 **原則** 的 **允許的內容片段模型**.
* 如果空白，請嘗試使用繼承規則來決定原則。
* 如果繼承鏈沒有傳遞結果，請檢視 **Cloud Service** 該資料夾的設定（也請先直接設定，然後再透過繼承）。
* 如果以上所有內容均未提供任何結果，則該資料夾不允許使用模型。

## 刪除內容片段模型 {#deleting-a-content-fragment-model}

>[!CAUTION]
>
刪除內容片段模型可能會影響相依片段。

若要刪除內容片段模型：

1. 瀏覽至 **工具**， **一般**，然後開啟 **內容片段模型**.

1. 導覽至容納您的內容片段模式的資料夾。
1. 選取您的模型，然後 **刪除** 工具列中的。

   >[!NOTE]
   >
   如果參照了模型，系統會發出警告，以便您採取適當的動作。

## 發佈內容片段模型 {#publishing-a-content-fragment-model}

發佈任何相依內容片段時/之前，需要發佈內容片段模型。

若要發佈內容片段模型：

1. 瀏覽至 **工具**， **一般**，然後開啟 **內容片段模型**.

1. 導覽至容納您的內容片段模式的資料夾。
1. 選取您的模型，然後 **發佈** 工具列中的。
發佈狀態會顯示在主控台中。

   >[!NOTE]
   >
   如果您發佈的內容片段尚未發佈模式，選擇清單會指出這一點，模式會與片段一起發佈。

## 取消發佈內容片段模型 {#unpublishing-a-content-fragment-model}

如果內容片段模型未由任何片段參考，則可取消發佈這些模型。

若要取消發佈內容片段模型：

1. 瀏覽至 **工具**， **一般**，然後開啟 **內容片段模型**.

1. 導覽至容納您的內容片段模型的資料夾。
1. 選取您的模型，然後 **取消發佈** 工具列中的。
主控台會指出發佈狀態。

如果您嘗試取消發佈一個或多個片段目前使用的模型，則會顯示錯誤警告。 例如：

![取消發佈使用中的模型時顯示內容片段模型錯誤訊息](assets/cf-cfmodels-unpublish-error.png)

此訊息建議您檢查 [引用](/help/sites-cloud/authoring/basic-handling.md#references) 面板以進一步調查：

![參考中的內容片段模型](assets/cf-cfmodels-references.png)

## 鎖定的 (已發佈的) 內容片段模型 {#locked-published-content-fragment-models}

此功能為已發佈的內容片段模型提供控管。

### 挑戰 {#the-challenge}

* 內容片段模型決定AEM中GraphQL查詢的結構描述。

   * AEM GraphQL結構描述會在建立內容片段模型後立即建立，而且可存在於製作和發佈環境中。

   * 發佈上的結構描述最為關鍵，因為它們為JSON格式的內容片段內容的即時傳送奠定了基礎。

* 修改內容片段模型或編輯內容片段模型時，可能會出現問題。 這表示結構描述變更，進而可能影響現有的GraphQL查詢。

* 將新欄位新增到內容片段模式通常不應有任何有害影響。 但是，修改現有資料欄位（例如，其名稱）或刪除欄位定義時，將會在請求這些欄位時中斷現有GraphQL查詢。

### 需求 {#the-requirements}

* 讓使用者瞭解在編輯已用於即時內容傳送的模型（即已發佈的模型）時的風險。

* 此外，也可避免非預期的變更。

如果修改後的模型重新發佈，則其中任何一個條件都可能中斷查詢。

### 解決方案 {#the-solution}

為了解決這些問題，內容片段模型包括 *已鎖定* 在發佈後立即對作者設為唯讀模式。 此狀態由以下指示 **已鎖定**：

![鎖定內容片段模型的卡片](assets/cf-cfmodels-locked.png)

當模型為 **已鎖定** （在「唯讀」模式中），您可以檢視模型的內容和結構，但無法加以編輯。

您可以管理 **已鎖定** 從主控台或模型編輯器中的模型：

* 主控台

  在主控台中，您可以使用來管理唯讀模式 **解鎖** 和 **鎖定** 工具列中的動作：

  ![鎖定的內容片段模型的工具列](assets/cf-cfmodels-locked.png)

   * 您可以 **解鎖** 啟用編輯的模型。

     如果您選取 **解鎖** 警告隨即顯示，您必須確認 **解鎖** 動作：
     ![解鎖內容片段模型時的訊息](assets/cf-cfmodels-unlock-message.png)

     然後您可以開啟模型以進行編輯。

   * 您也可以 **鎖定** 之後模型。
   * 重新發佈模型會立即將其傳回 **已鎖定** （唯讀）模式。

* 模型編輯器

   * 當您開啟已鎖定的模型時，系統會警告您，並顯示三個動作： **取消**， **以唯讀方式檢視**， **編輯**：

     ![檢視鎖定的內容片段模型時的訊息](assets/cf-cfmodels-editor-lock-message.png)

   * 如果您選取 **以唯讀方式檢視**，您可以檢視模型的內容和結構：

     ![檢視唯讀 — 鎖定的內容片段模型](assets/cf-cfmodels-editor-locked-view-only.png)

   * 如果您選取 **編輯**，您可以編輯並儲存更新：

     ![編輯 — 鎖定的內容片段模型](assets/cf-cfmodels-editor-locked-edit.png)

     >[!NOTE]
     >
     頂端可能仍會顯示警告，但此時模型已由現有內容片段使用。

   * **取消** 將您帶回主控台。
