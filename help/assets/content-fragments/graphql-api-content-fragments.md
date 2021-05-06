---
title: 與內AEM容片段搭配使用的GraphQL API
description: 瞭解如何使用Adobe Experience Manager(AEM)的內容片段做為GraphQL API的Cloud Service,AEM以進行無頭內容傳送。
feature: 內容片段，GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
translation-type: tm+mt
source-git-commit: dab4c9393c26f5c3473e96fa96bf7ec51e81c6c5
workflow-type: tm+mt
source-wordcount: '3901'
ht-degree: 1%

---


# 用AEM於內容片段{#graphql-api-for-use-with-content-fragments}的GraphQL API

瞭解如何使用Adobe Experience Manager(AEM)的內容片段做為GraphQL API的Cloud Service,AEM以進行無頭內容傳送。

因AEM為Cloud ServiceGraphQL API與內容片段搭配使用，很大程度上是以標準的開放原始碼GraphQL API為基礎。

使用中的GraphQL APIAEM，可在無頭CMS實作中，將內容片段有效率地傳送至JavaScript用戶端：

* 避免重複的API要求，就像REST一樣，
* 確保交付內容僅限於特定要求，
* 允許大量傳送呈現為單一API查詢回應所需的內容。

>[!NOTE]
>
>GraphQL目前用於Adobe Experience Manager()的兩個（單獨）情AEM形中作為Cloud Service:
>
>* [AEM商務透過GraphQL從商務平台取用資料](/help/commerce-cloud/integrating/magento.md)。
>* 內AEM容片段與AEMGraphQL API（以標準GraphQL為基礎的自訂實作）搭配運作，以提供結構化內容供您的應用程式使用。


## GraphQL API {#graphql-api}

GraphQL是：

