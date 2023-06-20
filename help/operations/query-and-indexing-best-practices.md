---
title: 查詢和編製索引最佳實務
description: 瞭解如何根據Adobe的最佳實務准則最佳化您的索引和查詢。
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 0%

---

# 查詢和編製索引最佳實務 {#query-and-indexing-best-practices}

在AEMas a Cloud Service中，有關索引的所有操作方面都已自動化。 如此一來，開發人員就能專注於建立有效率的查詢，以及對應的索引定義。

## 何時使用查詢 {#when-to-use-queries}

查詢是存取內容的一種方式，但不是唯一的可能性。 在許多情況下，可以透過其他方法更有效率地存取存放庫中的內容。 您應該考慮查詢是否是存取使用案例內容的最佳且最有效率的方法。

### 存放庫和分類設計 {#repository-and-taxonomy-design}

在設計存放庫的分類法時，需要考慮幾個因素。 這些功能包括存取控制、本地化、元件和頁面屬性繼承等等。

在設計解決這些擔憂的分類法時，考慮索引設計的「可通行性」也很重要。 在這種情況下，可通行性是分類法允許根據其路徑以可預測方式存取內容的能力。 與需要執行多個查詢的系統相比，這樣可使系統更有效率且更容易維護。

此外，在設計分類法時，請務必考慮排序是否重要。 如果不需要明確排序，並且需要大量同層級節點，則最好使用無序節點型別，例如 `sling:Folder` 或 `oak:Unstructured`. 如果需要排序， `nt:unstructured` 和 `sling:OrderedFolder` 會更合適。

### 元件中的查詢 {#queries-in-components}

由於查詢可能是在AEM系統上執行的最繁重的操作之一，因此最好在元件中避免查詢。 每次轉譯頁面時執行數個查詢通常會降低系統效能。 有兩種策略可用來避免在轉譯元件時執行查詢： **[周遊節點](#traversing-nodes)** 和 **[預先擷取結果。](#prefetching-results)**

### 周遊節點 {#traversing-nodes}

如果設計存放庫的方式允許事先瞭解所需資料的位置，則可以部署從必要路徑擷取此資料的程式碼，而無需執行查詢來尋找它。

這方面的一個範例是呈現適合特定類別的內容。 一種方法是使用類別屬性來組織內容，可以查詢該屬性以填入顯示類別中專案的元件。

更好的方式是依類別以分類法建構此內容，以便手動擷取。

例如，如果內容儲存在類似以下的分類法中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

此 `/content/myUnstructuredContent/parentCategory/childCategory` 節點只需擷取，其子系可剖析並用於演算元件。

此外，當您處理小型或同質結果集時，遍歷存放庫並收集所需節點會比手工建立查詢以傳回相同的結果集更快。 作為一般考量，應儘可能避免查詢。

### 預先擷取結果 {#prefetching-results}

有時候，元件周圍的內容或需求不允許使用節點周遊作為擷取所需資料的方法。 在這種情況下，需要在轉譯元件之前執行所需的查詢，以確保最佳效能。

如果元件所需的結果可以在編寫時計算，並且預期內容不會變更，則可以在完成變更後執行查詢。

如果資料或內容會定期變更，可依排程或透過監聽器執行查詢，以取得基礎資料的更新。 然後，可將結果寫入存放庫中的共用位置。 任何需要此資料的元件都可以從此單一節點提取值，而不需要在執行階段執行查詢。

類似的策略可用於將結果儲存在記憶體中的快取記憶體中，該快取記憶體會在啟動時填入，並會在進行變更時更新（使用JCR） `ObservationListener` 或Sling `ResourceChangeListener`)。

## 正在最佳化查詢 {#optimizing-queries}

Oak檔案提供 [查詢執行方式的概觀。](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing) 這是本檔案所述所有最佳化活動的基礎。

AEMas a Cloud Service提供查詢效能工具，其設計可支援實作有效率的查詢。

* 它會顯示已執行的查詢及其相關的效能特性和查詢計畫。
* 它可讓您在不同層級執行特定查詢，從僅顯示查詢計畫到執行完整查詢。

查詢效能工具可透過 [Cloud Manager中的開發人員控制檯。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries) 與AEM 6.x版相比，AEM as a Cloud Service的查詢效能工具可提供更多有關查詢執行細節的資訊。

