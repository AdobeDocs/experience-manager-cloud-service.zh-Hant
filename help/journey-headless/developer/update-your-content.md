---
title: 如何通過AEM AssetsAPI更新您的內容
description: 在「無頭開發AEM者之旅」的這一部分，瞭解如何使用REST API訪問和更新內容片段的內容。
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 2%

---

# 如何通過AEM AssetsAPI更新您的內容 {#update-your-content}

在 [無AEM頭開發者之旅，](overview.md) 瞭解如何使用REST API訪問和更新內容片段的內容。

## 到目前為止的故事 {#story-so-far}

在前一篇無頭旅AEM程中， [如何通過交付API訪AEM問內容](access-your-content.md) 您已經學會了如何通過AEMAEMGraphQL API訪問您的無頭內容，您現在應：

* 對GraphQL有深入的瞭解。
* 瞭解AEMGraphQL API的工作原理。
* 瞭解一些實用的示例查詢。

本文基於這些基礎知識，因此您可以瞭解如何通過REST API更新AEM現有無頭內容。

## 目標 {#objective}

* **觀眾**:高級
* **目標**:瞭解如何使用REST API訪問和更新內容片段的內容：
   * 介紹AEM AssetsHTTP API。
   * 介紹並討論API中的內容片段支援。
   * 說明API的詳細資訊。

<!--
  * Look at sample code to see how things work in practice.
-->

## 為什麼需要內容片段的資產HTTP API {#why-http-api}

在「無頭之旅」的上一階段，您學習了使用AEMGraphQL API使用查詢檢索內容。

那麼，為什麼需要另一個API?

資產HTTP API允許您 **閱讀** 您的內容，但它還允許您 **建立**。 **更新** 和 **刪除** 內容 — GraphQL API不能執行的操作。

Assets REST API可用於最新Adobe Experience Manager as a Cloud Service版本的每個出廠安裝。

## Assets HTTP API {#assets-http-api}

資產HTTP API包括：

* 資產REST API
* 包括對內容片段的支援

Assets HTTP API的當前實現基於 **休息** 體系結構樣式，使您能夠通過 **克魯德** 操作（建立、讀取、更新、刪除）。

通過這些操作， API允許您通過向JavaScript前端應用程式提供內容服務，將Adobe Experience Manager as a Cloud Service作為無頭CMS（內容管理系統）進行操作。 或可以執行HTTP請求和處理JSON響應的任何其他應用程式。 例如，單頁應用程式(SPA)、基於框架或自定義，需要通過API提供內容，通常採用JSON格式。

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

## 資產HTTP API和內容片段 {#assets-http-api-content-fragments}

內容片段用於無頭傳遞，而內容片段是一種特殊類型的資產。 它們用於訪問結構化資料，如文本、數字、日期等。

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

資產REST API使用 `/api/assets` 端點，並需要資產的路徑才能訪問它(沒有前導 `/content/dam`)。

* 這意味著訪問以下位置的資產：
   * `/content/dam/path/to/asset`
* 您需要請求：
   * `/api/assets/path/to/asset`

例如，訪問 `/content/dam/wknd/en/adventures/cycling-tuscany`。 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>訪問：
>
>* `/api/assets` **不** 需要使用 `.model` 選擇器。
>* `/content/path/to/page` **是** 要求使用 `.model` 選擇器。


### 作業 {#operation}

HTTP方法確定要執行的操作：

* **GET**  — 檢索資產或資料夾的JSON表示法
* **POST**  — 建立新資產或資料夾
* **PUT**  — 更新資產或資料夾的屬性
* **DELETE**  — 刪除資產或資料夾

>[!NOTE]
>
>請求正文和/或URL參數可用於配置其中的一些操作；例如，定義資料夾或資產應由 **POST** 請求。

支援的請求的確切格式在API參考文檔中定義。

使用情況可能會因您使用的是作者還是AEM發佈環境以及您的特定使用案例而異。

* 強烈建議將建立綁定到作者實例（目前沒有方法使用此API複製要發佈的片段）。
* 可從兩者進行傳遞，因AEM為僅以JSON格式提供請求的內容。

   * 從作者實例AEM進行儲存和傳遞應足以滿足防火牆後的媒體庫應用程式。

   * 對於即時Web交AEM付，建議使用發佈實例。

>[!CAUTION]
>
>雲實例上的調AEM度程式配置可能會阻止 `/api`。

>[!NOTE]
>
>有關詳細資訊，請參閱API參考。 特別是， [Adobe Experience Manager資產API — 內容片段](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)。

### 讀取/傳遞 {#read-delivery}

用法：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

響應是以內容片段中的結構化內容進行序列化的JSON。 引用作為引用URL傳遞。

有兩種讀操作：

* 按路徑讀取特定內容片段，這將返回內容片段的JSON表示。
* 按路徑讀取內容片段的資料夾：這將返回資料夾內所有內容片段的JSON表示法。

### 建立 {#create}

用法：

`POST /{cfParentPath}/{cfName}`

主體必須包含要建立的內容片段的JSON表示法，包括應在內容片段元素上設定的任何初始內容。 必須設定 `cq:model` 屬性，並且它必須指向有效的內容片段模型。 如果無法執行此操作，將導致錯誤。 還需要添加標題 `Content-Type` 設定為 `application/json`。

### 更新 {#update}

使用是通過

`PUT /{cfParentPath}/{cfName}`

主體必須包含為給定內容片段更新的內容的JSON表示。

這可以只是內容片段、單個元素或所有元素值和/或元資料的標題或說明。

### 刪除 {#delete}

用法：

`DELETE /{cfParentPath}/{cfName}`

有關使用AEM AssetsREST API的詳細資訊，可參考：

* Adobe Experience Manager資產HTTP API（附加資源）
* AEM AssetsHTTP API中的內容片段支援（其他資源）

## 下一步 {#whats-next}

現在，您已完成了「無頭開發AEM者之旅」的這一部分，您應：

* 瞭解AEM AssetsHTTP API的基礎知識。
* 瞭解此API中如何支援內容片段。

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

您應繼續無AEM頭之旅，下次查看文檔 [如何將所有內容放在一起 — 您的應用和您的內容以無AEM頭](put-it-all-together.md) 在此，您將熟悉將應AEM用程式組合起來所需的體系結構基礎知識和工具。

## 其他資源 {#additional-resources}

* [資產HTTP API](/help/assets/mac-api-assets.md)
* [內容片段REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API參考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager資產API — 內容片段](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)
* [使用內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [AEM 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)
* [CORS/解AEM釋](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [視頻 — 為CORS開AEM發](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
