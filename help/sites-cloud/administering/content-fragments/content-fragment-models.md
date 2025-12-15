---
title: 定義內容片段模型
description: 瞭解內容片段模型如何作為您在AEM中內容片段的基礎，讓您建立結構化內容，以用於Headless傳送或頁面編寫。
feature: Content Fragments
role: User, Developer
exl-id: 8ab5b15f-cefc-45bf-a388-928e8cc8c603
solution: Experience Manager Sites
source-git-commit: ce807274d6138473ff9661897a0816e0feb99f15
workflow-type: tm+mt
source-wordcount: '2217'
ht-degree: 3%

---

# 定義內容片段模型 {#defining-content-fragment-models}

Adobe Experience Manager (AEM) as a Cloud Service中的內容片段模型定義[內容片段](/help/sites-cloud/administering/content-fragments/overview.md)的內容結構。 這些片段隨後可用於頁面製作，或用作Headless內容的基礎。

本頁涵蓋如何使用專用編輯器定義您的內容片段模式。 請參閱[管理您的內容片段模式](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)，瞭解建立片段後可用的進一步工作與選項，包括[內容片段主控台可用的動作](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#actions)、[允許在資料夾上建立模式](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)以及[發佈模式](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model)。

>[!NOTE]
>
>使用您的內容片段模型和內容片段時，請留意[最佳實務](/help/sites-cloud/administering/content-fragments/overview.md#best-practices)。

>[!CAUTION]
>
>如果要查詢多個引用的片段，則建議不要讓各種片段模式具有名稱相同，但型別不同的欄位名稱。
>
>如需詳細資訊，請參閱搭配內容片段使用的[AEM GraphQL API — 限制](/help/headless/graphql-api/content-fragments.md#limitations)

>[!NOTE]
>
>如果您使用此新編輯器建立模型，您應該一律將此編輯器用於該模型。
>
>如果您接著使用[原始模型編輯器](/help/assets/content-fragments/content-fragments-models.md)開啟模型，您會看到訊息：
>
>* 「此模型已設定自訂UI結構描述。 此UI中顯示的欄位順序可能與UI結構描述不相符。 若要檢視與UI結構描述對齊的欄位，您必須切換到新的內容片段編輯器。」

## 定義內容片段模型 {#defining-your-content-fragment-model}

內容片段模式透過選擇&#x200B;**[資料型別](#data-types)**，有效地定義了結果內容片段的結構。 使用模型編輯器，您可以新增資料型別的例項，然後將其設定以建立必填欄位：

>[!CAUTION]
>
>編輯現有內容片段已使用的模型可能會影響這些相依片段。

1. 在內容片段主控台中，選取[內容片段模式](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#basic-structure-handling-content-fragment-models-console)的面板，並導覽至儲存您的內容片段模式的資料夾。

   >[!NOTE]
   >
   >您也可以在[建立模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model)後直接開啟模型。

1. 開啟&#x200B;**編輯**&#x200B;所需的模型；使用其中一個快速動作連結，或選取模型，然後從工具列選取動作。


   ![屬性](assets/cf-cfmodels-empty-model.png)

   開啟模型編輯器後，會顯示：

   * 上：
      * **首頁**&#x200B;圖示
      * 在[原始](/help/assets/content-fragments/content-fragments-models.md)與新編輯器之間切換的選項
      * **取消**
      * **儲存**

   * 左： **資料型別**&#x200B;可用於建立欄位

   * 中間：欄位已與&#x200B;**新增**&#x200B;選項一起定義

   * 右：使用最右側的圖示，您可在以下兩者之間選取：

      * **屬性**：定義並檢視所選欄位的屬性
      * **模型詳細資料**：顯示&#x200B;**已啟用**&#x200B;狀態、**模型標題**、**標籤**、**描述**&#x200B;和&#x200B;**預覽URL**

1. **新增欄位**

   * 可以：

      * 將資料型別從左側面板拖曳至中間面板中欄位的必要位置。
      * 依資料型別選取&#x200B;**+**&#x200B;圖示以將其新增至欄位清單底部。
      * 在中間面板中選取「**新增**」，然後從產生的下拉式清單中選取所需的資料型別，以在清單底部新增欄位。

     >[!NOTE]
     >
     >**索引標籤預留位置**&#x200B;欄位必須一律顯示在現有欄位上方。

   * 您可以使用欄位方塊左側的點狀結構來重新定位欄位：

     ![移動欄位](assets/cf-cfmodels-move-field-icon.png)

   * 將欄位新增至模型（且已選取）後，右側面板會顯示可針對該特定資料型別定義的&#x200B;**屬性**。 您可以在此處定義特定的
欄位。

      * 許多屬性不言自明，如需詳細資訊，請參閱[屬性（資料型別）](#properties)。
      * 輸入&#x200B;**欄位標籤**&#x200B;會自動完成&#x200B;**屬性名稱** （如果空白），之後可以手動更新。

        >[!CAUTION]
        >
        >手動更新資料型別的屬性&#x200B;**Property Name**&#x200B;時，名稱必須僅包含&#x200B;*個* A-Z、a-z、0-9和下劃線「_」作為特殊字元。
        >
        >如果在舊版AEM中建立的模型包含非法字元，請移除或更新這些字元。

     例如：

     ![欄位屬性](assets/cf-cfmodels-field-properties.png)

     >[!NOTE]
     >
     >當欄位定義為&#x200B;**必要**&#x200B;時，中間窗格中標示的&#x200B;**標籤**&#x200B;會標示為字元(**&#42;**)。

1. **移除欄位**

   選取中間面板中適當欄位的垃圾桶圖示。

   ![移除](assets/cf-cfmodels-remove-icon.png)

1. 新增所有必要欄位，並視需要定義相關屬性。

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

     <!--
    * Internally the reference is held as a universally unique ID (UUID) that references the resource
    * You do not need to know the UUID; in the fragment editor you can browse to the required fragment.
    -->

  <!--
  >[!NOTE]
  >
  >The UUIDs are repository specific. If you use the [Content Copy Tool](/help/implementing/developing/tools/content-copy.md) to copy Content Fragments, the UUIDs will be recalculated in the target environment.
  -->

* **內容參考**
   * 參考任何型別的其他內容；可用於[建立巢狀內容](#using-references-to-form-nested-content)
   * 如果參照了影像，您可以選擇顯示縮圖
   * 欄位可設定為允許片段作者建立欄位的新執行個體
   * 參考指定參考資源的路徑；例如`/content/dam/path/to/resource`

     <!--
    * Internally the reference is held as a universally unique ID (UUID) that references the resource
    * You do not need to know the UUID; in the fragment editor you can browse to the required asset resource
    -->

  <!--
  >[!NOTE]
  >
  >The UUIDs are repository specific. If you use the [Content Copy Tool](/help/implementing/developing/tools/content-copy.md) to copy Content Fragments, the UUIDs will be recalculated in the target environment.
  -->

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
     >
     >**索引標籤預留位置**&#x200B;欄位必須一律顯示在現有欄位上方。

## 屬性（資料型別） {#properties}

許多屬性的含義一目瞭然，對於某些屬性，其他詳細資訊如下：

* **屬性名稱**

  手動更新資料型別的這個屬性時，名稱&#x200B;**必須**&#x200B;僅包含&#x200B;*個* A-Z、a-z、0-9和下劃線「_」作為特殊字元。

  >[!CAUTION]
  >
  >如果在舊版AEM中建立的模型包含非法字元，請移除或更新這些字元。

* **呈現為**

  在片段中實現/轉譯欄位的各種選項。 這通常可讓您定義作者將看到欄位的單一例項，還是允許建立多個例項。 使用&#x200B;**多個欄位**&#x200B;時，您可以定義專案的最小和最大數量 — 如需詳細資訊，請參閱[驗證](#validation)。

* **欄位標籤**
輸入**欄位標籤**&#x200B;會自動產生&#x200B;**屬性名稱**，然後可視需要手動更新。

* **驗證**
基本驗證可由機制使用，例如**Required**&#x200B;屬性。 有些資料型別有額外的驗證欄位。 如需詳細資訊，請參閱[驗證](#validation)。

* 對於「多行」 **資料類型** ，可將「預設類型 **** 」定義為：

   * **RTF 文字**
   * **Markdown**
   * **純文字**

  如果未指定，此欄位會使用預設值&#x200B;**RTF**。

  在內容片段模型中變更&#x200B;**預設型別**，只會在編輯器中開啟並儲存該片段後，對現有、相關的內容片段生效。

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

  已在[內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)中驗證這些專案。

## 使用參照來形成巢狀內容 {#using-references-to-form-nested-content}

內容片段可使用下列任一種資料型別來形成巢狀內容：

* [內容參考](#content-reference)
   * 提供其他內容的簡單參照；任何型別。
   * 由&#x200B;**內容參考**&#x200B;資料型別提供
   * 可以為一個或多個參考（在產生的片段中）設定。

* [片段參考](#fragment-reference-nested-fragments) （巢狀片段）
   * 根據指定的特定模型，參考其他片段。
   * 由&#x200B;**片段參考**&#x200B;資料型別提供
   * 可讓您包含/擷取結構化資料。

     >[!NOTE]
     >
     >當您透過GraphQL[使用內容片段的](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)Headless內容傳遞時，此方法特別令人感興趣。
   * 可以為一個或多個參考（在產生的片段中）設定。

<!--
>[!NOTE]
>
>See [Upgrade your Content Fragments for UUID References](/help/headless/graphql-api/uuid-reference-upgrade.md) for further information about Content/Fragment Reference and Content/Fragment Reference (UUID), and upgrading to the UUID-based data types.
-->

>[!NOTE]
>
>AEM針對下列專案提供週期性保護：
>
>* 內容參考
>  這可防止使用者新增對目前片段的引用，並可能導致空白的片段引用選取器對話方塊。
>
>* GraphQL中的片段參考
>  如果您建立深層查詢，且該查詢傳回多個互相參照的內容片段，則它會在第一次出現時傳回null。

>[!CAUTION]
>
>如果要查詢多個引用的片段，則建議不要讓各種片段模式具有名稱相同，但型別不同的欄位名稱。
>
>如需詳細資訊，請參閱搭配內容片段使用的[AEM GraphQL API — 限制](/help/headless/graphql-api/content-fragments.md#limitations)

### 內容參考 {#content-reference}

**內容參考**&#x200B;資料型別可讓您轉譯來自其他來源的內容；例如，影像、頁面或體驗片段。

除了標準屬性之外，您還可以指定：

* **根路徑**，指定或代表要儲存任何參考內容的位置

  >[!NOTE]
  >
  >如果您想在使用內容片段編輯器時直接在此欄位上傳和參考影像，則必須使用此選項。
  >
  >如需詳細資訊，請參閱[參考影像](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images)。

* 可參考的內容型別

  >[!NOTE]
  >
  >如果您想要在使用內容片段編輯器時直接上傳和參考此欄位中的影像，這些必須包含&#x200B;**影像**。
  >
  >如需詳細資訊，請參閱[參考影像](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images)。

* 檔案大小限制
* 如果參照影像：

   * 顯示縮圖
   * 影像高度和寬度的限制

![內容參考](assets/cf-cfmodels-content-reference.png)

### 片段參考（巢狀片段） {#fragment-reference-nested-fragments}

**片段參考**&#x200B;資料型別可以參考一或多個內容片段。 此功能可讓您擷取多個圖層的結構化資料，在擷取應用程式中使用的內容時特別感興趣。

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
>片段參考對搭配GraphQL[使用內容片段的](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)Headless內容傳遞特別感興趣。

除了標準屬性之外，您還可以定義：

* **呈現為**：

   * **multifield** — 片段作者可以建立多個個別參考

   * **fragmentreference** — 允許片段作者選取片段的單一參考

* **模型型別**
可選取多個模型。 將參照新增至內容片段時，任何參照的片段都必須使用這些模型建立。

* **根路徑**
這會指定或表示任何參考片段的根路徑。

* **允許建立片段**

  如此可讓片段作者根據適當的模型建立片段。

   * **fragmentreferencecomposite** — 允許片段作者藉由選取多個片段來建置複合

  ![片段參考](assets/cf-cfmodels-fragment-reference.png)

>[!NOTE]
>
>已建立重複保護機制。 它禁止使用者在片段參考中選取目前的內容片段，並可能導致空白的片段參考選擇器對話方塊。
>
>GraphQL中也有片段參考的週期性保護。 如果您在兩個互相參照的內容片段間建立深層查詢，則會傳回null。
