---
title: 如何透過傳送API存取您AEM的內容
description: 在「無頭開發人AEM員歷程」的這部分，瞭解如何使用GraphQL查詢來存取您的內容片段內容。
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 4a36cd3206784c0e4e3ed3d7007c83f44f1d5ee0
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 1%

---

# 如何透過傳送APIAEM存取您的內容{#access-your-content}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[無頭開發人員旅程的這部分AEM,](overview.md)您可以瞭解如何使用GraphQL查詢來存取您的內容片段，並將它餵送至您的應用程式（無頭傳送）。

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，您學習了內容建模的基本知識[](model-your-content.md)，因此您現在應瞭解如何建立內容結構模型，然後使用內容片段模型和內容片段來實AEM現該結構：

* 識別與內容模型相關的概念和術語。
* 瞭解為何需要建立內容模型才能傳送無頭內容。
* 瞭解如何使用內容片段模型AEM（以及使用內容片段製作內容）來實現此結構。
* 瞭解如何建立內容模型；基本樣本的原則。

本文以這些基礎為基礎，讓您瞭解如何使用GraphQL API存取您AEM現有的AEM無頭內容。

* **觀眾**:初學者
* **目標**:瞭解如何使用GraphQL查詢存取內容片段AEM的內容：
   * 介紹GraphQL和AEMGraphQL API。
   * 深入瞭解GraphQL AEM API的詳細資訊。
   * 檢視一些範例查詢，瞭解實際運作的方式。

## 所以您想要存取您的內容？{#so-youd-like-to-access-your-content}

所以……您擁有這些內容，結構精巧（在「內容片段」中），而且只要等待新應用程式的提供。 問題是，如何實現？

您需要的是定位特定內容、選擇所需內容並將它傳回應用程式，以便進一步處理。

以Adobe Experience Manager(AEM)為Cloud Service，您可以使用GraphQL API，選擇性地存取您的內容片段，以AEM僅傳回所需的內容。 這表示您可以實現無頭傳送結構化內容，以便用於您的應用程式。

>[!NOTE]
>
>GraphQL AEM API是根據標準GraphQL API規格而自訂的實作。

## GraphQL —— 簡介{#graphql-introduction}

GraphQL是開放原始碼規範，它提供：

* 查詢語言，可讓您從結構化物件中選擇特定內容。
* 執行階段，以便對結構化內容執行這些查詢。

GraphQL是&#x200B;*強*&#x200B;類型化API。 這表示&#x200B;*所有*&#x200B;內容必須依類型清楚地結構化和組織，以便GraphQL *瞭解*&#x200B;要訪問的內容和訪問方式。 資料欄位在GraphQL結構中定義，定義內容對象的結構。

然後，GraphQL端點提供響應GraphQL查詢的路徑。

所有這些都表示您的應用程式可以精確、可靠且有效率地選取所需的內容——只是搭配使用時所需的內AEM容。

>[!NOTE]
>
>請參閱&#x200B;*GraphQL*.org和&#x200B;*GraphQL*.com。

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## AEM GraphQL API {#aem-graphql-api}

GraphQL AEM API是以標準GraphQL API規格為基礎的自訂版本，特別設定為允許您對內容片段執行（複雜）查詢。

內容片段是使用的，因為內容是根據內容片段模型來建構的。 這滿足了GraphQL的基本要求。

* 內容片段模型由一或多個欄位組成。
   * 每個欄位都根據資料類型定義。
* 內容片段模型用於生成相應的AEMGraphQL模式。

要實際訪問GraphQLAEM（和內容），使用端點提供訪問路徑。

然後，您的應用程AEM式可透過GraphQL API傳回的內容。

為幫助您直接輸入和測試查詢，標準GraphQL介面的實現也可用於AEMGraphQL(可隨AEM安裝)。 它提供語法反白顯示、自動完成、自動建議等功能，以及歷史記錄和線上檔案。

>[!NOTE]
>
>GraphQL AEM API實施基於GraphQL Java庫。

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEM as a Cloud Service environment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM as a Cloud Service is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## 用於GraphQL API AEM {#content-fragments-use-with-aem-graphql-api}的內容片段

內容片段可用作GraphQL的架構和查詢AEM基礎，如下：

