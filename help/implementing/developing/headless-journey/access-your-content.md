---
title: 如何透過傳送API存取您AEM的內容
description: 在「無頭開發人AEM員歷程」的這部分，瞭解如何使用GraphQL查詢來存取您的內容片段內容。
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 7b04ae2bfa75fe3d3af13271efe567a5fc401f49
workflow-type: tm+mt
source-wordcount: '4636'
ht-degree: 1%

---

# 如何透過傳送APIAEM存取您的內容{#access-your-content}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[AEM Headless Developer Journey（無頭開發人員歷程）的這部分，您可以學習如何使用GraphQL查詢來存取您的內容片段。](overview.md)

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，您學習了資料建模的基本知識[如何建模內容](model-your-content.md)AEM，因此您現在應瞭解如何建模內容結構，然後使用內容片段模型和內容片段來實AEM現該結構：

* 識別與[資料建模](#data-modeling)相關的概念和術語。
* 瞭解[為什麼無頭內容傳送需要建立資料模型](#data-modeling-for-aem-headless)。
* 瞭解如何使用內容片段模型(AEM以及使用[內容片段](#use-content-to-author-content)製作內容)來實現此結構。[](#create-structure-content-fragment-models)
* 瞭解[如何建立內容模型](#getting-started-examples);基本樣本的原則。

本文以這些基礎為基礎，讓您瞭解如何使用GraphQL API存取您AEM現有的AEM無頭內容。

* **觀眾**:初學者
* **目標**:瞭解如何使用GraphQL查詢存取內容片段AEM的內容：
   * 介紹GraphQL和AEMGraphQL API。
   * 深入瞭解GraphQL AEM API的詳細資訊。
   * 檢視一些範例查詢，瞭解實際運作的方式。

## 您想存取資料嗎？{#so-youd-like-to-access-your-data}

所以……您擁有這些內容，結構精巧（在「內容片段」中），而且只要等待新應用程式的提供。 問題是，如何實現？

您需要的是定位特定內容、選擇所需內容並將它傳回應用程式，以便進一步處理。

以Adobe Experience Manager(AEM)為Cloud Service，您可以使用GraphQL API，選擇性地存取您的內容片段，以AEM僅傳回所需的內容。 這表示您可以實現無頭傳送結構化內容，以便用於您的應用程式。

>[!NOTE]
>
>GraphQL AEM API是以標準GraphQL為基礎的自訂實作。

## GraphQL —— 簡介{#graphql-introduction}

GraphQL是開放原始碼規範，它提供：

* 查詢語言，可讓您從結構化物件中選擇特定內容。
* 執行階段，以便對結構化內容執行這些查詢。

GraphQL是&#x200B;*強*&#x200B;類型化API。 這表示&#x200B;*所有*&#x200B;內容必須依類型清楚地結構化和組織，以便GraphQL *瞭解*&#x200B;要訪問的內容和訪問方式。 資料欄位在GraphQL結構中定義，定義內容對象的結構。

然後，GraphQL端點提供響應GraphQL查詢的路徑。

所有這些都表示您的應用程式可以精確、可靠且有效率地選取所需的資料——只是搭配使用時所需的資AEM料。

>[!NOTE]
>
>請參閱&#x200B;*GraphQL*.org和&#x200B;*GraphQL*.com。

## AEM和GraphQL {#aem-graphql}

GraphQL用於中的各種位AEM置；例如：

* 商務
   * GraphQL整合了各AEM種第三方商務解決方案，與CIF核心元件提供的擴充勾點搭配使用。
* 內容片段
   * 已針對此使用案例開發自訂的API。
   * 這是GraphQL AEM API。

>[!NOTE]
>
>「無頭歷程」的這個步驟僅與GraphQL APIAEM和內容片段有關。

## AEM GraphQL API {#aem-graphql-api}

GraphQL AEM API是標準GraphQL API的自訂版本，專門配置為允許您對內容片段執行（複雜）查詢。

內容片段是使用的，因為內容是根據內容片段模型來建構的。 這滿足了GraphQL的基本要求。

* 內容片段模型由一或多個欄位組成。
   * 每個欄位都根據資料類型定義。
* 內容片段模型用於生成相應的AEMGraphQL模式。

要實際訪問GraphQLAEM（和內容），使用端點提供訪問路徑。

然後，您的應用程AEM式可透過GraphQL API傳回的內容。

>[!NOTE]
>
>GraphQL AEM API實施基於GraphQL Java庫。

### 作者和發佈環境的使用案例{#use-cases-author-publish-environments}

GraphQL API的使AEM用案例取決於作為Cloud Service環境AEM的類型：

* 發佈環境；用於：
   * JS應用程式的查詢資料（標準使用案例）

* 作者環境；用於：
   * 查詢資料以「進行內容管理」:
      * GraphQL AEM in as aCloud Service當前是只讀API。
      * REST API可用於CR(u)D操作。

## 用於GraphQL API AEM {#content-fragments-use-with-aem-graphql-api}的內容片段

內容片段可用作GraphQL的架構和查詢AEM基礎，如下：

* 它們可讓您設計、建立、組織和發佈不受頁面限制的內容。
* 它們以內容片段模型為基礎，內容片段模型透過定義的資料類型預先定義產生片段的結構。
* 使用「片段參考」(Fragment Reference)資料類型（定義模型時可用）可實現其他結構層。

### 內容片段模型 {#content-fragments-models}

這些內容片段模型：

* 一次&#x200B;**Enabled**，用於生成方案。

* 提供GraphQL所需的資料類型和欄位。 它們可確保您的應用程式只要求可能的項目，並接收預期的項目。

* 您的模型中可使用資料類型&#x200B;**片段參考**&#x200B;來參考其他內容片段，因此引入其他層級的結構。

### 片段參考{#fragment-references}

**片段參考**:

* 與GraphQL結合使用特別受到關注。

* 是定義內容片段模型時可使用的特定資料類型。

* 參照另一個片段，取決於特定的內容片段模型。

* 可讓您擷取結構化資料。

   * 當定義為&#x200B;**multifeed**&#x200B;時，素數片段可參考（擷取）多個子片段。

### JSON預覽{#json-preview}

若要協助您設計和開發內容片段模型，您可以在內容片段編輯器中預覽JSON輸出。

## 從內容片段{#graphql-schema-generation-content-fragments}生成GraphQL模式

GraphQL是強式型別的API，這表示資料必須依類型清楚地結構化和組織。 GraphQL規範提供了一系列指引，說明如何建立用於查詢特定實例上資料的強穩API。 為此，客戶端需要獲取方案，該方案包含查詢所需的所有類型。

對於內容片段，GraphQL結構（結構和類型）基於&#x200B;**Enabled**&#x200B;內容片段模型及其資料類型。

>[!CAUTION]
>
>所有GraphQL結構（衍生自&#x200B;**Enabled**&#x200B;的內容片段模型）都可通過GraphQL端點讀取。
>
>這表示您需要確保沒有敏感資料可供使用，因為敏感資料可能會以此方式洩露；例如，這包括在模型定義中可能顯示為欄位名稱的資訊。

例如，如果用戶建立了名為`Article`的內容片段模型，AEM則生成類型為`ArticleModel`的對象`article`。 此類型中的欄位對應於模型中定義的欄位和資料類型。

1. 內容片段模型：

   ![用於GraphQL的內容片](assets/graphqlapi-cfmodel.png "段模型用於GraphQL")

1. 對應的GraphQL模式（從GraphiQL自動文檔輸出）:
   ![基於內容片段模型的GraphQL](assets/graphqlapi-cfm-schema.png "模式基於內容片段模型的GraphQL模式")

   這表示產生的類型`ArticleModel`包含數個[欄位](#fields)。

   * 其中3個由用戶控制：`author`、`main`和`referencearticle`。

   * 其他欄位則會自動加入，AEM並代表提供特定內容片段相關資訊的實用方法；在此範例中，`_path`、`_metadata`、`_variations`。 這些[幫助欄位](#helper-fields)標有前面的`_`，以區分用戶定義的內容和自動生成的內容。

1. 當使用者根據文章模型建立內容片段後，就可透過GraphQL進行詢問。 如需範例，請參閱Sample Queries.md#graphql-sample-querys)(根據與GraphQL搭配使用的範例內容片段結構。

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

## 圖AEM形QL端點{#aem-graphql-endpoints}

<!--
need details/examples
-->

端點是用於訪問GraphQL的路AEM徑。 您（或您的應用程式）可以使用此路徑：

* 訪問GraphQL模式，
* 發送您的GraphQL查詢，
* 接收響應（對您的GraphQL查詢）。

AEM允許：

* 全域端點——可供所有網站使用。
* 租用戶端點——您可以設定的，特定於指定的網站／專案。

## 權限 {#permissions}

權限是存取「資產」所需的權限。

## GraphiQLAEM介面{#aem-graphiql-interface}

為幫助您直接輸入和測試查詢，GraphQL介面的標準實現可與GraphQLAEM一起使用。 這可與一起安裝AEM。

它提供語法反白顯示、自動完成、自動建議等功能，以及歷史記錄和線上檔案。

![GraphiQL接](assets/graphiql-interface.png "口GraphiQL介面")

<!--
new page?
-->

## 使AEM用GraphQL API {#using-aem-graphiql}

### 端點{#endpoints}

GraphQL用於全局端點的存AEM儲庫路徑為：

`/content/cq:graphql/global/endpoint`

您的應用程式可在請求URL中使用下列路徑：

`/content/_cq_graphql/global/endpoint.json`

對於租用戶端點，路徑可比：

`/content/cq:graphql/your-tenant/endpoint`
`/content/_cq_graphql/your-tenant/endpoint.json`

使用前，必須啟用所有端點。 要為GraphQL啟用端點（全局或租用戶）,AEM您需要：

* 啟用GraphQL端點
* 發佈端點

>[!CAUTION]
>
>內容片段編輯器可允許一個租用戶的內容片段參考另一個租用戶的內容片段（透過政策）。
>
>在這種情況下，並非所有內容都可以使用租用戶特定端點進行檢索。
>
>內容作者應控制此情形；例如，考慮將共用內容片段模型放在「全域」租用戶下，可能會很有用。

### 啟用GraphQL端點{#enabling-graphql-endpoint}

要啟用GraphQL端點，您首先需要在配置瀏覽器中具有相應的配置。

>[!CAUTION]
>
>如果未啟用內容片段模型的使用，則&#x200B;**Create**&#x200B;選項將不可用。

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

### 安裝AEMGraphiQL介面{#installing-graphiql-interface}

GraphiQL用戶介面可隨專用包AEM一起安裝：[GraphiQL Content Package v0.0.6(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip)軟體包。

### GraphQLAEM結構{#aem-graphql-schemas}

要訪問資料，首先需要選擇所需的內容片段模型類型——由GraphQL模式表示。 GraphQLAEM結構是從內容片段模型派生的——用於GraphQL查詢。

<!--
Confirm is the schema city or CityModel? -->

如果您有名為`City`的內容片段模型，則會有名為`city`的對應架構。 您可以使用下列查詢來列出所有基於此模型的內容片段的`name`。

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

您可以使用以下查詢列出所有`types`可用方案的`name`和`description`:

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

### GraphQLAEM欄位{#aem-graphql-fields}

選擇所需的架構後，您將希望訪問由架構中的欄位表示的特定資料。

在架構中，有兩個基本類別的個別欄位：

* 您產生的欄位。

   選擇[欄位類型](#field-types)會用來根據您的內容片段模型設定欄位。 欄位名稱取自&#x200B;**資料類型**&#x200B;的&#x200B;**屬性名稱**&#x200B;欄位。

   * 還有&#x200B;**Render As**&#x200B;屬性要考慮，因為用戶可以配置某些資料類型；例如，單行文字或多欄位。

* GraphQL AEM for也生成許多幫助欄位。

   這些用來識別內容片段，或取得內容片段的詳細資訊。

### 欄位類型{#field-types}

GraphQL AEM for支援類型清單。 所有支援的內容片段模型資料類型和相應的GraphQL類型都表示：

| 內容片段模型——資料類型 | GraphQL類型 | 說明 |
|--- |--- |--- |
| 單行文字 | 字串、[字串] | 用於簡單字串，例如作者名稱、位置名稱等。 |
| 多行文字 | 字串 | 用於輸出諸如文章主體的文本 |
| 數量 | 浮點、[浮點] | 用於顯示浮點數和常規數 |
| 布林值 (Boolean) | 布林值 (Boolean) | 用於顯示複選框→簡單的true/false語句 |
| 日期和時間 | 日曆 | 用於以ISO 8086格式顯示日期和時間。 根據所選的類型，GraphQL中有三種可用AEM方式：`onlyDate`、`onlyTime`、`dateTime` |
| 列舉 | 字串 | 用於從建立模型時定義的選項清單中顯示選項 |
| 標記 | [String] | 用來顯示表示「標籤」的字串清單AEM |
| 內容參考資料 | 字串 | 用於顯示指向另一個資產的路徑，位於 |
| 片段引用 | *模型類型* | 用於引用某個「模型類型」的另一個「內容片段」（在建立模型時定義） |

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

>[!NOTE]
>
>請參閱範例查詢——單一特定城市片段。

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
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
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

>[!NOTE]
>
>請參閱中繼資料的範例查詢——列出標題為GB的獎項中繼資料。

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

>[!NOTE]
>
>請參閱範例查詢——具有命名變數的所有城市。

### GraphQLAEM變數{#aem-graphql-variables}

變數可用於任何形式的程式設計或查詢，因為它們可讓您將不同的值儲存在一個位置。 對AEM於GraphQL，這表示您無需為每個值編寫單獨的查詢，而是可以為一個變數編寫查詢，並且此變數的值可以根據需要進行更改。

GraphQL允許將變數放在查詢中。

>[!NOTE]
>
>有關詳細資訊，請參見GraphQL的變數文檔。

例如，要獲取具有特定變化類型`Article`的所有內容片段，可以在GraphiQL中指定變數`variation`。 將在`GetArticlesByVariation`中檢索所有實例，然後傳遞以用於`articleList`。

![GraphQL變](assets/graphqlapi-variables.png "量GraphQL變數")

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

### 圖AEM形QL指令{#aem-graphql-directives}

在GraphQL中，有可能根據變數更改查詢，稱為GraphQL指令。

例如，您可以在查詢中根據變數`includePrice`包含`adventurePrice`欄位，以查詢所有`AdventureModels`。

!![GraphQL Directives]（assets/graphqlapi-directives .png &quot;GraphQL指令&quot;）

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

### GraphQLAEM篩選器{#aem-graphql-filters}

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

* GraphQL for extensions的詳細資AEM訊

* 使用此示例內容和結構的示例查詢

### AEM GraphQL擴展{#aem-graphql-extensions}

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

### 持續查詢（快取）{#persisted-queries-caching}

在準備具有POST請求的查詢後，可使用HTTP快取或CDN快取的GET請求來執行查詢。

這是必要的，因為POST查詢通常不進行快取，而且如果將查詢與GET搭配使用作為參數，則很可能會使參數對HTTP服務和中間體過大。

持久查詢必須始終使用與適當（租用戶）配置相關的端點；這樣，它們就可以使用其中一種或兩種：

* 全局配置和端點
查詢可存取所有內容片段模型。
* 特定租用戶組態和端點
建立特定租用戶設定的持續查詢時，需要對應的租用戶特定端點（以提供對相關內容片段模型的存取）。
例如，若要為WKND租用戶特別建立持續查詢，必須事先建立對應的WKND特定租用戶組態，以及WKND特定端點。

>[!NOTE]
>
>如需詳細資訊，請參閱設定瀏覽器中的啟用內容片段功能。
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

### 從外部網站{#query-graphql-endpoint-from-external-website}查詢GraphQL端點

要從外部網站訪問GraphQL端點，您需要配置：

* CORS篩選
* 反向連結篩選

#### CORS篩選{#cors-filter}

>[!NOTE]
>
>如需CORS資源共用政策的詳細概觀，請參閱了AEM解跨原始資源共用(CORS)。

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

#### 反向連結篩選器{#referrer-filter}

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
>所有GraphQL結構（衍生自&#x200B;**Enabled**&#x200B;的內容片段模型）都可通過GraphQL端點讀取。
>
>這表示您需要確保沒有敏感資料可供使用，因為敏感資料可能會以此方式洩露；例如，這包括在模型定義中可能顯示為欄位名稱的資訊。

### GraphQLAEM驗證{#aem-graphql-authentication}

Adobe Experience Manager作為Cloud Service(AEM)GraphQL API的內容片段傳送的主要使用案例是接受來自第三方應用程式或服務的遠程查詢。 這些遠端查詢可能需要經過驗證的API存取，以確保無頭內容傳送的安全。

>[!NOTE]
>
>對於測試和開發，您也可以使AEM用GraphiQL介面直接訪問GraphQL API。

為了驗證協力廠商服務需要使用存取Token，然後才能用於GraphQL請求。

#### 檢索訪問Token {#retrieving-access-token}

如需完整詳細資訊，請參閱產生伺服器端API的存取Token。

#### 在GraphQL請求{#use-access-token-in-graphql-request}中使用訪問Token

對於要與實例連接的第AEM三方服務，它需要&#x200B;*訪問Token*。 然後，服務必須將此Token新增至POST請求的`Authorization`標題。

例如，GraphQL授權標題：

```xml
Authorization: Bearer <access_token>
```

#### 權限要求{#permission-requirements}

使用存取Token提出的所有請求實際上將由產生Token *的使用者帳戶發出*。

這表示您需要檢查帳戶是否具有運行GraphQL查詢所需的權限。

可以通過在本地實例上使用GraphiQL來檢查此問題。

## GraphQL查AEM詢示例{#samples-aem-graphql-queries}

如需完整範例查詢，請參AEM閱學習如何搭配使用GraphQL —— 範例內容與查詢。

<!--
## Code Samples for AEM GraphQL Queries {#code-samples-aem-graphql-queries}
-->

## 下一個{#whats-next}

現在，您已學會如何使用AEMGraphQL API存取和查詢無頭內容，您現在可以[瞭解如何使用REST API存取和更新內容片段](/help/implementing/developing/headless-journey/update-your-content.md)的內容。

## 其他資源 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [結構描述](https://graphql.org/learn/schema/)
   * [變數](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java庫](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [範例內容片段結構](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [學習如何搭配使用GraphQL AEM —— 範例內容與查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [範例查詢——單一特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [中繼資料的範例查詢——列出標題為GB的獎項中繼資料](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [範例查詢——具有命名變異的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [在配置瀏覽器中啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)
* [瞭解跨原始資源共用(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [產生伺服器端API的存取Token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [開始使用無AEM頭](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) -一個短片教學課程系列，其中概述了使用無頭AEM功能，包括資料建模和GraphQL。
