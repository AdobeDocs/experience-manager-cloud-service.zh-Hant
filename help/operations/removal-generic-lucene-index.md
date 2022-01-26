---
title: 刪除通用lucene索引
description: 刪除通用lucene索引
exl-id: fe0e00ac-f9c8-43cf-83c2-5a353f5eaeab
source-git-commit: bc7ef6567ad5baa4becd28a7e7d96bd6b579e1ad
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# 刪除「一般lucene」索引

Adobe打算刪除「generic lucene」索引(`/oak:index/lucene-*`)Adobe Experience Manager as a Cloud Service。 此索引自6.5AEM以來已棄用。在本文檔中介紹了此決定的影響，以及如何檢查實例是否受到影響的詳細AEM說明。 最後，它包含更改查詢的方法，以便在不存在此索引的情況下使查詢工作。

## 背景

在AEM中，「fulltext」查詢為使用以下函式的查詢：

* `jcr:contains()` 在JCR XPATH中
* `CONTAINS` 在JCR-SQL2中

如果不使用索引，則此類查詢無法返回結果。 與僅包含路徑或屬性限制的查詢不同，包含找不到索引（因此執行遍歷）的全文限制的查詢將始終返回0個結果。

「generic lucene」索引(`/oak:index/lucene-*`)自AEM6.0 / Oak 1.0以來就存在，以便在大多數儲存庫層次結構(某些路徑，如 `/jcr:system` 和 `/var` 但是，此索引在很大程度上被更特定節點類型上的索引所替代(例如 `damAssetLucene-*` )，它支援全文和屬性搜索。

在AEM6.5中，「generic lucene」索引被標籤為不建議使用（表示將在將來的版本中刪除），此後，在使用該索引時已記錄WARN:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

在最新AEM版本中，「generic lucene」索引已用於支援非常少的功能。 正在重新處理這些索引以使用其他索引，或以其他方式修改以刪除對此索引的依賴關係。
例如，下面所示格式的「reference lookup」查詢現在應使用「/oak:index/pathreference」（它僅對與查找JCR路徑的規則運算式匹配的String屬性值進行索引）。 

```
//*[jcr:contains(., '"/content/dam/mysite"')]
```

為了支援更大的客戶資料卷，Adobe將不再在新as a Cloud Service環境中建立「generic lucene」索引AEM，然後，將開始從現有儲存庫中刪除該索引。 我們已經調整了索引成本計算（通過「costPerEntry」和「costPerExecution」屬性），以確保其他索引(如 `/oak:index/pathreference`)優先使用 `/oak:index/lucene-*` 盡可能。 

使用仍然依賴此索引的查詢的客戶應用程式應立即更新，以利用其他現有索引（如果需要，可以自定義），或者應將新的自定義索引添加到客戶應用程式。 有關as a Cloud Service中索引管AEM理的完整說明，請參見 [索引文檔](/help/operations/indexing.md)。

## 如何判斷您的應用程式是否依賴於「generic lucene」索引？

如果沒有其他全文索引可以為查詢服務，則「generic lucene」索引當前用作「回退」。 使用此不建議使用的索引時，將在WARN級別記錄如下消息：

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

在某些情況下，Oak可能會嘗試使用另一個全文索引(例如 `/oak:index/pathreference`)以支援全文查詢，但如果查詢字串與索引定義上的規則運算式不匹配，則將在WARN級別記錄一條消息，並且查詢可能不會返回結果。

```
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

刪除「generic lucene」索引後，如果全文查詢找不到任何合適的索引定義，則會在WARN級別記錄如下所示的消息：

```
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

如果記錄了其中任何一個索引，則可能需要重新編寫查詢以使用不同的全文索引，或者提供新索引以支援查詢。 下面提供了您可能看到的依賴關係類型以及如何解決這些依賴關係的詳細資訊。

## 「一般lucene」索引的潛在依賴項

### 發佈

#### 自定義應用程式查詢

使用「發佈」上的「generic lucene」索引的查詢最常見的來源是自定義應用程式查詢。

在最簡單的情況下，這些查詢可能是未指定nodetype的查詢（表示顯式指定nt:base）或nt:base，例如：

```
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

需要操作：可以修改這些查詢以使用適當的節點類型 — 例如，返回匹配頁的結果（或cq:Page節點下的任何「aggagets」），查詢可能變為：

```
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

在其他情況下，查詢可能指定nodetype，但包含無法由另一個全文索引處理的全文限制，例如：

```
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

在這種情況下，查詢具有「dam:Asset」節點類型，但包含對相關 `jcr:content/metadata/@cq:tags` 屬性。

此屬性在damAssetLucene索引（最常用於對「dam:Asset」節點類型的查詢的全文索引）中未標籤為「analysed」，因此此索引不能用於此查詢。

因此，查詢將返回到「一般全文」索引上，其中所有包含的屬性都由位於的通配符匹配標籤為分析 `/oak:index/lucene-2/indexRules/nt:base/properties/prop`。

需要客戶操作：標籤 `jcr:content/metadata/@cq:tags` damAssetLucene索引的自定義版本中屬性as「analysed」將導致此查詢由此索引處理，並且不會記錄WARN。

### 作者 

除了在客戶應用程式servlet、OSGI元件和呈現指令碼中的查詢外，還可以使用「generic lucene」索引的許多特定於作者的用法。 

#### 引用搜索

過去，「generic lucene」索引用於支援「引用搜索」（搜索包含對其他內容路徑的引用的內容）。 此類查詢應已移動到使用新的「/oak:index/pathreference」索引。
需要客戶操作：不需要客戶操作。


#### 路徑欄位選取器搜索

包AEM括自定義對話框元件（Sling資源類型「granite/ui/components/coral/foundation/form/pathfield」），它提供用於選擇另一路徑的瀏覽器(選取AEM器)。  預設的路徑欄位選取器（在內容結構中未定義自定義「pickerSrc」屬性時使用）在彈出式對話框中呈現搜索欄。
可以使用「nodeTypes」屬性指定要針對的節點類型。

目前，如果沒有「nodeTypes」屬性，則基礎搜索查詢將使用「nt:base」nodetype，因此很可能使用「generic lucene」索引（通常記錄下面顯示的WARN消息）。

```
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

在刪除「generic lucene」之前，將更新路徑欄位元件，以便使用不提供「nodeTypes」屬性的預設選取器為元件隱藏搜索框。

| 帶搜索的路徑欄位選取器 | 不帶搜索的路徑欄位選取器 |
|---|---|
| ![帶搜索的路徑欄位選取器](assets/index-pathfield-picker-with-search.png) | ![不帶搜索的路徑欄位選取器](assets/index-pathfield-picker-without-search.png) |


需要客戶操作：如果不需要搜索，則不需要客戶執行任何操作。

如果客戶希望在路徑欄位選取器中保留搜索功能，應提供一個屬性「nodeTypes」，列出他們要查詢的節點類型。 這些可以指定為String屬性中以逗號分隔的節點類型清單。


>[!NOTE]
>內容片段模型編輯器使用帶有Sling資源類型「dam/cfm/models/editor/components/contentreference」的專用路徑欄位。
> * 目前，這些查詢執行時未指定節點類型 — 導致由於使用「generic lucene」索引而記錄WARN。
> * 這些元件的實例很快將自動預設為使用「cq:Page」和「dam:Asset」節點類型，而無需客戶進一步操作。
> * 可以添加「nodeTypes」屬性以覆蓋這些預設節點類型。 





## 刪除「一般lucene」的時間軸

Adobe將採取兩階段辦法，刪除&quot;一般lucene&quot;指數。

**階段1** （計畫於2022年1月31日開始）:不再在新as a Cloud Service環境中建立「/oak:index/lucene-*AEM」。

**階段2** （計畫於2022年3月31日起）:從新as a Cloud Service環境中刪除「/oak:index/lucene-*」索AEM引。

Adobe將監視上述日誌消息，並嘗試聯繫仍依賴「generic lucene」索引的客戶。

作為短期緩解措施，如果必要，Adobe將直接向客戶系統添加自定義索引定義，以防止由於刪除「一般lucene」索引而導致的功能或效能問題。

在這種情況下，將向客戶提供更新的索引定義，並建議客戶通過雲管理器將其納入其應用程式的未來版本。
