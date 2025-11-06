---
title: 查詢產生器述詞參考
description: AEM as a Cloud Service中查詢產生器API的述詞參考。
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2270'
ht-degree: 1%

---

# 查詢產生器述詞參考 {#query-builder-predicate-reference}

## 一般 {#general}

### 根 {#root}

根述詞群組。 它支援群組的所有功能，並允許設定全域查詢引數。

查詢中從未使用過名稱「root」，這是隱含的名稱。

#### 屬性 {#properties-18}

* **`p.offset`** — 表示結果頁面開始的數字，也就是要略過的專案數。
* **`p.limit`** — 表示頁面大小的數字。
* **`p.guessTotal`** — 建議：避免計算完整的結果總計，這可能非常昂貴。 指示要計算的總數上限的數字（例如，1000，這個數字可提供使用者對粗略大小和精確數字的足夠意見反應，以獲得較小結果）。 或者，`true`僅計算至最低必要值`p.offset` + `p.limit`。
* **`p.excerpt`** — 如果設為`true`，請在結果中包含全文檢索節選。
* **`p.indexTag`** — 如果設定，會在查詢中包含索引標籤選項（請參閱[查詢選項索引標籤](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)）。
* **`p.facetStrategy`** — 若設為`oak`，Query Builder會將Facet擷取委派給Oak （請參閱[Facet](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)）。
* **`p.hits`** - （僅適用於JSON servlet）選取點選寫入為JSON的方式，並使用這些標準點選（可透過ResultHitWriter服務擴充）。
   * **`simple`** — 最小專案，例如`path`、`title`、`lastmodified`、`excerpt` （如果已設定）。
   * **`full`** — 節點的Sling JSON轉譯，其中`jcr:path`表示點選的路徑。 依照預設，僅列出節點的直接屬性，包括包含`p.nodedepth=N`的較深樹狀結構，其中0表示整個無限子樹狀結構。 新增`p.acls=true`以包含指定結果專案上目前工作階段的JCR許可權（對應： `create` = `add_node`，`modify` = `set_property`，`delete` = `remove`）。
   * **`selective`** — 僅在`p.properties`中指定的屬性，這是相對路徑的空格分隔清單（在URL中使用`+`）。 如果相對路徑具有深度`>1`，這些屬性會表示為子物件。 特殊`jcr:path`屬性包含點選的路徑。

### 群組 {#group}

此述詞允許建立巢狀條件。 群組可以包含巢狀群組。 Query Builder查詢中的所有內容都以隱含方式位於根群組中，該根群組也可以有`p.or`和`p.not`引數。

以下範例是將兩個屬性之一與值比對：

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

概念上，它是`(1_property`或`2_property)`。

以下是巢狀群組的範例：

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

在&#x200B;**的頁面中或**&#x200B;的資產中搜尋字詞`/content/wknd/ch/de`Management`/content/dam/wknd`。

概念上，它是`fulltext AND ( (path AND type) OR (path AND type) )`。 基於效能原因，這些OR聯結需要良好的索引。

#### 屬性 {#properties-6}

* **`p.or`** — 若設為`true`，群組中只能有一個相符的述詞。 預設為`false`，表示所有專案都必須相符
* **`p.not`** — 若設為`true`，則會讓群組無效（預設為`false`）
* **`<predicate>`** — 新增巢狀述詞
* **`N_<predicate>`** — 同時新增多個巢狀述詞，例如`1_property, 2_property, ...`

### orderby {#orderby}

此述詞允許排序結果。 如果需要依多個屬性排序，則必須使用數字首碼多次新增此述詞，例如`1_orderby=first`、`2_oderby=second`。

#### 屬性 {#properties-13}

* **`orderby`** — 以開頭@表示的JCR屬性名稱，例如`@jcr:lastModified`或`@jcr:content/jcr:title`，或是查詢中要排序的另一個述詞，例如`2_property`
* **`sort`** — 排序方向，`desc`表示遞減，或`asc`表示遞增（預設）
* **`case`** — 若設為`ignore`，則會使排序不區分大小寫，表示`a`在`B`之前；若為空白或遺漏，排序會區分大小寫，表示`B`在`a`之前

## 述詞 {#predicates}

### 布林屬性 {#boolproperty}

此述詞符合JCR布林值屬性。 僅接受值`true`和`false`。 如果值為`false`，則符合該屬性的值為`false`或根本不存在該屬性。 此述詞在檢查布林值標幟時非常有用，這些標幟僅在啟用時才會設定。

繼承的`operation`引數沒有意義。

此述詞支援Facet擷取，並為每個`true`或`false`值提供值區，但僅針對現有屬性。

#### 屬性 {#properties}

