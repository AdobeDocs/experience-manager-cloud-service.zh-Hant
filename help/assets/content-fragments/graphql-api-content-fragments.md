---
title: AEM GraphQL API，用於內容片段
description: 瞭解如何搭配AEM GraphQL API將Adobe Experience Manager(AEM)中的內容片段用作雲端服務，以進行無頭內容傳送。
translation-type: tm+mt
source-git-commit: 36e0fd66c9119571cde5c8791862abed8b552d5a
workflow-type: tm+mt
source-wordcount: '3220'
ht-degree: 1%

---


# AEM GraphQL API，用於內容片段{#graphql-api-for-use-with-content-fragments}

與內容片段搭配使用的Adobe Experience Manager As a Cloud Service(AEM)GraphQL API，主要是以標準、開放原始碼的GraphQL API為基礎。

在AEM中使用GraphQL API，可在無頭CMS實作中，將內容片段有效率地傳送至JavaScript用戶端：

* 避免重複的API要求，就像REST一樣，
* 確保交付內容僅限於特定要求，
* 允許大量傳送呈現為單一API查詢回應所需的內容。

>[!NOTE]
>
>GraphQL目前用於Adobe Experience Manager(AEM)的兩個（個別）藍本中，做為雲端服務：
>
>* [AEM Commerce透過GraphQL從商務平台取用資料](/help/commerce-cloud/architecture/magento.md)。
>* AEM內容片段可與AEM GraphQL API（以標準GraphQL為基礎的自訂實作）搭配運作，以提供結構化內容以用於您的應用程式。


## GraphQL API {#graphql-api}

GraphQL是：

