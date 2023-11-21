---
title: 一般Lucene索引移除
description: 瞭解一般Lucene索引的計畫移除情況，以及您會受到哪些影響。
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---

# 一般Lucene索引移除 {#generic-lucene-index-removal}

Adobe打算移除「一般Lucene」索引(`/oak:index/lucene-*`)從Adobe Experience Manager as a Cloud Service取得。 自AEM 6.5起，此索引就已被取代。本檔案說明此決定的影響，並詳細說明如何檢查AEM執行個體是否受到影響。 它也包含變更查詢的方法，以便它們在不使用通用Lucene索引的情況下繼續運作。

## 背景 {#background}

在AEM中，全文檢索查詢是指使用下列函式的查詢：

* `jcr:contains()` 在JCR XPATH中
* `CONTAINS` JCR-SQL2中

若不使用索引，這類查詢就無法傳回結果。 與只包含路徑或屬性限制的查詢不同，如果查詢包含找不到索引的全文限制（因此執行周遊），則一律會傳回零結果。

一般Lucene索引(`/oak:index/lucene-*`)自AEM 6.0 / Oak 1.0起就已存在，可在大部分的存放庫階層中提供全文搜尋，不過有些路徑會使用 `/jcr:system` 和 `/var` 已一律從此排除。 不過，此索引在很大程度上已被更特定節點型別上的索引取代(例如 `damAssetLucene-*` 針對 `dam:Asset` 節點型別)，支援全文檢索和屬性搜尋。

在AEM 6.5中，一般Lucene索引被標籤為已過時，這表示它將在未來版本中遭到移除。 此後，當使用索引時，會記錄WARN，如下列記錄片段所示：

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Change the query or the index definitions.
```

在近期AEM版本中，通用Lucene索引已用於支援極少數功能。 正在重新處理這些內容，以使用其他索引或修改這些內容，移除對此索引的相依性。

例如，參考查閱查詢（如下列範例中的）現在應使用位於的索引 `/oak:index/pathreference`，僅編制索引 `String` 符合尋找JCR路徑的規則運算式的屬性值。

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

為了支援較大的客戶資料量，Adobe不再在新的AEMas a Cloud Service環境中建立通用Lucene索引。 此外，Adobe會從現有的存放庫移除索引。 [請參閱時間表](#timeline) 於本檔案末尾瞭解更多詳細資訊。

Adobe已透過以下方式調整指數成本： `costPerEntry` 和 `costPerExecution` 屬性以確保其他索引，例如 `/oak:index/pathreference` 會儘可能優先使用。

若客戶應用程式使用的查詢仍相依於此索引，則應立即更新以使用其他現有索引，如有必要，可自訂這些索引。 或者，可將新的自訂索引新增到客戶應用程式。 AEMas a Cloud Service索引管理的完整指示可在以下連結中找到： [索引檔案](/help/operations/indexing.md).

## 您有受到影響嗎？ {#are-you-affected}

如果沒有其他全文檢索索引可以為查詢提供服務，則目前會使用通用Lucene索引作為遞補。 使用此過時的索引時，會在WARN層級記錄類似下列的訊息：

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Change the query or the index definitions.
```

在某些情況下，Oak可能會嘗試使用另一個全文索引(例如 `/oak:index/pathreference`)以支援全文檢索查詢，但如果查詢字串不符合索引定義上的規則運算式，則會在WARN層級記錄訊息，且查詢可能不會傳回結果。

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

