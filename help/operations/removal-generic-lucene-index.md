---
title: 常規Lucene索引刪除
description: 了解計畫移除通用Lucene索引，以及您可能受到的影響。
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---

# 常規Lucene索引刪除 {#generic-lucene-index-removal}

Adobe打算移除「一般Lucene」索引(`/oak:index/lucene-*`)來自Adobe Experience Manager as a Cloud Service。 此索引自AEM 6.5起即已淘汰。本檔案中說明此決定的影響，以及如何檢查AEM例項是否受到影響的詳細說明。 它還包含更改查詢的方法，以便它們在沒有通用Lucene索引的情況下繼續運行。

## 背景 {#background}

在AEM中，全文查詢是指使用下列函式的查詢：

* `jcr:contains()` 在JCR XPATH中
* `CONTAINS` 在JCR-SQL2中

如果不使用索引，則此類查詢無法返回結果。 與僅包含路徑或屬性限制的查詢不同，包含全文限制的查詢將始終返回零結果，而無法找到索引（因此執行遍歷）。

通用Lucene索引(`/oak:index/lucene-*`)自AEM 6.0 / Oak 1.0起便已存在，只要部分路徑(例如 `/jcr:system` 和 `/var` 一律被排除在外。 但是，此索引已被更具體的節點類型上的索引(例如 `damAssetLucene-*` 針對 `dam:Asset` 節點類型)，可支援全文和屬性搜尋。

在AEM 6.5中，通用Lucene索引標示為已過時，表示將在未來版本中移除該索引。 此後，當使用索引時，將記錄WARN，如下列日誌片段所示：

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

在最新的AEM版本中，一般Lucene索引已用於支援非常少的功能。 這些索引正在重新工作以使用其他索引，或以其他方式修改以移除對此索引的依賴。

例如，參考查詢查詢（如以下範例中）現在應使用的索引位於 `/oak:index/pathreference`，僅索引 `String` 與尋找JCR路徑的規則運算式相符的屬性值。

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

為了支援較大的客戶資料卷，Adobe將不再在新的AEMas a Cloud Service環境上建立通用Lucene索引。 此外，Adobe將開始從現有儲存庫中刪除索引。 [查看時間軸](#timeline) 以取得詳細資訊。

Adobe已透過 `costPerEntry` 和 `costPerExecution` 屬性，以確保其他索引，例如 `/oak:index/pathreference` 會盡可能優先使用。

使用仍依賴此索引的查詢的客戶應用程式應立即更新，以利用其他現有索引，如有需要，可自訂這些索引。 或者，新的自訂索引可以新增至客戶應用程式。 如需AEMas a Cloud Service中索引管理的完整指示，請參閱 [索引文檔。](/help/operations/indexing.md)

## 您受影響嗎？ {#are-you-affected}

如果沒有其他全文索引可以為查詢服務，則當前將通用Lucene索引用作後援。 使用此已棄用的索引時，將在「警告」級別記錄類似的消息：

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

在某些情況下，Oak可能會嘗試使用其他全文索引(例如 `/oak:index/pathreference`)以支援全文查詢，但如果查詢字串與索引定義上的規則運算式不符，則訊息將記錄在WARN層級，且查詢可能不會傳回結果。

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

一旦刪除了通用Lucene索引，如果全文查詢找不到任何合適的索引定義，則將在「警告」級別記錄如下所示的消息：

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

>[!IMPORTANT]
>
>**需要客戶操作**
>
> 如果記錄了上述任何警告消息，則可能需要重新處理查詢以使用不同的全文索引，或者提供新索引以支援查詢。
>
>以下各節提供您可能看到的相依性類型，以及如何處理這些相依性。

## 一般Lucene索引的潛在依賴項 {#potential-dependencies}

在許多區域中，您的應用程式和AEM安裝可能取決於製作和發佈執行個體上的一般Lucene索引。

### 發佈例項 {#publish-instance}

#### 自定義應用程式查詢 {#custom-application-queries}

在發佈執行個體上使用一般Lucene索引的查詢最常見的來源是自訂應用程式查詢。

在最簡單的情況下，這些查詢可能沒有指定任何節點類型，因此會暗示 `nt:base` 或 `nt:base` 明確指定，例如：

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**需要客戶操作**
>
>應修改上述查詢，以使用適當的節點類型，如下節所述。

例如，可以修改查詢，以傳回結果比對頁面或 `cq:Page node`. 因此，查詢可能變成：

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

在其他情況下，查詢可能指定節點類型，但包含無法由其他全文索引處理的全文限制，例如：

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

在此案例中，查詢具有 `dam:Asset` 節點類型，但包含相對 `jcr:content/metadata/@cq:tags` 屬性。

此屬性未標示為分析，於 `damAssetLucene` 索引，此索引是最常用於針對 `dam:Asset` 節點類型。 因此，此索引不能用於此查詢。

因此，查詢會回復到一般全文索引，其中所有包含的屬性都會標示為由位於的萬用字元比對分析 `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**需要客戶操作**
>
>標示 `jcr:content/metadata/@cq:tags` 屬性，如自訂版本中所分析 `damAssetLucene` 索引將導致此查詢被此索引處理，並且不記錄任何WARN。

### 製作例項 {#author-instance}

除了客戶應用程式servlet、OSGi元件和呈現指令碼中的查詢外，一般Lucene索引還可以有許多特定於作者的用法。

#### 參考搜尋 {#reference-search}

過去，一般Lucene索引一直用於支援參考搜尋或搜尋包含其他內容路徑參考的內容。 此類查詢應已更新，以使用新 `/oak:index/pathreference` 索引。

#### 路徑欄位選擇器搜索 {#picker-search}

AEM包含具有Sling資源類型的自訂對話方塊元件 `granite/ui/components/coral/foundation/form/pathfield`，提供瀏覽器/選擇器以選取其他AEM路徑。 預設路徑欄位選擇器，在無自訂時使用 `pickerSrc` 屬性是在內容結構中定義，在彈出式對話方塊中呈現搜尋列。

可使用 `nodeTypes` 屬性。

目前，若否 `nodeTypes` 屬性存在，則基礎搜尋查詢將使用 `nt:base` 節點類型，因此可能使用通用Lucene索引，通常記錄類似以下的WARN消息。

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

在移除通用Lucene索引之前， `pathfield` 元件將會更新，以便使用預設選擇器（不提供）為元件隱藏搜索框 `nodeTypes` 屬性。

| 具有搜索的路徑欄位選擇器 | 不搜索的路徑欄位選擇器 |
|---|---|
| ![具有搜索的路徑欄位選擇器](assets/index-pathfield-picker-with-search.png) | ![不搜索的路徑欄位選擇器](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**需要客戶操作**
>
>如果客戶想要保留路徑欄位選擇器中的搜尋功能，請 `nodeTypes` 應提供屬性，列出其要查詢的節點類型。 這些可以指定為以逗號分隔的 `String` 屬性。 如果不需要搜尋，則無需客戶執行任何動作。

>[!NOTE]
>
>內容片段模型編輯器使用具有Sling資源類型的專用路徑欄位 `dam/cfm/models/editor/components/contentreference`.
> * 目前，這些查詢執行時未指定節點類型，導致由於使用通用Lucene索引而記錄WARN。
> * 這些元件的例項很快會自動預設為使用 `cq:Page` 和 `dam:Asset` 節點類型，無需客戶進一步操作。
> * 此 `nodeTypes` 可以新增屬性來覆寫這些預設節點類型。


## 一般Lucene移除時間軸 {#timeline}

Adobe將採取兩階段方法來移除通用Lucene索引。

* **階段1** （計畫於2022年1月31日開始）:不再建立 `/oak:index/lucene-*` 在新的AEMas a Cloud Service環境中。
* **階段2** （計畫於2022年3月31日開始）:移除 `/oak:index/lucene-*` 從現有AEMas a Cloud Service環境建立索引。

Adobe將監視上述日誌消息，並將嘗試與仍依賴通用Lucene索引的客戶聯繫。

作為短期緩解措施，Adobe將直接將自定義索引定義添加到客戶系統，以防止因必要時刪除通用Lucene索引而出現功能或效能問題。

在這種情況下，將會向客戶提供更新的索引定義，並建議將此內容納入未來透過Cloud Manager發行的應用程式中。
