---
title: 查詢生成器謂詞引用
description: 查詢生成器API的謂詞引用。
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 1%

---

# 查詢生成器謂詞引用 {#query-builder-predicate-reference}

## 一般 {#general}

### 根 {#root}

這是根謂片語。 它支援組的所有功能，並允許設定全局查詢參數。

「root」名稱從未在查詢中使用，它是隱式的。

#### 屬性 {#properties-18}

* **`p.offset`**  — 表示結果頁開始的編號，即要跳過的項數
* **`p.limit`**  — 指示頁面大小的數字
* **`p.guessTotal`**  — 建議：避免計算全部結果總和，這樣做成本高；一個數字，表示最多要計數的最大總數（例如1000，該數字為用戶提供了對粗略大小和精確數字的足夠反饋，以獲得較小結果），或 `true` 只計算最低值 `p.offset` + `p.limit`
* **`p.excerpt`**  — 如果設定為 `true`，在結果中包含全文摘要
* **`p.hits`**  — （僅用於JSON servlet）選擇將命中寫入JSON的方式，並使用這些標準命中（通過ResultHitWriter服務可擴展）:
   * **`simple`**  — 最小項目， `path`。 `title`。 `lastmodified`。 `excerpt` （如果設定）
   * **`full`**  — 對節點進行sling JSON呈現， `jcr:path` 指示命中路徑：預設情況下，僅列出節點的直接屬性，包括更深的樹 `p.nodedepth=N`,0表示整個、無限子樹；添加 `p.acls=true` 包括當前會話對給定結果項的JCR權限(映射： `create` = `add_node`。 `modify` = `set_property`。 `delete` = `remove`)
   * **`selective`**  — 僅指定的屬性 `p.properties`，即空間分隔(使用 `+` URL)相對路徑清單；如果相對路徑具有深度 `>1` 這些將表示為子對象；特別 `jcr:path` 屬性包括命中路徑

### 群組 {#group}

此謂詞允許生成嵌套條件。 組可以包含嵌套組。 查詢生成器查詢中的所有內容都隱式地位於根組中，根組可以 `p.or` 和 `p.not` 參數。

下面是將兩個屬性中的任意一個與值匹配的示例：

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

這在概念上 `(1_property` 或 `2_property)`。

以下是嵌套組的示例：

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

此搜索術語 **管理** 在頁面內 `/content/wknd/ch/de` 或在資產中 `/content/dam/wknd`。

這在概念上 `fulltext AND ( (path AND type) OR (path AND type) )`。 請注意，出於效能原因，此類OR連接需要良好的索引。

#### 屬性 {#properties-6}

* **`p.or`**  — 如果設定為 `true`，組中只能有一個謂詞匹配。 此預設值為 `false`表示必須匹配
* **`p.not`**  — 如果設定為 `true`，它會否定組(預設為 `false`)
* **`<predicate>`**  — 添加嵌套謂詞
* **`N_<predicate>`**  — 添加多個同時的嵌套謂詞，例如 `1_property, 2_property, ...`

### 排序 {#orderby}

此謂詞允許對結果進行排序。 如果需要按多個屬性排序，則需要使用數字前置詞多次添加此謂語，如 `1_orderby=first`。 `2_oderby=second`。

#### 屬性 {#properties-13}

* **`orderby`** - JCR屬性名稱，例如，由前導@表示 `@jcr:lastModified` 或 `@jcr:content/jcr:title`，或查詢中的其他謂語，例如 `2_property`，排序
* **`sort`**  — 排序方向 `desc` 用於降序或 `asc` 升序（預設）
* **`case`**  — 如果設定為 `ignore` 將使排序不區分大小寫，意思 `a` 在 `B`;如果為空或漏掉，排序區分大小寫，表示 `B` 在 `a`

## 謂語 {#predicates}

### 布爾屬性 {#boolproperty}

此謂詞與JCR布爾屬性匹配。 僅接受值 `true` 和 `false`。 在 `false`，如果屬性具有值，則匹配 `false` 或者根本不存在。 這對於檢查只有在啟用時才設定的布爾標誌非常有用。

繼承的 `operation` 參數沒有意義。

此謂語支援小平面提取，並為每個小平面提供儲存桶 `true` 或 `false` 值，但僅用於現有屬性。

#### 屬性 {#properties}

* **`boolproperty`**  — 屬性的相對路徑，例如 `myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`
* **`value`**  — 值，檢查屬性， `true` 或 `false`

### 內容片段 {#contentfragment}

此謂詞將結果限制為內容片段。

