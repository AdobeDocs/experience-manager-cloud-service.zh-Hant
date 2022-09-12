---
title: 查詢和索引最佳實務
description: 了解如何根據Adobe的最佳實務准則來最佳化索引和查詢。
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: afeff7cfb8606eb58126a4ca62ce9e6e58c44215
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# 查詢和索引最佳實務 {#query-and-indexing-best-practices}

在AEMas a Cloud Service中，與索引相關的所有操作方面都實現了自動化。 這可讓開發人員專注於建立有效查詢及其對應的索引定義。

## 查詢的使用時機 {#when-to-use-queries}

查詢是存取內容的一種方式，但並非唯一的可能。 在許多情況下，儲存庫中的內容可以通過其他方法更有效地訪問。 對於您的使用案例，查詢是否是存取內容的最佳且最有效的方式，您應該考慮。

### 儲存庫和分類設計 {#repository-and-taxonomy-design}

在設計儲存庫的分類法時，需要考慮幾個因素。 這些功能包括存取控制、本地化、元件和頁面屬性繼承等。

在設計可解決這些問題的分類法時，也必須考慮索引設計的「可遍歷性」。 在此情境中，可遍歷性是分類法允許根據內容的路徑可預測地訪問內容的能力。 這使得一個比需要執行多個查詢的系統更容易維護的系統更加高效。

此外，在設計分類法時，請務必考慮排序是否重要。 在不需要顯式排序且需要大量同級節點的情況下，最好使用無序節點類型，例如 `sling:Folder` 或 `oak:Unstructured`. 如果需要訂購， `nt:unstructured` 和 `sling:OrderedFolder` 更合適。

### 元件中的查詢 {#queries-in-components}

由於查詢可能是在AEM系統上執行的較繁重作業之一，最好在元件中避免查詢。 每次呈現頁面時執行多個查詢通常會降低系統的效能。 可使用兩種策略來避免在呈現元件時執行查詢： **[遍歷節點](#traversing-nodes)** 和 **[預取結果。](#prefetching-results)**

### 遍歷節點 {#traversing-nodes}

如果儲存庫的設計方式允許事先了解所需資料的位置，則可從必要路徑檢索此資料的代碼可以部署，而無需運行查詢才能查找。

例如，會轉譯符合特定類別的內容。 一種方法是使用類別屬性來組織內容，可查詢該屬性以填入顯示類別中項目的元件。

更好的方法是依類別將此內容結構化，以便手動擷取。

例如，如果內容儲存在類似以下的分類法中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

the `/content/myUnstructuredContent/parentCategory/childCategory` 節點可以被簡單地檢索，其子項可以被剖析並用於呈現元件。

此外，處理小型或同構的結果集時，遍歷儲存庫和收集所需節點的速度可能會更快，而不是將查詢精心構建以返回相同的結果集。 作為一般考慮，在可能的情況下應避免查詢。

### 預取結果 {#prefetching-results}

有時，元件周圍的內容或需求不允許使用節點遍歷作為檢索所需資料的方法。 在這種情況下，需要在呈現元件之前執行所需的查詢，以確保最佳效能。

如果元件所需的結果可在製作時計算，而且內容不會變更的預期值，則可在完成變更後執行查詢。

如果資料或內容會定期變更，則可依排程或透過監聽程式執行查詢，以更新基礎資料。 然後，可將結果寫入儲存庫中的共用位置。 然後，需要此資料的任何元件都可以從此單一節點提取值，而無需在執行階段執行查詢。

可使用類似策略將結果保留在記憶體內快取中，快取在啟動時填入，並且每當更改完成時更新（使用JCR） `ObservationListener` 或Sling `ResourceChangeListener`)。

## 最佳化查詢 {#optimizing-queries}

Oak檔案提供 [概述查詢的執行方式。](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing) 這構成本檔案所述所有最佳化活動的基礎。

AEM as a Cloud Service提供查詢效能工具，其設計可支援實作有效查詢。

* 它顯示已執行的查詢及其相關的效能特徵和查詢計畫。
* 它允許在各個級別執行臨機查詢，從僅顯示查詢計畫到執行完整查詢。

