---
title: 查詢和編製索引最佳做法
description: 瞭解如何根據Adobe的最佳實務准則來最佳化您的索引和查詢。
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
feature: Operations
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3086'
ht-degree: 0%

---

# 查詢和編製索引最佳做法 {#query-and-indexing-best-practices}

在AEM as a Cloud Service中，有關索引的所有作業方面都已自動化。 如此一來，開發人員就能專注於建立有效率的查詢，以及對應的索引定義。

## 何時使用查詢 {#when-to-use-queries}

查詢是存取內容的一種方式，但不是唯一的可能方式。 在許多情況下，可以透過其他方式更有效地存取存放庫中的內容。 您應該考慮查詢是否是存取使用案例內容的最佳且最有效率的方法。

### 存放庫和分類法設計 {#repository-and-taxonomy-design}

在設計存放庫的分類法時，需要考慮幾個因素。 這些功能包括存取控制、本地化、元件和頁面屬性繼承等。

在設計解決這些問題的分類法時，考慮索引設計的「可通行性」也很重要。 在此情境中，可周遊性是分類法允許根據其路徑以可預測的方式存取內容的能力。 與需要執行多個查詢的系統相比，這種方式的系統效率更高，更容易維護。

此外，在設計分類法時，考慮排序是否重要也很重要。 若不需要明確排序，且預期會有大量同層級節點，則最好使用無序節點型別，例如`sling:Folder`或`oak:Unstructured`。 在需要排序的情況下，`nt:unstructured`和`sling:OrderedFolder`會更適合。

### 元件中的查詢 {#queries-in-components}