* 它不支援過濾。
* 它不支援刻面提取。

#### 屬性 {#properties-1}

* **`contentfragment`**  — 它可與任何值一起用於檢查內容片段。

### `dateComparison` {#datecomparison}

此謂語將兩個JCR日期屬性相互比較。 test是否等於、不等於、大於或大於等。

這是僅篩選謂詞，無法利用搜索索引。

#### 屬性 {#properties-2}

* **`property1`**  — 第一個日期屬性的路徑
* **`property2`**  — 第二個日期屬性的路徑
* **`operation`**
   * `=` 完全匹配（預設）
   * `!=` 不等式比較
   * `>` 為 `property1` 大於 `property2`
   * `>=` 為 `property1` 大於或等於 `property2`

### 達朗格 {#daterange}

此謂語將JCR日期屬性與日期/時間間隔匹配。 這使用ISO8601格式記錄日期和時間(`YYYY-MM-DDTHH:mm:ss.SSSZ`)並允許部分表示，例如 `YYYY-MM-DD`。 或者，時間戳可以作為POSIX時間提供。

您可以查找兩個時間戳之間的任何內容，任何比給定日期更新或更舊的內容，也可以在包含時間戳和開啟時間間隔之間進行選擇。

它支援小平面提取並提供桶 `today`。 `this week`。 `this month`。 `last 3 months`。 `this year`。 `last year`, `earlier than last year`。

它不支援過濾。

#### 屬性 {#properties-3}

* **`property`**  — 相對路徑 `DATE` 屬性，例如 `jcr:lastModified`
* **`lowerBound`**  — 綁定到的日期下限，例如 `2014-10-01`
* **`lowerOperation`** - `>` （較新）或 `>=` （在或更新） `lowerBound`。 預設值為 `>`
* **`upperBound`**  — 上界檢查屬性，例如 `2014-10-01T12:15:00`
* **`upperOperation`** - `<` （較舊）或 `<=` （在或更舊），適用於 `upperBound`。 預設值為 `<`
* **`timeZone`**  — 未將其指定為ISO-8601日期字串時要使用的時區ID。 預設值是系統的預設時區。

### 排除路徑 {#excludepaths}

此謂語從其路徑與規則運算式匹配的結果中排除節點。

這是僅篩選謂詞，無法利用搜索索引。

它不支援刻面提取。

#### 屬性 {#properties-4}

* **`excludepaths`**  — 與結果路徑匹配的規則運算式，將匹配的路徑從結果中排除。

### 全文 {#fulltext}

此謂語在全文索引中搜索術語。

它不支援過濾。

它不支援刻面提取。

#### 屬性 {#properties-5}

* **`fulltext`**  — 全文搜索詞
* **`relPath`**  — 屬性或子節點中要搜索的相對路徑。 此屬性是可選的。

### 具有權限 {#haspermission}

此謂詞將結果限制為當前會話具有指定的項 [JCR權限。](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

這是僅篩選謂詞，無法利用搜索索引。 它不支援刻面提取。

#### 屬性 {#properties-7}

* **`hasPermission`**  — 當前用戶會話必須具有針對有關節點的逗號分隔的JCR權限；例如 `jcr:write`。 `jcr:modifyAccessControl`

### 語言 {#language}

此謂語以AEM特定語言查找頁面。 這會查看頁面語言屬性和頁面路徑，這些路徑通常包括頂級站點結構中的語言或區域設定。

這是僅篩選謂詞，無法利用搜索索引。

它支援小面提取，並為每個唯一語言代碼提供儲存桶。

#### 屬性 {#properties-8}

* **`language`** - ISO語言代碼，例如 `de`

### 維護 {#mainasset}

此謂語檢查節點是否是DAM主資產而不是子資產。 這基本上是每個節點，而不是子資產節點。 請注意，這不檢查 `dam:Asset` 節點類型。 要使用此謂語，只需設定 `mainasset=true` 或 `mainasset=false`。 沒有其他屬性。

這是僅篩選謂詞，無法利用搜索索引。

它支援小面提取，並為主資產和子資產提供兩個儲存桶。

#### 屬性 {#properties-9}

* **`mainasset`**  — 布爾值 `true` 對於主資產， `false` 子資產

### 成員 {#memberof}

此謂詞查找屬於特定成員的項 [sling資源收集](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)。

這是僅篩選謂詞，無法利用搜索索引。

它不支援刻面提取。

#### 屬性 {#properties-10}

* **`memberOf`** - Sling資源收集路徑

### 諾登姆 {#nodename}

此謂語與JCR節點名稱匹配。

它支援多面抽取，並為每個唯一節點名稱（檔案名）提供儲存桶。

#### 屬性 {#properties-11}

* **`nodename`**  — 允許通配符的節點名稱模式： `*` =任何字元或無字元， `?` =任何字元， `[abc]` =只有括弧中的字元

### 諾德皮 {#notexpired}

此謂語通過檢查JCR日期屬性是否大於或等於當前伺服器時間來匹配項。 這可用於檢查 `expiresAt` 值並僅限於尚未過期的結果(`notexpired=true`)或已過期(`notexpired=false`)。

它不支援過濾。

它支援以與 [`daterange`](#daterange) 謂語。

#### 屬性 {#properties-12}

* **`notexpired`**  — 布爾值 `true` 日期或等於), `false` 過期（過去的日期）（必需）
* **`property`**  — 指向 `DATE` 要檢查的屬性（必需）

### 路徑 {#path}

此謂語在給定路徑內搜索。

它不支援刻面提取。

#### 屬性 {#properties-14}

* **`path`**  — 這定義了路徑模式。
   * 取決於 `exact` 屬性，整個子樹將匹配(如附加 `//*` 在xpath中，但請注意，這不包括基本路徑)，或僅包括完全匹配的路徑（其中可包括通配符）`*`)。
      * 預設為 `true`
   * 如果 `self`屬性被設定，將搜索包括基節點的整個子樹。
