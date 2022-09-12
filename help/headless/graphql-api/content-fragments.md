---
title: AEM GraphQL API以搭配內容片段使用
description: 了解如何透過AEM GraphQL API在Adobe Experience Manager(AEM)中as a Cloud Service使用內容片段來傳送無周邊內容。
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: f773671e3c62e2dff6f843d42a5b36211e2d1fc3
workflow-type: tm+mt
source-wordcount: '2708'
ht-degree: 1%

---


# AEM GraphQL API以搭配內容片段使用 {#graphql-api-for-use-with-content-fragments}

了解如何透過AEM GraphQL API在Adobe Experience Manager(AEM)中as a Cloud Service使用內容片段來傳送無周邊內容。

AEMas a Cloud Service的GraphQL API與內容片段搭配使用，其基礎是標準的開放原始碼GraphQL API。

在AEM中使用GraphQL API，可在無周邊CMS實作中，有效將內容片段傳送至JavaScript用戶端：

* 避免像REST一樣迭代API請求，
* 確保傳送內容僅限於特定需求，
* 允許大量傳送要呈現為單一API查詢回應所需的內容。

>[!NOTE]
>
>Adobe Experience Manager(AEM)as a Cloud Service中，GraphQL目前用於兩種（個別）的情況：
>
>* [AEM商務會透過GraphQL取用來自商務平台的資料](/help/commerce-cloud/integrating/magento.md).
>* AEM內容片段可與AEM GraphQL API（以標準GraphQL為基礎的自訂實作）搭配使用，提供結構化內容以供您的應用程式使用。


## GraphQL API {#graphql-api}

GraphQL為：

