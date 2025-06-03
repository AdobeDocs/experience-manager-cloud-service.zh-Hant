---
title: Assets HTTP API中的Adobe Experience Manager as a Cloud Service內容片段支援
description: 瞭解Adobe Experience Manager HTTP API支援內容片段，這是Assets的Headless傳送功能的重要一環。
feature: Content Fragments, Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
role: User, Admin
source-git-commit: 1995c84bb669fd52ecd53c7e695acc518a5226e8
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 14%

---

# AEM Assets HTTP API 中的內容片段支援 {#content-fragments-support-in-aem-assets-http-api}

## 概觀 {#overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/extending/assets-api-content-fragments.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

>[!CAUTION]
>
>Assets HTTP API中的內容片段支援現在[已棄用](/help/release-notes/deprecated-removed-features.md)。
>
>已由[使用OpenAPI的內容片段傳送](/help/headless/aem-content-fragment-delivery-with-openapi.md)以及[內容片段和內容片段模型管理OpenAPI](/help/headless/content-fragment-openapis.md)取代。

瞭解Assets HTTP API支援內容片段，這是Adobe Experience Manager (AEM) Headless傳送功能的重要一環。

>[!NOTE]
>
>請參閱[結構化內容傳遞與管理的AEM API](/help/headless/apis-headless-and-content-fragments.md)，以取得各種可用API的概觀，以及所涉及概念的比較。
>
>也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。

>[!NOTE]
>
>[Assets HTTP API](/help/assets/mac-api-assets.md)包含：
>
>* Assets REST API
>* 包含支援內容片段
>
>Assets HTTP API目前的實作是以[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)架構樣式為基礎。

>[!NOTE]
>
>如需Experience Manager API的最新資訊，請造訪[Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)。

[Assets REST API](/help/assets/mac-api-assets.md)可讓Adobe Experience Manager as a Cloud Service的開發人員透過CRUD （建立、讀取、更新、刪除）作業，直接透過HTTP API存取內容(儲存在AEM中)。

此API可讓您藉由向Adobe Experience Manager as a Cloud Service前端應用程式提供內容服務，以將JavaScript當作Headless CMS （內容管理系統）來運作。 或任何可執行HTTP要求及處理JSON回應的其他應用程式。

例如，[單頁應用程式(SPA)](/help/implementing/developing/hybrid/introduction.md) （以框架為基礎或自訂）需要透過HTTP API提供的內容，通常為JSON格式。

雖然[AEM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)提供可自訂的API，可提供此用途的必要讀取作業，並可自訂其JSON輸出，但實作時確實需要AEM WCM （Web內容管理）技術。 這是因為它們必須在以專用的AEM範本為基礎的頁面中託管。 並非所有SPA開發組織都能直接存取這些知識。

此時可使用Assets REST API。 它可讓開發人員直接存取資產（例如影像和內容片段），而不需要先將資產內嵌在頁面中，並以序列化JSON格式傳送其內容。

>[!NOTE]
>
>無法從Assets REST API自訂JSON輸出。

Assets REST API也可讓開發人員透過建立新、更新或刪除現有資產、內容片段和資料夾，來修改內容。

Assets REST API：

