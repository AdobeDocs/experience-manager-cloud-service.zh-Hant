---
title: Query Builder Predicate Reference
description: 查詢產生器API的謂詞參考。
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Query Builder Predicate Reference {#query-builder-predicate-reference}

## 一般 {#general}

### root {#root}

這是根謂片語。 它支援組的所有功能，並允許設定全局查詢參數。

「root」名稱從未用於查詢，它是隱式的。

#### 屬性 {#properties-18}

* **`p.offset`** -表示結果頁面開始的編號，即要跳過的項目數
* **`p.limit`** -表示頁面大小的數字
* **`p.guessTotal`** -建議：避免計算全部結果總和，代價高昂；指出總計上限的數字（例如1000，此數字可讓使用者獲得對粗細大小的足夠意見，並精確地輸入數字，以取得較小的結果），或 `true` 只計算最小的必要 `p.offset` +  `p.limit`
* **`p.excerpt`** -如果設定為 `true`，則在結果中包含全文摘錄
* **`p.hits`** -（僅適用於JSON servlet）選取點擊以JSON格式寫入的方式，並使用這些標準點擊（可透過ResultHitWriter服務擴充）:
   * **`simple`** -最小項 `path`目，如 `title`、 `lastmodified`、 `excerpt` （如果已設定）
   * **`full`** -結點的sling JSON轉譯，並 `jcr:path` 指出點擊路徑：預設情況下，只列出節點的直接屬性，包含一個更深的樹，其中 `p.nodedepth=N`0表示整個無窮子樹；添加 `p.acls=true` 以包括當前會話對給定結果項的JCR權限(映射： `create` =  `add_node`,  `modify` =  `set_property`,  `delete` =  `remove`)
   * **`selective`** -僅在中指定 `p.properties`的屬性，即相對路徑的空 `+` 間分隔（在URL中使用）清單；如果相對路徑有深度， `>1` 這些將表示為子對象；特殊 `jcr:path` 屬性包含點擊的路徑

### 群組 {#group}

此謂語允許建立巢狀條件。 群組可以包含巢狀群組。 查詢建立工具查詢中的所有項目都會隱式顯示在根群組中，而根群組中也可以有`p.or`和`p.not`參數。

以下是將兩個屬性中的任一屬性與值配對的範例：

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

這在概念上是`(1_property`或`2_property)`。

以下是巢狀群組的範例：

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

這會在`/content/wknd/ch/de`的頁面或`/content/dam/wknd`的資產中搜尋&#x200B;**Management**&#x200B;一詞。

這在概念上是`fulltext AND ( (path AND type) OR (path AND type) )`。 請注意，由於效能原因，此類OR連接需要良好的索引。

#### 屬性 {#properties-6}

* **`p.or`** -如果設定為 `true`，則組中只有一個謂詞必須匹配。此預設為`false`，表示所有項目都必須符合
* **`p.not`** -如果設為 `true`，則會否定群組(預設為 `false`)
* **`<predicate>`** -添加嵌套謂語
* **`N_<predicate>`** -新增同時的多個巢狀謂語，如  `1_property, 2_property, ...`

### orderby {#orderby}

此謂語允許對結果進行排序。 如果需要按多個屬性排序，則需要使用數字前置詞多次添加此謂語，如`1_orderby=first`、`2_oderby=second`。

#### 屬性 {#properties-13}

* **`orderby`** - JCR屬性名稱由前導@(例如 `@jcr:lastModified` 或 `@jcr:content/jcr:title`)指示，或查詢中的其他謂語(例如，要對其排序 `2_property`)
* **`sort`** -排序方向， `desc` 遞減或 `asc` 遞增（預設）
* **`case`** -如果設定為 `ignore` ，則使排序不區分大 `a` 小寫 `B`;如果空或缺，則排序會區分大小寫，這表示排序 `B` 會先於  `a`

## 謂語{#predicates}

### boolproperty {#boolproperty}

此謂語與JCR布林屬性相符。 僅接受值`true`和`false`。 對於`false`，如果屬性的值為`false`，或完全不存在，則它將匹配。 這對於檢查僅在啟用時設定的布爾標誌非常有用。

繼承的`operation`參數沒有意義。

此謂語支援Facet擷取，並為每個`true`或`false`值提供儲存貯體，但僅提供現有屬性。

#### 屬性 {#properties}

* **`boolproperty`** -屬性的相對路徑，例如 `myFeatureEnabled` 或  `jcr:content/myFeatureEnabled`
* **`value`** -值，用於檢查屬 `true` 性  `false`

### contentfragment {#contentfragment}

此謂語將結果限制為內容片段。

* 它不支援篩選。
* 它不支援Facet擷取。

#### 屬性 {#properties-1}

* **`contentfragment`** -可搭配任何值來檢查內容片段。

### `dateComparison` {#datecomparison}

此謂語將兩個JCR日期屬性相互比較。 可以測試它們是等於、不等於、大於或等於。

這是僅限篩選的謂語，無法運用搜尋索引。

#### 屬性 {#properties-2}

* **`property1`** -第一個日期屬性的路徑
* **`property2`** -第二個日期屬性的路徑
* **`operation`**
   * `=` 完全相符（預設）
   * `!=` 不等式比較
   * `>` 對於 `property1` 大於  `property2`
   * `>=` 對於 `property1` 大於或等於  `property2`

### daterange {#daterange}

此謂語與日期／時間間隔的JCR日期屬性相符。 這使用ISO8601
格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，並允許部分表示，例如`YYYY-MM-DD`。 或者，可以將時間戳提供為POSIX時間。

您可以尋找兩個時間戳記之間的任何項目（任何比指定日期更新或更舊的項目），也可以選擇包含和開啟的間隔。

它支援Facet擷取，並提供儲存區`today`、`this week`、`this month`、`last 3 months`、`this year`、`last year`和`earlier than last year`。

它不支援篩選。

#### 屬性 {#properties-3}

* **`property`** -屬性的相 `DATE` 對路徑，例如  `jcr:lastModified`
* **`lowerBound`** - lower date bound to check property for，例如  `2014-10-01`
* **`lowerOperation`** -  `>` （較新） `>=` 或（at或更新），則套用至 `lowerBound`。預設值為`>`
* **`upperBound`** -上限，例如檢查屬性  `2014-10-01T12:15:00`
* **`upperOperation`** -  `<` （舊版） `<=` 或（舊版）適用於 `upperBound`。預設值為`<`
* **`timeZone`** -未指定為ISO-8601日期字串時使用的時區ID。預設為系統的預設時區。

### 排除路徑{#excludepaths}

此謂語從其路徑與規則運算式匹配的結果中排除節點。

這是僅限篩選的謂語，無法運用搜尋索引。

它不支援Facet擷取。

#### 屬性 {#properties-4}

* **`excludepaths`** -規則運算式與結果路徑相符，從結果中排除相符的路徑。

### 全文{#fulltext}

此謂語在全文索引中搜尋詞語。

它不支援篩選。

它不支援Facet擷取。

#### 屬性 {#properties-5}

* **`fulltext`** -全文搜尋詞
* **`relPath`** -屬性或子節點中要搜索的相對路徑。此屬性為可選屬性。

### hasPermission {#haspermission}

此謂語將結果限制為當前會話具有指定[JCR權限的項目。](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

這是僅限篩選的謂語，無法運用搜尋索引。 它不支援Facet擷取。

#### 屬性 {#properties-7}

* **`hasPermission`** -當前用戶會話必須對有問題的節點具有逗號分隔的JCR權限；例如 `jcr:write`,  `jcr:modifyAccessControl`

### 語言 {#language}

此謂語會尋找AEM特定語言的頁面。 這會查看頁面語言屬性和頁面路徑，這些路徑通常包含頂層網站結構中的語言或地區設定。

這是僅限篩選的謂語，無法運用搜尋索引。

它支援Facet擷取，並為每個獨特語言程式碼提供區段。

#### 屬性 {#properties-8}

* **`language`** -例如ISO語言代碼  `de`

### mainasset {#mainasset}

此謂語會檢查節點是否為DAM主資產而非子資產。 這基本上是子資產節點內部的每個節點。 請注意，這不會檢查`dam:Asset`節點類型。 若要使用此謂語，請簡單設定`mainasset=true`或`mainasset=false`。 沒有其他屬性。

這是僅限篩選的謂語，無法運用搜尋索引。

它支援Facet擷取，並為主資產和子資產提供兩個儲存貯體。

#### 屬性 {#properties-9}

* **`mainasset`** -布爾型， `true` 用於主資產， `false` 用於子資產

### {#memberof}的成員

此謂語會尋找屬於特定[sling resource collection](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/resource/collection/ResourceCollection.html)成員的項目。

這是僅限篩選的謂語，無法運用搜尋索引。

它不支援Facet擷取。

#### 屬性 {#properties-10}

* **`memberOf`** - Sling資源集合的路徑

### nodename {#nodename}

此謂語與JCR節點名稱匹配。

它支援Facet擷取，並為每個唯一節點名稱（檔案名稱）提供儲存貯體。

#### 屬性 {#properties-11}

* **`nodename`** -允許通配符的節點名模式： `*` = any or no char,  `?` = any char,  `[abc]` = only chares

### notexpired {#notexpired}

此謂語會檢查JCR日期屬性是否大於或等於目前伺服器時間，以比對項目。 這可用於檢查`expiresAt`值，並僅將結果限制為尚未過期(`notexpired=true`)或已過期(`notexpired=false`)的值。

它不支援篩選。

它支援與[`daterange`](#daterange)謂語相同的Facet擷取。

#### 屬性 {#properties-12}

* **`notexpired`** -布林值， `true` 對於尚未到期（日期未來或等於）, `false` 對於到期（過去日期）（必要）
* **`property`** -要檢查的屬 `DATE` 性的相對路徑（必需）

### 路徑 {#path}

此謂語在給定路徑內搜索。

它不支援Facet擷取。

#### 屬性 {#properties-14}

* **`path`** -這定義了路徑模式。
   * 根據`exact`屬性，整個子樹將匹配（例如在xpath中附加`//*`，但請注意，這不包括基本路徑），或僅匹配精確的路徑，其中可以包含通配符(`*`)。
      * 預設為 `true`
   * 如果設定了`self`屬性，將搜索包含基節點的整個子樹。
* **`exact`** -如 `exact` 果 `true`匹配，則精確路徑必須匹配，但可以包含簡單通配符(`*`)、匹配名稱但不匹配的通配符 `/`;如果是 `false` （預設），則會包含所有子系（選用）
* **`flat`** -僅搜索直接子項(如附加 `/*` 到xpath)(僅在不 `exact` 是true時使用，可選)
* **`self`** -搜索子樹，但包含作為路徑指定的基節點（無通配符）

### 屬性 {#property}

此謂語與JCR屬性及其值相符。

它支援Facet擷取，並為結果中的每個唯一屬性值提供儲存區。

#### 屬性 {#properties-15}

* **`property`** -屬性的相對路徑，例如  `jcr:title`
* **`value`** -值，用於檢查屬性；跟隨JCR屬性類型到字串轉換
* **`N_value`** -使用 `1_value`、 `2_value`、...若要檢查多個值(依預 `OR` 設結合， `AND` if `and=true`)
* **`and`** -設為 `true` 結合多個值(`N_value`)  `AND`
* **`operation`**
   * `equals` 完全相符（預設）
   * `unequals` 不等式比較
   * `like` 用於使 `jcr:like` 用xpath函式（可選）
   * `not` 對於無匹配項(例如， `not(@prop)` 在xpath中，值參數將被忽略)
   * `exists` 存在檢查
      * `true` 屬性必須存在
      * `false` 與相同， `not` 且為預設值
* **`depth`** -屬性／相對路徑可存在的通配符級別數(例如， `property=size depth=2` 將檢查 `node/size`和 `node/*/size`  `node/*/*/size`)

### rangeproperty {#rangeproperty}

此謂語與JCR屬性與間隔匹配。 這適用於具有線性類型的屬性，例如`LONG`、`DOUBLE`和`DECIMAL`。 如需`DATE`，請參閱[`daterange`](#daterange)謂語，其中已最佳化日期格式輸入。

您可以定義下界、上界或兩者。 也可以分別為下界限和上界限指定操作（例如小於或等於）。

它不支援Facet擷取。

#### 屬性 {#properties-16}

* **`property`** -屬性的相對路徑
* **`lowerBound`** -下界限檢查屬性
* **`lowerOperation`** -  `>` （預設值） `>=`或，套用至  `lowerValue`
* **`upperBound`** -上界，檢查屬性
* **`upperOperation`** -  `<` （預設值） `<=`或，套用至  `lowerValue`
* **`decimal`** -如 `true` 果選中的屬性類型為Decimal

### 相對變更範圍{#relativedaterange}

此謂語使用相對於目前伺服器時間的時間偏移，將`JCR DATE`屬性與日期／時間間隔相符。 您可以使用毫秒值或Bugzilla語法`1s 2m 3h 4d 5w 6M 7y`（一秒、二分鐘、三小時、四天、五週、六個月、七年）來指定`lowerBound`和`upperBound`。 前置詞`-`，表示目前時間前有負偏移。 如果您只指定`lowerBound`或`upperBound`，則另一個預設為`0`，代表目前時間。

例如：

* `upperBound=1h` (且無 `lowerBound`)在下一小時內選取任何項目
* `lowerBound=-1d` (且無 `upperBound`)在過去24小時內選取任何項目
* `lowerBound=-6M` 在 `upperBound=-3M` 過去3到6個月裡選擇任何
* `lowerBound=-1500` 並選 `upperBound=5500` 擇1500毫秒到5500毫秒之間的任意選項
* `lowerBound=1d` 然後 `upperBound=2d` 在後天選擇任何東西

請注意，這並不需要花上多年時間，而且所有月份都是30天。

它不支援篩選。

它支援與[`daterange`](#daterange)謂語相同的Facet擷取。

#### 屬性 {#properties-17}

* **`upperBound`** -相對於目前伺服器時間的上限日 `1s 2m 3h 4d 5w 6M 7y` 期界限（一秒、二分鐘、三小時、四天、五週、六個月、七年），用於負 `-` 偏移
* **`lowerBound`** -相對於當前伺服器時間 `1s 2m 3h 4d 5w 6M 7y` （1秒、2分鐘、3小時、4天、5週、6個月、7年）的較低日期界限，用於負 `-` 偏移

### savedquery {#savedquery}

此謂語將持續存在的Query Builder查詢的所有謂語作為子組謂語包含到當前查詢中。

請注意，這不會執行額外查詢，但會延伸目前的查詢。

查詢可使用`QueryBuilder#storeQuery()`以程式設計方式保存。 格式可以是多行`String`屬性或`nt:file`節點，該節點將查詢作為Java屬性格式的文本檔案包含。

它不支援儲存查詢的謂語的Facet擷取。

#### 屬性 {#properties-19}

* **`savedquery`** -保存查詢的路徑(屬`String` 性或節 `nt:file` 點)

### 類似{#similar}

此謂語是使用JCR XPath的`rep:similar()`進行的相似性搜索。

它不支援篩選，也不支援Facet擷取。

#### 屬性 {#properties-20}

* **`similar`** -查找相似節點的節點的絕對路徑
* **`local`** -子代節點或當前節 `.` 點的相對路徑(可選，預設為 `.`)

### 標籤{#tag}

此謂語通過指定標籤標題路徑搜索用一個或多個標籤標籤的內容。

它支援Facet擷取，並使用每個唯一標籤的目前標籤標題路徑，提供區段。

#### 屬性 {#properties-21}

* **`tag`** -標籤標題路徑，例如  `properties:orientation/landscape`
* **`N_value`** -使用 `1_value`、 `2_value`、...若要檢查多個標籤(依預 `OR` 設結合， `AND` if `and=true`)
* **`property`** -屬性（或屬性的相對路徑），以查看(預設 `cq:tags`)

### tagid {#tagid}

此謂語會透過指定標籤ID來搜尋以一或多個標籤標籤的內容。

它支援Facet擷取，並使用每個唯一標籤的目前標籤ID來提供區段。

#### 屬性 {#properties-22}

* **`tagid`** -標籤ID，例如  `properties:orientation/landscape`
* **`N_value`** -使用 `1_value`、 `2_value`、...若要檢查多個標籤ID(依預 `OR` 設與， `AND` if `and=true`)
* **`property`** -屬性（或屬性的相對路徑），以查看(預設 `cq:tags`)

### tagsearch {#tagsearch}

此謂語透過指定關鍵字，搜尋以一或多個標籤標籤標籤的內容。 這會先搜尋標題中包含這些關鍵字的標籤，然後將結果限制為僅包含這些標籤的項目。

它不支援Facet擷取。

#### 屬性 {#Properties-1}

* **`tagsearch`** -在標籤標題中搜尋的關鍵字
* **`property`** -要考慮的屬性（或屬性的相對路徑）(預設 `cq:tags`)
* **`lang`** -僅在特定本地化標籤標題中搜尋(例如 `de`)
* **`all`** -用於搜索整個標籤全文的布爾值，即所有標題、說明等。（優先於`lang`）

### 類型 {#type}

此謂語將結果限制為特定的JCR節點類型，包括主節點類型或混合類型。 這也會找出該節點類型的子類型。 請注意，儲存庫搜索索引需要涵蓋節點類型，以便高效執行。

它支援Facet擷取，並為結果中的每個獨特類型提供區段。

#### 屬性 {#Properties-2}

* **`type`** -節點類型或混合名稱，以進行搜尋，例如  `cq:Page`
