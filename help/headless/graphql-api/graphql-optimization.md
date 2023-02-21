---
title: 最佳化GraphQL查詢
description: 了解如何在Adobe Experience Manager as a Cloud Service中篩選、分頁及排序內容片段以傳送無頭式內容時，最佳化您的GraphQL查詢。
source-git-commit: 0fe0bd301fb09cdc631878926f2e40df51a2cc23
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 0%

---


# 最佳化GraphQL查詢 {#optimizing-graphql-queries}

>[!NOTE]
>
>套用這些最佳化建議前，請考慮 [在GraphQL篩選中更新內容片段以進行分頁和排序](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md) 以獲得最佳效能。

在具有大量共用相同模型的內容片段的AEM例項上，GraphQL清單查詢可能會變得昂貴（就資源而言）。

這是因為 *all* 共用GraphQL查詢內使用之模型的片段必須載入記憶體中。 這會耗用時間和記憶體。 篩選只能套用，這可以減少（最終）結果集中的項目數 **after** 將整個結果集載入到記憶體中。

這可能導致以下印象：即使是小的結果集（可能）也會導致效能不佳。 但實際上，速度緩慢是由初始結果集的大小造成，因為必須在內部處理才能應用篩選。

為了降低效能和記憶體問題，必須盡可能小地保持初始結果集。

AEM提供兩種最佳化GraphQL查詢的方法：

* [混合濾波](#hybrid-filtering)
* [分頁](#paging) （或分頁）

   * [排序](#sorting) 與最佳化無直接關係，但與分頁有關

每種方法都有各自的使用案例和限制。 本檔案提供混合篩選和分頁的相關資訊，部分 [最佳實務](#best-practices) 以最佳化GraphQL查詢。

## 混合濾波 {#hybrid-filtering}

混合篩選結合了JCR篩選與AEM篩選。

它會先套用JCR篩選器（以查詢限制的形式），再將結果集載入記憶體中以進行AEM篩選。 這是為了減少載入到記憶體中的結果集，因為JCR篩選器會在此之前移除多餘的結果。

>[!NOTE]
>
>由於技術原因（例如彈性、片段巢狀）,AEM無法將整個篩選委派給JCR。

此技術可保留GraphQL篩選器提供的彈性，同時將盡可能多的篩選委派給JCR。

## 分頁 {#paging}

AEM中的GraphQL支援兩種分頁類型：

* [限制/偏移分頁](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
這用於清單查詢；這些結尾 
`List`;例如， `articleList`.
若要使用，您必須提供要傳回之第一個項目的位置( `offset`)和要傳回的項目數( `limit`，或頁面大小)。

* [游標分頁](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (代表 `first`和 `after`)這可為每個項目提供唯一ID;也稱為游標。
在查詢中，您指定上一頁的最後一個項目的游標，加上頁面大小（要返回的項目數上限）。

   由於游標分頁無法符合清單查詢的資料結構，AEM已導入 `Paginated` 查詢類型；例如， `articlePaginated`. 使用的資料結構和參數遵循 [GraphQL游標連接規範](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM目前支援轉送(使用 `after`/`first` 參數)。
   >
   >反向分頁(使用 `before`/`last` 參數)。

## 排序 {#sorting}

只有所有排序標準都與頂層片段相關時，排序才會有效。

如果排序順序包含位於巢狀片段上的一個或多個欄位，則共用頂級模型的所有片段都必須載入到記憶體中。 這會造成負面的效能影響。

>[!NOTE]
>
>對頂層欄位進行排序也會對效能造成（雖然幅度較小）影響。

## 最佳作法 {#best-practices}

所有最佳化的主要目標是減少初始結果集。 此處列出的最佳實務可提供執行此作業的方法。 它們可以（而且應該）結合。

### 僅篩選頂層屬性 {#filter-top-level-properties-only}

目前，JCR層級的篩選只適用於頂層片段。

如果篩選器處理巢狀片段的欄位，AEM必須回復到載入（記憶體中）共用基礎模型的所有片段。

您仍可將上層片段欄位上的篩選運算式，以及巢狀片段欄位上的篩選運算式與 [AND運算子](#logical-operations-in-filter-expressions).

### 使用內容結構 {#use-content-structure}

在AEM中，通常認為使用存放庫結構來縮小要處理的內容範圍是正確的做法。

此方法也應套用至GraphQL查詢。

您可以對 `_path` 頂層片段的欄位：

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>結尾 `/` on `value` 才能獲得最佳效能。

### 使用分頁 {#use-paging}

您也可以使用分頁來減少初始結果集；尤其是如果您的請求未使用任何篩選和排序。

如果您對巢狀片段進行篩選或排序，編頁查詢可能仍會緩慢，因為AEM可能仍需將大量片段載入記憶體中。 因此，如果您結合了篩選和分頁，請考慮篩選規則（如上所述）。

對於分頁，排序同樣重要，因為編頁結果總是以明確或隱含的方式排序。

如果您主要想要只擷取前幾個頁面，則使用 `...List` 或 `...Paginated` 查詢。 不過，如果您的應用程式只想要閱讀一或兩頁以上的內容，您應考慮 `...Paginated` 查詢，因為後續頁面的效能明顯較佳。

### 篩選器表達式中的邏輯運算 {#logical-operations-in-filter-expressions}

如果您要篩選巢狀片段，您仍可在使用 `AND` 運算元。

典型的使用案例是使用篩選器來限制查詢的範圍， `_path` 欄位，然後篩選可能位於頂層或巢狀片段的其他欄位。

在此情況下，不同的篩選運算式會與 `AND`. 因此， `_path` 可以有效地限制初始結果集。 頂層欄位上的所有其他篩選器也有助於減少初始結果集，只要它們結合 `AND`.

篩選運算式結合 `OR` 如果涉及巢狀片段，則無法最佳化。 `OR` 只有在 *no* 會涉及巢狀片段。

### 避免在多行文本欄位上進行篩選 {#avoid-filtering-multiline-textfields}

多行文字欄位（html、markdown、純文字、json）的欄位無法透過JCR查詢篩選，因為這些欄位的內容必須即時計算。

如果您仍需要對多行文本欄位進行篩選，請考慮通過添加其他篩選表達式來限制初始結果集的大小，並將它們與 `AND`. 通過篩選 `_path` 外地也是個好辦法。

### 避免篩選虛擬欄位 {#avoid-filtering-virtual-fields}

虛擬欄位(大部分欄位的開頭為 `_`)會在執行GraphQL查詢時計算，因此不在JCR型篩選的範圍內。

一個重要的例外是 `_path` 欄位，可有效用來縮小初始結果集的大小 — 如果內容已據以結構化(請參閱 [使用內容結構](#use-content-structure))。

### 篩選：排除項目 {#filtering-exclusions}

在其他幾種情況下，無法在JCR層級評估篩選器運算式（因此，應避免達到最佳效能）:

* 對 `Float` 值 `_sensitiveness` 篩選選項，其中 `_sensitiveness` 設為 `0.0` .

* 對 `String` 值使用 `_ignoreCase` 篩選。

* 篩選 `null` 值。

* 陣列上的篩選器 `_apply: ALL_OR_EMPTY`.

* 陣列上的篩選器 `_apply: INSTANCES`, `_instances: 0`.

* 使用 `CONTAINS_NOT` 運算元。

* 對 `Calendar`, `Date` 或 `Time` 值 `NOT_AT` 運算元。