* **`boolproperty`** — 屬性的相對路徑，例如`myFeatureEnabled`或`jcr:content/myFeatureEnabled`
* **`value`** — 要檢查屬性，`true`或`false`的值

### contentfragment {#contentfragment}

此述詞將結果限製為內容片段。

* 不支援篩選。
* 不支援多面向擷取。

#### 屬性 {#properties-1}

* **`contentfragment`** — 可與任何值搭配使用以檢查內容片段。

### `dateComparison` {#datecomparison}

此述詞會比較兩個JCR日期屬性。 可以測試這些值是否相等、不相等、大於或大於或等於。

僅限篩選的述詞，且無法使用搜尋索引。

#### 屬性 {#properties-2}

* **`property1`** — 第一個日期屬性的路徑
* **`property2`** — 路徑至第二個日期屬性
* **`operation`**
   * `=`為完全相符（預設）
   * 不相等比較的`!=`
   * `>`的`property1`大於`property2`
   * `>=`的`property1`大於或等於`property2`

### 日期範圍 {#daterange}

此述詞比對JCR日期屬性與日期/時間間隔。 使用ISO8601
日期和時間的格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，並允許部分表示，如`YYYY-MM-DD`。 或者，時間戳記可以作為POSIX時間提供。

您可以尋找兩個時間戳記之間的任何專案，或比指定日期新或舊的專案，也可以選擇介於包含間隔和開啟間隔之間的專案。

它支援Facet擷取並提供貯體`today`、`this week`、`this month`、`last 3 months`、`this year`、`last year`和`earlier than last year`。

不支援篩選。

#### 屬性 {#properties-3}

* **`property`** - `DATE`屬性的相對路徑，例如`jcr:lastModified`
* **`lowerBound`** — 檢查屬性的日期下限，例如`2014-10-01`
* **`lowerOperation`** - `>` （較新）或`>=` （大於或等於），套用至`lowerBound`。 預設值為`>`
* **`upperBound`** — 檢查屬性的上限，例如`2014-10-01T12:15:00`
* **`upperOperation`** - `<` （較舊）或`<=` （等於或較舊），適用於`upperBound`。 預設值為`<`
* **`timeZone`** — 未指定為ISO-8601日期字串時要使用的時區ID。 預設為系統的預設時區。

### 排除路徑 {#excludepaths}

此述詞會從結果中排除其路徑符合規則運算式的節點。

僅限篩選的述詞，且無法使用搜尋索引。

不支援多面向擷取。

#### 屬性 {#properties-4}

* **`excludepaths`** — 符合結果路徑的規則運算式，排除結果中符合的路徑。

### 全文 {#fulltext}

搜尋全文檢索索引中的詞語。

不支援篩選。

不支援多面向擷取。

#### 屬性 {#properties-5}

* **`fulltext`** — 全文檢索搜尋詞
* **`relPath`** — 在屬性或子節點中搜尋的相對路徑。 此屬性是選用的。

### hasPermission {#haspermission}

此述詞將結果限製為目前工作階段具有指定[JCR許可權](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)的專案。

僅限篩選的述詞，且無法使用搜尋索引。 不支援多面向擷取。

#### 屬性 {#properties-7}

* **`hasPermission`** — 目前使用者工作階段必須擁有有關節點的所有逗號分隔JCR許可權。 例如，`jcr:write`， `jcr:modifyAccessControl`

### 語言 {#language}

此述詞會尋找特定語言的AEM頁面。 它會同時檢視頁面語言屬性和頁面路徑，這通常會包含頂層網站結構中的語言或地區設定。

僅限篩選的述詞，且無法使用搜尋索引。

它支援Facet擷取，並為每個唯一語言程式碼提供貯體。

#### 屬性 {#properties-8}

* **`language`** - ISO語言代碼，例如`de`

### 主要資產 {#mainasset}

此述詞檢查節點是否為DAM主資產而非子資產。 這基本上是每個不在子資產節點內的節點。 它不會檢查`dam:Asset`節點型別。 若要使用此述詞，請設定`mainasset=true`或`mainasset=false`。 沒有其他屬性。

僅限篩選的述詞，且無法使用搜尋索引。

它支援多面向擷取，並為主要和子資產提供兩個貯體。

#### 屬性 {#properties-9}

* **`mainasset`** — 布林值，`true`用於主要資產，`false`用於子資產

### memberOf {#memberof}

此述詞尋找屬於特定[sling資源集合](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)成員的專案。

僅限篩選的述詞，且無法使用搜尋索引。

不支援多面向擷取。

#### 屬性 {#properties-10}

* **`memberOf`** - Sling資源集合的路徑

### nodename {#nodename}

此述詞在JCR節點名稱上相符。

