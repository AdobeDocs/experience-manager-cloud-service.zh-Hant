---
title: 如何透過AEM AssetsAPI更新您的內容
description: 在這部分的「無AEM頭開發人員歷程」中，瞭解如何使用REST API存取和更新您的內容片段內容。
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 4a36cd3206784c0e4e3ed3d7007c83f44f1d5ee0
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 2%

---

# 如何透過AEM AssetsAPI{#update-your-content}更新您的內容

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[無頭開發人AEM員歷程的這部分，](overview.md)瞭解如何使用REST API存取和更新您的內容片段。

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，[如何透過傳送API存取您的內容AEM](access-your-content.md)您學習了如何透過GraphQL AEM API存取您的無頭內容，您現在應該AEM:

* 對GraphQL有深入的瞭解。
* 瞭解GraphQL AEM API的運作方式。
* 瞭解一些實用的範例查詢。

本文以這些基本內容為基礎，讓您瞭解如何透過REST API更新現有AEM的無頭內容。

## 目標 {#objective}

* **觀眾**:進階
* **目標**:瞭解如何使用REST API存取和更新您的內容片段：
   * 介紹AEM AssetsHTTP API。
   * 介紹並討論API中的內容片段支援。
   * 說明API的詳細資訊。

<!--
  * Look at sample code to see how things work in practice.
-->

## 為什麼您需要內容片段{#why-http-api}的資產HTTP API

在「無頭歷程」的上一階段，您學習了如何使用AEMGraphQL API來使用查詢來擷取您的內容。

那麼，為什麼需要另一個API?

資產HTTP API允許您讀取&#x200B;**內容，但也允許您**&#x200B;建立&#x200B;**、**&#x200B;更新&#x200B;**和**&#x200B;刪除&#x200B;**內容- GraphQL API無法執行的動作。**

Assets REST API是以Cloud Service版本形式提供於最近Adobe Experience Manager的每次現成安裝。

## Assets HTTP API {#assets-http-api}

資產HTTP API包含：

* 資產REST API
* 包括支援內容片段

資產HTTP API的目前實作是以&#x200B;**REST**&#x200B;架構樣式為基礎，可讓您透過&#x200B;**CRUD**&#x200B;作業（建立、讀取、更新、刪除）存取內容(儲存於AEM)。

透過這些操作，API可讓您將Adobe Experience Manager作為無頭CMS（內容管理系統）的Cloud Service，以JavaScript前端應用程式提供內容服務的方式運作。 或是任何其他可執行HTTP要求和處理JSON回應的應用程式。 例如，「單頁應用程式」(SPASingle Page Applications)、架構或自訂需要透過API提供的內容，通常是JSON格式。

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## 資產HTTP API和內容片段{#assets-http-api-content-fragments}

內容片段用於無頭傳送，而內容片段是特殊類型的資產。 它們用於存取結構化資料，例如文字、數字、日期等。

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a new content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## 使用資產REST API {#using-aem-assets-rest-api}

### 存取 {#access}

Assets REST API使用`/api/assets`端點，並需要資產路徑來存取它（沒有前導`/content/dam`）。

* 這表示若要存取資產，請造訪：
   * `/content/dam/path/to/asset`
* 您需要要求：
   * `/api/assets/path/to/asset`

例如，若要存取`/content/dam/wknd/en/adventures/cycling-tuscany`，請求`/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>存取：
>
>* `/api/assets` **不** 需要使用選擇 `.model` 器。
>* `/content/path/to/page` **需** 要使用選擇 `.model` 器。


### 操作{#operation}

HTTP方法確定要執行的操作：

* **GET** -擷取資產或資料夾的JSON表示法
* **POST** -建立新資產或檔案夾
* **PUT** -更新資產或資料夾的屬性
* **DELETE** -刪除資產或資料夾

>[!NOTE]
>
>請求正文和／或URL參數可用於配置其中的一些操作；例如，定義資料夾或資產應由&#x200B;**POST**&#x200B;請求建立。

支援請求的確切格式已在API參考檔案中定義。

使用情形可能因您使用作者或發AEM布環境以及特定使用案例而異。

* 強烈建議建立作業系結至作者例項（目前無法使用此API復製片段以發佈）。
* 兩者皆可傳送，因AEM為僅以JSON格式提供要求的內容。

   * 從作者實例AEM儲存和傳送應足以在防火牆後提供媒體庫應用程式。

   * 若是即時Web傳送，建議使AEM用發佈例項。

>[!CAUTION]
>
>雲端例項上的AEMDispatcher設定可能會封鎖對`/api`的存取。

>[!NOTE]
>
>如需詳細資訊，請參閱API參考。 尤其是[Adobe Experience Manager資產API —— 內容片段](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)。

### 讀取／傳送{#read-delivery}

使用方式：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

回應會序列化JSON，內容結構化如內容片段。 參考會以參考URL的形式傳遞。

可能有兩種讀取操作：

* 依路徑讀取特定內容片段時，會傳回內容片段的JSON表示法。
* 依路徑讀取內容片段的資料夾：這會傳回資料夾內所有內容片段的JSON表示法。

### 建立 {#create}

使用方式：

`POST /{cfParentPath}/{cfName}`

內文必須包含要建立之內容片段的JSON表示法，包括應在內容片段元素上設定的任何初始內容。 必須設定`cq:model`屬性，且必須指向有效的內容片段模型。 若無法這麼做，將會導致錯誤。 此外，還需要添加將設定為`application/json`的標題`Content-Type`。

### 更新 {#update}

使用方式是透過

`PUT /{cfParentPath}/{cfName}`

內文必須包含JSON表示法，以說明要針對指定內容片段更新的內容。

這只能是內容片段的標題或說明、單一元素，或所有元素值和／或中繼資料。

### 刪除 {#delete}

使用方式：

`DELETE /{cfParentPath}/{cfName}`

如需使用AEM AssetsREST API的詳細資訊，請參考：

* Adobe Experience Manager資產HTTP API（其他資源）
* AEM AssetsHTTP API（其他資源）中的內容片段支援

## 下一個{#whats-next}

現在，您已完成這部分的無AEM頭開發人員旅程，您應：

* 瞭解AEM AssetsHTTP API的基本概念。
* 瞭解此API支援內容片段的方式。

<!--
* Have experience with sample code and know how the API works in practice.
-->

您應繼AEM續無頭歷程，請閱讀[檔案](put-it-all-together.md)如何將一切整合在一起——無頭中的應用程式和您的內容&lt;a1/AEM>，以瞭解如何將無頭專案帶入現場並做好準備。

[如何使用SPAAEM建立單頁應用程式(SPA)也將說明您如何使用SPAAEMEditor架構來建立可編輯的檔案，以及整合SPA外部，以視需要啟用編輯功能。](create-spa.md) 

## 其他資源 {#additional-resources}

* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [內容片段REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API參考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager資產API —— 內容片段](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
* [AEM 核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)
* [CORS/AEM說明](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [視訊——針對CORS進行開發，具AEM備](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

