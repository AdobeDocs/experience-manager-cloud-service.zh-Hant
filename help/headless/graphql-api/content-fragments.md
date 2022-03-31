---
title: 用AEM於內容片段的GraphQL API
description: 瞭解如何在GraphQL API中使用Adobe Experience Manager(AEM)as a Cloud Service的內AEM容片段進行無頭內容傳遞。
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: e43feb24adad7ef16dd92f59ed1f37638febd631
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 1%

---


# 用AEM於內容片段的GraphQL API {#graphql-api-for-use-with-content-fragments}

瞭解如何在GraphQL API中使用Adobe Experience Manager(AEM)as a Cloud Service的內AEM容片段進行無頭內容傳遞。

與內AEM容片段一起使用的as a Cloud ServiceGraphQL API主要基於標準的開源GraphQL API。

在中使用GraphQL APIAEM可以在無頭CMS實現中將內容片段高效傳送到JavaScript客戶端：

* 避免像REST一樣的迭代API請求，
* 確保交付僅限於具體要求，
* 允許批量交付作為對單個API查詢的響應的呈現所需的內容。

>[!NOTE]
>
>GraphQL目前在Adobe Experience Manager()as a Cloud Service的兩種(單獨AEM的)情形中使用：
>
>* [通AEM過GraphQL從Commerce平台消耗資料](/help/commerce-cloud/integrating/magento.md)。
>* 內AEM容片段與AEMGraphQL API（基於標準GraphQL的自定義實現）一起工作，以提供結構化內容供您的應用程式使用。


## GraphQL API {#graphql-api}

GraphQL為：

