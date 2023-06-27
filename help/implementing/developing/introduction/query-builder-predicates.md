---
title: 查詢產生器述詞參考
description: 查詢產生器API的述詞參考。
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 1%

---

# 查詢產生器述詞參考 {#query-builder-predicate-reference}

## 一般 {#general}

### 根 {#root}

根述詞群組。 它支援群組的所有功能，並允許設定全域查詢引數。

查詢中從未使用名稱「root」；這是隱含的。

#### 屬性 {#properties-18}

* **`p.offset`**  — 表示結果頁面開始的數字，也就是要略過多少專案。
* **`p.limit`**  — 表示頁面大小的數字。
* **`p.guessTotal`**  — 建議：避免計算完整結果總計，這可能代價高昂。 指示要計算的總數上限的數字（例如1000，這個數字可提供使用者對粗略大小和精確數字的足夠意見回饋，以獲得較小結果）。 或者， `true` 以只計算至所需的最小值 `p.offset` + `p.limit`.
* **`p.excerpt`**  — 若設為 `true`，在結果中包含全文摘錄。
* **`p.hits`** - （僅適用於JSON servlet）選取點選作為JSON寫入的方式，並包含這些標準點選（可透過ResultHitWriter服務擴充）。
   * **`simple`**  — 最小專案，例如 `path`， `title`， `lastmodified`， `excerpt` （若有設定）。
   * **`full`**  — 節點的sling JSON轉譯，使用 `jcr:path` 表示點選的路徑。 預設情況下，僅列出節點的直接屬性，包括更深層的樹狀結構 `p.nodedepth=N`，0表示完整、無限的子樹狀結構。 新增 `p.acls=true` 在指定的結果專案上包含目前工作階段的JCR許可權(對應： `create` = `add_node`， `modify` = `set_property`， `delete` = `remove`)。
   * **`selective`**  — 僅指定屬性 `p.properties`，以空格分隔(使用 `+` （在URL中）相對路徑的清單。 如果相對路徑有深度 `>1`時，這些屬性會表示為子物件。 特殊 `jcr:path` 屬性包含點選的路徑。

### 群組 {#group}

此述詞允許建立巢狀條件。 群組可包含巢狀群組。 Query Builder查詢中的所有內容都隱含在根群組中，該根群組可能具有 `p.or` 和 `p.not` 引數。

以下是比對兩個屬性之一與值的範例：

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

在概念上，這是 `(1_property` 或 `2_property)`.

以下是巢狀群組的範例：

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

搜尋字詞 **管理** 在中的頁面內 `/content/wknd/ch/de` 或在中的資產中 `/content/dam/wknd`.

在概念上，這是 `fulltext AND ( (path AND type) OR (path AND type) )`. 基於效能原因，此類OR聯結需要良好的索引。

#### 屬性 {#properties-6}

* **`p.or`**  — 若設為 `true`，群組中只有一個述詞必須相符。 預設為 `false`，表示所有專案都必須相符
* **`p.not`**  — 若設為 `true`，這會讓群組失效(預設為 `false`)
* **`<predicate>`**  — 新增巢狀述詞
* **`N_<predicate>`**  — 同時新增多個巢狀述詞，例如 `1_property, 2_property, ...`

### orderby {#orderby}

此述詞允許排序結果。 如果需要依多個屬性排序，則必須使用數字首碼多次新增此述詞，例如 `1_orderby=first`， `2_oderby=second`.

#### 屬性 {#properties-13}

* **`orderby`**  — 例如，以前導@表示的JCR屬性名稱 `@jcr:lastModified` 或 `@jcr:content/jcr:title`，或是查詢中的其他述詞，例如 `2_property`，排序依據
* **`sort`**  — 排序方向，可以 `desc` 降序或 `asc` 遞增（預設）
* **`case`**  — 若設為 `ignore`，這會使排序不區分大小寫，意思是 `a` 早於 `B`；如果為空白或省略，排序會區分大小寫，這表示 `B` 早於 `a`

## 述詞 {#predicates}

### 布林屬性 {#boolproperty}

此述詞符合JCR布林值屬性。 僅接受值 `true` 和 `false`. 如果值為 `false`，則會比對屬性是否具有值 `false`，或如果它根本不存在。 此述詞對於檢查只在啟用時設定的布林值標幟很有用。

繼承的 `operation` 引數沒有意義。

此述詞支援Facet擷取，並為每個提供Bucket `true` 或 `false` 值，但僅適用於現有屬性。

#### 屬性 {#properties}

* **`boolproperty`**  — 屬性的相對路徑，例如 `myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`
* **`value`**  — 檢查屬性的值， `true` 或 `false`

### contentfragment {#contentfragment}

此述詞將結果限製為內容片段。

* 不支援篩選。
* 不支援多面向擷取。

#### 屬性 {#properties-1}

* **`contentfragment`**  — 可與任何值搭配使用以檢查內容片段。

### `dateComparison` {#datecomparison}

此述詞會比較兩個JCR日期屬性。 可以測試它們是否相等、不相等、大於或大於或等於。

僅限篩選的述詞，無法使用搜尋索引。

#### 屬性 {#properties-2}

* **`property1`**  — 第一個日期屬性的路徑
* **`property2`**  — 第二個日期屬性的路徑
* **`operation`**
   * `=` 完全符合（預設）
   * `!=` 不等式比較
   * `>` 的 `property1` 大於 `property2`
   * `>=` 的 `property1` 大於或等於 `property2`

### 日期範圍 {#daterange}

此述詞比對JCR日期屬性與日期/時間間隔。 對日期和時間使用ISO8601格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)並允許部分表示，例如 `YYYY-MM-DD`. 或者，時間戳記可以作為POSIX時間提供。