* &quot;*...API的查詢語言，以及使用您現有資料完成這些查詢的執行階段。 GraphQL提供API中資料的完整且易於理解的說明，讓用戶端能夠確切要求他們需要的內容，而無需其他任何內容，讓API隨著時間而更易於演變，並支援功能強大的開發人員工具。*」。

   請參閱 [GraphQL.org](https://graphql.org)

* &quot;*...靈活API層的開放規格。 將GraphQL放在您現有的後端，以比以往更快的速度構建產品…….*」。

   請參閱 [了解GraphQL](https://www.graphql.com).

* *&quot;。..由Facebook於2012年在內部開發的資料查詢語言和規格，2015年公開開放。 它提供了基於REST的體系結構的替代方案，其目的是提高開發人員的工作效率，並最大限度地減少資料傳輸量。 GraphQL被數百個大小的組織用於生產……」*

   請參閱 [GraphQL基礎](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

如需GraphQL API的詳細資訊，請參閱下列章節（以及其他許多資源）:

* At [graphql.org](https://graphql.org):

   * [GraphQL簡介](https://graphql.org/learn)

   * [GraphQL規格](https://spec.graphql.org/)

* At [graphql.com](https://graphql.com):

   * [指南](https://www.graphql.com/guides/)

   * [教學課程](https://www.graphql.com/tutorials/)

   * [案例分析](https://www.graphql.com/case-studies/)

適用於AEM實作的GraphQL以標準GraphQL Java程式庫為基礎。 請參閱：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub上的GraphQL Java](https://github.com/graphql-java)

### GraphQL術語 {#graphql-terminology}

GraphQL使用下列功能：

* **[查詢](https://graphql.org/learn/queries/)**

* **[結構和類型](https://graphql.org/learn/schema/)**:

   * 結構由AEM根據內容片段模型產生。
   * GraphQL會使用您的結構來呈現GraphQL for AEM實作所允許的類型和操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **[GraphQL端點](graphql-endpoint.md)**
   * AEM中的路徑，可回應GraphQL查詢，並提供對GraphQL結構的存取。

   * 請參閱 [啟用GraphQL端點](graphql-endpoint.md) 以取得詳細資訊。

請參閱 [(GraphQL.org)GraphQL簡介](https://graphql.org/learn/) 全面詳情，包括 [最佳實務](https://graphql.org/learn/best-practices/).

### GraphQL查詢類型 {#graphql-query-types}

使用GraphQL，您可以執行查詢以返回：

* A **單次登入**

* A **[條目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

您也可以執行：

* [持續查詢，已快取](/help/headless/graphql-api/persisted-queries.md)

### GraphQL查詢最佳作法(Dispatcher) {#graphql-query-best-practices}

此 [持續查詢](/help/headless/graphql-api/persisted-queries.md) 建議的方法如下：

* 快取
* 由AEMas a Cloud Service集中管理

不建議使用直接和/或POST，因為未快取查詢，因此在預設例項中，Dispatcher會設定為封鎖這類查詢。

>[!NOTE]
>
>若要允許直接和/或POSTDispatcher中的查詢，您可以要求系統管理員：
>
>* 建立Cloud Manager環境變數，稱為 `ENABLE_GRAPHQL_ENDPOINT`
>* 值 `true`


>[!NOTE]
>
>未來某個時間點可能會淘汰執行直接查詢的功能。

### GraphiQL IDE {#graphiql-ide}

您可以使用 [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md).

## 製作和發佈環境的使用案例 {#use-cases-author-publish-environments}

使用案例取決於AEMas a Cloud Service環境的類型：

* 發佈環境；用於：
   * JS應用程式的查詢資料（標準使用案例）

* 製作環境；用於：
   * 查詢資料以用於「內容管理目的」：
      * AEMas a Cloud Service中的GraphQL目前是唯讀API。
      * REST API可用於CR(u)D操作。

## 權限 {#permission}

權限是存取資產所需的權限。

## 結構產生 {#schema-generation}

GraphQL是強式類型的API，這表示資料必須依類型清楚地建構和組織。

GraphQL規範提供了一系列准則，說明如何建立強大的API，以查詢特定執行個體上的資料。 若要這麼做，用戶端必須擷取 [結構](#schema-generation)，包含查詢所需的所有類型。

對於內容片段，GraphQL結構（結構和類型）以 **已啟用** [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) 及其資料類型。

>[!CAUTION]
>
>所有GraphQL結構(衍生自已 **已啟用**)可透過GraphQL端點讀取。
>
>這意味著，您需要確保沒有敏感資料可用，因為這些資料可能會以這種方式洩露；例如，這包括可以在模型定義中顯示為欄位名稱的資訊。

例如，如果使用者建立的內容片段模型稱為 `Article`，則AEM會產生物件 `article` 屬於 `ArticleModel`. 此類型中的欄位與模型中定義的欄位和資料類型相對應。

1. 內容片段模型：

   ![與GraphQL搭配使用的內容片段模型](assets/cfm-graphqlapi-01.png "與GraphQL搭配使用的內容片段模型")

1. 對應的GraphQL架構（從GraphiQL自動文檔輸出）:
   ![基於內容片段模型的GraphQL架構](assets/cfm-graphqlapi-02.png "基於內容片段模型的GraphQL架構")

   這會顯示產生的類型 `ArticleModel` 包含數個 [欄位](#fields).

   * 其中三個由使用者控制： `author`, `main` 和 `referencearticle`.

   * 其他欄位是由AEM自動新增的，是提供特定內容片段相關資訊的實用方法；在本例中， `_path`, `_metadata`, `_variations`. 這些 [輔助欄位](#helper-fields) 標籤有 `_` 區分使用者定義的項目和自動產生的項目。

1. 使用者根據文章模型建立內容片段後，就可透過GraphQL進行詢問。 如需範例，請參閱 [範例查詢](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (根據 [與GraphQL搭配使用的範例內容片段結構](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql))。

在AEM適用的GraphQL中，架構是有彈性的。 這表示每次建立、更新或刪除內容片段模型時，都會自動產生內容片段模型。 更新內容片段模型時，也會重新整理資料架構快取。

Sites GraphQL服務會監聽（在背景）對內容片段模型所做的任何修改。 檢測到更新時，只重新生成該架構的該部分。 此最佳化可節省時間並提供穩定性。

例如，如果您：

1. 安裝包含 `Content-Fragment-Model-1` 和 `Content-Fragment-Model-2`:

   1. 適用於的GraphQL類型 `Model-1` 和 `Model-2` 即會產生。

1. 然後修改 `Content-Fragment-Model-2`:

   1. 僅 `Model-2` GraphQL類型將會更新。

   1. 而 `Model-1` 會保持不變。

>[!NOTE]
>
>請務必注意，以備您想透過REST api或其他方式，對內容片段模型執行大量更新時使用。

架構是透過與GraphQL查詢相同的端點提供，用戶端會處理使用擴充功能呼叫架構的事實 `GQLschema`. 例如，執行簡單 `GET` 要求 `/content/cq:graphql/global/endpoint.GQLschema` 會導致輸出具有Content-type的架構： `text/x-graphql-schema;charset=iso-8859-1`.

### 結構產生 — 取消發佈的模型 {#schema-generation-unpublished-models}

巢狀內嵌內容片段時，可能會發佈上層內容片段模型，但未發佈參考模型。

>[!NOTE]
>
>AEM UI可防止此情況發生，但如果以程式設計方式或使用內容套件進行發佈，便可能發生。

發生此情況時，AEM會產生 *不完整* 上層內容片段模型的結構。 這表示會從架構中移除片段參考（取決於未發佈的模型）。

## 欄位 {#fields}

在結構中，有兩個基本類別的個別欄位：

* 您產生的欄位。

   選取 [欄位類型](#field-types) 可用來根據您如何設定內容片段模型來建立欄位。 欄位名稱取自 **屬性名稱** 欄位 **資料類型**.

   * 還有 **呈現為** 屬性，因為使用者可以設定某些資料類型；例如，作為單行文字或多欄位。

* AEM適用的GraphQL也會產生 [輔助欄位](#helper-fields).

   這些用於識別內容片段，或用於取得有關內容片段的詳細資訊。

### 欄位類型 {#field-types}

GraphQL for AEM支援類型清單。 所有支援的內容片段模型資料類型和對應的GraphQL類型均表示：

| 內容片段模型 — 資料類型 | GraphQL類型 | 說明 |
|--- |--- |--- |
| 單行文字 | 字串， [字串] |  用於簡單字串，例如作者名稱、位置名稱等。 |
| 多行文本 | 字串 |  用於輸出文本，例如物品的本體 |
| 數量 |  漂浮， [浮點數] | 用於顯示浮點數和規則數 |
| 布林值 |  布林值 |  用於顯示複選框→簡單的true/false語句 |
| 日期和時間 | 日曆 |  用於以ISO 8086格式顯示日期和時間。 根據選取的類型，AEM GraphQL中有三種可用的方式： `onlyDate`, `onlyTime`, `dateTime` |
| 列舉 |  String |  用於從建立模型時定義的選項清單中顯示選項 |
|  標記 |  [String] |  用來顯示代表AEM中所用標籤之字串的清單 |
| 內容參考資料 |  字串 |  用於顯示AEM中其他資產的路徑 |
| 片段引用 |  *模型類型* |  用於參照建立模型時定義的特定模型類型的另一個內容片段 |

### 協助欄位 {#helper-fields}

除了使用者產生欄位的資料類型外，GraphQL for AEM也會產生許多 *協助者* 欄位，以協助識別內容片段，或提供有關內容片段的其他資訊。

#### 路徑 {#path}

路徑欄位是作為GraphQL中的識別碼。 它代表AEM存放庫內的內容片段資產路徑。 我們選擇此作為內容片段的識別碼，因為它：

* 在AEM中是唯一的，
* 很容易被牽引。

下列程式碼會顯示根據內容片段模型建立的所有內容片段路徑 `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

若要擷取特定類型的單一內容片段，您也必須先判斷其路徑。 例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

請參閱 [範例查詢 — 單一特定城市片段](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### 中繼資料 {#metadata}

AEM也會透過GraphQL公開內容片段的中繼資料。 中繼資料是描述內容片段的資訊，例如內容片段的標題、縮圖路徑、內容片段的說明、建立日期等。

由於中繼資料是透過結構編輯器產生，因此沒有特定結構，因此， `TypedMetaData` 已實作GraphQL類型，以公開內容片段的中繼資料。 `TypedMetaData` 顯示按以下標量類型分組的資訊：

| 欄位 |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

每個標量類型表示單個名稱值對或名稱值對陣列，其中該對的值屬於其分組的類型。

例如，如果您想要擷取內容片段的標題，我們知道此屬性是字串屬性，因此我們會查詢所有字串中繼資料：

要查詢元資料：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

如果查看生成的GraphQL架構，則可以查看所有元資料GraphQL類型。 所有模型類型都具有相同 `TypedMetaData`.

>[!NOTE]
>
>**一般和陣列中繼資料的差異**
>請記住 `StringMetadata` 和 `StringArrayMetadata` 兩者都指儲存在存放庫中的內容，而非擷取儲存庫的方式。
>
>例如，通過調用 `stringMetadata` 欄位中，您會收到儲存在存放庫中、作為 `String` ，若 `stringArrayMetadata` 您會收到儲存在存放庫中、儲存為 `String[]`.

請參閱 [中繼資料的範例查詢 — 列出題為GB的獎項中繼資料](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb).

#### 變數 {#variations}

此 `_variations` 欄位已實作，以簡化查詢內容片段所含變數的程式。 例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

請參閱 [範例查詢 — 具有已命名變數的所有城市](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

>[!NOTE]
>
>如果內容片段不存在指定的變數，則主變數會傳回為（後援）預設值。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL變數 {#graphql-variables}

GraphQL允許將變數放置在查詢中。 如需詳細資訊，請參閱 [變數的GraphQL檔案](https://graphql.org/learn/queries/#variables).

例如，若要取得類型的所有內容片段 `Article` 具有特定變數時，您可以指定變數 `variation` 在GraphiQL中。

![GraphQL變數](assets/cfm-graphqlapi-03.png "GraphQL變數")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "Introduction"
}
```

## GraphQL指令 {#graphql-directives}

在GraphQL中，可以根據變數（稱為GraphQL指令）更改查詢。

例如，您可以在 `adventurePrice` 欄位（在查詢中） `AdventureModels`，根據變數 `includePrice`.

![GraphQL指令](assets/cfm-graphqlapi-04.png "GraphQL指令")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## 篩選 {#filtering}

您也可以在GraphQL查詢中使用篩選功能來傳回特定資料。

篩選使用以邏輯運算子和運算式為基礎的語法。

例如，下列（基本）查詢會篩選名稱為 `Jobs` 或 `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

如需更多範例，請參閱：

* 的 [適用於AEM擴充功能的GraphQL](#graphql-extensions)

* [使用此範例內容和結構的範例查詢](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * 而 [範例內容與結構](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) 準備用於示例查詢

* [基於WKND項目的查詢示例](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

<!-- CQDOC-19418 -->

<!--
## Sorting {#sorting}

This feature allows you to sort the query results according to a specified field.

For example:

```graphql
query {
  articleList(sort:"author, _uuid DESC") {
    items {
      author
      _path
    }
  }
}
```

## Paging {#paging}

This feature allows you to perform paging on query types that returns a list. Two methods are provided:

* `offset` and `limit` in a `List` query
* `first` and `after` in a `Paginated` query

### List query - offset and limit {#list-offset-limit}

In a `...List`query you can use `offset` and `limit` to return a specific subset of results:

* `offset`: Specifies the first data set to return
* `limit`: Specifies the maximum number of data sets to be returned

For example, to output the page of results containing up to five articles, starting from the fifth article from the *complete* results list:

```graphql
query {
   articleList(offset: 5, limit:5) {
    items {
      author
      _path
    }
  }
}
```

>[!NOTE]
>
>* Paging is impacted by the order to the jcr query result set. By default it uses `jcr:path` to make sure the order is always the same. If a different sort order is used, and if that sorting cannot be done at jcr query level, then there will be a negative performance impact as the paging cannot be done in memory.
>
>* The higher the offset, the more time it will take to skip the items from the complete jcr query result set. An alternative solution for large result sets is to use the Paginated query with `first` and `after` method.

### Paginated query - first and after {#paginated-first-after}

The `...Paginated` query type reuses most of the `...List` query type features (filtering, sorting), but instead of using `offset`/`limit` arguments, it uses the standard `first`/`after` arguments defined by [GraphQL](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`: The `n` first items to return. The default is `50`.
* `after`: The cursor-id as returned in the complete result set - if `cursor` is selected.

For example, output the page of results containing up to five adventures, starting from the given cursor item in the *complete* results list:

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            adventureTitle
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

>[!NOTE]
>
>* Paging defaults use `_uuid` for ordering to ensure the order of results is always the same. When `sort` is used, `_uuid` is added as a last order-by field.
>
>* Performance is expected to be degraded if sort/filter parameters cannot be executed at jcr query level, as the query first has to gather the results in memory then sort them, then finally apply paging. Therefore it is recommended to use filter/sort fields stored at root level.
-->

## GraphQL for AEM — 擴充功能摘要 {#graphql-extensions}

使用AEM適用的GraphQL進行查詢的基本操作符合標準GraphQL規範。 若是使用AEM的GraphQL查詢，有幾個擴充功能：

<!-- CQDOC-19418 -->

<!--
* If you expect a list of results:
  * add `List` to the model name; for example,  `cityList`
  * See [Sample Query - All Information about All Cities](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)
  
  You can then:
  
  * [Sort the results](#sorting)

  * Return a page of results using either:

    * [A List query with offset and limit](#list-offset-limit)
    * [A Paginated query with first and after](#paginated-first-after)
  * See [Sample Query - All Information about All Cities](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)
-->

* 如果您需要單一結果：
   * 使用模型名稱；eg city

* 如果您希望得到結果清單：
   * 新增 `List` 至模型名稱；例如，  `cityList`
   * 請參閱 [範例查詢 — 所有城市的所有資訊](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

* 如果要使用邏輯OR:
   * use ` _logOp: OR`
   * 請參閱 [Sample Query — 名為「Jobs」或「Smith」的所有人員](/help/headless/graphql-api/sample-queries.md#sample-all-persons-jobs-smith)

* 邏輯AND也存在，但（通常）是隱含的

* 您可以查詢與內容片段模型內欄位對應的欄位名稱
   * 請參閱 [示例查詢 — 公司CEO和員工的完整詳細資訊](/help/headless/graphql-api/sample-queries.md#sample-full-details-company-ceos-employees)

* 除了模型中的欄位之外，還有一些系統生成的欄位（前面有下划線）:

   * 內容：

      * `_locale` :揭示語言；基於語言管理器
         * 請參閱 [指定地區的多個內容片段的查詢範例](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` :顯示片段的中繼資料
         * 請參閱 [中繼資料的範例查詢 — 列出題為GB的獎項中繼資料](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)
      * `_model` :允許查詢內容片段模型（路徑和標題）
         * 請參閱 [從模型中查詢內容片段模型的範例](/help/headless/graphql-api/sample-queries.md#sample-wknd-content-fragment-model-from-model)
      * `_path` :存放庫內內容片段的路徑
         * 請參閱 [範例查詢 — 單一特定城市片段](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)
      * `_reference` :顯示參照；在RTF編輯器中包含內嵌參考
         * 請參閱 [具有預先擷取的參考之多個內容片段的查詢範例](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` :顯示內容片段中的特定變體

         >[!NOTE]
         >
         >如果內容片段不存在指定的變數，則主變數會傳回為（後援）預設值。

         * 請參閱 [範例查詢 — 具有已命名變數的所有城市](#sample-cities-named-variation)
   * 操作：

      * `_operator` :應用特定運算子； `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * 請參閱 [示例查詢 — 沒有「Jobs」名稱的所有人員](/help/headless/graphql-api/sample-queries.md#sample-all-persons-not-jobs)
         * 請參閱 [範例查詢 — 所有冒險，其中 `_path` 開頭為特定首碼](/help/headless/graphql-api/sample-queries.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` :具體條件；例如，  `AT_LEAST_ONCE`
         * 請參閱 [範例查詢 — 對項目必須至少發生一次的陣列進行篩選](/help/headless/graphql-api/sample-queries.md#sample-array-item-occur-at-least-once)
      * `_ignoreCase` :在查詢時忽略大小寫
         * 請參閱 [示例查詢 — 名稱中包含SAN的所有城市（不考慮大小寫）](/help/headless/graphql-api/sample-queries.md#sample-all-cities-san-ignore-case)









* 支援GraphQL聯合類型：

   * use `... on`
      * 請參閱 [具有內容參考之特定模型的內容片段查詢範例](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-content-reference)

* 查詢巢狀片段時回退：

   * 如果巢狀片段中不存在指定的變數，則 **主版** 會傳回變數。

## 從外部網站查詢GraphQL端點 {#query-graphql-endpoint-from-external-website}

若要從外部網站存取GraphQL端點，您需要設定：

* [CORS篩選器](/help/headless/deployment/cross-origin-resource-sharing.md)
* [反向連結篩選](/help/headless/deployment/referrer-filter.md)

## 驗證 {#authentication}

請參閱 [內容片段的遠端AEM GraphQL查詢驗證](/help/headless/security/authentication.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## 常見問題集 {#faqs}

出現的問題：

1. **Q**:&quot;*適用於AEM的GraphQL API與Query Builder API有何不同？*&quot;

   * **A**:&quot;*AEM GraphQL API提供對JSON輸出的完整控制，且是查詢內容的業界標準。
日後，AEM計畫投資AEM GraphQL API。*&quot;

## 教學課程 — 開始使用AEM無周邊和GraphQL {#tutorial}

尋找實作教學課程？ 結帳 [開始使用AEM無周邊和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) 端對端教學課程，說明如何在無周邊CMS情境下，使用AEM GraphQL API建置和公開內容，並供外部應用程式使用。
