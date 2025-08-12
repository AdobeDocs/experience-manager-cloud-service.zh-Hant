---
title: AEM as a Cloud Service 中的快取
description: 瞭解AEM as a Cloud Service中的快取基本概念
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '3071'
ht-degree: 1%

---

# 簡介 {#intro}

流量會透過CDN傳遞至Apache網頁伺服器層，其支援Dispatcher等模組。 為了提高效能，Dispatcher主要用作快取，以限制發佈節點上的處理作業。
規則可以套用至Dispatcher設定，以修改任何預設的快取逾期設定，從而在CDN上產生快取。 如果在Dispatcher設定中啟用了`enableTTL`，Dispatcher也會遵守產生的快取過期標頭，這表示它重新整理特定內容，即使重新發佈的內容除外。

本頁也說明Dispatcher快取如何失效，以及在瀏覽器層級如何針對使用者端程式庫執行快取。

## 快取 {#caching}

AEM as a Cloud Service CDN中HTTP回應的快取是由以下來自來源的HTTP回應標題所控制： `Cache-Control`、`Surrogate-Control`或`Expires`。

這些快取標頭通常在使用mod_headers的AEM Dispatcher vhost設定中設定，但也可以在AEM Publish本身中執行的自訂Java™程式碼中設定（請參閱[如何啟用CDN快取](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/caching/how-to/enable-caching)）。