您可以尋找兩個時間戳記之間的任何專案，或尋找比指定日期新或舊的專案，也可以選擇包含和開啟的間隔。

它支援Facet擷取並提供貯體 `today`， `this week`， `this month`， `last 3 months`， `this year`， `last year`、和 `earlier than last year`.

不支援篩選。

#### 屬性 {#properties-3}

* **`property`**  — 相對路徑 `DATE` 屬性，例如 `jcr:lastModified`
* **`lowerBound`**  — 下限為檢查屬性的日期，例如 `2014-10-01`
* **`lowerOperation`** - `>` （較新）或 `>=` （at或更新版本），套用至 `lowerBound`. 預設值為 `>`
* **`upperBound`**  — 上限以檢查屬性，例如 `2014-10-01T12:15:00`
* **`upperOperation`** - `<` （較舊）或 `<=` （等於或大於），適用於 `upperBound`. 預設值為 `<`
* **`timeZone`**  — 未作為ISO-8601日期字串提供時區使用的ID。 預設值是系統的預設時區。

### 排除路徑 {#excludepaths}

此述詞會從結果中排除其路徑符合規則運算式的節點。

僅限篩選的述詞，無法使用搜尋索引。

不支援多面向擷取。

#### 屬性 {#properties-4}

* **`excludepaths`**  — 符合結果路徑的規則運算式，排除結果中符合的路徑。

### 全文 {#fulltext}

搜尋全文檢索索引中的詞語。

不支援篩選。

不支援多面向擷取。

#### 屬性 {#properties-5}

* **`fulltext`**  — 全文檢索搜尋詞
* **`relPath`**  — 在屬性或子節點中搜尋的相對路徑。 此屬性是選用的。

### hasPermission {#haspermission}

