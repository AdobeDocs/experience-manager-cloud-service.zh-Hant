---
title: Adobe Experience Manager作為Assets HTTP API中的雲端服務內容片段支援
description: 瞭解Adobe Experience Manager如何在資產HTTP API中以雲端服務內容片段支援的方式提供。
translation-type: tm+mt
source-git-commit: 68f799349a4a1a9d5a09fb0cb23e0f5620d77d2f
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 2%

---


# AEM Assets HTTP API 內容片段支援{#content-fragments-support-in-aem-assets-http-api}

## 概覽 {#overview}

>[!NOTE]
>
>[Assets HTTP API](/help/assets/mac-api-assets.md)包含：
>
>* 資產REST API
>* 包括支援內容片段

>
>
資產HTTP API的目前實作是以[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)架構樣式為基礎。

[Assets REST API](/help/assets/mac-api-assets.md)可讓Adobe Experience Manager做為雲端服務的開發人員透過HTTP API直接存取內容（儲存在AEM中），透過CRUD作業（建立、讀取、更新、刪除）。

此API可讓您將Adobe Experience Manager當成雲端服務，以無頭CMS（內容管理系統）的形式運作，為JavaScript前端應用程式提供內容服務。 或是任何其他可執行HTTP要求和處理JSON回應的應用程式。

例如，單頁應用程式(SPA)、架構或自訂需要透過HTTP API提供的內容，通常是JSON格式。

雖然[AEM核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)提供非常完整、有彈性且可自訂的API，可針對此用途提供必要的讀取作業，而且可自訂其JSON輸出，但是它們確實需要AEM WCM(Web Content Management)專業知識，才能在以專用AEM範本為基礎的頁面中代管實作。 並非每個SPA開發組織都能直接獲得此類知識。

此時即可使用資產REST API。 它可讓開發人員直接存取資產（例如影像和內容片段），而不需先將資產內嵌在頁面中，然後以序號化JSON格式傳送其內容。

>[!NOTE]
>
>無法從Assets REST API自訂JSON輸出。

Assets REST API也允許開發人員建立新資產、內容片段和資料夾，以修改內容。

資產REST API:

* 遵循[HATEOAS原則](https://en.wikipedia.org/wiki/HATEOAS)

* 實施[SIREN格式](https://github.com/kevinswiber/siren)

## 必備條件 {#prerequisites}

資產REST API可在最新Adobe Experience Manager的每次即裝即用安裝中，以雲端服務版本提供。

## 重要概念 {#key-concepts}

Assets REST API提供對儲存在AEM例項中的資產的[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)樣式存取。

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
* **PUT**  —— 更新資產或資料夾的屬性
* **刪除** -刪除資產或資料夾

>[!NOTE]
>
>請求正文和／或URL參數可用於配置其中的一些操作；例如，定義資料夾或資產應由&#x200B;**POST**&#x200B;請求建立。

<!--
The exact format of supported requests is defined in the [API Reference](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) documentation.
-->

### 事務行為{#transactional-behavior}

所有請求都是原子的。

這表示後續(`write`)請求無法合併為單一實體可能成功或失敗的單一交易。

### AEM(Assets)REST API與AEM元件{#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>外觀</td>
   <td>資產REST API<br/> </td>
   <td>AEM Component<br/>（使用Sling Models的元件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支援的使用案例</td>
   <td>一般用途。</td>
   <td><p>已針對單頁應用程式(SPA)或任何其他（內容消費）內容的使用最佳化。</p> <p>也可以包含版面資訊。</p> </td>
  </tr>
  <tr>
   <td>支援的作業</td>
   <td><p>建立、讀取、更新、刪除。</p> <p>視實體類型而定，具有其他操作。</p> </td>
   <td>唯讀.</td>
  </tr>
  <tr>
   <td>存取</td>
   <td><p>可直接存取。</p> <p>使用映射到<code>/content/dam</code>（在儲存庫中）的<code>/api/assets </code>端點。</p> 
   <p>範例路徑如下所示： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>需要透過AEM頁面上的AEM元件來參考。</p> <p>使用<code>.model</code>選擇器來建立JSON表示法。</p> <p>範例路徑如下所示：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全性</td>
   <td><p>有多種選項。</p> <p>OAuth的提出；可與標準設定分開設定。</p> </td>
   <td>使用AEM的標準設定。</td>
  </tr>
  <tr>
   <td>建築注釋</td>
   <td><p>寫入存取權通常會針對作者例項。</p> <p>讀取內容也可以導向發佈實例。</p> </td>
   <td>由於此方法為唯讀，因此通常會用於發佈例項。</td>
  </tr>
  <tr>
   <td>輸出</td>
   <td>以JSON為基礎的SIREN輸出：詳細，但功能強大。 允許在內容中導覽。</td>
   <td>以JSON為基礎的專屬輸出；可透過Sling Models進行設定。 導覽內容結構很難實作（但不一定不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全性 {#security}

如果Assets REST API是在沒有特定驗證要求的環境中使用，AEM的CORS篩選器必須正確設定。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* [CORS/AEM說明](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [影片——使用AEM針對CORS進行開發](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



在具有特定驗證需求的環境中，建議使用OAuth。

## 可用功能{#available-features}

「內容片段」是特定資產類型，請參閱[使用內容片段](/help/assets/content-fragments/content-fragments.md)。

如需透過API提供之功能的詳細資訊，請參閱：

* [Assets REST API](/help/assets/mac-api-assets.md)
* [實體類型](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types)，其中說明每個支援類型的特定功能（與內容片段相關）

### 尋呼{#paging}

資產REST API支援透過URL參數進行分頁（針對GET請求）:

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

資料夾可當成資產和其他資料夾的容器。 它們反映AEM內容存放庫的結構。

Assets REST API會公開資料夾屬性的存取權；例如其名稱、標題等。 資產會以資料夾的子實體和子資料夾的形式公開。

>[!NOTE]
>
>根據子資產和資料夾的資產類型，子實體清單可能已包含定義各子實體的完整屬性集。 或者，在該子實體清單中，僅可針對實體公開一組縮小的屬性。

### 資產 {#assets}

如果要求資產，回應會傳回其中繼資料；例如標題、名稱及由個別資產架構定義的其他資訊。

資產的二進位資料以`content`類型的SIREN連結的形式公開。

資產可以有多個轉譯。 這些項目通常以子實體形式公開，但有一個例外是縮略圖格式副本，它以類型`thumbnail`(`rel="thumbnail"`)的連結形式公開。

### 內容片段 {#content-fragments}

[內容片段](/help/assets/content-fragments/content-fragments.md)是特殊類型的資產。 它們可用於存取結構化資料，例如文字、數字、日期等。

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

## 使用 {#using}

使用情形可能會因您使用AEM作者或發佈環境以及您的特定使用案例而異。

* 強烈建議建立作業系結至作者例項（[，目前無法使用此API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)復製片段以發佈）。
* 兩者皆可傳送，因為AEM僅以JSON格式提供要求的內容。

   * 從AEM作者實例儲存和傳送的內容，應該足以滿足防火牆後、媒體程式庫應用程式的需求。

   * 若是即時網路傳送，建議使用AEM發佈例項。

>[!CAUTION]
>
>AEM雲端例項上的Dispatcher設定可能會封鎖對`/api`的存取。

<!--
>[!NOTE]
>
>For further details, see the [API Reference](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). In particular, [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html). 
-->

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

## 限制 {#limitations}

有幾個限制：

* **目前不支援內容片段模型**:無法讀取或建立。為了能夠建立新的內容片段或更新現有的內容片段，開發人員必須知道內容片段模型的正確路徑。 目前，唯一可以透過管理UI來取得這些概觀的方法。
* **將忽略引用**。目前不會檢查是否參考現有的內容片段。 因此，例如，刪除內容片段可能會在包含對已刪除內容片段之參考的頁面上產生問題。

<!--
* **Variations cannot be written and updated.** If those variations are added to a payload (e.g. for updates) they will be ignored. However, the variation will be served via delivery ( `GET`).
-->

## 狀態代碼和錯誤消息{#status-codes-and-error-messages}

在相關情況下，可看到以下狀態代碼：

* **200** (OK)在下列情況下傳回：

   * 透過`GET`請求內容片段
   * 透過`PUT`成功更新內容片段

* **201** （已建立）在下列情況下傳回：

   * 透過`POST`成功建立內容片段

* **404** （找不到）在下列情況下傳回：

   * 請求的內容片段不存在

* **500** （內部伺服器錯誤）

   >[!NOTE]
   >
   >傳回此錯誤：
   >
   >* 發生無法以特定程式碼識別的錯誤時
   >* 當指定的裝載無效時


   以下列出返回此錯誤狀態時的常見情況，以及生成的錯誤消息（單空格）:

   * 父資料夾不存在（通過`POST`建立內容片段時）
   * 未提供任何內容片段模型（cq:model遺失）、無法讀取（因為路徑無效或權限問題）或沒有有效片段模型：

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * 無法建立內容片段（可能是權限問題）:

      * `Could not create content fragment`
   * 無法更新標題和說明：

      * `Could not set value on content fragment`
   * 無法設定中繼資料：

      * `Could not set metadata on content fragment`
   * 找不到或無法更新內容元素

      * `Could not update content element`
      * `Could not update fragment data of element`

   詳細的錯誤訊息通常會以下列方式傳回：

   ```xml
   {
     "class": "core/response",
     "properties": {
       "path": "/api/assets/foo/bar/qux",
       "location": "/api/assets/foo/bar/qux.json",
       "parentLocation": "/api/assets/foo/bar.json",
       "status.code": 500,
       "status.message": "...{error message}.."
     }
   }
   ```

## API參考{#api-reference}

如需詳細的API參考，請參閱此處：

<!--
* [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
-->

* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#available-features)

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱：

* [資產HTTP API檔案](/help/assets/mac-api-assets.md)
* [AEM Gem作業：OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