* &quot;*...API的查詢語言，以及使用您現有資料完成這些查詢的執行時期。 GraphQL提供您API中資料的完整且易於理解的描述，讓客戶能夠要求確切的所需內容，而不需要其他內容，讓API隨著時間推移而更容易發展，並提供功能強大的開發人員工具。*&quot;。

   請參閱[GraphQL.org](https://graphql.org)

* &quot;*...開放式規格，以提供有彈性的API圖層。 將GraphQL置於您現有的後端，以前所未有的速度建立產品…….*&quot;。

   請參閱[瀏覽GraphQL](https://www.graphql.com)。

* *」...Facebook於2012年在內部開發了一種資料查詢語言和規範，2015年在公開開源於Facebook。它為基於REST的體系結構提供了替代方案，其目的是提高開發人員的生產力並將傳輸的資料量減至最少。 GraphQL由數百個各種規模的組織在生產中使用……&quot;*

   請參見[GraphQL Foundation](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

有關GraphQL API的詳細資訊，請參見以下各節（以及其他許多資源）:

* 在[graphql.org](https://graphql.org):

   * [GraphQL簡介](https://graphql.org/learn)

   * [GraphQL規範](http://spec.graphql.org/)

* 在[graphql.com](https://graphql.com):

   * [參考線](https://www.graphql.com/guides/)

   * [教學課程](https://www.graphql.com/tutorials/)

   * [精彩案例](https://www.graphql.com/case-studies/)

適用於AEM實作的GraphQL是以標準GraphQL Java程式庫為基礎。 請參閱：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java at GitHub](https://github.com/graphql-java)

### GraphQL術語{#graphql-terminology}

GraphQL使用下列功能：

* **[查詢](https://graphql.org/learn/queries/)**

* **[結構和類型](https://graphql.org/learn/schema/)**:

   * 結構描述是由AEM根據內容片段模型產生。
   * 使用您的結構描述，GraphQL顯示GraphQL在AEM實施中允許的類型和操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **[GraphQL端點](#graphql-aem-endpoint)**
   * AEM中回應GraphQL查詢並提供GraphQL結構描述存取的路徑。

   * 有關詳細資訊，請參見[啟用GraphQL端點](#enabling-graphql-endpoint)。

有關詳細資訊，請參閱[(GraphQL.org)GraphQL](https://graphql.org/learn/)簡介，包括[ Best Practices](https://graphql.org/learn/best-practices/)。

### GraphQL查詢類型{#graphql-query-types}

使用GraphQL，您可以執行查詢以返回：

* A **單個條目**

* **[條目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

您也可以執行：

* [持續查詢，已快取](#persisted-queries-caching)

## 適用於AEM端點的GraphQL {#graphql-aem-endpoint}

端點是用來存取GraphQL for AEM的路徑。 您（或您的應用程式）可以使用此路徑：

* 訪問GraphQL模式，
* 發送您的GraphQL查詢，
* 接收響應（對您的GraphQL查詢）。

GraphQL for AEM端點的儲存庫路徑為：

`/content/cq:graphql/global/endpoint`

您的應用程式可在請求URL中使用下列路徑：

`/content/_cq_graphql/global/endpoint.json`

若要啟用GraphQL for AEM的端點，您需要：

>[!CAUTION]
>
>這些步驟在不久的將來可能會有所改變。

* [啟用GraphQL端點](#enabling-graphql-endpoint)
* [執行其他配置](#additional-configurations-graphql-endpoint)

### 啟用GraphQL端點{#enabling-graphql-endpoint}

>[!NOTE]
>
>如需Adobe提供的套件的詳細資訊，請參閱[支援套件](#supporting-packages)以簡化這些步驟。

若要在AEM中啟用GraphQL查詢，請在`/content/cq:graphql/global/endpoint`處建立端點：

* 節點`cq:graphql`和`global`必須為`sling:Folder`類型。
* 節點`endpoint`必須為`nt:unstructured`類型，並包含`graphql/sites/components/endpoint`的`sling:resourceType`。

>[!CAUTION]
>
>端點目前存在已知問題：
>
>* 在&#x200B;**Sites**&#x200B;控制台中看到`cq:graphql`條目；在頂層。
   >  不得使用。


>[!CAUTION]
>
>每個人都能存取端點。 這可能會——尤其是在發佈例項上——造成安全性顧慮，因為GraphQL查詢可能會對伺服器造成沈重負載。
>
>您可以在端點上設定與您的使用案例相應的ACL。

>[!NOTE]
>
>您的端點不會立即可用。 您必須分別為GraphQL端點提供[其他配置](#additional-configurations-graphql-endpoint)。

>[!NOTE]
>此外，您還可以使用[GraphiQL IDE](#graphiql-interface)測試和調試GraphQL查詢。

### GraphQL端點{#additional-configurations-graphql-endpoint}的其他配置

>[!NOTE]
>
>如需Adobe提供的套件的詳細資訊，請參閱[支援套件](#supporting-packages)以簡化這些步驟。

需要其他配置：

* Dispatcher:
   * 若要允許必要的URL
   * 必要
* 虛名 URL:
   * 為端點分配簡化的URL
   * 可選
* OSGi配置：
   * GraphQL Servlet配置：
      * 處理對端點的請求
      * 配置名稱為`org.apache.sling.graphql.core.GraphQLServlet`。 它需要作為OSGi工廠配置提供
      * `sling.servlet.extensions` 必須設為  `[json]`
      * `sling.servlet.methods` 必須設為  `[GET,POST]`
      * `sling.servlet.resourceTypes` 必須設為  `[graphql/sites/components/endpoint]`
      * 必要
   * 架構Servlet配置：
      * 建立GraphQL模式
      * 配置名稱為`com.adobe.aem.graphql.sites.adapters.SlingSchemaServlet`。 它需要作為OSGi工廠配置提供
      * `sling.servlet.extensions` 必須設為  `[GQLschema]`
      * `sling.servlet.methods` 必須設為  `[GET]`
      * `sling.servlet.resourceTypes` 必須設為  `[graphql/sites/components/endpoint]`
      * 必要
   * CSRF配置：
      * 端點的安全保護
      * 配置名稱為`com.adobe.granite.csrf.impl.CSRFFilter`
      * 將`/content/cq:graphql/global/endpoint`新增至現有的已排除路徑清單(`filter.excluded.paths`)
      * 必要

### 支援軟體包{#supporting-packages}

為簡化GraphQL端點的設定，Adobe提供了[GraphQL Sample Project](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-sample.zip)套件。

此存檔同時包含[所需的附加配置](#additional-configurations-graphql-endpoint)和[ GraphQL端點](#enabling-graphql-endpoint)。 如果安裝在普通AEM實例上，則會在`/content/cq:graphql/global/endpoint`處顯示完全工作的GraphQL端點。

此軟體包旨在成為您自己的GraphQL項目的藍圖。 有關如何使用軟體包的詳細資訊，請參閱軟體包&#x200B;**README**。

如果您偏好手動建立所需的組態，Adobe也提供專屬的[GraphQL端點內容套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-global-endpoint.zip)。 此內容包僅包含GraphQL端點，無需任何配置。

## 圖形QL介面{#graphiql-interface}

<!--
AEM Graph API includes an implementation of the standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) interface. This allows you to directly input, and test, queries.
-->

標準[GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)介面的實作可與AEM GraphQL搭配使用。 這可與AEM](#installing-graphiql-interface)一起安裝。[

此介面可讓您直接輸入並測試查詢。

例如：

* `http://localhost:4502/content/graphiql.html`

它提供語法反白顯示、自動完成、自動建議等功能，以及歷史記錄和線上檔案：

![GraphiQL接](assets/cfm-graphiql-interface.png "口GraphiQL介面")

### 安裝AEM GraphiQL介面{#installing-graphiql-interface}

GraphiQL使用者介面可安裝在AEM上，並附上專用的套件：[GraphiQL Content Package v0.0.4](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphiql-0.0.4.zip)套件。

<!--
See the package **README** for full details; including full details of how it can be installed on an AEM instance - in a variety of scenarios.
-->

## 作者和發佈環境的使用案例{#use-cases-author-publish-environments}

使用案例可視AEM的雲端服務環境類型而定：

* 發佈環境；用於：
   * JS應用程式的查詢資料（標準使用案例）

* 作者環境；用於：
   * 查詢資料以「進行內容管理」:
      * AEM中的GraphQL（雲端服務）目前是唯讀API。
      * REST API可用於CR(u)D操作。

## 權限 {#permission}

權限是存取「資產」所需的權限。

## 方案生成{#schema-generation}

GraphQL是強式型別的API，這表示資料必須依類型清楚地結構化和組織。

GraphQL規範提供了一系列指引，說明如何建立用於查詢特定實例上資料的強穩API。 為此，客戶端需要讀取[Schema](#schema-generation)，該包含查詢所需的所有類型。

對於內容片段，GraphQL結構（結構和類型）基於&#x200B;**Enabled** [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其資料類型。

>[!CAUTION]
>
>所有GraphQL結構（衍生自&#x200B;**Enabled**&#x200B;的內容片段模型）都可通過GraphQL端點讀取。
>
>這表示您需要確保沒有敏感資料可供使用，因為敏感資料可能會以此方式洩露；例如，這包括在模型定義中可能顯示為欄位名稱的資訊。

例如，如果使用者建立名為`Article`的內容片段模型，AEM會產生類型為`ArticleModel`的物件`article`。 此類型中的欄位對應於模型中定義的欄位和資料類型。

1. 內容片段模型：

   ![用於GraphQL的內容片](assets/cfm-graphqlapi-01.png "段模型用於GraphQL")

1. 對應的GraphQL模式（從GraphiQL自動文檔輸出i）:
   ![基於內容片段模型的GraphQL](assets/cfm-graphqlapi-02.png "模式基於內容片段模型的GraphQL模式")

   這表示產生的類型`ArticleModel`包含數個[欄位](#fields)。

   * 其中3個由用戶控制：`author`、`main`和`referencearticle`。

   * AEM會自動新增其他欄位，並代表提供特定內容片段相關資訊的實用方法；在此範例中，`_path`、`_metadata`、`_variations`。 這些[幫助欄位](#helper-fields)標有前面的`_`，以區分由用戶定義的內容和已自動生成的內容。

1. 當使用者根據文章模型建立內容片段後，就可透過GraphQL進行詢問。 如需範例，請參閱[範例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)（根據[範例內容片段結構，以便與GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)搭配使用）。

在GraphQL for AEM中，架構是有彈性的。 這表示每次建立、更新或刪除內容片段模型時都會自動產生此片段。 更新內容片段模型時，也會重新整理資料結構快取。

Sites GraphQL服務會監聽（在背景）對內容片段模型所做的任何修改。 檢測到更新時，只會重新生成模式的該部分。 此最佳化可節省時間並提供穩定性。

例如，如果：

1. 安裝包含`Content-Fragment-Model-1`和`Content-Fragment-Model-2`的軟體包：

   1. 將生成`Model-1`和`Model-2`的GraphQL類型。

1. 然後修改`Content-Fragment-Model-2`:

   1. 只有`Model-2` GraphQL類型會更新。

   1. 而`Model-1`則保持不變。

>[!NOTE]
>
>請務必注意，以防您透過REST api或其他方式對內容片段模型進行大量更新。

模式通過與GraphQL查詢相同的端點服務，客戶端處理以`GQLschema`副檔名調用模式的事實。 例如，對`/content/cq:graphql/global/endpoint.GQLschema`執行簡單的`GET`請求將導致輸出具有Content-type的架構：`text/x-graphql-schema;charset=iso-8859-1`。

## 欄位 {#fields}

在架構中，有兩個基本類別的個別欄位：

* 您產生的欄位。

   選擇[欄位類型](#field-types)會用來根據您的內容片段模型設定欄位。 欄位名稱取自&#x200B;**資料類型**&#x200B;的&#x200B;**屬性名稱**&#x200B;欄位。

   * 還有&#x200B;**Render As**&#x200B;屬性要考慮，因為用戶可以配置某些資料類型；例如，單行文字或多欄位。

* GraphQL for AEM也會產生許多[協助欄位](#helper-fields)。

   這些用來識別內容片段，或取得內容片段的詳細資訊。

### 欄位類型{#field-types}

GraphQL for AEM支援類型清單。 所有支援的內容片段模型資料類型和相應的GraphQL類型都表示：

| 內容片段模型——資料類型 | GraphQL類型 | 說明 |
|--- |--- |--- |
| 單行文字 | 字串、[字串] |  用於簡單字串，例如作者名稱、位置名稱等 |
| 多行文字 | 字串 |  用於輸出文字，例如文章的正文 |
| 數量 |  浮點、[浮點] | 用於顯示浮點數和常規數 |
| 布林值 (Boolean) |  布林函數 |  用於顯示複選框→簡單的true/false語句 |
| 日期和時間 | 日曆 |  用於以ISO 8086格式顯示日期和時間 |
| 列舉 |  String |  用於從建立模型時定義的選項清單中顯示選項 |
|  標記 |  [String] |  用於顯示代表AEM中使用之標籤之字串清單 |
| 內容參考資料 |  字串 |  用於在AEM中顯示指向其他資產的路徑 |
| 片段引用 |  *A模型類型* |  用於引用某個「模型類型」的另一個「內容片段」（在建立模型時定義） |

### 輔助欄位{#helper-fields}

除了使用者產生欄位的資料類型外，GraphQL for AEM也會產生許多&#x200B;*helper*&#x200B;欄位，以協助識別內容片段，或提供內容片段的其他資訊。

#### 路徑 {#path}

路徑欄位用作GraphQL中的標識符。 它代表AEM儲存庫內的「內容片段」資產路徑。 我們選擇此為內容片段的識別碼，因為它：

* 在AEM中是唯一的，
* 很容易被牽扯。

下列程式碼會顯示根據內容片段模型`Person`所建立之所有內容片段的路徑。

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

若要擷取特定類型的單一內容片段，您還需要先決定其路徑。 例如：

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

請參閱[範例查詢——單一特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)。

#### 中繼資料 {#metadata}

AEM也透過GraphQL公開內容片段的中繼資料。 中繼資料是描述內容片段的資訊，例如內容片段的標題、縮圖路徑、內容片段的說明、建立日期等。

由於中繼資料是透過架構編輯器產生，因此沒有特定結構，因此`TypedMetaData` GraphQL類型已實作以公開內容片段的中繼資料。 `TypedMetaData` 公開按以下標量類型分組的資訊：

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

每個標量類型代表單個名稱——值對或名稱——值對陣列，其中該對的值是其所分組的類型。

例如，如果您想要擷取內容片段的標題，我們知道此屬性是字串屬性，因此我們會查詢所有字串中繼資料：

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

如果查看生成的GraphQL模式，則可以查看所有元資料GraphQL類型。 所有型號類型都有相同的`TypedMetaData`。

>[!NOTE]
>
>**正常元資料和陣列元資料之間的差異**
>請記住，`StringMetadata`和`StringArrayMetadata`都引用儲存在儲存庫中的內容，而不是如何檢索它們。
>
>因此，例如，通過調用`stringMetadata`欄位，您將收到儲存在儲存庫中的所有元資料的陣列作為`String`，如果調用`stringArrayMetadata`，您將收到儲存在儲存庫中的所有元資料的陣列作為`String[]`。

請參閱[中繼資料的範例查詢——列出標題為GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)的獎項中繼資料。

#### 變數 {#variations}

`_variations`欄位已實作，以簡化查詢內容片段的變化。 例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

請參閱[範例查詢——具有命名變數的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL變數{#graphql-variables}

GraphQL允許將變數放在查詢中。 有關詳細資訊，請參見GraphiQL的[GraphQL文檔。](https://graphql.org/learn/queries/#variables)

例如，要獲取具有特定變化類型`Article`的所有內容片段，可以在GraphiQL中指定變數`variation`。

![GraphQL變](assets/cfm-graphqlapi-03.png "量GraphQL變數")

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
    "variation": "uk"
}
```

## GraphQL指令{#graphql-directives}

在GraphQL中，有可能根據變數更改查詢，稱為GraphQL指令。

例如，您可以在查詢中根據變數`includePrice`包含`adventurePrice`欄位，以查詢所有`AdventureModels`。

![GraphQL指](assets/cfm-graphqlapi-04.png "令GraphQL指令")

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

## 篩選{#filtering}

您也可以在GraphQL查詢中使用篩選來傳回特定資料。

篩選使用基於邏輯運算子和運算式的語法。

例如，以下（基本）查詢會篩選名稱為`Jobs`或`Smith`的所有人員：

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

* [GraphQL for AEM extensions](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-extensions)的詳細資訊

* [使用此示例內容和結構的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 以及準備用於範例查詢的[範例內容與結構](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [基於WKND項目的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## 持續查詢（快取）{#persisted-queries-caching}

在準備具有POST請求的查詢後，就可以使用GET請求執行，而HTTP快取或CDN可快取該查詢。

這是必要的，因為POST查詢通常不進行快取，而且如果將GET與查詢搭配使用，則參數對HTTP服務和中間產品而言變得過大的風險很大。

以下是保存給定查詢所需的步驟：

>[!NOTE]
>在此之前，**GraphQL持久性查詢**&#x200B;需要啟用，以便進行相應的配置。 如需詳細資訊，請參閱設定瀏覽器中的[啟用內容片段功能。](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)

1. 將查詢PUTing到新的端點URL `/graphql/persist.json/<config>/<persisted-label>`來準備該查詢。

   例如，建立持續查詢：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. 此時，請檢查回應。

   例如，檢查是否成功：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然後，您可以透過GETing the URL `/graphql/execute.json/<shortPath>`來重播持續查詢。

   例如，使用持續查詢：

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 將POSTing的持續查詢更新為現有的查詢路徑。

   例如，使用持續查詢：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. 建立包裝的普通查詢。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用快取控制建立包裝的純查詢。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用參數建立持續查詢：

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. 使用參數執行查詢。

   例如：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. 要在發佈時執行查詢，需要複製相關的持久樹

   * 使用POST進行複製：

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * 使用包：
      1. 建立新包定義。
      1. 包括配置（例如`/conf/wknd/settings/graphql/persistentQueries`）。
      1. 建立套件。
      1. 複製包。
   * 使用複製／分發工具。
      1. 前往「散發」工具。
      1. 為配置選擇樹激活（例如`/conf/wknd/settings/graphql/persistentQueries`）。
   * 使用工作流（通過工作流啟動程式配置）:
      1. 定義工作流啟動程式規則，用於執行將複製不同事件（例如，建立、修改等）上的配置的工作流模型。



1. 在查詢設定開啟發佈後，就會套用相同的原則，只要使用發佈端點。

   >[!NOTE]
   >
   >對於匿名訪問，系統假定ACL允許「每個人」訪問查詢配置。
   >
   >如果不是這樣，它將無法執行。

   >[!NOTE]
   >
   >URL中的任何分號(&quot;;&quot;)都需要進行編碼。
   >
   >例如，如同在「執行持續查詢」的請求中：
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## 從外部網站{#query-graphql-endpoint-from-external-website}查詢GraphQL端點

>[!NOTE]
>
>如需AEM中CORS資源共用原則的詳細概觀，請參閱[瞭解跨原始資源共用(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))。

若要允許協力廠商網站使用JSON輸出，必須在客戶Git儲存庫中設定CORS原則。 若要這麼做，請新增適當的OSGi CORS設定檔以用於所需端點。 此設定應指定應授與存取權的受信任網站名稱（或regex）。

* 訪問GraphQL端點：

   * alloworgin:[您的域]或alloworiginregexp:[您的網域regex]
   * 支援的方法：[POST]
   * 允許路徑：[&quot;/content/graphql/global/endpoint.json&quot;]

* 訪問GraphQL持久查詢端點：

   * alloworgin:[您的域]或alloworiginregexp:[您的網域regex]
   * 支援的方法：[GET]
   * 允許路徑：[&quot;/graphql/execute.json/.*&quot;]

>[!CAUTION]
>
>客戶仍有責任：
>
>* 僅授與受信任網域的存取權
>* 確保未公開任何敏感資訊
>* 不使用通配符[*]語法；這既將禁用對GraphQL端點的驗證訪問，也將它向全世界公開。


>[!CAUTION]
>
>所有GraphQL [方案](#schema-generation)（衍生自&#x200B;**已啟用**&#x200B;的內容片段模型）都可通過GraphQL端點讀取。
>
>這表示您需要確保沒有敏感資料可供使用，因為敏感資料可能會以此方式洩露；例如，這包括在模型定義中可能顯示為欄位名稱的資訊。

## 驗證 {#authentication}

請參閱[內容片段的遠端AEM GraphQL查詢驗證](/help/assets/content-fragments/graphql-authentication-content-fragments.md)。

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## 常見問題{#faqs}

出現的問題：

1. **問**:&quot;*GraphQL API for AEM與Query Builder API有何不同？*&quot;

   * **答**:「AEM *GraphQL API提供JSON輸出的完整控制，是查詢內容的業界標準。未來，AEM將計畫投資AEM GraphQL API。*&quot;

## 教學課程- AEM Headless和GraphQL {#tutorial}快速入門

正在尋找實作教學課程？ 請參閱[AEM無頭和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端對端教學課程，說明如何在無頭CMS案例中，使用AEM的GraphQL API建立和公開內容，並由外部應用程式使用。