CDN資源的快取索引鍵包含完整的請求url，包括查詢引數，因此每個不同的查詢引數都會產生不同的快取專案。 請考慮移除不要的查詢引數；[請參閱下文](#marketing-parameters)以改進快取命中率。

AEM as a Cloud Service的CDN不會快取`private`中包含`no-cache`、`no-store`或`Cache-Control`的原始回應（如需詳細資訊，請參閱[如何停用CDN快取](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/caching/how-to/disable-caching)）。  此外，設定Cookie （即具有`Set-Cookie`回應標題）的回應不會由CDN快取。

### HTML/文字 {#html-text}

Dispatcher設定會為`text/html`內容型別設定一些預設的快取標頭。

* 根據預設，瀏覽器會根據Apache圖層發出的`cache-control`標頭快取5分鐘。 CDN也會遵守此值。
* 可在`DISABLE_DEFAULT_CACHING`中定義`global.vars`變數，以停用預設的HTML/文字快取設定：

```
Define DISABLE_DEFAULT_CACHING
```

例如，當您的商業邏輯需要微調年齡標題（具有以行事曆日期為基準的值）時，此方法很有用，因為依預設，年齡標題設為0。 也就是說，**關閉預設快取時要小心。**

* 可以使用AEM as a Cloud Service SDK Dispatcher工具在`EXPIRATION_TIME`中定義`global.vars`變數，以覆寫所有HTML/文字內容。
* 可以使用下列Apache `mod_headers`指令在較精細的層級上覆寫，包括獨立控制CDN和瀏覽器快取：

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header set Cache-Control "max-age=200"
       Header set Surrogate-Control "max-age=3600"
       Header set Age 0
  </LocationMatch>
  ```

  >[!NOTE]
  >Surrogate-Control標頭會套用至Adobe管理的CDN。 如果使用[客戶管理的CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=zh-Hant#point-to-point-CDN)，則視您的CDN提供者而定，可能需要不同的標頭。

  設定全域快取控制標頭或符合寬範圍Regex的類似快取標頭時，請務必謹慎，以免套用至必須私人儲存的內容。 請考慮使用多個指示，以確保以微調的方式套用規則。 如此一來，如果AEM as a Cloud Service偵測到快取標題已套用至偵測到Dispatcher無法快取的專案，則會移除快取標題，如Dispatcher檔案所述。 若要強制AEM一律套用快取標頭，您可以新增&#x200B;**`always`**&#x200B;選項，如下所示：

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header unset Cache-Control
       Header unset Expires
       Header always set Cache-Control "max-age=200"
       Header set Age 0
  </LocationMatch>
  ```

  請確定`src/conf.dispatcher.d/cache`下的檔案有下列規則（在預設設定中）：

  ```
  /0000
  { /glob "*" /type "allow" }
  ```

* 若要防止在CDN **快取特定內容**，請將Cache-Control標頭設定為&#x200B;*private*。 例如，下列專案可防止在CDN快取名為&#x200B;**secure**&#x200B;的目錄下的html內容：

  ```
     <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
     Header unset Cache-Control
     Header unset Expires
     Header always set Cache-Control "private"
    </LocationMatch>
  ```

* 雖然CDN不會快取設定為私用的HTML內容，但若已設定[許可權敏感型快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hant)，則可以在Dispatcher快取該內容，以確保只有授權的使用者才能獲得該內容。

  >[!NOTE]
  >其他方法(包括[Dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))無法成功覆寫值。

  >[!NOTE]
  >Dispatcher可能仍會根據自己的[快取規則](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html?lang=zh-Hant)快取內容。 若要讓內容確實為私人，請確保Dispatcher不會快取內容。

### 使用者端資料庫(js，css) {#client-side-libraries}

* 使用AEM的使用者端程式庫架構時，JavaScript和CSS程式碼的產生方式會讓瀏覽器無限期快取它，因為任何變更都會顯示為具有唯一路徑的新檔案。 換言之，會視需要產生參考使用者端資料庫的HTML，讓客戶在發佈新內容時能夠體驗這些內容。 若舊版瀏覽器不遵循「不可變」值，則快取控制設為「不可變」，或設為30天。
* 如需其他詳細資訊，請參閱[使用者端程式庫和版本一致性](#content-consistency)一節。

### 影像和任何足以儲存在Blob儲存空間中的內容 {#images}

對於2022年5月中旬之後建立的計畫(特別是高於65000的計畫ID)，預設行為是快取，同時遵循請求的驗證上下文。 舊版程式(程式id等於或小於65000)預設不會快取blob內容。

在這兩種情況下，都可以使用Apache `mod_headers`指令在Apache/Dispatcher層的較精細層級上覆寫快取標題，例如：

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

在Dispatcher層修改快取標題時，請留意不要快取太廣泛。 請參閱HTML/文字區段[以上](#html-text)中的討論內容。 此外，請確定原本要保持私密狀態（而非快取）的資產不屬於`LocationMatch`指示詞篩選條件的一部分。

儲存在Blob存放區中的JCR資源（大於16KB）通常可由AEM做為302重新導向。 這些重新導向會遭到攔截並隨後導向CDN，而內容會直接從blob存放區傳送。 在這些回應中只能自訂有限的標題集。 例如，若要自訂`Content-Disposition`，您應該使用Dispatcher指示詞，如下所示：

```
<LocationMatch "\.(?i:pdf)$">
  ForceType application/pdf
  Header set Content-Disposition inline
  </LocationMatch>
```

可在blob回應上自訂的標頭清單為：

```
content-security-policy
x-frame-options
x-xss-protection
x-content-type-options
x-robots-tag
access-control-allow-origin
content-disposition
permissions-policy
referrer-policy
x-vhost
content-disposition
cache-control
vary
```

#### 新的預設快取行為 {#new-caching-behavior}

AEM層會根據是否已設定快取標題及請求型別的值來設定快取標題。 如果未設定快取控制標題，則會快取公開內容，且驗證的流量會設為私人。 如果設定了快取控制標題，則快取標題保持不變。

| 快取控制標頭是否存在？ | 請求類型 | AEM將快取標頭設為 |
|------------------------------|---------------|------------------------------------------------|
| 否 | 公共 | Cache-Control： public， max-age=600，不可變 |
| 否 | 已驗證 | Cache-Control： private， max-age=600，不可變 |
| 是 | 任何 | 未變更 |

雖然不建議使用，但您可以將Cloud Manager環境變數`AEM_BLOB_ENABLE_CACHING_HEADERS`設定為false，以變更新的預設行為，使其遵循舊有的行為(程式id等於或低於65000)。

#### 較舊的預設快取行為 {#old-caching-behavior}

AEM層預設不會快取blob內容。

>[!NOTE]
>將Cloud Manager環境變數AEM_BLOB_ENABLE_CACHING_HEADERS設定為true，以將較舊的預設行為變更為與新的行為(高於65000的程式ID)一致。 如果程式已上線，請務必確認在變更後，內容會如預期般運作。

現在，無法使用[許可權敏感型快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hant)，在Dispatcher快取標示為私用的Blob儲存體中的影像。 系統會一律向AEM來源要求影像，並在使用者獲得授權時提供影像。

>[!NOTE]
>其他方法(包括[dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))無法成功覆寫值。

### 節點存放區中的其他內容檔案型別 {#other-content}

* 無預設快取
* 無法以用於html/文字檔案型別的`EXPIRATION_TIME`變數設定預設值
* 透過指定適當的規則運算式，可以使用html/text一節中所述的相同LocationMatch策略來設定快取有效期

### 進一步最佳化 {#further-optimizations}

* 避免使用`User-Agent`做為`Vary`標頭的一部分。 舊版預設Dispatcher設定（原型版本28之前）包含該功能，Adobe建議您透過以下步驟將其移除。
   * 在`<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`中找到vhost檔案
   * 從所有vhost檔案中移除或註解行： `Header append Vary User-Agent env=!dont-vary`，但default.vhost為唯讀檔案除外
* 使用`Surrogate-Control`標頭可獨立於瀏覽器快取控制CDN快取
* 請考慮套用[`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate)和[`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error)指示詞，以允許背景重新整理並避免快取遺漏，讓使用者能夠快速且新鮮地儲存您的內容。
   * 有許多方式可套用這些指示，但將30分鐘的`stale-while-revalidate`新增至所有快取控制標題是很好的起點。
* 以下是各種內容型別的範例，在設定自己的快取規則時，這些範例可作為指南。 請仔細考慮並測試您的特定設定和需求：

   * 快取可變的使用者端程式庫資源達12小時，並在12小時後重新整理背景。

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 透過背景重新整理來快取不可變的使用者端程式庫資源長期（30天）以避免遺漏。

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 在瀏覽器上快取HTML頁面5分鐘，並在背景重新整理1小時，在CDN上重新整理12小時。 請一律新增Cache-Control標頭，因此請務必確保/content/*底下相符的html頁面為公開頁面。 如果沒有，請考慮使用更具體的規則運算式。

     ```
     <LocationMatch "^/content/.*\.html$">
        Header unset Cache-Control
        Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 快取內容服務/Sling模型匯出程式json回應達5分鐘，瀏覽器背景重新整理一小時，CDN背景重新整理十二小時。

     ```
     <LocationMatch "^/content/.*\.model\.json$">
        Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 使用背景重新整理來長期（30天）快取核心影像元件中的不可變URL，以避免MISS。

     ```
     <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 快取來自DAM的可變資源（例如影像和影片）24小時，並在12小時後重新整理背景以避免遺漏。

     ```
     <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

### 分析CDN快取命中率 {#analyze-chr}

請參閱[快取命中率分析教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/caching/cdn-cache-hit-ratio-analysis.html?lang=zh-Hant)，以取得有關使用儀表板下載CDN記錄檔和分析網站快取命中率的資訊。

### HEAD請求行為 {#request-behavior}

在Adobe CDN收到&#x200B;**非**&#x200B;快取之資源的HEAD要求時，該要求會轉換並由Dispatcher及/或AEM執行個體接收為GET要求。 如果回應可快取，則會從CDN提供後續HEAD請求。 如果回應無法快取，則會在`Cache-Control` TTL所依賴的時間內，將後續HEAD要求傳遞至Dispatcher或AEM執行個體或兩者。

### 行銷活動引數 {#marketing-parameters}

網站URL常包含用來追蹤促銷活動成功的行銷活動引數。

對於在2023年10月或之後建立的環境，為了更好的快取要求，CDN將移除常見的行銷相關查詢引數，特別是符合下列規則運算式模式的引數：

```
^(utm_.*|gclid|gdftrk|_ga|mc_.*|trk_.*|dm_i|_ke|sc_.*|fbclid|msclkid|ttclid)$
```

可以使用`requestTransformations`CDN設定[中的](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations)旗標來開啟或關閉此功能。

例如，若要停止移除CDN層級一的行銷引數，應使用包含下列區段的設定來部署`removeMarketingParams: false`。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  requestTransformations:
    removeMarketingParams: false
```

如果CDN層級的`removeMarketingParams`功能已停用，仍建議設定Dispatcher設定的`ignoreUrlParams`屬性；請參閱[設定Dispatcher — 忽略URL引數](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#ignoring-url-parameters)。

忽略行銷引數有兩種可能性。 （其中第一個偏好使用查詢引數來忽略防快取）：

1. 忽略所有引數，並選擇性地允許使用的引數。
在下列範例中，只有`page`和`product`引數不會被忽略，而且請求將轉送給發佈者。

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "allow" }
   /0002 { /glob "page" /type "deny" }
   /0003 { /glob "product" /type "deny" }
}
```

1. 允許行銷引數以外的所有引數。 檔案[marketing_query_parameters.any](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.dispatcher.d/cache/marketing_query_parameters.any)定義了將被忽略的常用行銷引數清單。 Adobe不會更新此檔案。 使用者可依其行銷提供者來擴充。

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   $include "../cache/marketing_query_parameters.any"
}
```


## Dispatcher快取失效 {#disp}

一般而言，不需要讓Dispatcher快取失效。 實際上，您應該仰賴Dispatcher在內容重新發佈時重新整理其快取，以及CDN遵循快取到期標頭。

### 在啟用/停用期間Dispatcher快取失效 {#cache-activation-deactivation}

和舊版AEM一樣，發佈或取消發佈頁面會從Dispatcher快取中清除內容。 如果懷疑有快取問題，您應重新發佈有問題的頁面，並確保有可用的虛擬主機符合Dispatcher快取失效所需的`ServerAlias` localhost。

>[!NOTE]
>為正確使Dispatcher失效，請確定來自「127.0.0.1」、「localhost」、「\*.local」、「\*.adobeaemcloud.com」和「\*.adobeaemcloud.net」的請求都符合，並由vhost設定處理，以便可以提供請求。 您可以依照參考[AEM原型](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost)中的模式，在全域比對「*」的全域vhost設定中執行此工作。 或者，您也可以確保前述清單是由其中一個主機擷取。

當發佈執行個體收到來自作者的新版本頁面或資產時，會使用排清代理程式來使其Dispatcher上的適當路徑失效。 更新的路徑會連同其父項一起從Dispatcher快取中移除，直到某個層級（您可以使用[statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant#invalidating-files-by-folder-level)設定此層級）。

## Dispatcher快取明確失效 {#explicit-invalidation}

Adobe建議您仰賴標準快取標題來控制內容傳送生命週期。 不過，如有需要，可直接在Dispatcher中讓內容失效。

下列清單包含您想要明確讓快取失效的情況（同時選擇性地接聽讓失效完成）：

* 發佈體驗片段或內容片段等內容後，讓參考這些元素的已發佈和快取內容失效。
* 在參照的頁面成功失效時通知外部系統。

有兩種方式可明確讓快取失效：

* 偏好使用的方法是使用Author的Sling Content Distribution (SCD)。
* 另一種方法是使用復寫API來叫用發佈Dispatcher排清復寫代理程式。

方法因階層可用性、去除重複事件的能力及事件處理保證而異。 下表總結了這些選項：

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>不適用</th>
    <th>階層可用性</th>
    <th>重複資料刪除 </th>
    <th>保證 </th>
    <th>動作 </th>
    <th>影響 </th>
    <th>說明 </th>
  </tr>  
  <tr>
    <td>Sling內容發佈(SCD) API</td>
    <td>作者</td>
    <td>可能使用探索API或啟用<a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">重複資料刪除模式</a>。</td>
    <td>至少一次。</td>
    <td>
     <ol>
       <li>新增</li>
       <li>刪除</li>
       <li>失效</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>階層/統計層級</li>
       <li>階層/統計層級</li>
       <li>僅層次資源</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>發佈內容並讓快取失效。</li>
       <li>移除內容並讓快取失效。</li>
       <li>讓內容失效而不發佈。</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>復寫API</td>
    <td>發佈</td>
    <td>不可能，事件會在每個發佈執行個體上引發。</td>
    <td>盡力而為。</td>
    <td>
     <ol>
       <li>啟用</li>
       <li>停用</li>
       <li>刪除</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>階層/統計層級</li>
       <li>階層/統計層級</li>
       <li>階層/統計層級</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>發佈內容並讓快取失效。</li>
       <li>從作者/發佈層 — 移除內容並使快取失效。</li>
       <li><p><strong>從作者階層</strong> — 移除內容並使快取失效(如果從發佈代理程式上的AEM作者階層觸發)。</p>
           <p><strong>從發佈階層</strong> — 僅讓快取失效(若是從Flush或Resource-only-flush代理程式上的AEM發佈階層觸發)。</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

與快取失效直接相關的兩個動作是Sling內容發佈(SCD) API失效和復寫API停用。

此外，從表格中，您可以觀察到：

* 當每個事件都必須得到保證時（例如，與需要精確知識的外部系統同步），就需要SCD API。 如果在失效呼叫時存在發佈層級升級事件，則在每個新發佈處理失效時會引發額外事件。

* 使用復寫API不是常見的使用案例，但可用於讓快取失效的觸發器來自發佈層級，而非製作層級的情況。 如果已設定Dispatcher TTL，此方法可能會相當實用。

總而言之，如果您想要讓Dispatcher快取失效，建議的選項是使用Author的SCD API失效動作。 此外，您也可以接聽事件，以便觸發後續的下游動作。

### Sling內容發佈(SCD) {#sling-distribution}

>[!NOTE]
>使用下列指示時，請在AEM雲端服務開發環境中測試自訂程式碼，而不是在本機測試。

使用Author的SCD動作時，實施模式如下：

1. 從Author撰寫自訂程式碼以叫用Sling內容發佈[API](https://sling.apache.org/documentation/bundles/content-distribution.html)，透過路徑清單傳遞失效動作：

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* （可選）接聽反映所有Dispatcher執行個體失效之資源的事件：


```
package org.apache.sling.distribution.journal.shared;

import org.apache.sling.discovery.DiscoveryService;
import org.apache.sling.distribution.journal.impl.event.DistributionEvent;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static org.apache.sling.distribution.DistributionRequestType.INVALIDATE;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_PATHS;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_TYPE;
import static org.apache.sling.distribution.event.DistributionEventTopics.AGENT_PACKAGE_DISTRIBUTED;
import static org.osgi.service.event.EventConstants.EVENT_TOPIC;

@Component(immediate = true, service = EventHandler.class, property = {
        EVENT_TOPIC + "=" + AGENT_PACKAGE_DISTRIBUTED
})
public class InvalidatedHandler implements EventHandler {
    private static final Logger LOG = LoggerFactory.getLogger(InvalidatedHandler.class);

    @Reference
    private DiscoveryService discoveryService;

    @Override
    public void handleEvent(Event event) {

        String distributionType = (String) event.getProperty(DISTRIBUTION_TYPE);

        if (INVALIDATE.name().equals(distributionType)) {
            boolean isLeader = discoveryService.getTopology().getLocalInstance().isLeader();
            // process the OSGi event on the leader author instance
            if (isLeader) {
                String[] paths = (String[]) event.getProperty(DISTRIBUTION_PATHS);
                String packageId = (String) event.getProperty(DistributionEvent.PACKAGE_ID);
                invalidated(paths, packageId);
            }
        }
    }

    private void invalidated(String[] paths, String packageId) {
        // custom logic
        LOG.info("Successfully applied package with id {}, paths {}", packageId, paths);
    }
}
```

<!-- Optionally, instead of using the isLeader approach, one could add an OSGi configuration for the PID org.apache.sling.distribution.journal.impl.publisher.DistributedEventNotifierManager and property deduplicateEvent=true. But we'll stick with just one strategy and not mention it (double-check this).**review this**-->

* （選擇性）在上述`invalidated(String[] paths, String packageId)`方法中執行商業邏輯。

>[!NOTE]
>
>Dispatcher失效時，不會排清Adobe CDN。 Adobe管理的CDN遵守TTL，因此不需要清除。

### 復寫API {#replication-api}

以下顯示的是使用復寫API停用動作時的實作模式：

1. 在發佈層上，呼叫復寫API以觸發發佈Dispatcher Flush復寫代理程式。

無法設定排清代理程式端點，而是預先設定為指向Dispatcher，與隨排清代理程式執行的發佈服務相符。

排清代理程式通常可由根據OSGi事件或工作流程的自訂程式碼觸發。

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals("flush");
  }
});

Replicator.replicate (session,ReplicationActionType.DELETE,paths, options);
```

<!-- In general, it will not be necessary to manually invalidate content in the dispatcher, but it is possible if needed.

>[!NOTE]
>Prior to AEM as a Cloud Service, there were two ways of invalidating the dispatcher cache.
>
>1. Invoke the replication agent, specifying the publish dispatcher flush agent
>2. Directly calling the `invalidate.cache` API (for example, `POST /dispatcher/invalidate.cache`)
>
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=zh-Hant) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache is not clearing, contact [customer support](https://helpx.adobe.com/tw/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/tw/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## 使用者端程式庫和版本一致性 {#content-consistency}

頁面由HTML、JavaScript、CSS和影像組成。 建議客戶使用[使用者端資料庫(clientlibs)架構](/help/implementing/developing/introduction/clientlibs.md)，將JavaScript和CSS資源匯入HTML頁面，並考慮JS資料庫之間的相依性。

clientlibs架構提供自動版本管理。 這表示開發人員可以在原始檔控制中籤入JS程式庫的變更，而且當客戶推送其版本時，就可以使用最新版本。 若沒有此工作流程，開發人員必須透過參考新版程式庫手動變更HTML，若相同程式庫共用許多HTML範本，情況會特別麻煩。

當新版本的程式庫發行至生產環境時，會更新參考HTML頁面的連結，其中包含已更新程式庫版本的新連結。 在指定HTML頁面的瀏覽器快取過期後，就不需要擔心舊程式庫會從瀏覽器快取載入。 原因是因為重新整理的頁面(來自AEM)現在保證會參照資料庫的新版本。 也就是說，重新整理的HTML頁面會包含所有最新程式庫版本。

此功能背後的機制是序列化雜湊，會附加至使用者端程式庫連結。 這可確保瀏覽器擁有版本控制的唯一URL來快取CSS/JS。 只有在使用者端程式庫的內容變更時，才會更新序列化雜湊。 這表示如果發生不相關的更新（也就是說，不會變更使用者端程式庫的基礎css/js），即使使用新部署，參照仍會維持不變。 反過來，它可確保對瀏覽器快取的中斷較少。

### 啟用使用者端程式庫的Longcache版本 — AEM as a Cloud Service SDK快速入門 {#enabling-longcache}

HTML頁面上的預設clientlib包含看起來像以下範例：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

啟用嚴格的clientlib版本設定時，會將長期雜湊金鑰作為選取器新增至使用者端程式庫。 因此，clientlib參照看起來像這樣：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

依預設，所有AEM as a Cloud Service環境中都會啟用嚴格clientlib版本設定。

若要在本機SDK快速入門中啟用嚴格的clientlib版本設定，請執行以下操作：

1. 瀏覽至OSGi Configuration管理員`<host>/system/console/configMgr`
1. 尋找Adobe Granite HTML Library Manager的OSGi設定：
   * 核取核取方塊，以啟用嚴格版本設定
   * 在標示為&#x200B;**長期使用者端快取金鑰**&#x200B;的欄位中，輸入/的值。*；雜湊
1. 儲存變更。 不需要在原始檔控制中儲存此設定，因為AEM as a Cloud Service會自動在開發、中繼和生產環境中啟用此設定。
1. 只要使用者端資料庫的內容有所變更，就會產生新的雜湊金鑰並更新HTML參考。