* 遵循[HATEOAS原則](https://en.wikipedia.org/wiki/HATEOAS)

* 實作[SIREN格式](https://github.com/kevinswiber/siren)

## 先決條件 {#prerequisites}

Adobe Experience Manager as a Cloud Service 最新版本的每個開箱即用安裝中都有提供 Assets REST API。

## 重要概念 {#key-concepts}

Assets REST API提供[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)樣式存取AEM執行個體中儲存的資產。

它使用`/api/assets`端點，並需要資產的路徑才能存取它（沒有前置的`/content/dam`）。

* 這表示要存取以下位置的資產：
   * `/content/dam/path/to/asset`
* 要求：
   * `/api/assets/path/to/asset`

例如，若要存取 `/content/dam/wknd/en/adventures/cycling-tuscany`，要求 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>存取：
>
>* `/api/assets`**不需要**&#x200B;使用 `.model` 選擇器。
>* `/content/path/to/page` **需要**&#x200B;使用 `.model` 選擇器。

HTTP 方法決定要執行的操作：

* **GET** - 檢索資產或資料夾的 JSON 表示
* **POST** — 建立資產或資料夾
* **PUT** - 更新資產或資料夾的屬性
* **DELETE** - 刪除資產或資料夾

>[!NOTE]
>
>要求內文和/或 URL 參數可用於設定其中一些操作；例如，定義資料夾或資產應由 **POST** 要求建立。

在[API參考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)檔案中定義了支援要求的確切格式。

>[!NOTE]
>
>也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。

### 異動行為 {#transactional-behavior}

所有要求都是原子的。

這表示後續(`write`)要求無法合併成單一交易，而單一實體可能會成功或失敗。

### AEM (Assets) REST API與AEM元件 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>層面</td>
   <td>Assets REST API<br/> </td>
   <td>AEM元件<br/> （使用Sling模型的元件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支援的使用案例</td>
   <td>一般用途。</td>
   <td><p>針對單頁應用程式(SPA)或任何其他（使用內容）內容的耗用量進行最佳化。</p> <p>它也可以包含版面配置資訊。</p> </td>
  </tr>
  <tr>
   <td>支援的作業</td>
   <td><p>建立、讀取、更新、刪除。</p> <p>檢視元型別而定，包含其他操作。</p> </td>
   <td>唯讀。</td>
  </tr>
  <tr>
   <td>存取</td>
   <td><p>可以直接存取。</p> <p>使用對應至<code>/content/dam</code> （在存放庫中）的<code>/api/assets </code>端點。</p> 
   <p>範例路徑如下所示： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>必須透過AEM頁面上的AEM元件來參照。</p> <p>使用<code>.model</code>選取器建立JSON表示方式。</p> <p>範例路徑如下所示：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全性</td>
   <td><p>可能有多個選項。</p> <p>建議使用OAuth；可與標準設定分開設定。</p> </td>
   <td>使用AEM的標準設定。</td>
  </tr>
  <tr>
   <td>架構註解</td>
   <td><p>寫入存取權通常可處理作者例項。</p> <p>讀取可能會被導向到發佈執行個體。</p> </td>
   <td>由於此方法為唯讀，因此通常會用於Publish例項。</td>
  </tr>
  <tr>
   <td>輸出</td>
   <td>JSON型SIREN輸出：冗長但功能強大。 它允許在內容內導覽。</td>
   <td>JSON型專有輸出；可透過Sling模型設定。 導覽內容結構難以實作（但並非一定不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全性 {#security}

如果是在沒有特定驗證需求的環境中使用Assets REST API，則必須正確設定AEM的CORS篩選器。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* [CORS/AEM 說明](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=zh-Hant)
>* [影片 — 使用AEM開發CORS (04:06)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html?lang=zh-Hant)
>

在有特定驗證需求的環境中，建議使用OAuth。

## 可用功能 {#available-features}

內容片段是特定型別的資產，請參閱[使用內容片段](/help/assets/content-fragments/content-fragments.md)。

如需透過API提供的功能詳細資訊，請參閱：

* [Assets REST API](/help/assets/mac-api-assets.md)
* [實體型別](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types)，其中說明每個支援型別的特定功能（與內容片段相關）

>[!NOTE]
>
>也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。

### 分頁 {#paging}

Assets REST API支援透過URL引數來分頁(針對GET請求)：

* `offset` — 要擷取的第一個（子項）實體數目
* `limit` — 傳回的實體數上限

回應包含分頁資訊，作為SIREN輸出之`properties`區段的一部分。 此`srn:paging`屬性包含要求中所指定的（子）實體總數( `total`)、位移和限制( `offset`、`limit`)。

>[!NOTE]
>
>分頁通常會套用至容器實體（即資料夾或具有轉譯的資產），因為它與請求實體的子系相關。

#### 範例：分頁 {#example-paging}

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

## 實體型別 {#entity-types}

### 資料夾 {#folders}

資料夾可作為資產和其他資料夾的容器。 它們反映了AEM內容存放庫的結構。

Assets REST API會公開資料夾屬性的存取權。 例如，其名稱和標題。 Assets會顯示為資料夾和子資料夾的子專案。

>[!NOTE]
>
>根據子資產和資料夾的資產型別，子實體清單可能已經包含定義個別子實體的完整屬性集。 或者，在此子圖元清單中，只能為圖元顯示縮減的屬性集。

### Assets {#assets}

如果請求資產，回應會傳回其中繼資料，例如標題、名稱和個別資產結構描述所定義的其他資訊。

資產的二進位資料會公開為型別`content`的SIREN連結。

Assets可以有多個轉譯。 這些通常會顯示為子實體，其中一個例外是縮圖轉譯，這會公開為型別`thumbnail` ( `rel="thumbnail"`)的連結。

### 內容片段 {#content-fragments}

[內容片段](/help/assets/content-fragments/content-fragments.md)是特殊型別的資產。 它們可用於存取結構化資料，例如文字、數字、日期等。

由於&#x200B;*標準*&#x200B;資產（例如影像或音訊）有幾項差異，因此處理這些資產需套用其他規則。

#### 表示 {#representation}

內容片段：

* 不要公開任何二進位資料。
* 包含在JSON輸出中（在`properties`屬性內）。

* 它們也被視為原子元素。 也就是說，元素和變數會作為片段屬性的一部分顯示，而不是作為連結或子實體顯示。 這樣可讓您有效率地存取片段的裝載。

#### 內容模型和內容片段 {#content-models-and-content-fragments}

目前，定義內容片段結構的模型不會透過HTTP API公開。 因此，*消費者*&#x200B;必須知道片段的模型（至少是最低限度） — 雖然大多數資訊可以從承載中推斷；因為資料型別等都是定義的一部分。

若要建立內容片段，必須提供模型的（內部存放庫）路徑。

#### 相關聯的內容 {#associated-content}

關聯內容未公開。

## 使用 {#using}

根據您使用的是AEM製作或發佈環境，以及您的特定使用案例，使用方式可能會有所不同。

* 建議將建立繫結至作者執行個體([)，目前沒有方法可使用此API將片段復寫至發佈](/help/assets/content-fragments/assets-api-content-fragments.md#limitations))。
* 都可以從兩者傳遞，因為 AEM 僅以 JSON 格式提供要求的內容。

   * 對於防火牆後的媒體庫應用程式，AEM編寫執行個體的儲存和傳送應已足夠。

   * 若要進行即時網頁傳送，建議使用AEM發佈執行個體。

>[!CAUTION]
>
>AEM雲端例項上的Dispatcher設定可能會封鎖對`/api`的存取。

>[!NOTE]
>
>請參閱[API參考](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)。 特別是 [Adobe Experience Manager Assets API - 內容片段](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)。
>
>也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。

## 限制 {#limitations}

有幾項限制：

* **目前不支援內容片段模型**：無法讀取或建立這些模型。 為了能夠建立或更新現有的內容片段，開發人員必須知道內容片段模型的正確路徑。 目前，取得這些內容的概觀的唯一方法就是透過管理UI。
* 已忽略&#x200B;**個參考**。 目前沒有檢查是否參考了現有的內容片段。 因此，例如，刪除內容片段可能會導致包含已刪除內容片段參考的頁面發生問題。
* **JSON資料型別** *JSON資料型別*&#x200B;的REST API輸出是&#x200B;*字串型輸出*。

## 狀態代碼和錯誤訊息 {#status-codes-and-error-messages}

在相關環境中可以看到下列狀態代碼：

* **200** （確定）

  傳回時間：

   * 透過`GET`請求內容片段
   * 透過`PUT`成功更新內容片段

* **201** （已建立）

  傳回時間：

   * 透過`POST`成功建立內容片段

* **404** （找不到）

  傳回時間：

   * 要求的內容片段不存在

* **500** （內部伺服器錯誤）

  >[!NOTE]
  >
  >系統會傳回此錯誤：
  >
  >* 當發生無法使用特定程式碼識別的錯誤時
  >* 當指定的裝載無效時

  以下列出傳回此錯誤狀態的常見案例，以及產生的錯誤訊息（等寬）：

   * 父資料夾不存在（透過`POST`建立內容片段時）
   * 未提供任何內容片段模型（缺少cq：model）、無法讀取（由於無效路徑或許可權問題）或沒有有效的片段模型：

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * 無法建立內容片段（可能是許可權問題）：

      * `Could not create content fragment`

   * 無法更新標題和/或說明：

      * `Could not set value on content fragment`

   * 無法設定中繼資料：

      * `Could not set metadata on content fragment`

   * 找不到內容元素或無法更新

      * `Could not update content element`
      * `Could not update fragment data of element`

  詳細的錯誤訊息會以下列方式傳回：

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

## API 參考 {#api-reference}

如需詳細的API參考資料，請參閱此處：

* [Adobe Experience Manager Assets API - 內容片段](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#available-features)

* 也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱：

* [Assets HTTP API檔案](/help/assets/mac-api-assets.md)
* [AEM Gem工作階段： OAuth](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-oauth-server-functionality-in-aem.html?lang=zh-Hant)