* **`exact`**  — 如果 `exact` 是 `true`，精確路徑必須匹配，但它可以包含簡單通配符(`*`)，與名字匹配，但不匹配 `/`;如果 `false` （預設）包括所有子體（可選）
* **`flat`**  — 僅搜索直接子項(例如附加 `/*` 在xpath中(僅在 `exact` 不是true，可選)
* **`self`**  — 搜索子樹，但包括作為路徑指定的基節點（無通配符）

### 屬性 {#property}

此謂語與JCR屬性及其值匹配。

它支援小平面提取，並為結果中的每個唯一屬性值提供桶。

#### 屬性 {#properties-15}

* **`property`**  — 屬性的相對路徑，例如 `jcr:title`
* **`value`**  — 值，用於檢查屬性；跟隨JCR屬性類型到字串轉換
* **`N_value`**  — 使用 `1_value`。 `2_value`,...要檢查多個值(與 `OR` 預設情況下，使用 `AND` 如果 `and=true`)
* **`and`**  — 設定為 `true` 用於組合多個值(`N_value`與 `AND`
* **`operation`**
   * `equals` 完全匹配（預設）
   * `unequals` 不等式比較
   * `like` 使用 `jcr:like` xpath函式（可選）
   * `not` 不匹配(例如 `not(@prop)` 在xpath中，值參數將被忽略)
   * `exists` 存在檢查
      * `true` 屬性必須存在
      * `false` 與 `not` 為預設值
* **`depth`**  — 屬性/相對路徑可以存在的通配符級別數(例如， `property=size depth=2` 將檢查 `node/size`。 `node/*/size` 和 `node/*/*/size`)

### 牧場 {#rangeproperty}

此謂語將JCR屬性與間隔匹配。 這適用於具有線性類型的屬性，如 `LONG`。 `DOUBLE` 和 `DECIMAL`。 對於 `DATE` 請參閱 [`daterange`](#daterange) 已優化日期格式輸入的謂詞。

可以定義下界、上界或兩者。 也可以為下界和上界分別指定操作（例如小於或等於）。

它不支援刻面提取。

#### 屬性 {#properties-16}

* **`property`**  — 屬性的相對路徑
* **`lowerBound`**  — 下界檢查屬性
* **`lowerOperation`** - `>` （預設）或 `>=`，適用於 `lowerValue`
* **`upperBound`**  — 檢查屬性的上限
* **`upperOperation`** - `<` （預設）或 `<=`，適用於 `lowerValue`
* **`decimal`** - `true` 如果checked屬性的類型為Decimal

### 相對變化 {#relativedaterange}

此謂詞匹配 `JCR DATE` 使用相對於當前伺服器時間的時間偏移對日期/時間間隔的屬性。 可以指定 `lowerBound` 和 `upperBound` 使用毫秒值或Bugzilla語法 `1s 2m 3h 4d 5w 6M 7y` （1秒、2分鐘、3小時、4天、5週、6個月、7年）。 前置詞為 `-` 指示當前時間之前的負偏移。 如果僅指定 `lowerBound` 或 `upperBound`，另一個將預設為 `0`，表示當前時間。

例如：

* `upperBound=1h` （否） `lowerBound`)在下一小時內選擇任何內容
* `lowerBound=-1d` （否） `upperBound`)選擇過去24小時內的任何內容
* `lowerBound=-6M` 和 `upperBound=-3M` 在過去3到6個月中選擇任何內容
* `lowerBound=-1500` 和 `upperBound=5500` 在將來選擇1500毫秒到5500毫秒之間的任何內容
* `lowerBound=1d` 和 `upperBound=2d` 選擇後天的任何內容

請注意，不考慮閏年，所有月份均為30天。

它不支援過濾。

它支援以與 [`daterange`](#daterange) 謂語。

#### 屬性 {#properties-17}

* **`upperBound`**  — 上限日期（以毫秒為界）或 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分鐘、三分鐘、三小時、四天、五週、六個月、六個月、七年）相對於當前伺服器時間，使用 `-` 負偏移
* **`lowerBound`**  — 下限日期（以毫秒或以毫秒為單位） `1s 2m 3h 4d 5w 6M 7y` （一秒、二分鐘、三分鐘、三小時、四天、五週、六個月、六個月、七年）相對於當前伺服器時間，使用 `-` 負偏移

### 保存查詢 {#savedquery}

此謂語將永續查詢生成器查詢的所有謂語作為子組謂詞包含到當前查詢中。

請注意，這不會執行額外查詢，而會擴展當前查詢。

可以通過寫程式方式保留查詢 `QueryBuilder#storeQuery()`。 格式可以是多行 `String` 屬性或 `nt:file` 節點，該節點將查詢作為Java屬性格式的文本檔案。

它不支援對已保存查詢的謂語進行刻面提取。

#### 屬性 {#properties-19}

* **`savedquery`**  — 已保存查詢的路徑(`String` 屬性 `nt:file` 節點)

### 相似 {#similar}

此謂語是使用JCR XPath的相似性搜索 `rep:similar()`。

它不支援過濾，也不支援刻面提取。

#### 屬性 {#properties-20}

* **`similar`**  — 要查找相似節點的節點的絕對路徑
* **`local`**  — 子代節點或 `.` 對於當前節點(可選，預設值為 `.`)

### 標籤 {#tag}

此謂語通過指定標籤標題路徑搜索用一個或多個標籤標籤的內容。

它支援方面提取，並使用每個唯一標籤的當前標籤標題路徑為它們提供儲存桶。

#### 屬性 {#properties-21}

* **`tag`**  — 標籤標題路徑，例如 `properties:orientation/landscape`
* **`N_value`**  — 使用 `1_value`。 `2_value`,...要檢查多個標籤(與 `OR` 預設情況下，使用 `AND` 如果 `and=true`)
* **`property`**  — 要查看的屬性（或屬性相對路徑）（預設） `cq:tags`)

### 標籤 {#tagid}

此謂詞通過指定標籤ID來搜索用一個或多個標籤標籤的內容。

它支援facet提取，並使用每個唯一標籤的當前標籤ID為它們提供儲存桶。

#### 屬性 {#properties-22}

* **`tagid`**  — 要查找的標籤ID，例如 `properties:orientation/landscape`
* **`N_value`**  — 使用 `1_value`。 `2_value`,...檢查多個標籤ID(與 `OR` 預設情況下，使用 `AND` 如果 `and=true`)
* **`property`**  — 要查看的屬性（或屬性相對路徑）（預設） `cq:tags`)

### 標籤 {#tagsearch}

此謂語通過指定關鍵字搜索用一個或多個標籤標籤的內容。 這將首先搜索標題中包含這些關鍵字的標籤，然後將結果限制為僅使用這些關鍵字標籤的項目。

它不支援刻面提取。

#### 屬性 {#Properties-1}

* **`tagsearch`**  — 在標籤標題中搜索的關鍵字
* **`property`**  — 要考慮的屬性（或屬性的相對路徑）（預設） `cq:tags`)
* **`lang`**  — 僅搜索某個本地化標籤標題(如 `de`)
* **`all`**  — 用於搜索整個標籤全文的布爾值，即所有標題、說明等。 (優先於 `lang`)

### 類型 {#type}

此謂語將結果限制為特定的JCR節點類型，即主節點類型或混合類型。 這還將查找該節點類型的子類型。 請注意，儲存庫搜索索引需要覆蓋節點類型，以便高效執行。

它支援小平面提取，並為結果中的每種唯一類型提供桶。

#### 屬性 {#Properties-2}

* **`type`**  — 要搜索的節點類型或混合名稱，例如 `cq:Page`