它支援Facet擷取，並為每個唯一節點名稱（檔案名稱）提供值區。

#### 屬性 {#properties-11}

* **`nodename`** — 允許萬用字元的節點名稱模式： `*` =任何或無字元，`?` =任何字元，`[abc]` =僅括弧中的字元

### notexpired {#notexpired}

此述詞會透過檢查JCR日期屬性是否大於或等於目前伺服器時間來比對專案。 它可用來檢查`expiresAt`值，並將結果限製為僅限尚未過期(`notexpired=true`)或已過期(`notexpired=false`)的值。

不支援篩選。

它支援Facet擷取，其方式與[`daterange`](#daterange)述詞相同。

#### 屬性 {#properties-12}

* **`notexpired`** — 布林值，`true`代表尚未過期（未來日期或相等），`false`代表過期（過去的日期） （必要）
* **`property`** — 要檢查的`DATE`屬性的相對路徑（必要）

### 路徑 {#path}

此述詞在給定路徑內搜尋。

不支援多面向擷取。

#### 屬性 {#properties-14}

* **`path`** — 定義路徑模式。
   * 根據`exact`屬性，可能是整個子樹狀結構相符（例如在xpath中附加`//*`，但請注意，它不包含基底路徑），或是隻符合一個完全相符的路徑，其中可包含萬用字元(`*`)。
      * 預設為`true`。
&lt;!—   *如果設定了`self`屬性，則會搜尋包含基底節點的整個子樹狀結構。—>
* **`exact`** — 如果`exact`是`true`，則確切的路徑必須相符，但它可以包含符合名稱的簡單萬用字元(`*`)，但不包含`/`；如果是`false` （預設），則包含所有子代（選擇性）。
* **`flat`** — 僅搜尋直接子系（例如在xpath中附加`/*`） （僅在`exact`不是true時才使用，為選用）。
* **`self`** — 搜尋子樹狀結構，但包含以路徑指定的基底節點（無萬用字元）。
   * *重要備註*：在目前實作查詢產生器的`self`屬性中識別出問題，且將其用於查詢可能無法產生正確的搜尋結果。 變更`self`屬性的目前實作也無法執行，因為它可能會中斷依賴它的現有應用程式。 由於此功能，`self`屬性現已過時；建議避免使用它。

### 屬性 {#property}

此述詞符合JCR屬性及其值。

它支援Facet擷取，並為結果中的每個唯一屬性值提供值區。

#### 屬性 {#properties-15}

* **`property`** — 屬性的相對路徑，例如`jcr:title`。
* **`value`** — 要檢查屬性的值；遵循JCR屬性型別進行字串轉換。
* **`N_value`** — 使用`1_value`、`2_value`、...檢查多個值（預設會與`OR`結合，如果`AND`則為`and=true`）。
* **`and`** — 設定為`true`以結合多個值(`N_value`)與`AND`
* **`operation`**
   * `equals`為完全相符（預設）。
   * 不相等比較的`unequals`。
   * 使用`like` xpath函式的`jcr:like` （選擇性）。
   * 沒有相符專案的`not` （例如xpath中的`not(@prop)`，會忽略值引數）。
   * `exists`是否存在。
      * `true`屬性必須存在。
      * `false`與`not`相同，且為預設值。
* **`depth`** — 屬性/相對路徑可以存在的萬用字元層級數目（例如，`property=size depth=2`檢查`node/size`、`node/*/size`和`node/*/*/size`）。

### rangeproperty {#rangeproperty}

此述詞比對JCR屬性與間隔。 它適用於線性型別的屬性，例如`LONG`、`DOUBLE`和`DECIMAL`。 若為`DATE`，請參閱具有最佳化日期格式輸入的[`daterange`](#daterange)述詞。

您可以定義下限、上限或兩者。 也可以為上下限分別指定操作（例如，小於或小於或等於）。

不支援多面向擷取。

#### 屬性 {#properties-16}

* **`property`** — 屬性的相對路徑
* **`lowerBound`** — 檢查屬性的下限
* **`lowerOperation`** - `>` （預設）或`>=`套用至`lowerValue`
* **`upperBound`** — 檢查屬性的上限
* **`upperOperation`** - `<` （預設）或`<=`套用至`lowerValue`
* 如果核取的屬性型別為Decimal，則為&#x200B;**`decimal`** - `true`

### 相對日期範圍 {#relativedaterange}

此述詞使用相對於目前伺服器時間的時間位移，針對日期/時間間隔比對`JCR DATE`屬性。 您可以使用毫秒值或Bugzilla語法`lowerBound` （一秒、兩分鐘、三小時、四天、五週、六個月、七年）來指定`upperBound`和`1s 2m 3h 4d 5w 6M 7y`。 前置詞為`-`，表示目前時間之前的負位移。 如果您只指定`lowerBound`或`upperBound`，則另一個預設為`0`，代表目前時間。

例如：

* `upperBound=1h` （沒有任何`lowerBound`）在下一個小時選擇任何專案
* `lowerBound=-1d` （沒有任何`upperBound`）在過去24小時內選取任何專案
* `lowerBound=-6M`和`upperBound=-3M`在過去3到6個月內選擇任何專案
* `lowerBound=-1500`與`upperBound=5500`選取的選項介於1500毫秒與5500毫秒之間
* `lowerBound=1d`和`upperBound=2d`選取後天的任何專案

這不考慮閏年，所有月份都是30天。

不支援篩選。

它支援Facet擷取，其方式與[`daterange`](#daterange)述詞相同。

#### 屬性 {#properties-17}

* **`upperBound`** — 以毫秒為單位的上限日期或相對於目前伺服器時間的`1s 2m 3h 4d 5w 6M 7y` （一秒、兩分鐘、三小時、四天、五週、六個月、七年），使用`-`作為負位移
* **`lowerBound`** — 以毫秒為單位的下限日期或相對於目前伺服器時間的`1s 2m 3h 4d 5w 6M 7y` （一秒、兩分鐘、三小時、四天、五週、六個月、七年），使用`-`作為負位移

### savedquery {#savedquery}

此述詞包含持續查詢產生器查詢的所有述詞，這些述詞會作為子群組述詞加入目前的查詢。

它不會執行額外的查詢，但會擴充目前的查詢。

可以使用`QueryBuilder#storeQuery()`以程式設計方式保留查詢。 格式可以是多行`String`屬性，或是包含查詢作為Java™屬性格式文字檔的`nt:file`節點。

不支援為已儲存查詢的述詞擷取Facet。

#### 屬性 {#properties-19}

* **`savedquery`** — 已儲存查詢的路徑（`String`屬性或`nt:file`節點）

### 相似 {#similar}

此述詞是使用JCR XPath的`rep:similar()`進行相似性搜尋。

不支援篩選和不支援Facet擷取。

#### 屬性 {#properties-20}

* **`similar`** — 要尋找類似節點的節點的絕對路徑
* **`local`** — 子系節點的相對路徑或目前節點的`.` （選擇性，預設為`.`）

### 標籤 {#tag}

此述詞會指定標籤標題路徑，以搜尋標籤有一或多個標籤的內容。

它支援Facet擷取，並使用其目前的標籤標題路徑為每個唯一標籤提供貯體。

#### 屬性 {#properties-21}

* **`tag`** — 要尋找的標籤標題路徑，例如`properties:orientation/landscape`
* **`N_value`** — 使用`1_value`、`2_value`、...來檢查多個標籤（預設會與`OR`結合，如果`AND`則會與`and=true`結合）
* **`property`** — 要檢視的屬性（或屬性的相對路徑） （預設`cq:tags`）

### 標籤ID {#tagid}

此述詞會指定標籤ID，以搜尋標籤有一或多個標籤的內容。

它支援Facet擷取，並使用其目前的標籤ID為每個唯一標籤提供貯體。

#### 屬性 {#properties-22}

* **`tagid`** — 要尋找的標籤識別碼，例如`properties:orientation/landscape`
* **`N_value`** — 使用`1_value`、`2_value`、...來檢查多個標籤ID （預設會與`OR`結合，如果`AND`則為`and=true`）
* **`property`** — 要檢視的屬性（或屬性的相對路徑） （預設`cq:tags`）

### tagsearch {#tagsearch}

此述詞會指定關鍵字，以搜尋標籤有一或多個標籤的內容。 它會先搜尋標題中包含這些關鍵字的標籤，然後將結果限製為僅包含具有這些關鍵字標籤的專案。

不支援多面向擷取。

#### 屬性 {#Properties-1}

* **`tagsearch`** — 要在標籤標題中搜尋的關鍵字
* **`property`** — 要考慮的屬性（或屬性的相對路徑） （預設`cq:tags`）
* **`lang`** — 僅搜尋特定當地語系化標籤標題（例如，`de`）
* **`all`** — 布林值可搜尋整個標籤全文，也就是所有標題、說明等（優先於`lang`）

### 類型 {#type}

此述詞將結果限製為特定的JCR節點型別，包括主要節點型別或`mixin`型別。 它也會尋找該節點型別的子型別。 存放庫搜尋索引必須涵蓋節點型別，才能有效執行。

它支援多面向擷取，並為結果中的每個唯一型別提供值區。

#### 屬性 {#Properties-2}

* **`type`** — 要搜尋的節點型別或`mixin`名稱，例如`cq:Page`