此述詞將結果限製為目前工作階段具有指定值的專案 [JCR許可權。](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

僅限篩選的述詞，無法使用搜尋索引。 不支援多面向擷取。

#### 屬性 {#properties-7}

* **`hasPermission`**  — 目前使用者工作階段必須擁有的對相關節點的所有逗號分隔JCR許可權。 例如， `jcr:write`， `jcr:modifyAccessControl`

### 語言 {#language}

此述詞尋找特定語言的AEM頁面。 它會同時檢視頁面語言屬性和頁面路徑，後者通常包含頂層網站結構中的語言或地區設定。

僅限篩選的述詞，無法使用搜尋索引。

它支援Facet擷取，並為每個唯一語言程式碼提供貯體。

#### 屬性 {#properties-8}

* **`language`**  — 例如ISO語言代碼 `de`

### mainasset {#mainasset}

此述詞檢查節點是否為DAM主要資產而不是子資產。 它基本上是子資產節點以外的每個節點。 它不會檢查 `dam:Asset` 節點型別。 若要使用此述詞，請設定 `mainasset=true` 或 `mainasset=false`. 沒有其他屬性。

僅限篩選的述詞，無法使用搜尋索引。

它支援Facet擷取，並為主要和子資產提供兩個貯體。

#### 屬性 {#properties-9}

* **`mainasset`**  — 布林值， `true` 主要資產： `false` 用於子資產

### memberOf {#memberof}

此述詞尋找屬於特定成員的專案 [sling資源集合](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

僅限篩選的述詞，無法使用搜尋索引。

不支援多面向擷取。

#### 屬性 {#properties-10}

* **`memberOf`** - Sling資源集合的路徑

### nodename {#nodename}

此述詞在JCR節點名稱上相符。

它支援Facet擷取，並為每個唯一節點名稱（檔案名稱）提供貯體。

#### 屬性 {#properties-11}

* **`nodename`**  — 允許萬用字元的節點名稱模式： `*` =任何或無字元， `?` =任何字元， `[abc]` =僅括弧中的字元

### notexpired {#notexpired}

此述詞會透過檢查JCR日期屬性是否大於或等於目前伺服器時間來比對專案。 它可用來檢查 `expiresAt` 值和將結果限製為僅限尚未過期的值(`notexpired=true`)，或已過期的檔案(`notexpired=false`)。

不支援篩選。

它支援面向(Facet)擷取，其方式與以下程式碼相同： [`daterange`](#daterange) 述詞。

#### 屬性 {#properties-12}

* **`notexpired`**  — 布林值， `true` 對於尚未過期（未來日期或相等）， `false` （過期日期） （必填）
* **`property`**  — 相對路徑 `DATE` 要檢查的屬性（必要）

### path {#path}

此述詞在指定路徑內搜尋。

不支援多面向擷取。

#### 屬性 {#properties-14}

* **`path`**  — 定義路徑模式。
   * 根據 `exact` 屬性，整個子樹狀結構相符(如附加 `//*` 在xpath中，但請注意，其中不包含基本路徑)，或只有完全相符的路徑，其中可包含萬用字元(`*`)。
      * 預設為 `true`.
&lt;!— *若 `self`屬性已設定，則會搜尋包含基本節點的整個子樹狀結構。—>
* **`exact`** - if `exact` 是 `true`，確切路徑必須相符，但可包含簡單萬用字元(`*`)，則名稱相符，但不符合 `/`；如果是 `false` （預設）包含所有子代（選擇性）。
* **`flat`**  — 僅搜尋直接子項(如附加 `/*` 在xpath中) (僅用於 `exact` 不為true，則為選用)。
* **`self`**  — 搜尋子樹狀結構，但包含指定為路徑的基本節點（無萬用字元）。
   * *重要注意事項*：問題已識別 `self` 查詢產生器目前實作中的屬性，以及在查詢中使用它可能不會產生正確的搜尋結果。 變更目前的實作 `self` 屬性也不可行，因為它可能會中斷依賴它的現有應用程式。 由於此功能， `self` 屬性現已棄用，建議避免使用。

### 屬性 {#property}

此述詞在JCR屬性及其值上相符。

它支援Facet擷取，並為結果中的每個唯一屬性值提供值區。

#### 屬性 {#properties-15}

* **`property`**  — 屬性的相對路徑，例如 `jcr:title`.
* **`value`**  — 要檢查屬性的值；會遵循JCR屬性型別來進行字串轉換。
* **`N_value`**  — 使用 `1_value`， `2_value`， ...以檢查多個值(結合 `OR` 依預設，使用 `AND` 如果 `and=true`)。
* **`and`**  — 設定為 `true` 用於組合多個值(`N_value`)，搭配 `AND`
* **`operation`**
   * `equals` 以取得完全相符（預設）。
   * `unequals` 用於不等式比較。
   * `like` 使用 `jcr:like` xpath函式（選用）。
   * `not` 找不到相符專案(例如， `not(@prop)` 在xpath中，會忽略value引數)。
   * `exists` 以檢查是否存在。
      * `true` 屬性必須存在。
      * `false` 與 `not` 和是預設值。
* **`depth`**  — 可存在屬性/相對路徑的萬用字元層級數目(例如， `property=size depth=2` 檢查 `node/size`， `node/*/size`、和 `node/*/*/size`)。

### rangeproperty {#rangeproperty}

此述詞比對JCR屬性與間隔。 它適用於具有線性型別的屬性，例如 `LONG`， `DOUBLE`、和 `DECIMAL`. 對象 `DATE`，請參閱 [`daterange`](#daterange) 具有最佳化日期格式輸入的述詞。

您可以定義下限、上限或兩者。 也可以分別為下限和上限指定操作（例如，小於或小於或等於）。

不支援多面向擷取。

#### 屬性 {#properties-16}

* **`property`**  — 屬性的相對路徑
* **`lowerBound`**  — 檢查屬性的下限
* **`lowerOperation`** - `>` （預設）或 `>=`，套用至 `lowerValue`
* **`upperBound`**  — 檢查屬性的上限
* **`upperOperation`** - `<` （預設）或 `<=`，套用至 `lowerValue`
* **`decimal`** - `true` 如果checked屬性的型別為Decimal

### 相對日期範圍 {#relativedaterange}

此述詞相符 `JCR DATE` 屬性會使用相對於目前伺服器時間的時間位移，來對應日期/時間間隔。 您可以指定 `lowerBound` 和 `upperBound` 使用毫秒值或Bugzilla語法 `1s 2m 3h 4d 5w 6M 7y` （一秒、兩分鐘、三小時、四天、五週、六個月、七年）。 前置詞為 `-` 表示目前時間之前的負位移。 如果您只指定 `lowerBound` 或 `upperBound`，則另一個預設為 `0`，代表目前時間。

例如：

* `upperBound=1h` (而否 `lowerBound`)在下一個小時內選取任何專案
* `lowerBound=-1d` (而否 `upperBound`)選取過去24小時內的任何專案
* `lowerBound=-6M` 和 `upperBound=-3M` 選取過去3到6個月的任何專案
* `lowerBound=-1500` 和 `upperBound=5500` 選取介於1500毫秒和5500毫秒之間的任何值
* `lowerBound=1d` 和 `upperBound=2d` 選取後天的任何專案

這不會將閏年列入考量，所有月份都是30天。

不支援篩選。

它支援面向(Facet)擷取，其方式與以下程式碼相同： [`daterange`](#daterange) 述詞。

#### 屬性 {#properties-17}

* **`upperBound`**  — 以毫秒為單位的上限日期或 `1s 2m 3h 4d 5w 6M 7y` （一秒、兩分鐘、三小時、四天、五週、六個月、七年）相對於目前伺服器時間，使用 `-` 負位移
* **`lowerBound`**  — 以毫秒為單位的下限日期或 `1s 2m 3h 4d 5w 6M 7y` （一秒、兩分鐘、三小時、四天、五週、六個月、七年）相對於目前伺服器時間，使用 `-` 負位移

### savedquery {#savedquery}

此述詞包含持續查詢產生器查詢的所有述詞作為子群組述詞放入目前查詢。

它不會執行額外的查詢，但會擴充目前的查詢。

可使用以下程式設計方式儲存查詢： `QueryBuilder#storeQuery()`. 格式可以是多行 `String` 屬性或 `nt:file` 以Java™屬性格式將查詢作為文字檔案包含的節點。

不支援已儲存查詢的述詞多面向擷取。

#### 屬性 {#properties-19}

* **`savedquery`**  — 已儲存查詢的路徑(`String` 屬性或 `nt:file` 節點)

### 相似 {#similar}

此述詞是使用JCR XPath的相似性搜尋 `rep:similar()`.

不支援篩選和不支援Facet擷取。

#### 屬性 {#properties-20}

* **`similar`**  — 要尋找類似節點的節點的絕對路徑
* **`local`**  — 下級節點或 `.` 對於目前節點(選擇性，預設為 `.`)

### 標籤 {#tag}

此述詞會指定標籤標題路徑，以搜尋以一或多個標籤標籤標籤的內容。

它支援Facet擷取，並使用其目前的標籤標題路徑為每個唯一標籤提供貯體。

#### 屬性 {#properties-21}

* **`tag`**  — 要尋找的標籤標題路徑，例如 `properties:orientation/landscape`
* **`N_value`**  — 使用 `1_value`， `2_value`， ...以檢查多個標籤(與 `OR` 依預設，使用 `AND` 如果 `and=true`)
* **`property`**  — 要檢視的屬性（或屬性的相對路徑） （預設） `cq:tags`)

### tagid {#tagid}

此述詞會指定標籤ID，以搜尋以一或多個標籤標籤的內容。

它支援Facet擷取，並使用其目前的標籤ID為每個唯一標籤提供貯體。

#### 屬性 {#properties-22}

* **`tagid`**  — 要尋找的標籤ID，例如 `properties:orientation/landscape`
* **`N_value`**  — 使用 `1_value`， `2_value`， ...以檢查多個標籤ID (與 `OR` 依預設，使用 `AND` 如果 `and=true`)
* **`property`**  — 要檢視的屬性（或屬性的相對路徑） （預設） `cq:tags`)

### tagsearch {#tagsearch}

此述詞會指定關鍵字，以搜尋以一或多個標籤標籤標籤的內容。 它會先搜尋其標題中包含這些關鍵字的標籤，然後將結果限製為僅標籤這些關鍵字的專案。

不支援多面向擷取。

#### 屬性 {#Properties-1}

* **`tagsearch`**  — 要在標籤標題中搜尋的關鍵字
* **`property`**  — 要考慮的屬性（或屬性的相對路徑） （預設） `cq:tags`)
* **`lang`**  — 僅搜尋特定本地化的標籤標題(例如， `de`)
* **`all`**  — 布林值，可搜尋整個標籤全文，也就是所有標題、說明等(優先於 `lang`)

### 類型 {#type}

此述詞將結果限製為特定的JCR節點型別，包括主要節點型別或 `mixin` 型別。 它也會尋找該節點型別的子型別。 存放庫搜尋索引必須涵蓋節點型別，才能有效執行。

它支援面向擷取，並為結果中的每個唯一型別提供貯體。

#### 屬性 {#Properties-2}

* **`type`**  — 節點型別或 `mixin` 要搜尋的名稱，例如 `cq:Page`
