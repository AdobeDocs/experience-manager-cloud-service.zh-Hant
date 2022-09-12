---
title: 查詢產生器述詞參考
description: 查詢產生器API的述詞參考。
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 1%

---

# 查詢產生器述詞參考 {#query-builder-predicate-reference}

## 一般 {#general}

### 根 {#root}

這是根謂語組。 它支援組的所有功能，並允許設定全局查詢參數。

查詢中從未使用「root」名稱，此名稱為隱式。

#### 屬性 {#properties-18}

* **`p.offset`**  — 表示結果頁面開始的數字，即要略過的項目數
* **`p.limit`**  — 表示頁面大小的數字
* **`p.guessTotal`**  — 建議：避免計算全部結果總計，而這可能會造成很大成本；表示最多總計的數字（例如1000，該數字讓使用者對粗細大小有足夠的意見，而且結果較小）或 `true` 只計算最少必要值 `p.offset` + `p.limit`
* **`p.excerpt`**  — 若設為 `true`，在結果中加入全文摘要
* **`p.hits`**  — （僅限JSON servlet）選取將點擊寫入為JSON的方式，並搭配這些標準點擊（可透過ResultHitWriter服務擴充）:
   * **`simple`**  — 最小項目，例如 `path`, `title`, `lastmodified`, `excerpt` （若已設定）
   * **`full`**  — 節點的sling JSON轉譯，搭配 `jcr:path` 指出點擊的路徑：預設情況下，僅列出節點的直接屬性，包括更深的樹，其中 `p.nodedepth=N`,0表示整個無限子樹；新增 `p.acls=true` 要包含當前會話對給定結果項的JCR權限(映射： `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)
   * **`selective`**  — 僅指定屬性 `p.properties`，即分隔的空格(使用 `+` （在URL中）相對路徑清單；如果相對路徑具有深度 `>1` 這些將表示為子對象；特別 `jcr:path` 屬性包含點擊的路徑

### 群組 {#group}

此述詞允許建立巢狀條件。 群組可包含巢狀群組。 查詢產生器查詢中的所有內容都會以隱含的方式顯示在根群組中，根群組可具有 `p.or` 和 `p.not` 參數。

以下是比對兩個屬性其中之一與值的範例：

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

從概念上講 `(1_property` 或 `2_property)`.

以下是巢狀群組的範例：

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

這會搜尋詞 **管理** 在 `/content/wknd/ch/de` 或在 `/content/dam/wknd`.

從概念上講 `fulltext AND ( (path AND type) OR (path AND type) )`. 請注意，由於效能原因，此類OR連接需要良好的索引。

#### 屬性 {#properties-6}

* **`p.or`**  — 若設為 `true`，群組中只有一個述詞必須符合。 此預設為 `false`表示所有必須符合
* **`p.not`**  — 若設為 `true`，則會否定群組(預設為 `false`)
* **`<predicate>`**  — 添加嵌套謂詞
* **`N_<predicate>`**  — 新增多個同時的巢狀謂語，例如 `1_property, 2_property, ...`

### orderby {#orderby}

此謂語允許排序結果。 如果需要依多個屬性排序，則需要使用數字首碼多次新增此述詞，例如 `1_orderby=first`, `2_oderby=second`.

#### 屬性 {#properties-13}

* **`orderby`**  — 以前導@表示的JCR屬性名稱，例如 `@jcr:lastModified` 或 `@jcr:content/jcr:title`，或查詢中的其他謂語，例如 `2_property`，排序
* **`sort`**  — 排序方向 `desc` 適用於降序或 `asc` 遞增（預設）
* **`case`**  — 若設為 `ignore` 會使排序不區分大小寫，表示 `a` 之前 `B`;如果空白或遺漏，則排序會區分大小寫，表示 `B` 之前 `a`

## 謂語 {#predicates}

### 布爾屬性 {#boolproperty}

此謂語與JCR布林屬性相符。 僅接受值 `true` 和 `false`. 若 `false`，如果屬性具有值則相符 `false` 或者，如果它根本不存在。 這對於檢查僅在啟用時設定的布林值標幟非常有用。

繼承 `operation` 參數沒有意義。

此述詞支援Facet擷取，並提供每個的貯體 `true` 或 `false` 值，但僅限現有屬性。

#### 屬性 {#properties}

* **`boolproperty`**  — 屬性的相對路徑，例如 `myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`
* **`value`**  — 要檢查屬性的值， `true` 或 `false`

### contentfragment {#contentfragment}

此述詞將結果限制為內容片段。

* 不支援篩選。
* 不支援小面擷取。

#### 屬性 {#properties-1}

* **`contentfragment`**  — 可與任何值搭配使用，以檢查內容片段。

### `dateComparison` {#datecomparison}

此謂語會比較兩個JCR日期屬性。 可以測試它們是否相等、不等、是否大於或等於。

這是僅限篩選的謂語，無法使用搜尋索引。

#### 屬性 {#properties-2}

* **`property1`**  — 第一個日期屬性的路徑
* **`property2`**  — 第二個日期屬性的路徑
* **`operation`**
   * `=` 完全相符（預設）
   * `!=` 不等式比較
   * `>` for `property1` 大於 `property2`
   * `>=` for `property1` 大於或等於 `property2`

### 達特朗日 {#daterange}

此述詞會比對日期/時間間隔的JCR日期屬性。 日期和時間(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，也允許部分表示，例如 `YYYY-MM-DD`. 或者，時間戳記可以提供為POSIX時間。

您可以尋找兩個時間戳記之間的任何項目，任何較新或較指定日期舊的項目，也可以在包含和開啟的間隔之間進行選擇。

它支援Facet擷取，並提供貯體 `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`，和 `earlier than last year`.

不支援篩選。

#### 屬性 {#properties-3}

* **`property`**  — 相對於 `DATE` 屬性，例如 `jcr:lastModified`
* **`lowerBound`**  — 例如，下限界限以檢查屬性 `2014-10-01`
* **`lowerOperation`** - `>` （較新）或 `>=` （at或更新版本），則會套用至 `lowerBound`. 預設為 `>`
* **`upperBound`**  — 例如，上界可檢查屬性 `2014-10-01T12:15:00`
* **`upperOperation`** - `<` （舊）或 `<=` （at或ler）)，適用於 `upperBound`. 預設為 `<`
* **`timeZone`**  — 未指定為ISO-8601日期字串時使用的時區ID。 預設為系統的預設時區。

### 排除路徑 {#excludepaths}

此謂語會從其路徑符合規則運算式的結果中排除節點。

這是僅限篩選的謂語，無法使用搜尋索引。

不支援小面擷取。

#### 屬性 {#properties-4}

* **`excludepaths`**  — 與結果路徑匹配的規則表達式，將匹配的表達式從結果中排除。

### 全文 {#fulltext}

此謂語會搜尋全文索引中的詞語。

不支援篩選。

不支援小面擷取。

#### 屬性 {#properties-5}

* **`fulltext`**  — 全文搜尋詞
* **`relPath`**  — 屬性或子節點中要搜索的相對路徑。 此屬性為選用。

### hasPermission {#haspermission}

此謂語將結果限制為目前工作階段已指定的項目 [JCR權限。](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

這是僅限篩選的謂語，無法使用搜尋索引。 不支援小面擷取。

#### 屬性 {#properties-7}

* **`hasPermission`**  — 目前使用者工作階段必須具有的逗號分隔JCR權限，「全部」才能擁有相關節點；例如 `jcr:write`, `jcr:modifyAccessControl`

### 語言 {#language}

此謂語會尋找特定語言的AEM頁面。 這會同時查看頁面語言屬性和頁面路徑，這些路徑通常包括頂層網站結構中的語言或地區設定。

這是僅限篩選的謂語，無法使用搜尋索引。

它支援Facet擷取，並為每個唯一語言程式碼提供貯體。

#### 屬性 {#properties-8}

* **`language`**  — 例如ISO語言代碼 `de`

### mainasset {#mainasset}

此述詞會檢查節點是否為DAM主要資產，而非子資產。 這基本上是每個節點，而不是子資產節點內。 請注意，這不會檢查 `dam:Asset` 節點類型。 若要使用此述詞，只需設定 `mainasset=true` 或 `mainasset=false`. 沒有其他屬性。

這是僅限篩選的謂語，無法使用搜尋索引。

它支援Facet擷取，並提供主要和子資產的兩個貯體。

#### 屬性 {#properties-9}

* **`mainasset`**  — 布林值 `true` 主要資產， `false` 子資產

### memberOf {#memberof}

此謂語會找出屬於特定 [sling資源集合](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

這是僅限篩選的謂語，無法使用搜尋索引。

不支援小面擷取。

#### 屬性 {#properties-10}

* **`memberOf`** - Sling資源收集路徑

### nodename {#nodename}

此謂語與JCR節點名稱相符。

它支援Facet擷取，並提供每個唯一節點名稱（檔案名稱）的貯體。

#### 屬性 {#properties-11}

* **`nodename`**  — 允許通配符的節點名稱模式： `*` =任何字元或無字元， `?` =任何字元， `[abc]` =僅括弧中的字元

### notexpired {#notexpired}

此述詞會檢查JCR日期屬性是否大於或等於目前伺服器時間來比對項目。 這可用來檢查 `expiresAt` 值並將結果限制為僅限尚未過期的(`notexpired=true`)或已過期(`notexpired=false`)。

不支援篩選。

其支援小面擷取的方式與 [`daterange`](#daterange) 謂語。

#### 屬性 {#properties-12}

* **`notexpired`**  — 布林值 `true` （未來日期或等於）, `false` 過期（過去的日期）（必要）
* **`property`**  — 相對路徑 `DATE` 要檢查的屬性（必要）

### 路徑 {#path}

此述詞會在指定路徑內搜尋。

不支援小面擷取。

#### 屬性 {#properties-14}

* **`path`**  — 這會定義路徑模式。
   * 視 `exact` 屬性，則整個子樹狀結構會相符(例如附加 `//*` 在xpath中，但請注意，這不包含基本路徑)，或僅包含完全相符的路徑，其中可能包含萬用字元(`*`)。
      * 預設為 `true`
   * 若 `self`屬性已設定，則會搜尋包含基礎節點的整個子樹狀結構。
* **`exact`**  — 如果 `exact` is `true`，則完全路徑必須符合，但可包含簡單的萬用字元(`*`)，該名稱符合，但不符合 `/`;如果 `false` （預設）包含所有子系（可選）
* **`flat`**  — 僅搜索直接子項(如附加 `/*` (僅用於 `exact` 不是true，選用)
* **`self`**  — 搜索子樹，但包含指定為路徑的基節點（無通配符）

### 屬性 {#property}

此謂語與JCR屬性及其值相符。

它支援Facet擷取，並為結果中的每個唯一屬性值提供貯體。

#### 屬性 {#properties-15}

* **`property`**  — 屬性的相對路徑，例如 `jcr:title`
* **`value`**  — 要檢查屬性的值；會遵循JCR屬性類型來轉換字串
* **`N_value`**  — 使用 `1_value`, `2_value`,...檢查多個值(結合 `OR` 預設情況下，使用 `AND` if `and=true`)
* **`and`**  — 設為 `true` 組合多個值(`N_value`)搭配 `AND`
* **`operation`**
   * `equals` 完全相符（預設）
   * `unequals` 不等式比較
   * `like` 用於 `jcr:like` xpath函式（可選）
   * `not` 不符合(例如 `not(@prop)` 在xpath中，值參數將被忽略)
   * `exists` 存在檢查
      * `true` 屬性必須存在
      * `false` 與相同 `not` 和是預設值
* **`depth`**  — 屬性/相對路徑可存在的通配符級別數(例如 `property=size depth=2` 將檢查 `node/size`, `node/*/size` 和 `node/*/*/size`)

### 範圍屬性 {#rangeproperty}

此述詞與間隔的JCR屬性相符。 這會套用至具有線性類型的屬性，例如 `LONG`, `DOUBLE` 和 `DECIMAL`. 針對 `DATE` 請參閱 [`daterange`](#daterange) 已最佳化日期格式輸入的述詞。

您可以定義下界限、上界限或兩者。 也可以為上下界限分別指定操作（例如小於或等於）。

不支援小面擷取。

#### 屬性 {#properties-16}

* **`property`**  — 屬性的相對路徑
* **`lowerBound`**  — 下限以檢查屬性
* **`lowerOperation`** - `>` （預設）或 `>=`，則會套用至 `lowerValue`
* **`upperBound`**  — 上限，檢查屬性
* **`upperOperation`** - `<` （預設）或 `<=`，則會套用至 `lowerValue`
* **`decimal`** - `true` 如果選定的屬性類型為「小數」

### relativedaterange {#relativedaterange}

此謂語符合 `JCR DATE` 使用相對於目前伺服器時間的時間偏移來比較日期/時間間隔的屬性。 您可以指定 `lowerBound` 和 `upperBound` 使用毫秒值或Bugzilla語法 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分鐘、三小時、四天、五週、六個月、七年）。 前置詞為 `-` 表示當前時間之前的負偏移。 如果您僅指定 `lowerBound` 或 `upperBound`，另一個會預設為 `0`，代表目前時間。

例如：

* `upperBound=1h` （否） `lowerBound`)會在下一小時內選取任何項目
* `lowerBound=-1d` （否） `upperBound`)會在過去24小時內選取任何項目
* `lowerBound=-6M` 和 `upperBound=-3M` 會在過去3到6個月內選擇任何項目
* `lowerBound=-1500` 和 `upperBound=5500` 會選取1500毫秒到5500毫秒之間的任何值
* `lowerBound=1d` 和 `upperBound=2d` 後天選擇任何東西

請注意，不需要考慮閏年，且所有月份均為30天。

不支援篩選。

其支援小面擷取的方式與 [`daterange`](#daterange) 謂語。

#### 屬性 {#properties-17}

* **`upperBound`**  — 以毫秒或以毫秒為單位的上日期界限 `1s 2m 3h 4d 5w 6M 7y` （一秒，二分鐘，三小時，四天，五週，六個月，七年）相對於當前伺服器時間，使用 `-` 負偏移
* **`lowerBound`**  — 以毫秒或毫秒為單位的下限日期 `1s 2m 3h 4d 5w 6M 7y` （一秒，二分鐘，三小時，四天，五週，六個月，七年）相對於當前伺服器時間，使用 `-` 負偏移

### savedquery {#savedquery}

此述詞包含持續存在的查詢產生器查詢的所有述詞，並以子群組述詞的形式放入目前的查詢中。

請注意，這不會執行額外的查詢，而會延伸目前的查詢。

查詢可以用程式保存，使用 `QueryBuilder#storeQuery()`. 格式可以是多行 `String` 屬性或 `nt:file` 包含查詢的節點，該查詢以Java屬性格式為文本檔案。

它不支援儲存查詢的述詞的Facet擷取。

#### 屬性 {#properties-19}

* **`savedquery`**  — 儲存查詢的路徑(`String` 屬性或 `nt:file` node)

### 相似 {#similar}

此謂語是使用JCR XPath的相似性搜尋 `rep:similar()`.

不支援篩選，也不支援小面擷取。

#### 屬性 {#properties-20}

* **`similar`**  — 要查找類似節點的節點的絕對路徑
* **`local`**  — 到子節點的相對路徑，或 `.` 對於目前節點(選用，預設為 `.`)

### 標籤 {#tag}

此述詞會指定標籤標題路徑，以搜尋標籤有一或多個標籤的內容。

它支援Facet擷取，並使用每個唯一標籤的目前標籤標題路徑，為每個標籤提供貯體。

#### 屬性 {#properties-21}

* **`tag`**  — 要尋找的標題路徑，例如 `properties:orientation/landscape`
* **`N_value`**  — 使用 `1_value`, `2_value`,...檢查多個標籤(結合 `OR` 預設情況下，使用 `AND` if `and=true`)
* **`property`**  — 要查看的屬性（或相對屬性路徑）（預設） `cq:tags`)

### tagid {#tagid}

此述詞會指定標籤ID，以搜尋標籤有一或多個標籤的內容。

它支援Facet擷取，並使用每個唯一標籤的目前標籤ID，為每個標籤提供貯體。

#### 屬性 {#properties-22}

* **`tagid`**  — 要尋找的標籤ID，例如 `properties:orientation/landscape`
* **`N_value`**  — 使用 `1_value`, `2_value`, ...以檢查多個標籤ID(結合 `OR` 預設情況下，使用 `AND` if `and=true`)
* **`property`**  — 要查看的屬性（或相對屬性路徑）（預設） `cq:tags`)

### tagsearch {#tagsearch}

此述詞會指定關鍵字，以搜尋標籤有一或多個標籤的內容。 這會先搜尋標題中包含這些關鍵字的標籤，然後將結果限制為僅限標籤這些關鍵字的項目。

不支援小面擷取。

#### 屬性 {#Properties-1}

* **`tagsearch`**  — 要在標籤標題中搜索的關鍵字
* **`property`**  — 要考慮的屬性（或相對屬性路徑）（預設） `cq:tags`)
* **`lang`**  — 僅搜尋特定本地化標籤標題(例如 `de`)
* **`all`**  — 用於搜索整個標籤全文的布爾值，即所有標題、說明等。 (優先於 `lang`)

### 類型 {#type}

此謂語將結果限制為特定的JCR節點類型，主節點類型或混合類型皆可。 這也會找到該節點類型的子類型。 請注意，儲存庫搜索索引需要涵蓋節點類型，才能有效執行。

它支援Facet擷取，並為結果中的每個唯一類型提供貯體。

#### 屬性 {#Properties-2}

* **`type`**  — 要搜尋的節點類型或混合名稱，例如 `cq:Page`