* 它們可讓您設計、建立、組織和發佈不受頁面限制的內容，而且這些內容可以無端傳遞。
* 它們以內容片段模型為基礎，內容片段模型使用選取的資料類型預先定義產生片段的結構。
* 使用「片段參考」(Fragment Reference)資料類型（定義模型時可用）可實現其他結構層。

### 內容片段模型 {#content-fragments-models}

這些內容片段模型：

* 一次&#x200B;**Enabled**，用於生成方案。
* 提供GraphQL所需的資料類型和欄位。 它們可確保您的應用程式只要求可能的項目，並接收預期的項目。
* 您的模型中可使用資料類型&#x200B;**片段參考**&#x200B;來參考其他內容片段，因此引入其他層級的結構。

### 片段參考{#fragment-references}

**片段參考**:

* 是定義內容片段模型時可用的特定資料類型。
* 參照另一個片段，取決於特定的內容片段模型。
* 可讓您建立並擷取結構化資料。

   * 當定義為&#x200B;**multifeed**&#x200B;時，素數片段可參考（擷取）多個子片段。

### JSON預覽{#json-preview}

若要協助您設計和開發內容片段模型，您可以在內容片段編輯器中預覽JSON輸出。

![JSON預](assets/cfm-model-json-preview.png "覽JSON預覽")

<!--
## GraphQL Schema Generation from Content Fragments {#graphql-schema-generation-content-fragments}

GraphQL is a strongly typed API, which means that content must be clearly structured and organized by type. The GraphQL specification provides a series of guidelines on how to create a robust API for interrogating content on a certain instance. To do this, a client needs to fetch the Schema, which contains all the types necessary for a query. 

For Content Fragments, the GraphQL schemas (structure and types) are based on **Enabled** Content Fragment Models and their data types.

>[!CAUTION]
>
>All the GraphQL schemas (derived from Content Fragment Models that have been **Enabled**) are readable through the GraphQL endpoint.
>
>This means that you need to ensure that no sensitive content is available, to ensure that no sensitive data is exposed via GraphQL endpoints; for example, this includes information that could be present as field names in the model definition.

For example, if a user created a Content Fragment Model called `Article`, then AEM generates the object `article` that is of a type `ArticleModel`. The fields within this type correspond to the fields and data types defined in the model.

1. A Content Fragment Model:

   ![Content Fragment Model for use with GraphQL](assets/graphqlapi-cfmodel.png "Content Fragment Model for use with GraphQL")

