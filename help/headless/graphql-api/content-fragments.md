---
title: 與內容片段搭配使用的 AEM GraphQL API
description: 了解如何將 Adobe Experience Manager (AEM) as a Cloud Service 中的內容片段與 AEM GraphQL API 搭配使用，以實現 Headless 內容傳遞。
feature: Headless, Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
role: Admin, Developer
source-git-commit: 32344eb9668aefd5efe44a073bc4c66c2496f003
workflow-type: tm+mt
source-wordcount: '5984'
ht-degree: 91%

---


# 與內容片段搭配使用的 AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

了解如何將 Adobe Experience Manager (AEM) as a Cloud Service 中的內容片段與 AEM GraphQL API 搭配使用，以實現 Headless 內容傳遞。

與內容片段搭配使用的 AEM as a Cloud Service GraphQL API，在很大程度上是以標準、開放原始碼的 GraphQL API 為基礎。

在 AEM 中使用 GraphQL API 可以在 Headless CMS 實作中高效率地將內容片段傳遞給 JavaScript 用戶端：

* 避免與 REST 一樣的反覆 API 要求，
* 確保傳遞限於特定要求，
* 允許大量傳遞需要轉譯的內容做為對單一 API 查詢的回應。

>[!NOTE]
>
>GraphQL 目前在 Adobe Experience Manager (AEM) as a Cloud Service 中用於兩個 (獨立) 情況：
>
>* [AEM Commerce 透過 GraphQL 取用來自 Commerce 平台的資料](/help/commerce-cloud/integrating/magento.md)。
>* AEM 內容片段與 AEM GraphQL API (基於標準 GraphQL 的自訂實作) 搭配運作，以傳遞結構化內容以供您的應用程式使用。

>[!NOTE]
>
>請參閱[結構化內容傳遞與管理的AEM API](/help/headless/apis-headless-and-content-fragments.md)，以取得各種可用API的概觀，以及所涉及概念的比較。

>[!NOTE]
>
>如需 Experience Manager API 的最新資訊，另請造訪「[Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)」。

## GraphQL API {#graphql-api}

GraphQL 是：

