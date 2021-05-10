---
title: 如何透過AEM AssetsAPI更新您的內容
description: 在這部分的「無AEM頭開發人員歷程」中，瞭解如何使用REST API存取和更新您的內容片段內容。
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 787af0d4994bf1871c48aadab74d85bd7c3c94fb
workflow-type: tm+mt
source-wordcount: '1668'
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

[Assets HTTP API](/help/assets/mac-api-assets.md)包含：

* 資產REST API
* 包括支援內容片段

資產HTTP API的目前實作是以&#x200B;**REST**&#x200B;架構樣式為基礎。

Assets REST API可讓Adobe Experience Manager的開發人員以Cloud Service身分，透過&#x200B;**CRUD**&#x200B;作業（建立、讀取、更新、刪除），直接透過HTTP API存取內容(儲存於AEM)。

透過這些操作，API可讓您將Adobe Experience Manager作為無頭CMS（內容管理系統）的Cloud Service，以JavaScript前端應用程式提供內容服務的方式運作。 或是任何其他可執行HTTP要求和處理JSON回應的應用程式。 例如，「單頁應用程式」(SPASingle Page Applications)、架構或自訂需要透過API提供的內容，通常是JSON格式。

>[!NOTE]
>
>無法從Assets REST API自訂JSON輸出。

資產REST API:

* 遵循HATEOAS原則
* 實現SIREN格式

## 重要概念 {#key-concepts}

資產REST API提供對儲存在例項中的資產的REST樣式AEM存取。

它使用`/api/assets`端點，並要求資產的路徑來存取它（沒有前導`/content/dam`）。

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


HTTP方法確定要執行的操作：

* **GET** -擷取資產或資料夾的JSON表示法
* **POST** -建立新資產或檔案夾
* **PUT** -更新資產或資料夾的屬性
* **DELETE** -刪除資產或資料夾

>[!NOTE]
>
>請求正文和／或URL參數可用於配置其中的一些操作；例如，定義資料夾或資產應由&#x200B;**POST**&#x200B;請求建立。

支援請求的確切格式已在API參考檔案中定義。

### 事務行為{#transactional-behavior}

所有請求都是原子的。

這表示後續(`write`)請求無法合併為單一實體可能成功或失敗的單一交易。

### 安全性 {#security}

如果Assets REST API是在沒有特定驗證要求的環境中使用，AEMCORS篩選器必須正確設定。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* CORS/AEM說明
>* 視訊——針對CORS進行開發，具AEM備


在具有特定驗證需求的環境中，建議使用OAuth。

## 可用功能{#available-features}

「內容片段」是特定的資產類型，請參閱使用內容片段。

如需透過API提供之功能的詳細資訊，請參閱：

* 資產REST API（其他資源）
* 實體類型，其中說明每個支援類型的特定功能（與內容片段相關）

### 尋呼{#paging}

資產REST API支援透過URL參數進行分頁(針對GET請求):

* `offset` -要檢索的第一個（子）實體的編號
* `limit` -傳回的實體數上限

響應將包含作為SIREN輸出`properties`部分的分頁資訊。 此`srn:paging`屬性包含請求中指定的（子）實體(`total`)總數、偏移和限制(`offset`、`limit`)。

>[!NOTE]
>
>分頁通常套用至容器實體（即資料夾或具有轉譯的資產），因為它與所請求實體的子系相關。

#### 範例：尋呼{#example-paging}

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

## 實體類型{#entity-types}

### 資料夾 {#folders}

資料夾可當成資產和其他資料夾的容器。 它們反映了內容儲存庫AEM的結構。

Assets REST API會公開資料夾屬性的存取權；例如其名稱、標題等。 資產會以資料夾的子實體和子資料夾的形式公開。

>[!NOTE]
>
>根據子資產和資料夾的資產類型，子實體清單可能已包含定義各子實體的完整屬性集。 或者，在該子實體清單中，僅可針對實體公開一組縮小的屬性。

### 資產 {#assets}

如果要求資產，回應會傳回其中繼資料；例如標題、名稱及由個別資產架構定義的其他資訊。

資產的二進位資料以`content`類型的SIREN連結的形式公開。

資產可以有多個轉譯。 這些項目通常以子實體形式公開，但有一個例外是縮略圖格式副本，它以類型`thumbnail`(`rel="thumbnail"`)的連結形式公開。

### 內容片段 {#content-fragments}

「內容片段」是特殊的資產類型。 它們可用於存取結構化資料，例如文字、數字、日期等。

由於&#x200B;*standard*&#x200B;資產（例如影像或音訊）有數項差異，因此處理資產時會套用一些其他規則。

#### 表示{#representation}

內容片段：

* 請勿公開任何二進位資料。
* 完全包含在JSON輸出中（位於`properties`屬性中）。

* 也被視為原子，即元素和變化作為片段屬性的一部分而暴露，而不是作為連結或子實體。 這允許有效訪問片段的負載。

#### 內容模型和內容片段{#content-models-and-content-fragments}

目前，定義內容片段結構的模型不會透過HTTP API公開。 因此，*consumer*&#x200B;需要瞭解片段的模型（至少是最小值）-儘管大部分資訊可以從負載中推斷出來；資料類型等。 是定義的一部分。

要建立新內容片段，必須提供模型的（內部儲存庫）路徑。

#### 相關聯的內容 {#associated-content}

相關內容目前未公開。

## 使用資產REST API {#using-aem-assets-rest-api}

使用情形可能因您使用作者或發AEM布環境以及特定使用案例而異。

* 強烈建議建立作業系結至作者例項（[，目前無法使用此API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)復製片段以發佈）。
* 兩者皆可傳送，因AEM為僅以JSON格式提供要求的內容。

   * 從作者實例AEM儲存和傳送應足以在防火牆後提供媒體庫應用程式。

   * 若是即時Web傳送，建議使AEM用發佈例項。

>[!CAUTION]
>
>雲端例項上的AEMDispatcher設定可能會封鎖對`/api`的存取。

>[!NOTE]
>
>如需詳細資訊，請參閱[API參考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)。 尤其是[Adobe Experience Manager資產API —— 內容片段](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)。

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

## 其他資源 {#additional-resources}

* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [HATEOAS原則](https://en.wikipedia.org/wiki/HATEOAS)
* [SIREN格式](https://github.com/kevinswiber/siren)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [內容片段REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API參考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
* [AEM 核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)
* [CORS/AEM說明](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [視訊——針對CORS進行開發，具AEM備](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