移除通用Lucene索引後，如果全文檢索查詢找不到任何合適的索引定義，則會在WARN層級記錄如下所示的訊息：

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results are returned
```

>[!IMPORTANT]
>
>**需要客戶動作**
>
> 如果記錄了上述任何警告訊息，您可能需要重新編寫查詢以使用不同的全文索引，或提供新索引來支援查詢。
>
>以下各節提供您可能會看到的相依性型別以及如何解決這些型別的詳細資訊。

## 一般Lucene索引的潛在相依性 {#potential-dependencies}

在幾個區域，您的應用程式和AEM安裝可能會依賴製作和發佈執行個體上的通用Lucene索引。

### 發佈執行個體 {#publish-instance}

#### 自訂應用程式查詢 {#custom-application-queries}

在發佈執行個體上使用一般Lucene索引的查詢最常見來源是自訂應用程式查詢。

在最簡單的情況下，這些可能是未指定節點型別的查詢，因此意味著 `nt:base` 或 `nt:base` 已明確指定，例如：

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**需要客戶動作**
>
>上述查詢應修改為使用適當的節點型別，詳見下節。

例如，可以修改查詢以傳回符合頁面的結果或 `cq:Page node`. 因此，查詢可能會變成：

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

在其他情況下，查詢可能會指定節點型別，但包含無法由其他全文檢索索引處理的全文檢索限制，例如：

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

在此情況下，查詢具有 `dam:Asset` 節點型別，但包含相對節點的全文限制 `jcr:content/metadata/@cq:tags` 屬性。

此屬性不會標籤為在中分析 `damAssetLucene` index，這是最常用於查詢 `dam:Asset` 節點型別。 因此，此索引無法用於此查詢。

因此，查詢會退回一般全文檢索索引，其中所有包含的屬性都標示為已由，其上的萬用字元比對來分析。 `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**需要客戶動作**
>
>標示 `jcr:content/metadata/@cq:tags` 在自訂版本中分析的屬性 `damAssetLucene` 此索引正在處理此查詢中的索引，並且不會記錄任何WARN。

### 編寫執行個體 {#author-instance}

除了在客戶應用程式servlet、OSGi元件和轉譯指令碼中進行的查詢之外，通用Lucene索引還可以有幾個作者特定的用法。

#### 引用搜尋 {#reference-search}

在過去，通用Lucene索引用於支援參考搜尋或搜尋包含其他內容路徑參考的內容。 這類查詢應該已經更新為使用新的 `/oak:index/pathreference` 索引。

#### 路徑欄位選擇器搜尋 {#picker-search}

AEM包含具有Sling資源型別的自訂對話方塊元件 `granite/ui/components/coral/foundation/form/pathfield`，提供瀏覽器/選擇器來選取其他AEM路徑。 預設路徑欄位選擇器，可在無自訂專案時使用 `pickerSrc` 屬性定義於內容結構中，在快顯對話方塊中呈現搜尋列。

可透過以下方式指定要搜尋的節點型別： `nodeTypes` 屬性。

目前，如果否 `nodeTypes` 屬性存在，則基礎搜尋查詢將使用 `nt:base` 節點型別，因此可能使用通用Lucene索引，通常記錄類似於以下的WARN訊息。

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Change the query or the index definitions.
```

在移除通用Lucene索引之前， `pathfield` 元件將會更新，因此使用預設選擇器的元件會隱藏搜尋方塊，這些元件不會提供 `nodeTypes` 屬性。

| 包含搜尋的路徑欄位選擇器 | 不含搜尋的路徑欄位選擇器 |
|---|---|
| ![包含搜尋的路徑欄位選擇器](assets/index-pathfield-picker-with-search.png) | ![不含搜尋的路徑欄位選擇器](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**需要客戶動作**
>
>如果客戶想要在路徑欄位選擇器中保留搜尋功能， `nodeTypes` 應提供屬性，列出其要查詢的節點型別。 這些節點型別可以在中以逗號分隔的清單形式指定 `String` 屬性。 如果不需要搜尋，客戶就不需要採取任何動作。

>[!NOTE]
>
>內容片段模式編輯器使用具有Sling資源型別的專門路徑欄位 `dam/cfm/models/editor/components/contentreference`.
>
> * 目前，這些會在未指定節點型別的情況下執行查詢，導致由於使用通用Lucene索引而記錄WARN。
> * 這些元件的例項很快就會自動預設為使用 `cq:Page` 和 `dam:Asset` 節點型別，無需客戶進一步動作。
> * 此 `nodeTypes` 可以新增屬性來覆寫這些預設節點型別。

## 一般Lucene移除的時間表 {#timeline}

Adobe將採取兩階段方法移除一般Lucene索引。

* **階段1** （計畫於2022年1月31日開始）：不再建立 `/oak:index/lucene-*` 在新的AEMas a Cloud Service環境中。
* **階段2** （預計於2022年3月31日開始）：移除 `/oak:index/lucene-*` 從現有AEMas a Cloud Service環境建立索引。

Adobe將監控上述紀錄訊息，並嘗試聯絡依賴一般Lucene索引的客戶。

為了短期緩解此問題，Adobe會直接將自訂索引定義新增到客戶系統，以防止在必要時移除通用Lucene索引而導致功能或效能問題。

在這種情況下，會向客戶提供更新的索引定義，並通知他們將其包含在透過Cloud Manager發行的未來應用程式版本中。