* 「*...API 的查詢語言和使用現有資料完成這些查詢的執行階段。GraphQL 可完整清楚地描述 API 中的資料，使用戶端能夠準確地要求所需內容，別無其他，如此可輕鬆地隨著時間發展 API，造就強大的開發人員工具。*」。

  請參閱 [GraphQL.org](https://graphql.org)

* 「*...靈活 API 層的開放規格。將 GraphQL 置於現有後端之上，可比以往更快速地建置產品....*」。

  請參閱[探索 GraphQL](https://www.graphql.com)。

* *「...一種資料查詢語言和規格，由 Facebook 於 2012 年在內部開發，然後於 2015 年公開原始碼。它是REST架構的替代方案，目的是提高開發人員生產力並儘量減少傳輸資料量。 GraphQL 用於生產環境，數百個各種規模的組織都在使用...」*

  請參閱 [GraphQL 基礎](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world the tools they need to understand and adopt GraphQL.*". 
-->

如需 GraphQL API 的資訊，請參閱以下章節 (以及許多其他資源)：

* 位於 [graphql.org](https://graphql.org)：

   * [GraphQL 簡介](https://graphql.org/learn)

   * [GraphQL 規格](https://spec.graphql.org/)

* 位於 [graphql.com](https://graphql.com)：

   * [指南](https://www.graphql.com/guides/)

   * [教學課程](https://www.graphql.com/tutorials/)

   * [案例研究](https://www.graphql.com/case-studies/)

GraphQL for AEM 實作是以標準 GraphQL Java 庫為基礎。請參閱：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub 上的 GraphQL Java](https://github.com/graphql-java)

### GraphQL 術語 {#graphql-terminology}

GraphQL 使用以下項目：

* **[查詢](https://graphql.org/learn/queries/)**

* **[結構描述和類型](https://graphql.org/learn/schema/)**：

   * 結構描述是由 AEM 根據內容片段模型所產生。
   * 使用您的結構描述，GraphQL 呈現 GraphQL for AEM 實作可用的類型和操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **[GraphQL 端點](graphql-endpoint.md)**
   * AEM 中回應 GraphQL 查詢並提供 GraphQL 結構描述存取權的路徑。

   * 如需詳細資訊，請參閱[啟用 GraphQL 端點](graphql-endpoint.md)。

請參閱 [(GraphQL.org) GraphQL 簡介](https://graphql.org/learn/) 了解完整的詳細資訊，包括[最佳做法](https://graphql.org/learn/best-practices/)。

### GraphQL 查詢類型 {#graphql-query-types}

使用 GraphQL，您可以執行查詢以傳回以下兩者之一：

* **單一項目**

* **[項目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM提供將查詢（兩種型別）轉換為[持續查詢的功能，可由Dispatcher和CDN快取](/help/headless/graphql-api/persisted-queries.md)。

### GraphQL 查詢最佳做法 (Dispatcher 和 CDN) {#graphql-query-best-practices}

[持續性查詢](/help/headless/graphql-api/persisted-queries.md)是建議用於發佈執行個體的方法，如下：

* 它們被快取
* 它們由 AEM as a Cloud Service 集中管理

>[!NOTE]
>
>通常編寫執行個體沒有 Dispatcher/CDN，因此在那裡使用持續性查詢沒有任何好處；除了測試它們。

不建議使用 POST 要求的 GraphQL 查詢，因為它們不會被快取，因此在預設執行個體上，Dispatcher 設定為阻擋此類查詢。

雖然 GraphQL 也支援 GET 要求，但這些要求可能會達到限制 (例如，URL 的長度)，而使用持續性查詢可以避免此狀況。

如需更多的詳細資訊，請參閱[啟用持續性查詢的快取](/help/headless/deployment/dispatcher-caching.md)。

>[!NOTE]
>
>若要在 Dispatcher 中允許直接和/或 POST 查詢，您可以要求您的系統管理員：
>
>* 建立稱為 `ENABLE_GRAPHQL_ENDPOINT` 的 [Cloud Manager 環境變數](/help/implementing/cloud-manager/environment-variables.md)
>* 值為 `true`

>[!NOTE]
>
>執行直接查詢的功能可能會在未來的某個時間被淘汰。

### GraphiQL IDE {#graphiql-ide}

您可以使用 [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) 測試和偵錯 GraphQL 查詢。

## 作者、預覽和發佈的使用案例 {#use-cases-author-preview-publish}

使用案例取決於 AEM as a Cloud Service 環境的類型：

* 發佈環境：用於：
   * 為 JS 應用程式查詢資料 (標準使用案例)

* 預覽環境；用於：
   * 部署在發佈環境中之前預覽查詢
      * 為 JS 應用程式查詢資料 (標準使用案例)

* 編寫環境：用於：
   * 為「內容管理目的」查詢資料：
      * AEM as a Cloud Service 中的 GraphQL 目前是唯讀 API。
      * REST API 可用於 CR(u)D 操作。

## 權限 {#permission}

權限是存取資產所需的權限。

GraphQL 查詢是在基礎要求之 AEM 使用者的許可下執行的。如果使用者沒有某些片段 (儲存為資產) 的讀取權限，它們將不會包含在結果集中。

此外，使用者必須可以存取 GraphQL 端點才能執行 GraphQL 查詢。

## 結構描述產生 {#schema-generation}

GraphQL 是強式類型 API，這表示資料必須結構明確並按類型組織。

GraphQL 規格提供了一系列指南，說明如何建立健全的 API 來查詢特定執行個體上的資料。為此，用戶端必須擷取[結構描述](#schema-generation)，其中包含查詢所需的所有類型。

對於內容片段，GraphQL 結構描述 (結構和類型) 是以&#x200B;**啟用的**[內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)及其資料類型為基礎。

>[!CAUTION]
>
>所有 GraphQL 結構描述 (衍生自已&#x200B;**啟用**&#x200B;的內容片段模型) 都可透過 GraphQL 端點讀取。
>
>這表示您必須確保沒有敏感資料，因為它可能會以這種方式洩露；例如，這包括可以在模型定義中做為欄位名稱出現的資訊。

例如，如果使用者建立了一個名為 `Article` 的內容片段模型，則 AEM 會產成一個 GraphQL 類型 `ArticleModel`。此類型中的欄位對應於模型中定義的欄位和資料類型。此外，它還為操作此類型的查詢建立一些登入點，例如 `articleByPath` 或 `articleList`。

1. 內容片段模型：

   ![與 GraphQL 搭配使用的內容片段模型](assets/cfm-graphqlapi-01.png "與 GraphQL 搭配使用的內容片段模型")

1. 對應的 GraphQL 結構描述 (來自 GraphiQL 自動文件的輸出)：
   ![根據內容片段模型的 GraphQL 結構描述](assets/cfm-graphqlapi-02.png "根據內容片段模型的 GraphQL 結構描述")

   此顯示產生的類型 `ArticleModel` 包含多個[欄位](#fields)。

   * 其中三個已由使用者控制：`author`、`main` 和 `referencearticle`。

   * 其他欄位由 AEM 自動新增，並代表可提供特定內容片段資訊的有用方法；在此範例中，([Helper 欄位](#helper-fields)) `_path`、`_metadata`、`_variations`。

1. 使用者根據文章模型建立內容片段後，就可以透過 GraphQL 對其進行查詢。例如，請參閱[範例查詢](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (根據[與 GraphQL 搭配使用的範例內容片段結構](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql))。

在 GraphQL for AEM 中，結構描述是靈活的。這表示著每次建立、更新或刪除內容片段模型時都會自動產生它。當您更新內容片段模型時，資料結構描述快取也會重新整理。

<!-- move the following to a separate "in depth" page -->

當您更新內容片段模型時，資料結構描述快取也會重新整理。

Sites GraphQL 服務偵聽 (在背景) 對內容片段模型所做的任何修改。當偵測到更新時，只有該部分的結構描述會重新產生。這種最佳化作業可以節省時間並提供穩定性。

例如，您可以：

1. 安裝包含 `Content-Fragment-Model-1` 和 `Content-Fragment-Model-2` 的套件：

   1. 會產生 `Model-1` 和 `Model-2` 的 GraphQL 類型。

1. 然後修改 `Content-Fragment-Model-2`：

   1. 只有 `Model-2` GraphQL 類型會更新。

   1. 而 `Model-1` 將保持不變。

>[!NOTE]
>
>如果您想透過 REST API 或其他方式對內容片段模型進行大量更新，請務必注意這一點。

結構描述透過與 GraphQL 查詢相同的端點提供服務，用戶端處理以 `GQLschema` 副檔名呼叫結構描述這一事實。例如，對 `/content/cq:graphql/global/endpoint.GQLschema` 執行簡單的 `GET` 要求，將導致內容類型為 `text/x-graphql-schema;charset=iso-8859-1` 的結構描述輸出。

<!-- move through to here to a separate "in depth" page -->

### 結構描述產生 - 未發佈的模型 {#schema-generation-unpublished-models}

巢狀內嵌內容片段時，可能會發佈父內容片段模型，但不會發佈被參考的模型。

>[!NOTE]
>
>AEM UI 可防止這種情況發生，但如果以程式設計方式或使用內容套件進行發佈，則可能會發生這種情況。

發生這種情況時，AEM 會為父內容片段模型產生&#x200B;*不完整*&#x200B;結構描述。這表示相依於未發佈模型的片段參考已從結構描述中刪除。

## 欄位 {#fields}

在結構描述中有個別欄位，分成兩個基本類別：

* 產生的欄位。

  一系列[資料類型](#Data-types)用於根據內容片段模型的設定方式建立欄位。欄位名稱取自&#x200B;**資料類型**&#x200B;索引標籤的&#x200B;**屬性名稱**&#x200B;欄位。

   * 也必須考慮&#x200B;**轉譯為**&#x200B;設定，因為使用者可以設定某些資料類型。例如，從下拉選單中選擇 `multifield`，可以將單行文字欄位設定為包含多個單行文字。

* GraphQL for AEM 也會產生幾個 [Helper 欄位](#helper-fields)。

### 資料類型 {#data-types}

GraphQL for AEM 支援類型清單。表示所有支援的內容片段模型資料類型和對應的 GraphQL 類型：

| 內容片段模型 - 資料類型 | GraphQL 類型 | 說明 |
|--- |--- |--- |
| 單行文字 | `String`、`[String]` | 用於簡單的字串，例如作者姓名、位置名稱等。 |
| 多行文字 | `String`、`[String]` | 用於輸出文字，例如文章正文 |
| 數字 | `Float`、`[Float]` | 用於顯示浮點數和正規數 |
| 布林值 | `Boolean` | 用於顯示核取方塊 → 簡單的 true/false 陳述式 |
| 日期和時間 | `Calendar` | 用於以 ISO 8601 格式顯示日期和時間。視所選類型而定，AEM GraphQL 中可使用三種風格：`onlyDate`、`onlyTime`、`dateTime` |
| 列舉 | `String` | 用於顯示模型建立時定義之選項清單中的選項 |
| 標記 | `[String]` | 用於顯示字串清單，字串代表 AEM 中使用的標記 |
| 內容參考 | `String`、`[String]` | 用於顯示 AEM 中另一個資產的路徑 |
| 內容參考 (UUID) | `String`、`[String]` | 用來顯示路徑，以AEM中另一個資產的UUID表示 |
| 片段參考 |  *模型類型* <br><br>單一欄位：`Model` - 模型類型，直接參考<br><br>多個欄位，具單一參考類型：`[Model]` - `Model` 類型陣列，從陣列直接參考<br><br>多個欄位，具多個參考類型：`[AllFragmentModels]` - 所有模型類型陣列，從聯合類型的陣列參考 | 用於參考特定模型類型的一個或多個內容片段，在建立模型時定義 |
| 片段參考 (UUID) |  *模型類型* <br><br>單一欄位：`Model` - 模型類型，直接參考<br><br>多個欄位，具單一參考類型：`[Model]` - `Model` 類型陣列，從陣列直接參考<br><br>多個欄位，具多個參考類型：`[AllFragmentModels]` - 所有模型類型陣列，從聯合類型的陣列參考 | 用於參考特定模型類型的一個或多個內容片段，在建立模型時定義 |

{style="table-layout:auto"}

### Helper 欄位 {#helper-fields}

除了使用者產生之欄位的資料類型外，GraphQL for AEM 也會產生幾個 *Helper* 欄位，以協助識別內容片段，或提供有關內容片段的其他資訊。

這些 [Helper 欄位](#helper-fields)前面加上 `_` 以區分是使用者定義的還是自動產生的。

#### 路徑 {#path}

路徑欄位作為 AEM GraphQL 中的標識符。它代表 AEM 存放庫中內容片段資產的路徑。我們選擇它作為內容片段的標識符，因為它：

* 在 AEM 中是唯一的，
* 容易撷取。

以下程式碼將顯示根據內容片段模型 `Author` (WKND 教學課程提供) 建立之所有內容片段的路徑。

```graphql
{
  authorList {
    items {
      _path
    }
  }
}
```

若要撷取特定類型的單一內容片段，您還需要先確定其路徑。例如：

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
      _path
      firstName
      lastName
    }
  }
}
```

請參閱[範例查詢 - 單一特定城市片段](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)。

#### ID (UUID) {#id-uuid}

此ID欄位也會用作AEM GraphQL中的識別碼。 它代表AEM存放庫中內容片段資產的路徑，但不會儲存實際路徑，而是儲存代表資源的UUID。 我們選擇它作為內容片段的標識符，因為它：

* 在 AEM 中是唯一的，
* 可以輕鬆擷取，
* 不會變更資源移動的時間。

內容片段和參照內容片段或資產的UUID，可透過JSON屬性`_id`傳回。

```graphql
{
  articleList {
    items {
        _id
        _path
    }
  }
}
```

#### 中繼資料 {#metadata}

透過 GraphQL，AEM 還公開內容片段的中繼資料。中繼資料是描述內容片段的資訊，例如內容片段的標題、縮圖路徑、內容片段的描述、建立日期等。

由於中繼資料是透過結構描述編輯器產生的，因此沒有特定的結構，所以實作 `TypedMetaData` GraphQL 類型來公開內容片段的中繼資料。`TypedMetaData` 公開依以下純量類型群組的資訊：

| 欄位 |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

每個純量類型代表單一名稱-值配對或名稱-值配對組，配對中的值屬於該群組的類型。

例如，如果你想擷取內容片段的標題，我們知道這個屬性是字串屬性，所以我們會查詢所有的字串中繼資料：

若要查詢中繼資料：

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
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

如果檢視產生的 GraphQL 結構描述，則可以檢視所有中繼資料 GraphQL 類型。所有模型類型都具有相同的 `TypedMetaData`。

>[!NOTE]
>
>**一般和陣列中繼資料的區別**
>>請記住，`StringMetadata` 和 `StringArrayMetadata` 都是指儲存在存放庫的中繼資料，而不是擷取它們的方式。
>
>例如，呼叫 `stringMetadata` 欄位，您將收到以 `String` 儲存在存放庫之所有中繼資料的陣列，如果呼叫 `stringArrayMetadata`，則會收到以 `String[]` 儲存在存放庫之所有中繼資料的陣列。

請參閱[中繼資料的範例查詢 - 列出 GB 獎項的中繼資料](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)。

#### 變化 {#variations}

`_variations` 欄位已實作以簡化查詢內容片段具有的變化。例如：

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>`_variations` 欄位不包含 `master` 變化，在技術上，原始資料 (在 UI 中參考為&#x200B;*主版*) 不視為明確變化。

請參閱「[範例查詢 - 所有具有名稱變化的城市](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)」。

>[!NOTE]
>
>如果內容片段不存在特定的變化，則原始資料 (也稱為主版變化) 會作為 (備援) 預設值傳回。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 變數 {#graphql-variables}

GraphQL 允許在查詢中放置變數。如需詳細資訊，請參閱 [GraphQL 變數文件](https://graphql.org/learn/queries/#variables)。

例如，若要取得特定變化 (若有) 中類型為 `Author` 的所有內容片段，您可以在 GraphiQL 中指定引數 `variation`。

![GraphQL 變數](assets/cfm-graphqlapi-03.png "GraphQL 變數")

**查詢**：

```graphql
query($variation: String!) {
  authorList(variation: $variation) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

**查詢變數**：

```json
{
  "variation": "another"
}
```

此查詢將傳回完整的作者清單。沒有 `another` 變化的作者將回復到原始資料 (在此情況下，`_variation` 將回報 `master`)。

如果您想將清單限制為提供特定變化的作者 (並略過會回復到原始資料的作者)，請套用[篩選器](#filtering)：

```graphql
query($variation: String!) {
  authorList(variation: $variation, filter: {
    _variation: {
      _expressions: {
        value: $variation
      }
    }
  }) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

## GraphQL 指示詞 {#graphql-directives}

在 GraphQL 中，可以根據變數變更查詢，稱為 GraphQL 指示詞。

例如，您可以根據變數 `includePrice`，在對所有 `AdventureModels` 的查詢中加入 `adventurePrice` 欄位。

![GraphQL 指示詞](assets/cfm-graphqlapi-04.png "GraphQL 指示詞")

**查詢**：

```graphql
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      title
      price @include(if: $includePrice)
    }
  }
}
```

**查詢變數**：

```json
{
    "includePrice": true
}
```

## 篩選 {#filtering}

您還可以在 GraphQL 查詢中使用篩選來傳回特定資料。

篩選使用以邏輯運算子和運算式的語法。

最不可部分完成的部分是可套用到特定欄位內容的單一運算式。它將欄位內容與特定的常數值進行比較。

例如，運算式：

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

會將欄位內容與值 `some text` 進行比較，如果內容等於該值則成功。否則，運算式將失敗。

以下運算子可用於將欄位與特定值相比較：

| 運算子 | 類型 | 運算式成功，如果... |
|--- |--- |--- |
| `EQUALS` | `String`, `ID`, `Boolean` | ...值與欄位內容完全相同 |
| `EQUALS_NOT` | `String`, `ID` | ...值與欄位內容&#x200B;*不*&#x200B;相同 |
| `CONTAINS` | `String` | ...欄位內容包含值 (`{ value: "mas", _op: CONTAINS }` 將符合 `Christmas`、`Xmas`、`master`...) |
| `CONTAINS_NOT` | `String` | ...欄位內容 *不*&#x200B;包含值 |
| `STARTS_WITH` | `ID` | ... ID 以特定值開頭 (`{ value: "/content/dam/", _op: STARTS_WITH` 將符合 `/content/dam/path/to/fragment`，但不符合 `/namespace/content/dam/something` |
| `EQUAL` | `Int`, `Float` | ...值與欄位內容完全相同 |
| `UNEQUAL` | `Int`, `Float` | ...值與欄位內容&#x200B;*不*&#x200B;相同 |
| `GREATER` | `Int`, `Float` | ...欄位內容大於值 |
| `GREATER_EQUAL` | `Int`, `Float` | ...欄位內容大於或等於值 |
| `LOWER` | `Int`, `Float` | ...欄位內容小於值 |
| `LOWER_EQUAL` | `Int`, `Float` | ...欄位內容小於或等於值 |
| `AT` | `Calendar`, `Date`, `Time` | ...欄位內容與值完全相同 (包含時區設定) |
| `NOT_AT` | `Calendar`, `Date`, `Time` | ...欄位內容與值&#x200B;*不*&#x200B;相同 |
| `BEFORE` | `Calendar`, `Date`, `Time` | ...值表示的時間點在欄位內容表示的時間點之前 |
| `AT_OR_BEFORE` | `Calendar`, `Date`, `Time` | ... 值表示的時間點在欄位內容表示的時間點之前或相同 |
| `AFTER` | `Calendar`, `Date`, `Time` | ...值表示的時間點在欄位內容表示的時間點之後 |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ...值表示的時間點在欄位內容表示的時間點之後或相同 |

某些類型也可讓您指定其他選項來修改評估運算式的方式：

| 選項 | 類型 | 說明 |
|--- |--- |--- |
| `_ignoreCase` | `String` | 忽略字串的大小寫，例如 `time` 值與 `TIME`、`time`、`tImE` 相符... |
| `_sensitiveness` | `Float` | 允許 `float` 值的某些差數視為相同 (以解決由於 `float` 值的內部表示造成的技術限制；應避免，因為此選項可能對效能有負面影響 |

運算式可以使用邏輯運算子 (`_logOp`) 合併成一個集合：

* `OR`- 如果至少有一個運算式成功，則運算式集成功
* `AND` - 如果所有運算式成功，則運算式集成功 (預設)

每個欄位都可以由自己的運算式集進行篩選。篩選器引數中提到的所有欄位的運算式集最終將由自己的邏輯運算子合併。

篩選器定義 (作為 `filter` 引數傳遞給查詢) 包含：

* 每個欄位的子定義 (欄位可以透過其名稱存取，例如，資料 (欄位) 類型中的 `lastName` 欄位其篩選器中有一個 `lastName` 欄位)
* 每個子定義包含 `_expressions` 陣列，其提供運算式集，以及 `_logOp` 欄位，其定義應用來將運算式合併的邏輯運算子
* 每個運算式由值 (`value` 欄位) 和運算子 (`_operator` 欄位) 定義，應比較欄位內容與

如果您要將項目與 `AND` 合併，則可以省略 `_logOp`；如果要檢查是否相等，則可以省略 `_operator`，因為這些是預設值。

以下範例示範一個完整的查詢，該查詢會篩選所有 `lastName`為 `Provo` 或包含 `sjö` 的人，不受大小寫影響：

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

雖然您也可以對巢狀欄位進行篩選，但不建議這樣做，因為這可能會導致效能問題。

如需進一步範例，請參閱：

* [GraphQL for AEM 擴充功能](#graphql-extensions) 的詳細資訊

* [使用此範例內容和結構的範例查詢](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * 以及準備用於範例查詢的[範例內容和結構](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) 

* [以 WKND 專案為基礎的範例查詢](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## 排序 {#sorting}

>[!NOTE]
>
>為獲得最佳效能，請考慮[更新內容片段以便在 GraphQL 篩選中進行分頁和排序](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md)。

此功能可讓您根據指定的欄位將查詢結果進行排序。

排序標準：

* 以逗號分隔的值清單，這些值代表欄位路徑
   * 清單中的第一個欄位將定義主要排序順序，如果主要排序標準的兩個值相等，將使用第二個欄位，如果前兩個標準相等，則使用第三個欄位
   * 點符號，即 field1.subfield.subfield 等...
* 具有順序方向 (選擇性)
   * ASC (遞增) 或 DESC (遞減)；預設是套用 ASC
   * 可以為每個欄位指定方向，這表示您可以對一個欄位遞增排序，對另一個欄位遞減排序 (姓名，名字 DESC)

例如：

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

同時：

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

您也可以使用 `nestedFragmentname.fieldname`格式，對巢狀片段內的欄位進行排序。

>[!NOTE]
>
>這可能會對效能產生負面影響。

例如：

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## 分頁 {#paging}

>[!NOTE]
>
>為獲得最佳效能，請考慮[更新內容片段以便在 GraphQL 篩選中進行分頁和排序](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md)。

此功能可讓您針對傳回清單的查詢類型執行分頁。提供兩種方法：

* 在 `List` 查詢中，`offset` 和 `limit`
* 在 `Paginated` 查詢中，`first` 和 `after`

### 清單查詢 - offset 和 limit {#list-offset-limit}

在 `...List` 查詢中，您可以使用 `offset` 和 `limit` 傳回特定的結果子集：

* `offset`：指定第一個要傳回的資料集
* `limit`：指定傳回的資料集數量上限

例如，要輸出最多包含五篇文章的結果頁面，從&#x200B;*完整*&#x200B;結果清單中的第五篇文章開始：

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* 分頁需要穩定的排序順序，才能在多個查詢要求同一結果集的不同頁面時，跨多個查詢正常運作。依預設，它使用結果集中每個項目的存放庫路徑來確保順序始終相同。如果使用不同的排序順序，且如果無法在 JCR 查詢層級進行排序，則會對效能產生負面影響，因為在確定頁面之前必須先將整個結果集載入到記憶體中。
>
>* 偏移量越高，從完整的 JCR 查詢結果集中略過項目所需的時間就越多。針對大型結果集的替代解決方案是使用已分頁查詢搭配 `first` 和 `after` 方法。

### 已分頁查詢 - first 和 after {#paginated-first-after}

`...Paginated` 查詢類型重複使用大部分的 `...List` 查詢類型功能 (篩選、排序)，但沒有使用 `offset`/`limit` 引數，而是使用 `first`/`after`，如 [GraphQL 游標連接規格](https://relay.dev/graphql/connections.htm)所定義。您可以在 [GraphQL 簡介](https://graphql.org/learn/pagination/#pagination-and-edges)中找到不太正式的簡介。

* `first`：要傳回的前 `n` 個項目。
預設為 `50`。
最大值為 `100`。
* `after`：決定所要求頁面開始的游標；請注意，游標所代表的項目不包含在結果集中；項目的游標由 `edges` 結構的 `cursor` 欄位決定。

例如，要輸出最多包含五篇文章的結果頁面，從&#x200B;*完整*&#x200B;結果清單中的特定游標項目開始：

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* 依預設，分頁使用代表片段的存放庫節點 UUID 進行排序，以確保結果的順序始終相同。使用 `sort` 時，會以隱含的方式使用 UUID 以確保唯一排序；即使是排序鍵相同的兩個項目也一樣。
>
>* 由於內部技術限制，如果對巢狀欄位套用排序和篩選，效能會降低。因此，建議使用儲存在根層級的篩選/排序欄位。如果要查詢大型已分頁結果集，同樣也建議使用此方法。

## GraphQL 查詢中的 Web 最佳化影像傳遞 {#web-optimized-image-delivery-in-graphql-queries}

Web 最佳化影像傳遞可讓您使用 Graphql 查詢進行下列作業：

* 要求 DAM 資產影像的 URL (由 **內容參考**&#x200B;進行參考)

* 透過查詢傳遞參數，以便自動產生並傳回特定的影像轉譯

  >[!NOTE]
  >
  >指定的轉譯未存儲在 AEM Assets 中。轉譯會在快取中產生並保留一小段時間。

* 將 URL 作為 JSON 傳遞的一部分傳回

您可以使用 AEM 進行以下作業：

* 將[Web 最佳化影像傳遞](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html?lang=zh-Hant)傳遞至 GraphQL 查詢。

這表示在查詢執行期間會套用命令，其方式與這些影像的 GET 要求中的 URL 參數相同。

這可讓您為 JSON 傳遞動態地建立影像轉譯，即不必手動建立這些轉譯並將其儲存在存放庫中。

GraphQL 中的解決方案代表您可以：

* 要求 URL：在 `_dynamicUrl` 參考上使用 `ImageRef`

* 傳遞參數：新增 `_assetTransform` 到您定義篩選器的清單標頭中

>[!NOTE]
>
>**內容參考** 可用於 DAM 資產和 Dynamic Media 資產。擷取適當的 URL 使用不同的參數：
>* `_dynamicUrl`：DAM 資產
>* `_dmS7Url`：Dynamic Media 資產
> 
>如果參考的資產是 DAM 資產，則 `_dmS7Url` 的值將為 `null`。請參閱「[透過 GraphQL 查詢以 URL 進行動態媒體資產傳遞](#dynamic-media-asset-delivery-by-url)」。

### 轉換要求結構 {#structure-transformation-request}

`AssetTransform`(`_assetTransform`) 用於發出 URL 轉換要求。

結構和語法是：

* `format`：分項清單，包含所有支援格式 (依據其副檔名：GIF、PNG、PNG8、JPG、PJPG、BJPG、WEBP、WEBPLL 或 WEBPLY)
* `seoName`：字串，做為檔案名稱而不是節點名稱
* `crop`：框架子結構，如果省略寬度或高度，則高度或寬度會使用相同值
   * `xOrigin`：框架的 x 原點，必須存在
   * `yOrigin`：框架的 y 原點，必須存在
   * `width`：框架的寬度
   * `height`：框架的高度
* `size`：維度子結構，如果省略寬度或高度，則高度或寬度會使用相同值
   * `width`：維度的寬度
   * `height`：維度的高度
* `rotation`：分項清單，包含所有支援的旋轉：R90、R180、R270
* `flip`：分項清單，包含 HORIZONTAL、VERTICAL、HORIZONTAL_AND_VERTICAL
* `quality`：1–100 的整數，表示影像品質的百分比
* `width`：整數，在定義輸出影像寬度，但會被影像產生器忽略

URL 轉換適用於所有查詢類型：按路徑、清單或分頁。

### 具有完整參數的 Web 最佳化影像傳遞 {#web-optimized-image-delivery-full-parameters}

以下是具有一組完整參數的範例查詢：

```graphql
{
  articleList(
    _assetTransform: {
      format:GIF
      seoName:"test"
      crop:{
        xOrigin:10
        yOrigin:20
        width:50
        height:45
      }
      size:{
        height:100
        width:200
      }
      rotation:R90
      flip:HORIZONTAL_AND_VERTICAL
      quality:55
      width:123
    }
  ) {
    items {
      _path
      featuredImage {
        ... on ImageRef {
          _dynamicUrl
        }
      }
    }
  }
}
```

### 具有單一查詢變數的 Web 最佳化影像傳遞 {#web-optimized-image-delivery-single-query-variable}

以下範例顯示如何使用單一查詢變數：

```graphql
query ($seoName: String!) {
  articleList(
    _assetTransform: {
      format:GIF
      seoName:$seoName
      crop:{
        xOrigin:10
        yOrigin:20
        width:50
        height:45
      }
      size:{
        height:100
        width:200
      }
      rotation:R90
      flip:HORIZONTAL_AND_VERTICAL
      quality:55
      width:123
    }
  ) {
    items {
      _path
      featuredImage {
        ... on ImageRef {
          _dynamicUrl
        }
      }
    }
  }
}
```

### 具有多個查詢變數的 Web 最佳化影像傳遞 {#web-optimized-image-delivery-multiple-query-variables}

以下範例顯示如何使用多個查詢變數：

```graphql
query ($seoName: String!, $format: AssetTransformFormat!) {
  articleList(
    _assetTransform: {
      format:$format
      seoName:$seoName
      crop:{
        xOrigin:10
        yOrigin:20
        width:50
        height:45
      }
      size:{
        height:100
        width:200
      }
      rotation:R90
      flip:HORIZONTAL_AND_VERTICAL
      quality:55
      width:123
    }
  ) {
    items {
      _path
      featuredImage {
        ... on ImageRef {
          _dynamicUrl
        }
      }
    }
  }
}
```

### 透過 URL 要求 Web 最佳化影像傳遞 {#web-optimized-image-delivery-request-url}

如果您將查詢儲存為持續性查詢 (例如，使用名稱`dynamic-url-x`)，那麼您可以[直接執行持續性查詢](/help/headless/graphql-api/persisted-queries.md#execute-persisted-query)。

例如，若要直接執行先前的範例 (儲存為持續性查詢)，請使用以下 URL：

* [單一參數](#dynamic-image-delivery-single-specified-parameter)；名稱為 `dynamic-url-x` 的持續性查詢

   * `http://localhost:4502/graphql/execute.json/wknd-shared/dynamic-url-x;seoName=xxx`

     回應如下所示：

     ![使用參數的影像傳遞](assets/cfm-graphiql-sample-image-delivery.png "使用參數的影像傳遞")

* [多個參數](#dynamic-image-delivery-multiple-specified-parameters)；名稱為 `dynamic` 的持續性查詢

   * `http://localhost:4502/graphql/execute.json/wknd-shared/dynamic;seoName=billiboy;format=GIF;`

     >[!CAUTION]
     >
     >若要乾淨地終止參數清單，結尾必須加上 `;`。

### Web 最佳化影像傳遞的限制 {#web-optimized-image-delivery-limitations}

存在以下限制：

* 套用到查詢所有影像部分的修飾詞 (全域參數)

* 快取標頭

   * 編寫時不可快取
   * 發佈時可快取 - 最長 10 分鐘 (用戶端無法變更)

## 透過 GraphQL 查詢以 URL 進行動態媒體資產傳遞{#dynamic-media-asset-delivery-by-url}

GraphQL for AEM Content Fragments 可讓您要求 AEM Dynamic Media (Scene7) 資產的 URL (由&#x200B;**內容參考**&#x200B;所參考)。

GraphQL 中的解決方案代表您可以：

* 在 `ImageRef` 參考中使用 `_dmS7Url`
   * 檢視依URL的Dynamic Media資產傳遞的[範例查詢 — 影像參考](#sample-query-dynamic-media-asset-delivery-by-url-imageref)
* 在多個參考上使用`_dmS7Url`；`ImageRef`、`MultimediaRef`和`DocumentRef`
   * 檢視依URL的Dynamic Media資產傳遞的[範例查詢 — 多個參考](#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs)

* 搭配智慧型裁切功能使用`_dmS7Url`

   * `_smartCrops`屬性會公開特定資產可用的智慧型裁切設定

   * 請參閱依URL的Dynamic Media資產傳遞[範例查詢 — 使用智慧型裁切](#sample-query-dynamic-media-asset-delivery-by-url-smart-crop)

>[!NOTE]
>
>若要這樣做，您需要有 [Dynamic Media 雲端設定](/help/assets/dynamic-media/config-dm.md)。
>
>這會在建立資產時，將 `dam:scene7File` 和 `dam:scene7Domain` 屬性新增到資產的中繼資料中。

>[!NOTE]
>
>**內容參考**&#x200B;可用於 DAM 資產和 Dynamic Media 資產。擷取適當的 URL 使用不同的參數：
>
>* `_dmS7Url`：Dynamic Media 資產
>* `_dynamicUrl`：DAM 資產
> 
>如果參考的資產是 Dynamic Media 資產，則 `_dynamicURL` 的值將為 `null`。請參閱「[GraphQL 查詢中的 Web 最佳化影像傳遞](#web-optimized-image-delivery-in-graphql-queries)」。

### Dynamic Media 資產透過 URL 進行傳遞的範例查詢 - 影像參考{#sample-query-dynamic-media-asset-delivery-by-url-imageref}

以下是範例查詢：
* 對於類型為 `team` 和 `person` 的多個內容片段，傳回 `ImageRef`

```graphql
query allTeams {
  teamList {
    items {
      _path
      title
      teamMembers {
        fullName
        profilePicture {
          __typename
          ... on ImageRef{
            _dmS7Url
            height
            width
          }
        }
      }
    }
  }
} 
```

### Dynamic Media 資產透過 URL 進行傳遞的範例查詢 - 多個參考{#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs}

以下是範例查詢：
* 對於類型為 `team` 和 `person` 的多個內容片段，傳回 `ImageRef`、`MultimediaRef` 和 `DocumentRef`：

```graphql
query allTeams {
  teamList {
    items {
      _path
      title
      teamMembers {
        fullName
        profilePicture {
          __typename
          ... on ImageRef{
            _dmS7Url
            height
            width
          }
        }
       featureVideo {
          __typename
          ... on MultimediaRef{
            _dmS7Url
            size
          }
        }
      about-me {
          __typename
          ... on DocumentRef{
            _dmS7Url
            _path
          }
        }
      }
    }
  }
}
```

### 依URL的Dynamic Media資產傳遞的範例查詢 — 使用智慧型裁切 {#sample-query-dynamic-media-asset-delivery-by-url-smart-crop}

以下是範例查詢：

* 以公開可用於請求資產的智慧型裁切設定

```graphql
query allTeams {
  teamList {
    items {
      title
      teamMembers {
        profilePicture {
          ... on ImageRef {
            height
            width
            _dmS7Url
            _smartCrops {
              width
              height
              name
            }
          }
        }
      }
    }
  }
} 
```

## 適用於OpenAPI資產支援的Dynamic Media (遠端Assets) {#dynamic-media-for-openapi-asset-support}

[遠端資產](/help/sites-cloud/administering/content-fragments/authoring.md#reference-remote-assets)整合可讓您從內容片段編輯器參考非目前AEM執行個體本機的Assets。 它是由Dynamic Media在內容片段編輯器和GraphQL JSON中實作，以提供OpenAPI資產支援。

### 適用於OpenAPI資產支援的Dynamic Media範例查詢(遠端Assets) {#sample-query-dynamic-media-for-openapi-asset-support}

以下是範例要求：

* 以說明參照遠端資產的概念

  ```graphql
  {
    testModelList {
      items {
        remoteasset {
          ... on RemoteRef {
              repositoryId
                  assetId
          }
        }
        multiplecontent {
          ... on ImageRef {
            _path
            _authorUrl
            _publishUrl
          }
          ... on RemoteRef {
              repositoryId
              assetId
          }
        }
      }
      _references {
        ... on ImageRef {
            _path
            _authorUrl
            _publishUrl
          }
          ... on RemoteRef {
              repositoryId
              assetId
          }
      }
    }
  }
  ```

* 回應

  ```graphql
  {
    "data": {
      "testModelList": {
        "items": [
          {
            "remoteasset": {
              "repositoryId": "delivery-p123456-e123456.adobeaemcloud.com",
              "assetId": "urn:aaid:aem:1fb05fe4-c12b-4f85-b1ca-aa92cdbd6a62"
            },
            "multiplecontent": [
              {
                "repositoryId": "delivery-p123456-e123456.adobeaemcloud.com",
                "assetId": "urn:aaid:aem:1fb05fe4-c12b-4f85-b1ca-aa92cdbd6a62"
              },
              {
                "_path": "/content/dam/test-folder/test.jpg",
                "_authorUrl": "http://localhost:4502/content/dam/test-folder/test.jpg",
                "_publishUrl": "http://localhost:4503/content/dam/test-folder/test.jpg"
              }
            ]
          }
        ],
        "_references": [
          {
            "repositoryId": "delivery-p123456-e123456.adobeaemcloud.com",
            "assetId": "urn:aaid:aem:1fb05fe4-c12b-4f85-b1ca-aa92cdbd6a62"
          },
          {
            "_path": "/content/dam/test-folder/test.jpg",
            "_authorUrl": "http://localhost:4502/content/dam/test-folder/test.jpg",
            "_publishUrl": "http://localhost:4503/content/dam/test-folder/test.jpg"
          }
        ]
      }
    }
  }  
  ```

**限制**

目前的限製為：

* GraphQL傳遞僅支援`repositoryId`和`assetId` （不會傳回其他資產中繼資料）

  >[!NOTE]
  >
  >接著需要在使用者端根據[資產傳送API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat)建構完整的URL。

* 只有&#x200B;*個已核准的*&#x200B;個資產可供遠端存放庫參考
* 如果從遠端存放庫移除所參考的資產，這將導致內容片段資產參考損毀。
* 使用者有權存取的所有傳遞資產存放庫都將可供選擇，可用的清單無法限制。
* AEM執行個體和遠端資產存放庫執行個體都必須是相同版本。
* 沒有透過[管理網站API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)和使用OpenAPI的[AEM內容片段傳送](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/)公開的資產中繼資料。 您必須使用資產中繼資料API來擷取資產中繼資料詳細資訊。

## GraphQL for AEM - 擴充功能摘要 {#graphql-extensions}

使用 GraphQL for AEM 進行查詢的基本操作符合標準 GraphQL 規格。使用 GraphQL for AEM 進行查詢，有一些擴充功能：

* 如果您需要單一結果：
   * 使用模型名稱，例如城市

* 如果您期望結果清單：
   * 新增 `List` 到模型名稱，例如 `cityList`
   * 請參閱[範例查詢 - 所有城市的所有資訊](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

  然後，您可以：

   * [排序結果](#sorting)

      * `ASC`：遞增
      * `DESC`：遞減

   * 使用以下任一方法傳回一頁結果：

      * [清單查詢，使用 offset 和 limit](#list-offset-limit)
      * [已分頁查詢，使用 first 和 after](#paginated-first-after)

   * 請參閱[範例查詢 - 所有城市的所有資訊](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

* 篩選器 `includeVariations` 會包含在 `List` 和 `Paginated` 的查詢類型中。若要在查詢結果中擷取內容片段變化，則 `includeVariations` 篩選器必須設定為 `true`。

   * 請參閱[特定模式的多個內容片段與其變化的範例查詢](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragment-variations-given-model)

  >[!CAUTION]
  >篩選器 `includeVariations` 和系統產生的欄位 `_variation` 無法同時用於同一個查詢定義中。

* 如果要使用邏輯 OR：
   * 使用 ` _logOp: OR`
   * 請參閱[範例查詢 - 姓名為「Jobs」或「Smith」的所有人員](/help/headless/graphql-api/sample-queries.md#sample-all-persons-jobs-smith)

* 邏輯 AND 也存在，但 (通常) 是隱含的

* 您可以查詢與內容片段模型內欄位相對應的欄位名稱
   * 請參閱[範例查詢 - 公司 CEO 和員工的完整詳細資料](/help/headless/graphql-api/sample-queries.md#sample-full-details-company-ceos-employees)

* 除了模型內的欄位外，還有一些系統產生的欄位 (前面有底線)：

   * 對於內容：

      * `_locale`：顯示語言，根據語言管理員
         * 請參閱[範例查詢：特定地區設定的多個內容片段](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-given-locale)

      * `_metadata`：顯示片段的中繼資料
         * 請參閱[中繼資料的範例查詢 - 列出 GB 獎項的中繼資料](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)

      * `_model`：允許查詢內容片段模型 (路徑和標題)
         * 請參閱[從模型進行的內容片段模型範例查詢](/help/headless/graphql-api/sample-queries.md#sample-wknd-content-fragment-model-from-model)

      * `_path`：存放庫中內容片段的路徑
         * 請參閱[範例查詢 - 單一特定城市片段](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)

      * `_id` ：存放庫中內容片段的UUID

         * 檢視具有UUID參考之特定模型的內容片段的[範例查詢](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-uuid-references)
         * [請參閱依UUID參考的內容片段範例查詢](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-uuid-reference)

      * `_reference`：顯示參考；包含 RTF 編輯器中的內聯參考
         * 請參閱[預先擷取參考之多個內容片段的範例查詢](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-prefetched-references)

      * `_variation`：顯示內容片段中的特定變化

        >[!NOTE]
        >
        >如果內容片段不存在特定的變化，則主變化會作為 (備援) 預設值傳回。

        >[!CAUTION]
        >
        >系統產生的欄位 `_variation` 不能和篩選器 `includeVariations` 同時使用。

         * 請參閱[範例查詢 - 所有具有名稱變化的城市](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)

   * 對於影像傳遞：

      * `_authorURL`：AEM Author 上影像資產的完整 URL
      * `_publishURL`：AEM Publish 上影像資產的完整 URL

      * 對於 [Web 最佳化影像傳遞](#web-optimized-image-delivery-in-graphql-queries) (DAM 資產)：

         * `_dynamicUrl`：`ImageRef` 參考上經過 Web 最佳化的 DAM 資產的完整 URL

           >[!NOTE]
           >
           >`_dynamicUrl` 是用於 Web 最佳化 DAM 資產的理想 URL，並應在可行時取代 `_path`、`_authorUrl` 和 `_publishUrl` 的使用。

         * `_assetTransform`：在您定義篩選器的清單標頭上傳遞參數

         * 請參閱：

            * [具有完整參數的 Web 最佳化影像傳遞的範例查詢](#web-optimized-image-delivery-full-parameters)

            * [具有單一特定參數進行 Web 最佳化影像傳遞的範例查詢](#web-optimized-image-delivery-single-query-variable)

      * `_dmS7Url`：將 URL 傳遞到 [Dynamic Media](#dynamic-media-asset-delivery-by-url) 資產的 `ImageRef` 參考

         * 請參閱「[透過 URL 進行 Dynamic Media 資產傳遞的範例查詢 - ImageRef](#sample-query-dynamic-media-asset-delivery-by-url-imageref)」

         * 請參閱「[透過 URL 進行 Dynamic Media 資產傳遞的範例查詢 - 多個參考](#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs)」

   * `_tags`：顯示包含標記的內容片段或變化的 ID；這是一個 `cq:tags` 識別碼的陣列。

      * 請參閱[範例查詢 - 所有標記為 City Breaks 的城市名稱](/help/headless/graphql-api/sample-queries.md#sample-names-all-cities-tagged-city-breaks)
      * 請參閱[對附加了特定標記的特定模式之內容片段變化的範例查詢](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-variations-given-model-specific-tag)
      * 請參閱[依 _tags ID 進行篩選並排除變化的範例查詢](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-not-variations)
      * 請參閱[依 _tags ID 進行篩選並包含變化的範例查詢](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-with-variations)

     >[!NOTE]
     >
     >對標記的查詢還能透過列出內容片段的中繼資料進行。

   * And 操作：

      * `_operator`：套用特定的運算子；`EQUALS`、`EQUALS_NOT`、`GREATER_EQUAL`、`LOWER`、`CONTAINS`、`STARTS_WITH`
         * 請參閱[範例查詢 - 所有姓名沒有「Jobs」的人員](/help/headless/graphql-api/sample-queries.md#sample-all-persons-not-jobs)
         * 請參閱[範例查詢 - 所有 `_path` 以特定前置詞開頭的冒險](/help/headless/graphql-api/sample-queries.md#sample-wknd-all-adventures-cycling-path-filter)

      * `_apply`：套用特定條件；例如，`AT_LEAST_ONCE`
         * 請參閱[範例查詢 - 篩選內含必須至少出現一次之項目的陣列](/help/headless/graphql-api/sample-queries.md#sample-array-item-occur-at-least-once)

      * `_ignoreCase`：查詢時忽略大小寫
         * 請參閱[範例查詢 - 所有名稱包含 SAN 的城市，不區分大小寫](/help/headless/graphql-api/sample-queries.md#sample-all-cities-san-ignore-case)

* 支援 GraphQL 聯合類型：

   * 使用 `... on`
      * 請參閱[含內容參考之特定模型的內容片段的範例查詢](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-content-reference)

* 查詢巢狀片段時的備援：

   * 如果巢狀片段不存在特定變化，則將傳回&#x200B;**主版**&#x200B;變化。

## 從外部網站查詢 GraphQL 端點 {#query-graphql-endpoint-from-external-website}

若要從外部網站查詢 GraphQL 端點，您需要設定：

* [CORS 篩選器](/help/headless/deployment/cross-origin-resource-sharing.md)
* [查閱者篩選器](/help/headless/deployment/referrer-filter.md)

## 驗證 {#authentication}

請參閱[針對內容片段之遠端 AEM GraphQL 查詢的驗證](/help/headless/security/authentication.md)。

## 自動化測試 {#automated-testing}

在 AEM Cloud Manager 中執行部署管道時，會在管道執行期間執行自動化測試。

為了提供準確的結果，您的 AEM as a Cloud Service **中繼**&#x200B;環境應盡可能與您的&#x200B;**生產**&#x200B;環境相似。這對於內容來說非常重要。

您可以透過使用 AEM as a Cloud Service [內容複製工具](/help/implementing/developing/tools/content-copy.md) 將生產內容複製到中繼環境來實現這一點。

## 限制 {#limitations}

為了防範潛在問題，對您的查詢會施加預設限制：

* 查詢不能包含超過 1M (1024 * 1024) 個字元
* 查詢不能包含超過 15000 個語彙基元
* 查詢不能包含超過 200000 個空白語彙基元

您還需要了解：

* 當您的 GraphQL 查詢在兩個 (或多個) 模型中具有相同名稱的欄位，並且滿足以下條件時，將傳回欄位衝突錯誤：

   * 當：

      * 將兩個 (或更多模型) 當作可能的參考時，並且它們在內容片段參考中定義為允許的&#x200B;**模型類型**。

     和：

      * 這兩個模型的欄位具有相同的名稱；即兩個模型中出現相同的名稱。

     和

      * 這些欄位的資料類型不同。

   * 例如：

      * 當兩個 (或多個) 具有不同模型 (例如，`M1`、`M2`) 的片段用作來自另一個片段的可能參考 (內容參考或片段參考) 時；例如 `Fragment1` `MultiField/List`
      * 而這兩個具有不同模型 (`M1`，`M2`) 的片段擁有相同名稱但不同類型的欄位。
說明：
         * `M1.Title` 作為 `Text`
         * `M2.Title` 作為 `Text/MultiField`
      * 那麼如果 GraphQL 查詢包含 `Title` 欄位，就會出現欄位衝突錯誤。

## 常見問題 {#faqs}

出現的問題：

1. **問題**：「*GraphQL API for AEM 與查詢產生器 API 有何不同？*」

   * **答案**：
「*AEM GraphQL API 可讓您完全控制 JSON 輸出，是業界的查詢內容標準。
在未來，AEM 計畫投資 AEM GraphQL API。*」

## 教學課程 - AEM Headless 和 GraphQL 快速入門 {#tutorial}

正在尋找實作教學課程？查看 [AEM Headless 和 GraphQL 快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=zh-Hant)端對端教學課程，說明如何在 Headless CMS 情境下使用 AEM GraphQL API 建立和公開內容並供外部應用程式取用。