1. The corresponding GraphQL schema (output from GraphiQL automatic documentation):
   ![GraphQL Schema based on Content Fragment Model](assets/graphqlapi-cfm-schema.png "GraphQL Schema based on Content Fragment Model")

   This shows that the generated type `ArticleModel` contains several [fields](#fields). 
   
   * Three of them have been controlled by the user: `author`, `main` and `referencearticle`.

   * The other fields were added automatically by AEM, and represent helpful methods to provide information about a certain Content Fragment; in this example, `_path`, `_metadata`, `_variations`. These [helper fields](#helper-fields) are marked with a preceding `_` to distinguish between what has been defined by the user and what has been auto-generated.

1. After a user creates a Content Fragment based on the Article model, it can then be interrogated through GraphQL. For examples, see the Sample Queries.md#graphql-sample-queries) (based on a sample Content Fragment structure for use with GraphQL.

In GraphQL for AEM, the schema is flexible. This means that it is auto-generated each and every time a Content Fragment Model is created, updated or deleted. The data schema caches are also refreshed when you update a Content Fragment Model.

The Sites GraphQL service listens (in the background) for any modifications made to a Content Fragment Model. When updates are detected, only that part of the schema is regenerated. This optimization saves time and provides stability.

So for example, if you:

1. Install a package containing `Content-Fragment-Model-1` and `Content-Fragment-Model-2`:
 
   1. GraphQL types for `Model-1` and `Model-2` will be generated.

1. Then modify `Content-Fragment-Model-2`:

   1. Only the `Model-2` GraphQL type will get updated.

   1. Whereas `Model-1` will remain the same. 

>[!NOTE]
>
>This is important to note in case you want to do bulk updates on Content Fragment Models through the REST api, or otherwise.

The schema is served through the same endpoint as the GraphQL queries, with the client handling the fact that the schema is called with the extension `GQLschema`. For example, performing a simple `GET` request on `/content/cq:graphql/global/endpoint.GQLschema` will result in the output of the schema with the Content-type: `text/x-graphql-schema;charset=iso-8859-1`.

### Schema Generation - Unpublished Models {#schema-generation-unpublished-models}

When Content Fragments are nested it can happen that a parent Content Fragment Model is published, but a referenced model is not.

>[!NOTE]
>
>The AEM UI prevents this happening, but if publishing is made programmatically, or with content packages, it can occur.

When this happens, AEM generates an *incomplete* Schema for the parent Content Fragment Model. This means that the Fragment Reference, which is dependent on the unpublished model, is removed from the schema.

## AEM GraphQL Endpoints {#aem-graphql-endpoints}

An endpoint is the path used to access GraphQL for AEM. Using this path you (or your app) can:

* access the GraphQL schemas,
* send your GraphQL queries,
* receive the responses (to your GraphQL queries).

AEM allows for:

* A global endpoint - available for use by all sites.
* Endpoints for specific Sites configurations - that you can configure (in the Configuration Browser), specific to a specified site/project.

## Permissions {#permissions}

The permissions are those required for accessing Assets.

## The AEM GraphiQL Interface {#aem-graphiql-interface}

To help you directly input, and test queries, an implementation of the standard GraphiQL interface is available for use with AEM GraphQL. This can be installed with AEM.

>[!NOTE]
>
>GraphiQL is bound the global endpoint (and does not work with other endpoints for specific Sites configurations).

It provides features such as syntax-highlighting, auto-complete, auto-suggest, together with a history and online documentation.

![GraphiQL Interface](assets/graphiql-interface.png "GraphiQL Interface")
-->

## 實際使AEM用GraphQL API {#actually-using-aem-graphiql}

### 初始設定{#initial-setup}

在開始查詢您的內容之前，您需要：

* 啟用端點
   * 使用工具->站點-> GraphQL
   * [啟用GraphQL端點](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)

* 安裝GraphiQL（如果需要）
   * 安裝為專用軟體包
   * [安裝AEMGraphiQL介面](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)

### 範例結構{#sample-structure}

要在查詢中實AEM際使用GraphQL API，我們可以使用兩個非常基本的內容片段模型結構：

* 公司
   * 名稱——文本
   * CEO（人員）-片段參考
   * 員工（人員）-片段參考
* 人員
   * 名稱——文本
   * 名字——文字

如您所見，CEO和員工欄位中會參考「人員」片段。

將使用碎片模型：

* 在內容片段編輯器中建立內容時
* 生成要查詢的GraphQL方案

### 在何處測試查詢{#where-to-test-your-queries}

查詢可在GraphiQL介面中輸入，例如：

* `http://localhost:4502/content/graphiql.html `

![GraphiQL接](assets/graphiql-interface.png "口GraphiQL介面")

### 查詢快速入門{#getting-Started-with-queries}

直接查詢是返回公司架構中所有條目的名稱。 在此，您會要求列出所有公司名稱：

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

稍為複雜的查詢是選擇沒有「工作」名稱的所有人員。 這將過濾所有沒有「Jobs」名稱的人員。 這是使用EQUALS_NOT運算子實現的（還有更多）:

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
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

您也可以建立更複雜的查詢。 例如，查詢至少擁有一名名為&quot;Smith&quot;的員工的所有公司。 此查詢說明對名稱為&quot;Smith&quot;的任何人員進行篩選，從巢狀片段返回資訊：

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

<!-- need code / curl / cli examples-->

有關使用GraphQL API的完AEM整詳細資訊，以及配置必要的元素，您可以參考：

* 學習搭配使用GraphQL AEM
* 範例內容片段結構
* 學習如何搭配使用GraphQL AEM —— 範例內容與查詢

## 下一個{#whats-next}

現在，您已學會如何使用AEMGraphQL API存取和查詢無頭內容，您現在可以[瞭解如何使用REST API存取和更新內容片段](/help/implementing/developing/headless-journey/update-your-content.md)的內容。

## 其他資源 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [結構描述](https://graphql.org/learn/schema/)
   * [變數](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java庫](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [學習搭配使用GraphQL AEM](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [啟用GraphQL端點](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)
   * [安裝AEMGraphiQL介面](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)
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
* [開始使用無AEM頭](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) -一個短片教學課程系列，提供使用無頭功AEM能的概觀，包括內容建模和GraphQL。