由於查詢可能是在AEM系統上執行的最繁重的操作之一，因此最好在元件中避免查詢。 每次轉譯頁面時執行數個查詢通常會降低系統效能。 有兩種策略可用來在轉譯元件時避免執行查詢： **[周遊節點](#traversing-nodes)**&#x200B;和&#x200B;**[預先擷取結果](#prefetching-results)**。

### 周遊節點 {#traversing-nodes}

如果設計存放庫的方式允許事先瞭解所需資料的位置，則可以部署從必要路徑擷取此資料的程式碼，而無需執行查詢來尋找它。

這方面的一個範例是呈現適合特定類別的內容。 其中一種方式是使用類別屬性來組織內容，而可以查詢該屬性以填入顯示類別中專案的元件。

更好的方式是依類別以分類法建構此內容，以便手動擷取。

例如，如果內容儲存在類似以下的分類法中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

可以簡單地擷取`/content/myUnstructuredContent/parentCategory/childCategory`節點，剖析其子系並用於演算元件。

此外，當您處理小型或同質結果集時，周遊存放庫並收集所需節點會比手工建立查詢以傳回相同的結果集更快。 一般而言，應儘可能避免查詢。

### 預先擷取結果 {#prefetching-results}

有時候，元件周圍的內容或需求不允許使用節點周遊作為擷取所需資料的方法。 在這種情況下，需要在元件轉譯之前執行所需的查詢，以確保最佳效能。

如果可以在編寫元件時計算元件所需的結果，而且預期內容不會變更，則可以在完成變更後執行查詢。

如果資料或內容會定期變更，則可依排程或透過監聽器執行查詢，以更新基礎資料。 然後，可以將結果寫入存放庫中的共用位置。 任何需要此資料的元件都可以從此單一節點提取值，而不需要在執行階段執行查詢。

類似的策略可用於將結果儲存在記憶體中的快取中，該快取會在啟動時填入，並會在完成變更時更新（使用JCR `ObservationListener`或Sling `ResourceChangeListener`）。

## 正在最佳化查詢 {#optimizing-queries}

Oak檔案提供[查詢執行方式的高層級概觀](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing)。 這是本檔案所述所有最佳化活動的基礎。

AEM as a Cloud Service提供[查詢效能工具](#query-performance-tool)，其設計可支援實作有效率的查詢。

* 它會顯示已執行的查詢及其相關效能特性及查詢計畫。
* 它允許在不同層級執行特定查詢，從僅顯示查詢計畫到執行完整查詢。

查詢效能工具可透過Cloud Manager[中的](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=zh-Hant#queries)Developer Console存取。 與AEM 6.x版相比，AEM as a Cloud Service的查詢效能工具可提供更多有關查詢執行細節的資訊。

此圖表說明使用查詢效能工具最佳化查詢的一般流程。

![查詢最佳化流程](assets/query-optimization-flow.png)

### 使用索引 {#use-an-index}

每個查詢都應該使用索引來提供最佳效能。 在大多數情況下，現有的現成索引應足以處理查詢。

有時需要將自訂屬性新增到現有索引，因此可以使用索引查詢其他限制。 如需詳細資訊，請參閱檔案[內容搜尋與索引](/help/operations/indexing.md#changing-an-index)。 本檔案的[JCR查詢速查表](#jcr-query-cheatsheet)區段說明索引上的屬性定義必須如何支援特定查詢型別。

### 使用正確的條件 {#use-the-right-criteria}

任何查詢的主要限制都應是屬性相符，因為這是最有效的型別。 新增更多屬性限制會進一步限制結果。

查詢引擎只會考慮單一索引。 這表示可以而且應該透過新增更多自訂索引屬性來自訂現有索引。

本檔案的[JCR查詢速查表](#jcr-query-cheatsheet)區段列出可用的限制，並概述索引定義的外觀必須如何才能擷取。 使用[查詢效能工具](#query-performance-tool)測試查詢，並確定使用了正確的索引，而且查詢引擎不需要評估索引之外的限制。

### 排序 {#ordering}

如果請求的是結果的特定順序，則查詢引擎有兩種方式可達成此目的：

1. 索引可以以正確的順序完整傳遞結果。
   * 如果用於排序的屬性在索引定義中以`ordered=true`註釋，則此選項有效。
1. 查詢引擎會執行排序程式。
   * 當查詢引擎在索引之外執行篩選，或排序屬性未使用`ordered=true`屬性加上註解時，就可能發生這種情況。
   * 這需要將完整的結果集讀入記憶體進行排序，這比第一個選項慢得多。

### 限制結果大小 {#restrict-result-size}

查詢結果的擷取大小是查詢效能中的重要因素。 由於是以延遲方式擷取結果，所以無論在執行階段還是記憶體使用上，僅擷取前20個結果與擷取10,000個結果都不同。

這也表示只有在擷取所有結果時，才能正確決定結果集的大小。 因此，請務必限制擷取的結果集，要麼通過增加查詢（請參閱本檔案的[JCR查詢速查表](#jcr-query-cheatsheet)區段以取得詳細資料），要麼通過限制結果的讀取來進行限制。

這樣的限制也會防止查詢引擎達到100,000個節點的&#x200B;**周遊限制**，這會導致強制停止查詢。

如果必須完全處理潛在的大型結果集，請參閱本檔案的[具有大型結果集的查詢](#queries-with-large-result-sets)一節。

## 查詢效能工具 {#query-performance-tool}

查詢效能工具(位於`/libs/granite/operations/content/diagnosistools/queryPerformance.html`，可透過Cloud Manager[中的](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=zh-Hant#queries)Developer Console取得)提供 — 

* 任何「緩慢查詢」的清單；目前定義為讀取/掃描超過5000列的查詢。
* 「常見查詢」清單
* 「說明查詢」工具，用於瞭解Oak將如何執行特定查詢。

![查詢效能工具](assets/query-performance-tool.png)

「緩慢查詢」和「常見查詢」表格包括 — 

* 查詢陳述式本身。
* 最後一個執行查詢的執行緒的詳細資訊，允許識別執行查詢的頁面或應用程式功能。
* 查詢的「讀取最佳化」分數。
   * 這是以掃描以執行查詢的列數/節點數與讀取的比對結果數之間的比率來計算。
   * 可以在索引處處理每個限制（以及任何順序）的查詢通常分數為90%或以上。
* 最大列數的詳細資訊 — 
   * 讀取 — 表示某列已包含在結果集中。
   * 掃描 — 表示基礎索引查詢（在索引查詢的情況下）的結果中包含列，或從節點存放區讀取（在存放庫周遊的情況下）。

這些資料表可協助識別未完整編制索引的查詢(請參閱[使用索引](#use-an-index)或讀取太多節點（另請參閱[存放庫周遊](#repository-traversal)和[索引周遊](#index-traversal)）。 這類查詢將會反白顯示 — 以紅色標示適當的關注區域。

提供`Reset Statistics`選項，可移除資料表中收集的所有現有統計資料。 這允許執行特定查詢（透過應用程式本身或Explain Query工具）並分析執行統計資料。

### 說明查詢

Explain查詢工具可讓開發人員瞭解查詢執行計畫（請參閱[讀取查詢執行計畫](#reading-query-execution-plan)），包括執行查詢時使用的任何索引的詳細資訊。 這可用來瞭解查詢索引的成效，以便預測或追溯分析其效能。

#### 說明查詢

若要說明查詢，請執行下列動作：

* 使用`Language`下拉式清單選取適當的查詢語言。
* 在`Query`欄位中輸入查詢陳述式。
* 如有必要，請使用提供的核取方塊選取查詢的執行方式。
   * 依預設，JCR查詢不需要執行來識別查詢執行計畫（QueryBuilder查詢就不是這種情況）。
   * 提供三個選項來執行查詢 — 
      * `Include Execution Time` — 執行查詢，但不嘗試讀取任何結果。
      * `Read first page of results` — 執行查詢並讀取20個結果的第一個「頁面」（復寫執行查詢的最佳實務）。
      * `Include Node Count` — 執行查詢並讀取整個結果集（通常不建議這麼做 — 請參閱[索引周遊](#index-traversal)）。

#### 查詢說明快顯功能表 {#query-explanation-popup}

![查詢說明快顯視窗](./assets/query-explanation-popup.png)

選取`Explain`後，使用者會看到一個快顯視窗，說明查詢說明的結果（以及執行，如果選取）。
此快顯視窗包括 — 

* 執行查詢時使用的索引（如果查詢是使用[存放庫周遊](#repository-traversal)執行，則無索引）。
* 執行時間（如果已核取`Include Execution Time`核取方塊）和讀取的結果計數（如果已核取`Read first page of results`或`Include Node Count`核取方塊）。
* 執行計畫，允許查詢執行方式的詳細分析 — 請參閱[閱讀查詢執行計畫](#reading-query-execution-plan)以瞭解如何解譯。
* 前20個查詢結果的路徑（如果已核取`Read first page of results`核取方塊）
* 查詢計畫的完整記錄，顯示執行此查詢時所考量的索引的相對成本（成本最低的索引將會是所選索引）。

#### 讀取查詢執行計畫 {#reading-query-execution-plan}

「查詢執行計畫」包含預測（或解釋）特定查詢效能所需的一切。 透過將原始JCR （或查詢產生器）查詢中的限制和排序與在基礎索引（Lucene、Elastic或Property）中執行的查詢進行比較，瞭解查詢的執行效率。

請考量下列查詢 — 

```
/jcr:root/content/dam//element(*, dam:Asset) [jcr:content/metadata/dc:title = "My Title"] order by jcr:created
```

...其中包含 — 

* 3個限制
   * 節點型別(`dam:Asset`)
   * 路徑（`/content/dam`的子代）
   * 屬性(`jcr:content/metadata/dc:title = "My Title"`)
* 依`jcr:created`屬性排序

說明此查詢會產生下列計畫 — 

```
[dam:Asset] as [a] /* lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) +:ancestors:/content/dam +jcr:content/metadata/dc:title:My Title ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }] where ([a].[jcr:content/metadata/dc:title] = 'My Title') and (isdescendantnode([a], [/content/dam])) */
```

在這個計畫中，描述在基礎索引中執行的查詢的區段是 — 

```
lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) +:ancestors:/content/dam +jcr:content/metadata/dc:title:My Title ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]
```

計畫的這個區段指出 — 

* 索引是用來執行此查詢 — 
   * 在此案例中，將使用Lucene索引`/oak:index/damAssetLucene-9`，因此其餘資訊為Lucene查詢語法。
* 所有3個限制都由索引處理 — 
   * 節點型別限制
      * 隱含，因為`damAssetLucene-9`只索引dam:Asset型別的節點。
   * 路徑限制
      * 因為`+:ancestors:/content/dam`出現在Lucene查詢中。
   * 屬性限制
      * 因為`+jcr:content/metadata/dc:title:My Title`出現在Lucene查詢中。
* 排序由索引處理
   * 因為`ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]`出現在Lucene查詢中。

此類查詢的執行狀況可能良好，因為從索引查詢傳回的結果不會在查詢引擎中進一步篩選（除了存取控制篩選之外）。 但是，如果未遵循最佳實務，這類查詢仍可能執行緩慢 — 請參閱下方的[索引周遊](#index-traversal)。

考慮不同的查詢 — 

```
/jcr:root/content/dam//element(*, dam:Asset) [jcr:content/metadata/myProperty = "My Property Value"] order by jcr:created
```

...其中包含 — 

* 3個限制
   * 節點型別(`dam:Asset`)
   * 路徑（`/content/dam`的子代）
   * 屬性(`jcr:content/metadata/myProperty = "My Property Value"`)
* 依`jcr:created`屬性排序**

說明此查詢會產生下列計畫 — 

```
[dam:Asset] as [a] /* lucene:damAssetLucene-9-custom-1(/oak:index/damAssetLucene-9-custom-1) :ancestors:/content/dam ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }] where ([a].[jcr:content/metadata/myProperty] = 'My Property Value') and (isdescendantnode([a], [/content/dam])) */
```

在這個計畫中，描述在基礎索引中執行的查詢的區段是 — 

```
lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) :ancestors:/content/dam ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]
```

計畫的這個區段指出 — 

* 索引只會處理2個限制（共3個） — 
   * 節點型別限制
      * 隱含，因為`damAssetLucene-9`只索引dam:Asset型別的節點。
   * 路徑限制
      * 因為`+:ancestors:/content/dam`出現在Lucene查詢中。
* 屬性限制`jcr:content/metadata/myProperty = "My Property Value"`不是在索引上執行，而是將套用為查詢引擎篩選基礎Lucene查詢的結果。
   * 這是因為`+jcr:content/metadata/myProperty:My Property Value`未出現在Lucene查詢中，因為此屬性並未在用於此查詢的`damAssetLucene-9`索引中編制索引。

此查詢執行計畫會從索引中讀取`/content/dam`下的每個資產，然後由查詢引擎進一步篩選（這只會包含符合結果集中非索引屬性限制的資產）。

即使只有一小部分資產符合限制`jcr:content/metadata/myProperty = "My Property Value"`，查詢仍必須讀取大量節點以（嘗試）填入請求的結果的「頁面」。 這可能會導致查詢效能不佳，在查詢效能工具中會顯示為具有低`Read Optimization`分數)，並且可能會導致WARN訊息，指出正在周遊大量節點（請參閱[索引周遊](#index-traversal)）。

若要最佳化第二個查詢的效能，請建立`damAssetLucene-9`索引(`damAssetLucene-9-custom-1`)的自訂版本，並新增下列屬性定義 — 

```
"myProperty": {
  "jcr:primaryType": "nt:unstructured",
  "propertyIndex": true,
  "name": "jcr:content/metadata/myProperty"
}
```

## JCR查詢速查表 {#jcr-query-cheatsheet}

為了支援建立有效的JCR查詢和索引定義，[JCR查詢速查表](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=zh-Hant#jcrquerycheatsheet)可供下載，並可在開發期間作為參考使用。

它包含QueryBuilder、XPath和SQL-2的範例查詢，涵蓋了在查詢效能方面行為不同的多個案例。 此外，也提供如何建立或自訂Oak索引的建議。 本速查表內容適用於AEM as a Cloud Service和AEM 6.5。

## 索引定義最佳實務 {#index-definition-best-practices}

以下是定義或擴充索引時可考量的一些最佳實務。

* 對於具有現有索引（例如`dam:Asset`或`cq:Page`）的節點型別，除了新增新索引外，更偏好OOTB索引的延伸。
   * 強烈不建議在`dam:Asset`節點型別上新增索引，尤其是全文檢索索引（請參閱[此備註](/help/operations/indexing.md##index-names-index-names)）。
* 新增索引時
   * 一律定義「lucene」型別的索引。
   * 在索引定義（和相關聯的查詢）和`selectionPolicy = tag`中使用索引標籤，以確保該索引僅用於預期的查詢。
   * 請確定已同時提供`queryPaths`和`includedPaths` （通常使用相同的值）。
   * 使用`excludedPaths`排除不包含有用結果的路徑。
   * 只在需要時才使用`analyzed`屬性，例如，當您需要僅對該屬性使用全文查詢限制時。
   * 一律指定`async = [ async, nrt ] `、`compatVersion = 2`和`evaluatePathRestrictions = true`。
   * 只有在需要節點領域全文檢索索引時才指定`nodeScopeIndex = true`。

>[!NOTE]
>
>如需詳細資訊，請參閱[Oak Lucene索引檔案](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

自動化Cloud Manager管道檢查將強制執行上述部分最佳實務。

## 具有大型結果集的查詢 {#queries-with-large-result-sets}

雖然建議避免使用具有大型結果集的查詢，但在某些情況下，必須處理大型結果集。 通常結果的大小事先無法知道，因此應採取一些預防措施，讓處理變得可靠。

* 查詢不應在要求中執行。 相反，查詢應該作為Sling工作或AEM工作流程的一部分執行。 它們的總執行時間沒有任何限制，並且在處理查詢及其結果期間當執行個體發生故障時會重新啟動。
* 若要克服100,000個節點的查詢限制，您應該考慮使用[金鑰集分頁](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination)，並將查詢分割為多個子查詢。

## 存放庫周遊 {#repository-traversal}

周遊存放庫的查詢不使用索引，而是使用類似下列的訊息進行記錄。

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

使用此記錄檔片段，您可以判斷：

* 查詢本身： `//*`
* 執行此查詢的Java程式碼： `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics`可協助識別查詢的建立者。

有了這些資訊，就可以使用本檔案的[最佳化查詢](#optimizing-queries)區段中描述的方法最佳化此查詢。

### 索引周遊 {#index-traversal}

使用索引但仍讀取大量節點的查詢會記錄類似下列的訊息（請注意字詞`Index-Traversed`而非`Traversed`）。

```text
05.10.2023 10:56:10.498 *WARN* [127.0.0.1 [1696502982443] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.search.spi.query.FulltextIndex$FulltextPathCursor Index-Traversed 60000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [dam:Asset] as a where isdescendantnode(a, '/content/dam') order by [jcr:content/metadata/unindexedProperty] /* xpath: /jcr:root/content/dam//element(*, dam:Asset) order by jcr:content/metadata/unindexedProperty */, path=/content/dam//*)
```

發生此狀況有幾個原因 — 

1. 不是所有查詢限制都可以在索引上處理。
   * 在此情況下，將會從索引讀取最終結果集的超集，並接著在查詢引擎中篩選。
   * 這比在基礎索引查詢中套用限制要慢許多倍。
1. 查詢是以屬性排序，而該屬性在索引中未標示為「ordered」。
   * 在這種情況下，查詢引擎必須讀取索引傳回的所有結果，並在記憶體中排序。
   * 這比在基礎索引查詢中套用排序要慢許多倍。
1. 查詢的執行程式正在嘗試迭代大型結果集。
   * 發生此狀況可能有幾個原因，如下所列：

| 原因 | 緩解 |
|----------|--------------|
| `p.guessTotal`的省略（或使用非常大的guessTotal）會導致QueryBuilder重複大量結果計數結果 | 為`p.guessTotal`提供適當的值 |
| 在查詢產生器（即`p.limit=-1`）中使用大型或無限制限制 | 為`p.limit`使用適當的值（最好為1000或更低） |
| 在Query Builder中使用篩選述詞，從基礎JCR查詢中篩選大量結果 | 以可在基礎JCR查詢中套用的限制來取代篩選述詞 |
| 在QueryBuilder中使用以比較器為基礎的排序 | 取代為基礎JCR查詢中的屬性型排序（使用依排序編列索引的屬性） |
| 由於存取控制而篩選大量結果 | 將額外的索引屬性或路徑限制套用至查詢，以映象存取控制 |
| 使用具有大位移的「位移分頁」 | 請考慮使用[金鑰組分頁](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) |
| 大量或無限制結果的反複專案 | 請考慮使用[金鑰組分頁](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) |
| 選擇的索引不正確 | 在查詢和索引定義中使用標籤以確保使用預期的索引 |