* &quot;*...API的查詢語言和用現有資料完成這些查詢的運行時。 GraphQL提供了對API中資料的完整且易於理解的描述，使客戶能夠準確詢問他們需要什麼，而不需要更多，使API更易於隨時間推移而發展，並支援功能強大的開發人員工具。*。

   請參閱 [GraphQL.org](https://graphql.org)

* &quot;*...靈活API層的開放規範。 將GraphQL置於您現有的後端上，以比以往更快地構建產品……。*。

   請參閱 [瀏覽GraphQL](https://www.graphql.com)。

* *&quot;。..2012年，Facebook在內部開發了資料查詢語言和規範，2015年公開開源。 它提供了基於REST的體系結構的替代方案，目的是提高開發人員的工作效率並最大限度地減少資料傳輸量。 GraphQL由數百個不同規模的組織在生產中使用……」*

   請參閱 [GraphQL基礎](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

有關GraphQL API的詳細資訊，請參閱以下各節（包括許多其他資源）:

* 在 [graphql.org](https://graphql.org):

   * [GraphQL簡介](https://graphql.org/learn)

   * [GraphQL規範](https://spec.graphql.org/)

* 在 [graphql.com](https://graphql.com):

   * [參考線](https://www.graphql.com/guides/)

   * [教學課程](https://www.graphql.com/tutorials/)

   * [案例研究](https://www.graphql.com/case-studies/)

用於實現的AEMGraphQL基於標準的GraphQL Java庫。 請參閱：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub上的GraphQL Java](https://github.com/graphql-java)

### GraphQL術語 {#graphql-terminology}

GraphQL使用以下功能：

* **[查詢](https://graphql.org/learn/queries/)**

* **[方案和類型](https://graphql.org/learn/schema/)**:

   * 架構由基於AEM內容片段模型生成。
   * 使用您的架構，GraphQL將顯示GraphQL允許用於實現的類型和AEM操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **[GraphQL終結點](graphql-endpoint.md)**
   * 響應GraphQL查AEM詢並提供對GraphQL架構的訪問的路徑。

   * 請參閱 [啟用GraphQL終結點](graphql-endpoint.md) 的上界。

查看 [(GraphQL.org)GraphQL簡介](https://graphql.org/learn/) 全面詳情，包括 [最佳做法](https://graphql.org/learn/best-practices/)。

### GraphQL查詢類型 {#graphql-query-types}

使用GraphQL，您可以執行查詢以返回以下任一值：

* A **單項**

* A **[條目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

您還可以執行以下操作：

* [已快取的永續查詢](/help/headless/graphql-api/persisted-queries.md)

### GraphiQL IDE {#graphiql-ide}

可以使用test和調試GraphQL查詢 [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)。

## 作者和發佈環境的使用案例 {#use-cases-author-publish-environments}

使用案例可以取決於as a Cloud Service環境AEM的類型：

* 發佈環境；用於：
   * 查詢JS應用程式的資料（標準用例）

* 作者環境；用於：
   * 為「內容管理目的」查詢資料：
      * as a Cloud Service中AEM的GraphQL當前是只讀API。
      * REST API可用於CR(u)D操作。

## 權限 {#permission}

這些權限是訪問Assets所需的權限。

## 架構生成 {#schema-generation}

GraphQL是強類型API，這意味著資料必須按類型清晰地結構化和組織。

GraphQL規範提供了一系列指導原則，說明如何建立用於查詢特定實例上的資料的強健API。 要執行此操作，客戶端需要獲取 [架構](#schema-generation)，其中包含查詢所需的所有類型。

對於內容片段，GraphQL架構（結構和類型）基於 **已啟用** [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 以及資料類型。

>[!CAUTION]
>
>所有GraphQL架構（從已導出的內容片段模型派生） **已啟用**)可通過GraphQL終結點讀取。
>
>這意味著您需要確保沒有敏感資料可用，因為敏感資料可能會以這種方式洩露；例如，這包括在模型定義中可以作為欄位名稱顯示的資訊。

例如，如果用戶建立了名為 `Article`，然AEM後生成對象 `article` 是 `ArticleModel`。 此類型中的欄位與模型中定義的欄位和資料類型相對應。

1. 內容片段模型：

   ![用於GraphQL的內容片段模型](assets/cfm-graphqlapi-01.png "用於GraphQL的內容片段模型")

1. 相應的GraphQL架構（從GraphiQL自動文檔輸出）:
   ![基於內容片段模型的GraphQL模式](assets/cfm-graphqlapi-02.png "基於內容片段模型的GraphQL模式")

   這顯示生成的類型 `ArticleModel` 包含 [欄位](#fields)。

   * 其中三個由用戶控制： `author`。 `main` 和 `referencearticle`。

   * 其他欄位則由自動添加AEM，並代表提供某一內容片段資訊的有用方法；在本例中， `_path`。 `_metadata`。 `_variations`。 這些 [幫助器欄位](#helper-fields) 標有前面 `_` 區分用戶定義的內容和自動生成的內容。

1. 用戶根據文章模型建立內容片段後，可通過GraphQL查詢。 有關示例，請參見 [示例查詢](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (基於 [用於GraphQL的內容片段結構示例](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql))。

在GraphQL中AEM，架構是靈活的。 這意味著每次建立、更新或刪除內容片段模型時，都會自動生成它。 更新內容片段模型時，還會刷新資料架構快取。

站點GraphQL服務監聽（在後台）對內容片段模型進行的任何修改。 檢測到更新後，只會重新生成該模式的那一部分。 這種優化節省了時間並提供了穩定性。

例如，如果：

1. 安裝包含 `Content-Fragment-Model-1` 和 `Content-Fragment-Model-2`:

   1. GraphQL類型 `Model-1` 和 `Model-2` 生成。

1. 然後修改 `Content-Fragment-Model-2`:

   1. 僅 `Model-2` 將更新GraphQL類型。

   1. 然而 `Model-1` 將保持不變。

>[!NOTE]
>
>請注意，如果要通過REST api或其他方式對內容片段模型進行批量更新，則必須注意這一點。

通過與GraphQL查詢相同的終結點來提供架構，而客戶端則處理使用擴展調用架構的事實 `GQLschema`。 例如，執行簡單 `GET` 請求 `/content/cq:graphql/global/endpoint.GQLschema` 將導致輸出具有Content-type的架構： `text/x-graphql-schema;charset=iso-8859-1`。

### 架構生成 — 未發佈的模型 {#schema-generation-unpublished-models}

嵌套內容片段時，可能會發佈父內容片段模型，但引用的模型未發佈。

>[!NOTE]
>
>UI可AEM以阻止此情況發生，但如果以寫程式方式或使用內容包進行發佈，則可能發生此情況。

當發生這種情況時，AEM將生成 *不完整* 父內容片段模型的架構。 這意味著從架構中刪除依賴於未發佈模型的片段引用。

## 欄位 {#fields}

在架構中，有兩個基本類別的單個欄位：

* 生成的欄位。

   選擇 [欄位類型](#field-types) 用於根據配置內容片段模型的方式建立欄位。 欄位名稱取自 **屬性名稱** 的 **資料類型**。

   * 還有 **呈現為** 屬性需要考慮，因為用戶可以配置某些資料類型；例如，作為單行文本或多欄位。

* GraphQLAEM還生成 [幫助器欄位](#helper-fields)。

   這些內容用於標識內容片段或獲取有關內容片段的詳細資訊。

### 欄位類型 {#field-types}

用於AEM的GraphQL支援類型清單。 所有支援的內容片段模型資料類型和相應的GraphQL類型都表示：

| 內容片段模型 — 資料類型 | GraphQL類型 | 說明 |
|--- |--- |--- |
| 單行文本 | 字串， [字串] |  用於簡單字串，如作者名、位置名等。 |
| 多行文本 | 字串 |  用於輸出文本，例如文章的正文 |
| 數量 |  浮起， [浮動] | 用於顯示浮點數和常規數 |
| 布林值 (Boolean) |  布林函數 |  用於顯示複選框→簡單的true/false語句 |
| 日期和時間 | 日曆 |  用於以ISO 8086格式顯示日期和時間。 根據所選類型，GraphQL中有三種可用的AEM類型： `onlyDate`。 `onlyTime`。 `dateTime` |
| 列舉 |  String |  用於從建立模型時定義的選項清單中顯示選項 |
|  標記 |  [String] |  用於顯示表示中使用的標籤的字串列AEM表 |
| 內容參考資料 |  字串 |  用於在中顯示指向另一個資產的路AEM徑 |
| 片段引用 |  *模型類型* |  用於引用建立模型時定義的特定模型類型的另一個內容片段 |

### 幫助程式欄位 {#helper-fields}

除了用戶生成欄位的資料類型外，GraphQL還AEM生成許多 *幫助* 欄位，以幫助標識內容片段，或提供有關內容片段的其他資訊。

#### 路徑 {#path}

路徑欄位用作GraphQL中的標識符。 它表示儲存庫內的內容片段資AEM產路徑。 我們選擇此作為內容片段的標識符，因為它：

* 在AEM,
* 很容易摘取。

以下代碼將顯示基於內容片段模型建立的所有內容片段的路徑 `Person`。

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

要檢索特定類型的單個內容片段，還需要先確定其路徑。 例如：

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

請參閱 [示例查詢 — 單個特定城市片段](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)。

#### 中繼資料 {#metadata}

通過GraphQL還AEM會顯示內容片段的元資料。 元資料是描述內容片段的資訊，如內容片段的標題、縮略圖路徑、內容片段的說明、建立日期等。

由於元資料是通過架構編輯器生成的，因此沒有特定的結構，因此 `TypedMetaData` 實現了GraphQL類型以公開內容片段的元資料。 `TypedMetaData` 顯示按以下標量類型分組的資訊：

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

每個標量類型都表示單個名稱值對或名稱值對的陣列，其中該對的值屬於其分組的類型。

例如，如果要檢索內容片段的標題，我們知道此屬性是String屬性，因此我們將查詢所有String元資料：

要查詢元資料，請執行以下操作：

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

如果查看生成的GraphQL架構，則可以查看所有元資料GraphQL類型。 所有模型類型都具有相同 `TypedMetaData`。

>[!NOTE]
>
>**正常元資料和陣列元資料的差異**
>記住 `StringMetadata` 和 `StringArrayMetadata` 這兩個選項都引用儲存在儲存庫中的內容，而不是如何檢索它們。
>
>例如，通過調用 `stringMetadata` 欄位中，您將接收儲存在儲存庫中的所有元資料的陣列 `String` ，如果您 `stringArrayMetadata` 您將接收儲存在儲存庫中的所有元資料的陣列 `String[]`。

請參閱 [元資料查詢示例 — 列出標題為GB的獎項的元資料](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)。

#### 變數 {#variations}

的 `_variations` 已實現欄位，以簡化對內容片段的變體的查詢。 例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

請參閱 [示例查詢 — 具有命名變體的所有城市](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL變數 {#graphql-variables}

GraphQL允許將變數放在查詢中。 有關詳細資訊，請參閱 [變數的GraphQL文檔](https://graphql.org/learn/queries/#variables)。

例如，要獲取類型的所有內容片段 `Article` 具有特定變數的變數，可以 `variation` 在GraphiQL中。

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

在GraphQL中，有可能基於變數更改查詢，稱為GraphQL指令。

例如，您可以在 `adventurePrice` 查詢中的 `AdventureModels`，基於變數 `includePrice`。

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

您還可以在GraphQL查詢中使用篩選來返回特定資料。

篩選使用基於邏輯運算子和表達式的語法。

例如，以下（基本）查詢將篩選名稱為 `Jobs` 或 `Smith`:

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

有關更多示例，請參見：

* 詳細資訊 [GraphQL擴展AEM版](#graphql-extensions)

* [使用此示例內容和結構的示例查詢](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * 還有 [示例內容和結構](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) 準備用於示例查詢

* [基於WKND項目的示例查詢](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## GraphQL for AEM — 擴展摘要 {#graphql-extensions}

使用GraphQL查詢的基本操作，AEM以符合標準GraphQL規範。 對於具有以下幾AEM個副檔名的GraphQL查詢：

* 如果需要一個結果：
   * 使用模型名稱；eg城

* 如果您希望列出結果：
   * 添加 `List` 模型名稱；比如說，  `cityList`
   * 請參閱 [示例查詢 — 有關所有城市的所有資訊](#sample-all-information-all-cities)

* 如果要使用邏輯OR:
   * 使用 ` _logOp: OR`
   * 請參閱 [示例查詢 — 名稱為「Jobs」或「Smith」的所有人員](#sample-all-persons-jobs-smith)

* 邏輯AND也存在，但是（通常）是隱式的

* 可以查詢與內容片段模型中的欄位對應的欄位名稱
   * 請參閱 [示例查詢 — 公司CEO和員工的完整詳細資訊](#sample-full-details-company-ceos-employees)

* 除了模型中的欄位外，還有一些系統生成的欄位（前面帶下划線）:

   * 對於內容：

      * `_locale` :揭示語言；基於語言管理器
         * 請參閱 [給定區域設定的多個內容片段的示例查詢](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` :顯示片段的元資料
         * 請參閱 [元資料查詢示例 — 列出標題為GB的獎項的元資料](#sample-metadata-awards-gb)
      * `_model` :允許查詢內容片段模型（路徑和標題）
         * 請參閱 [從模型中查詢內容片段模型的示例](#sample-wknd-content-fragment-model-from-model)
      * `_path` :儲存庫中內容片段的路徑
         * 請參閱 [示例查詢 — 單個特定城市片段](#sample-single-specific-city-fragment)
      * `_reference` :顯示參考；包括RTF編輯器中的內聯引用
         * 請參閱 [具有預取引用的多個內容片段的示例查詢](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` :顯示內容片段中的特定變體
         * 請參閱 [示例查詢 — 具有命名變體的所有城市](#sample-cities-named-variation)
   * 及營運：

      * `_operator` :應用特定運算子； `EQUALS`。 `EQUALS_NOT`。 `GREATER_EQUAL`。 `LOWER`。 `CONTAINS`。 `STARTS_WITH`
         * 請參閱 [示例查詢 — 沒有「職務」名稱的所有人員](#sample-all-persons-not-jobs)
         * 請參閱 [示例查詢 — 所有冒險，其中 `_path` 以特定前置詞開頭](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` :具體條件；比如說，  `AT_LEAST_ONCE`
         * 請參閱 [示例查詢 — 對包含項的陣列進行篩選，該項必須至少發生一次](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` :在查詢時忽略案例
         * 請參閱 [示例查詢 — 名稱中包含SAN的所有城市，不考慮大小寫](#sample-all-cities-san-ignore-case)









* 支援GraphQL聯合類型：

   * 使用 `... on`
      * 請參閱 [具有內容引用的特定模型的內容片段的示例查詢](#sample-wknd-fragment-specific-model-content-reference)

* 查詢嵌套片段時回退：

   * 如果嵌套片段中不存在給定的變體，則 **母版** 將返回變異。

## 從外部網站查詢GraphQL終結點 {#query-graphql-endpoint-from-external-website}

要從外部網站訪問GraphQL終結點，您需要配置：

* [CORS篩選器](/help/headless/deployment/cross-origin-resource-sharing.md)
* [引用篩選器](/help/headless/deployment/referrer-filter.md)

## 驗證 {#authentication}

請參閱 [內容片段AEM上遠程GraphQL查詢的驗證](/help/headless/security/authentication.md)。

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## 常見問題 {#faqs}

出現的問題：

1. **問**:&quot;*GraphQL API與Query Builder APIAEM有何不同？*&quot;

   * **A**:&quot;*GraphQL APIAEM提供對JSON輸出的完全控制，是查詢內容的行業標準。
今後，AEM計畫投資GraphQLAEM API。*&quot;

## 教程 — 無頭和AEMGraphQL入門 {#tutorial}

想要實習教程嗎？ 簽出 [無頭和AEMGraphQL入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) 端到端教程，演示如何使用AEMGraphQL API構建和公開內容，並讓外部應用在無頭CMS方案中使用。