* &quot;*...API的查詢語言，以及使用您現有資料完成這些查詢的執行時期。 GraphQL提供您API中資料的完整且易於理解的描述，讓客戶能夠要求確切的所需內容，而不需要其他內容，讓API隨著時間推移而更容易發展，並提供功能強大的開發人員工具。*&quot;。

   請參閱[GraphQL.org](https://graphql.org)

* &quot;*...開放式規格，以提供有彈性的API圖層。 將GraphQL置於您現有的後端，以前所未有的速度建立產品…….*&quot;。

   請參閱[瀏覽GraphQL](https://www.graphql.com)。

* *」...facebook於2012年在內部開發的資料查詢語言和規格，2015年在公開開發源地之前。它為基於REST的體系結構提供了替代方案，其目的是提高開發人員的生產力並將傳輸的資料量減至最少。 GraphQL由數百個各種規模的組織在生產中使用……&quot;*

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

用於實AEM施的GraphQL基於標準GraphQL Java庫。 請參閱：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java at GitHub](https://github.com/graphql-java)

### GraphQL術語{#graphql-terminology}

GraphQL使用下列功能：

* **[查詢](https://graphql.org/learn/queries/)**

* **[結構和類型](https://graphql.org/learn/schema/)**:

   * 架構是根據內AEM容片段模型產生。
   * 使用方案，GraphQL顯示GraphQL允許用於實施的類型和AEM操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **[GraphQL端點](#graphql-aem-endpoint)**
   * 響應GraphQL查AEM詢並提供對GraphQL模式訪問的路徑。

   * 有關詳細資訊，請參見[啟用GraphQL端點](#enabling-graphql-endpoint)。

有關詳細資訊，請參閱[(GraphQL.org)GraphQL](https://graphql.org/learn/)簡介，包括[ Best Practices](https://graphql.org/learn/best-practices/)。

### GraphQL查詢類型{#graphql-query-types}

使用GraphQL，您可以執行查詢以返回：

* A **單個條目**

* **[條目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

您也可以執行：

* [持續查詢，已快取](#persisted-queries-caching)

>[!NOTE]
>可以使用[GraphiQL IDE](#graphiql-interface)測試和調試GraphQL查詢。

## GraphQL for AEM Endpoint {#graphql-aem-endpoint}

端點是用於訪問GraphQL的路AEM徑。 您（或您的應用程式）可以使用此路徑：

* 訪問GraphQL模式，
* 發送您的GraphQL查詢，
* 接收響應（對您的GraphQL查詢）。

端點有兩種類型AEM:

* 全域
   * 可供所有網站使用。
   * 此端點可使用所有租戶的所有內容片段模型。
   * 如果有任何內容片段模型應在租戶之間共用，則應在全域租戶下建立。
* 租用戶:
   * 與租用戶配置相對應，如[Configuration Browser](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中所定義。
   * 特定於指定的網站／專案。
   * 租用戶特定端點會使用該特定租用戶的內容片段模型與全球租用戶的內容片段模型。

>[!CAUTION]
>
>內容片段編輯器可允許一個租用戶的內容片段參考另一個租用戶的內容片段（透過政策）。
>
>在這種情況下，並非所有內容都可以使用租用戶特定端點進行檢索。
>
>內容作者應控制此情形；例如，考慮將共用內容片段模型放在「全域」租用戶下，可能會很有用。

GraphQL用於全局端點的存AEM儲庫路徑為：

`/content/cq:graphql/global/endpoint`

您的應用程式可在請求URL中使用下列路徑：

`/content/_cq_graphql/global/endpoint.json`

要為GraphQL啟用端點，AEM您需要：

* [啟用GraphQL端點](#enabling-graphql-endpoint)
* [發佈GraphQL端點](#publishing-graphql-endpoint)

### 啟用GraphQL端點{#enabling-graphql-endpoint}

要啟用GraphQL端點，首先需要有適當的配置。 請參閱[內容片段——設定瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md)。

>[!CAUTION]
>
>如果[未啟用內容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，則&#x200B;**Create**&#x200B;選項將不可用。

要啟用相應端點，請執行以下操作：

1. 導覽至&#x200B;**Tools**、**Sites**，然後選擇&#x200B;**GraphQL**。
1. 選擇 **建立**。
1. 將會開啟&#x200B;**建立新的GraphQL端點**&#x200B;對話框。 您可以在此處指定：
   * **名稱**:端點的名稱；您可以輸入任何文字。
   * **使用GraphQL模式，由**:使用下拉式清單來選取所需的網站／專案。

   >[!NOTE]
   >
   >對話方塊中會顯示下列警告：
   >
   >* *如果未妥善管理，GraphQL 端點可能會導致資料安全性和效能問題。在建立端點後，請務必設定適當的權限。*


1. 使用&#x200B;**Create**&#x200B;確認。
1. **後續步驟**&#x200B;對話框將提供指向安全控制台的直接連結，以便確保新建立的端點具有適當的權限。

   >[!CAUTION]
   >
   >每個人都能存取端點。 這可能會——尤其是在發佈例項上——造成安全性顧慮，因為GraphQL查詢可能會對伺服器造成沈重負載。
   >
   >您可以在端點上設定與您的使用案例相應的ACL。

### 發佈GraphQL端點{#publishing-graphql-endpoint}

選擇新端點和&#x200B;**Publish**，使其在所有環境中都可完全使用。

>[!CAUTION]
>
>每個人都能存取端點。
>
>在發佈例項上，這可能會引起安全性的顧慮，因為GraphQL查詢會給伺服器造成沈重負載。
>
>您必須在端點上設定與您的使用案例相應的ACL。

## 圖形QL介面{#graphiql-interface}

標準[GraphQL](https://graphql.org/learn/serving-over-http/#graphiql)介面的實現可用於GraphQLAEM。 這可與](#installing-graphiql-interface)一起安裝AEM[。

此介面可讓您直接輸入並測試查詢。

例如：

* `http://localhost:4502/content/graphiql.html`

它提供語法反白顯示、自動完成、自動建議等功能，以及歷史記錄和線上檔案：

![GraphiQL接](assets/cfm-graphiql-interface.png "口GraphiQL介面")

### 安裝AEMGraphiQL介面{#installing-graphiql-interface}

GraphiQL用戶介面可隨專用包AEM一起安裝：[GraphiQL Content Package v0.0.6(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip)軟體包。

## 作者和發佈環境的使用案例{#use-cases-author-publish-environments}

使用案例可視Cloud Service環AEM境類型而定：

* 發佈環境；用於：
   * JS應用程式的查詢資料（標準使用案例）

* 作者環境；用於：
   * 查詢資料以「進行內容管理」:
      * GraphQL AEM in as aCloud Service當前是只讀API。
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

例如，如果用戶建立了名為`Article`的內容片段模型，AEM則生成類型為`ArticleModel`的對象`article`。 此類型中的欄位對應於模型中定義的欄位和資料類型。

1. 內容片段模型：

   ![用於GraphQL的內容片](assets/cfm-graphqlapi-01.png "段模型用於GraphQL")

1. 對應的GraphQL模式（從GraphiQL自動文檔輸出）:
   ![基於內容片段模型的GraphQL](assets/cfm-graphqlapi-02.png "模式基於內容片段模型的GraphQL模式")

   這表示產生的類型`ArticleModel`包含數個[欄位](#fields)。

   * 其中3個由用戶控制：`author`、`main`和`referencearticle`。

   * 其他欄位則會自動加入，AEM並代表提供特定內容片段相關資訊的實用方法；在此範例中，`_path`、`_metadata`、`_variations`。 這些[幫助欄位](#helper-fields)標有前面的`_`，以區分用戶定義的內容和自動生成的內容。

1. 當使用者根據文章模型建立內容片段後，就可透過GraphQL進行詢問。 如需範例，請參閱[範例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)（根據[範例內容片段結構，以便與GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)搭配使用）。

在GraphQL中，AEM模式是靈活的。 這表示每次建立、更新或刪除內容片段模型時都會自動產生此片段。 更新內容片段模型時，也會重新整理資料結構快取。

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

### 方案生成——未發佈的模型{#schema-generation-unpublished-models}

當內容片段巢狀化時，可能會發佈父項內容片段模型，但參考的模型則不會。

>[!NOTE]
>
>UI可AEM防止此情況發生，但若以程式設計方式發佈，或使用內容封裝，則可能會發生此情況。

發生此情況AEM時，會為父內容片段模型產生&#x200B;*不完整*&#x200B;架構。 這表示從架構中移除與未發佈模型相關的片段參考。

## 欄位 {#fields}

在架構中，有兩個基本類別的個別欄位：

* 您產生的欄位。

   選擇[欄位類型](#field-types)會用來根據您的內容片段模型設定欄位。 欄位名稱取自&#x200B;**資料類型**&#x200B;的&#x200B;**屬性名稱**&#x200B;欄位。

   * 還有&#x200B;**Render As**&#x200B;屬性要考慮，因為用戶可以配置某些資料類型；例如，單行文字或多欄位。

* GraphQL AEM for也生成了[幫助欄位](#helper-fields)。

   這些用來識別內容片段，或取得內容片段的詳細資訊。

### 欄位類型{#field-types}

GraphQL AEM for支援類型清單。 所有支援的內容片段模型資料類型和相應的GraphQL類型都表示：

| 內容片段模型——資料類型 | GraphQL類型 | 說明 |
|--- |--- |--- |
| 單行文字 | 字串、[字串] |  用於簡單字串，例如作者名稱、位置名稱等。 |
| 多行文字 | 字串 |  用於輸出諸如文章主體的文本 |
| 數量 |  浮點、[浮點] | 用於顯示浮點數和常規數 |
| 布林值 (Boolean) |  布林函數 |  用於顯示複選框→簡單的true/false語句 |
| 日期和時間 | 日曆 |  用於以ISO 8086格式顯示日期和時間。 根據所選的類型，GraphQL中有三種可用AEM方式：`onlyDate`、`onlyTime`、`dateTime` |
| 列舉 |  String |  用於從建立模型時定義的選項清單中顯示選項 |
|  標記 |  [String] |  用來顯示表示「標籤」的字串清單AEM |
| 內容參考資料 |  字串 |  用於顯示指向另一個資產的路徑，位於 |
| 片段引用 |  *A模型類型* |  用於引用某個「模型類型」的另一個「內容片段」（在建立模型時定義） |

### 輔助欄位{#helper-fields}

除了用戶生成欄位的資料類型外，GraphQL AEM for還生成許多&#x200B;*helper*&#x200B;欄位，以幫助識別內容片段或提供有關內容片段的附加資訊。

#### 路徑 {#path}

路徑欄位用作GraphQL中的標識符。 它表示儲存庫內的「內容片段」資產的AEM路徑。 我們選擇此為內容片段的識別碼，因為它：

* 是獨一無二的AEM,
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

透過GraphQLAEM也公開內容片段的中繼資料。 中繼資料是描述內容片段的資訊，例如內容片段的標題、縮圖路徑、內容片段的說明、建立日期等。

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

GraphQL允許將變數放在查詢中。 有關詳細資訊，請參閱[GraphQL文檔中的變數](https://graphql.org/learn/queries/#variables)。

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

* [GraphQL的擴展AEM詳細資訊](#graphql-extensions)

* [使用此示例內容和結構的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 以及準備用於範例查詢的[範例內容與結構](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [基於WKND項目的示例查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL for AEM —— 擴展集{#graphql-extensions}摘要

使用GraphQL對查詢進行基本操AEM作，以符合標準GraphQL規範。 對於具有以下擴展AEM名的GraphQL查詢：

* 如果您需要單一結果：
   * 使用模型名稱；eg城市

* 如果您希望得到結果清單：
   * 將`List`添加到型號名稱；例如，`cityList`
   * 請參閱[範例查詢——所有城市的所有資訊](#sample-all-information-all-cities)

* 如果要使用邏輯OR:
   * 使用` _logOp: OR`
   * 請參閱[示例查詢——名稱為&quot;Jobs&quot;或&quot;Smith&quot;](#sample-all-persons-jobs-smith)的所有人員

* 邏輯AND也存在，但是是（通常）隱式的

* 您可以查詢與內容片段模型中欄位對應的欄位名稱
   * 請參閱[範例查詢——公司CEO和員工的完整詳細資訊](#sample-full-details-company-ceos-employees)

* 除了模型中的欄位外，還有一些系統產生的欄位（前面有底線）:

   * 針對內容：

      * `_locale` :揭露語言；基於語言管理器
         * 請參閱[特定地區設定之多個內容片段的範例查詢](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` :顯示片段的中繼資料
         * 請參閱[中繼資料的範例查詢——列出標題為GB](#sample-metadata-awards-gb)的獎項中繼資料
      * `_model` :允許查詢內容片段模型（路徑和標題）
         * 請參閱[範例查詢，以瞭解來自模型的內容片段模型](#sample-wknd-content-fragment-model-from-model)
      * `_path` :儲存庫內內容片段的路徑
         * 請參閱[範例查詢——單一特定城市片段](#sample-single-specific-city-fragment)
      * `_reference` :顯示參照；包括RTF編輯器中的內嵌引用
         * 請參閱[使用預先擷取的參照的多個內容片段的範例查詢](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` :以顯示內容片段中的特定變化
         * 請參閱[範例查詢——具有命名變數的所有城市](#sample-cities-named-variation)
   * 及營運：

      * `_operator` :適用特定運算子； `EQUALS`、 `EQUALS_NOT`、 `GREATER_EQUAL`、 `LOWER`、 `CONTAINS`、  `STARTS_WITH`
         * 請參閱[示例查詢——所有名稱不為&quot;Jobs&quot;的人員](#sample-all-persons-not-jobs)
         * 請參閱[範例查詢——所有冒險，其中`_path`以特定首碼](#sample-wknd-all-adventures-cycling-path-filter)開頭
      * `_apply` :適用特定條件；例如，   `AT_LEAST_ONCE`
         * 請參閱[範例查詢——篩選陣列上必須至少發生一次的項目](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` :在查詢時忽略大小寫
         * 請參閱[示例查詢——名稱中包含SAN的所有城市，而不考慮大小寫](#sample-all-cities-san-ignore-case)









* 支援GraphQL聯合類型：

   * 使用`... on`
      * 請參閱[範例查詢，以瞭解具有內容參考的特定模型內容片段](#sample-wknd-fragment-specific-model-content-reference)

## 持續查詢（快取）{#persisted-queries-caching}

在準備具有POST請求的查詢後，可使用HTTP快取或CDN快取的GET請求來執行查詢。

這是必要的，因為POST查詢通常不進行快取，而且如果將查詢與GET搭配使用作為參數，則很可能會使參數對HTTP服務和中間體過大。

持久查詢必須始終使用與[適當（租用戶）配置](#graphql-aem-endpoint)相關的端點；這樣，它們就可以使用其中一種或兩種：

* 全局配置和端點
查詢可存取所有內容片段模型。
* 特定租用戶組態和端點
建立特定租用戶設定的持續查詢時，需要對應的租用戶特定端點（以提供對相關內容片段模型的存取）。
例如，若要為WKND租用戶特別建立持續查詢，必須事先建立對應的WKND特定租用戶組態，以及WKND特定端點。

>[!NOTE]
>
>如需詳細資訊，請參閱設定瀏覽器中的[啟用內容片段功能。](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
>
>**GraphQL持久性查詢**&#x200B;需要為適當的租用戶配置啟用。

例如，如果有一個名為`my-query`的特定查詢，它使用租用戶配置`my-conf`中的模型`my-model`:

* 您可以使用`my-conf`特定端點建立查詢，然後將查詢保存為：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用`global`端點建立相同的查詢，但查詢將保存為：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>這是兩個不同的查詢——保存在不同的路徑下。
>
>他們恰巧使用相同的模型，但是透過不同的端點。


以下是保存給定查詢所需的步驟：

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

要從外部網站訪問GraphQL端點，您需要配置：

* [CORS篩選](#cors-filter)
* [反向連結篩選](#referrer-filter)

### CORS篩選{#cors-filter}

>[!NOTE]
>
>如需CORS資源分享政策的詳細概觀，請參AEM閱[瞭解跨來源資源分享(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))。

若要存取GraphQL端點，必須在客戶Git儲存庫中設定CORS原則。 若要這麼做，請新增適當的OSGi CORS設定檔，以用於所需的端點。

此配置必須指定必須授予訪問權的受信任網站源`alloworigin`或`alloworiginregexp`。

例如，要授予對`https://my.domain`的GraphQL端點和持久查詢端點的訪問權，可以使用：

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

如果您已為端點配置虛名路徑，也可以在`allowedpaths`中使用該路徑。

### 反向連結篩選器{#referrer-filter}

除了CORS設定外，必須設定「反向連結」篩選器，才能允許第三方主機的存取。

若要這麼做，請新增適當的OSGi反向連結篩選設定檔案，其中：

* 指定可信網站主機名；`allow.hosts`或`allow.hosts.regexp`,
* 授予此主機名的訪問權限。

例如，若要授與反向連結`my.domain`的請求存取權，您可以：

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

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

請參閱[內容片段AEM的遠端GraphQL查詢驗證](/help/assets/content-fragments/graphql-authentication-content-fragments.md)。

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

1. **問**:&quot;*GraphQL API與Query Builder APIAEM有何不同？*&quot;

   * **答**:「AEMGraphQL API提供JSON輸出的完整控制，是查詢內容的業界標準。*未來，AEM計畫投資AEMGraphQL API。*&quot;

## 教學課程——無AEM頭和GraphQL {#tutorial}快速入門

正在尋找實作教學課程？ 請參閱[無頭和GraphQL&lt;a1/AEM>端對端教學課程，說明如何在無頭CMS情境中使用外部應用程式AEM的GraphQL API來建立和公開內容。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)