此圖表說明使用查詢效能工具來最佳化查詢的一般流程。

![查詢最佳化流程](assets/query-optimization-flow.png)

### 使用索引 {#use-an-index}

每個查詢都應該使用索引來提供最佳效能。 在大多數情況下，現有的現成索引應足以處理查詢。

有時需要將自訂屬性新增到現有索引，以便使用該索引查詢其他限制。 檢視檔案 [內容搜尋與索引](/help/operations/indexing.md#changing-an-index) 以取得更多詳細資料。 此 [JCR查詢速查表](#jcr-query-cheatsheet) 本節說明索引上的屬性定義必須如何支援特定查詢型別。

### 使用正確的條件 {#use-the-right-criteria}

任何查詢的主要限制都應該是屬性相符，因為這是最有效的型別。 新增更多屬性限制會進一步限制結果。

查詢引擎只會考慮單一索引。 這表示可以而且應該透過新增更多自訂索引屬性來自訂現有索引。

此 [JCR查詢速查表](#jcr-query-cheatsheet) 本節列出可用的限制，並概述索引定義的外觀如何才能擷取。 使用 [查詢效能工具](#query-performance-tool) 測試查詢並確保使用了正確的索引，而且查詢引擎不需要評估索引之外的限制。

### 訂購 {#ordering}

如果請求結果的特定順序，查詢引擎有兩種方式可達成此目的：

1. 索引可以完全且以正確的順序傳送結果。
   * 如果用於排序的屬性有註釋，則此選項有效 `ordered=true` 在索引定義中。
1. 查詢引擎會執行排序程式。
   * 當查詢引擎在索引之外執行篩選，或排序屬性未使用註釋時，可能會發生這種情況 `ordered=true` 屬性。
   * 這要求將完整的結果集讀入記憶體以進行排序，這比第一個選項慢得多。

### 限制結果大小 {#restrict-result-size}

查詢結果的擷取大小是查詢效能的重要因素。 由於結果是以延遲方式擷取，所以無論是在執行階段還是記憶體使用上，僅擷取前20個結果與擷取10,000個結果都不同。

這也表示只有在擷取所有結果時，才能正確決定結果集的大小。 因此，擷取的結果集應一律加以限制，要麼透過增加查詢來限制(請參閱 [JCR查詢速查表](#jcr-query-cheatsheet) 詳細資訊)或限制結果的讀取次數。

此限制也會防止查詢引擎點選 **周遊限制** 100,000個節點中，這會導致強制停止查詢。

請參閱區段 [具有大型結果的查詢](#queries-with-large-result-sets) 如果必須完全處理潛在的大型結果集，則為本檔案。

## JCR查詢速查表 {#jcr-query-cheatsheet}

為了支援建立有效的JCR查詢和索引定義， [JCR查詢速查表](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet) 可供下載，並可在開發期間作為參考使用。

它包含QueryBuilder、XPath和SQL-2的範例查詢，涵蓋了在查詢效能方面表現不同的多個情境。 此外，也提供如何建立或自訂Oak索引的建議。 本速查表內容適用於AEMas a Cloud Service及AEM 6.5。

## 具有大型結果集的查詢 {#queries-with-large-result-sets}

雖然建議避免使用具有大型結果集的查詢，但在某些情況下，必須處理大型結果集。 通常結果的大小事先無法知道，因此應採取一些預防措施，以確保處理過程可靠。

* 查詢不應在要求內執行。 相反，查詢應該作為Sling工作或AEM工作流程的一部分執行。 這些執行個體的總執行時間沒有任何限制，並且在處理查詢及其結果期間執行個體發生故障時會重新啟動。
* 若要克服100,000個節點的查詢限制，您應考慮使用 [金鑰組分頁](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) 並將查詢分割為多個子查詢。

## 存放庫周遊 {#repository-traversal}

周遊存放庫的查詢不使用索引，而是使用類似下列的訊息進行記錄。

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

使用此記錄檔片段，您可以判斷：

* 查詢本身： `//*`
* 執行此查詢的Java程式碼： `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` 協助識別查詢的建立者。

有了這些資訊，就可以使用 [正在最佳化查詢](#optimizing-queries) 區段。