可透過 [Cloud Manager中的開發人員控制台。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries) AEM as a Cloud Service的「查詢效能工具」針對AEM 6.x版提供查詢執行詳細資訊。

此圖表說明了使用查詢效能工具優化查詢的一般流程。

![查詢最佳化流程](assets/query-optimization-flow.png)

### 使用索引 {#use-an-index}

每個查詢都應使用索引來提供最佳效能。 在大多數情況下，現有的現成索引應該足以處理查詢。

有時，自定義屬性需要添加到現有索引中，因此可以使用索引查詢其他約束。 請參閱檔案 [內容搜尋與索引](/help/operations/indexing.md#changing-an-index) 以取得更多詳細資訊。 此 [JCR查詢速查表](#jcr-query-cheatsheet) 本文檔的一節介紹索引的屬性定義如何查找以支援特定查詢類型。

### 使用正確的條件 {#use-the-right-criteria}

任何查詢的主要限制都應是屬性相符，因為這是最有效的類型。 新增更多屬性限制會進一步限制結果。

查詢引擎僅考慮單一索引。 這表示現有索引可以而且應該通過添加更多自定義索引屬性來自定義。

此 [JCR查詢工作表](#jcr-query-cheatsheet) 本文檔的部分列出了可用約束，並概述了索引定義需要如何查找以便提取。 使用 [查詢效能工具](#query-performance-tool) 測試查詢，並確保使用了正確的索引，並且查詢引擎不需要評估索引之外的約束。

### 訂購 {#ordering}

如果請求了結果的特定順序，查詢引擎有兩種方式可達成此目的：

1. 索引可以以正確的順序完整地傳遞結果。
   * 如果用於排序的屬性用注釋 `ordered=true` 在索引定義中。
1. 查詢引擎執行排序過程。
   * 當查詢引擎在索引外部執行篩選，或排序屬性未以 `ordered=true` 屬性。
   * 這要求將完成的結果集讀入記憶體以進行排序，這比第一個選項慢得多。

### 限制結果大小 {#restrict-result-size}

查詢結果的檢索大小是查詢效能的重要因素。 因為結果是以延遲的方式擷取，僅擷取前20個結果與擷取10,000個結果（執行階段和記憶體使用情形）有所不同。

這也表示只有擷取所有結果時，才能正確判斷結果集的大小。 因此，擷取的結果集應一律受限，方法是增加查詢(請參閱 [JCR查詢工作表](#jcr-query-cheatsheet) 部分，或限制結果的讀取。

此限制也可防止查詢引擎達到 **遍歷限制** 會導致強制停止查詢。

請參閱 [具有大結果的查詢](#queries-with-large-result-sets) ，如果必須完全處理可能較大的結果集，則此文檔將被刪除。

## JCR查詢速查表 {#jcr-query-cheatsheet}

為支援建立有效的JCR查詢和索引定義， [JCR查詢速查表](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet) 可供下載，並在開發期間作為參考使用。

它包含QueryBuilder、XPath和SQL-2的查詢示例，涵蓋多個情況，這些情況在查詢效能方面的行為不同。 此外也提供建議，說明如何建立或自訂Oak索引。 此「速查表」的內容適用於AEMas a Cloud Service以及AEM 6.5。

## 具有大結果集的查詢 {#queries-with-large-result-sets}

儘管建議避免使用大結果集的查詢，但在某些情況下，必須處理大結果集。 結果的大小往往事先不知道，因此應採取一些預防措施，使加工可靠。

* 查詢不應在要求內執行。 請改為在Sling工作或AEM工作流程中執行查詢。 這些變數在總執行階段中沒有任何限制，且會在處理查詢及其結果期間執行個體關閉時重新啟動。
* 若要克服100,000個節點的查詢限制，您應考慮使用 [鍵集分頁](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) 並在多個子查詢中分割查詢。

## 存放庫周遊 {#repository-traversal}

遍歷儲存庫的查詢不使用索引，且會以類似下列的訊息記錄。

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

使用此記錄程式碼片段，您可以判斷：

* 查詢本身： `//*`
* 執行此查詢的Java代碼： `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` 來幫助標識查詢的建立者。

有了這些資訊，就可以使用 [最佳化查詢](#optimizing-queries) 一節。
