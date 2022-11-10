---
title: AEM as a Cloud Service 中的快取
description: AEM as a Cloud Service 中的快取
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: e354443e4f21cd1bc61593b95f718fbb1126ea5a
workflow-type: tm+mt
source-wordcount: '2663'
ht-degree: 1%

---

# 簡介 {#intro}

流量會透過CDN傳遞至Apache Web伺服器層，該層支援模組，包括Dispatcher。 為了提高效能，Dispatcher主要用作快取，以限制發佈節點上的處理作業。
規則可套用至Dispatcher設定，以修改任何預設的快取過期設定，進而導致CDN快取。 請注意，若 `enableTTL` 在Dispatcher設定中啟用，表示即使在重新發佈的內容之外，也會重新整理特定內容。

本頁也說明Dispatcher快取失效的情形，以及快取在瀏覽器層級如何與用戶端程式庫搭配運作。

## 快取 {#caching}

### HTML/文字 {#html-text}

* 根據預設，由瀏覽器快取5分鐘， `cache-control` 由Apache層發出的標題。 CDN也會遵循此值。
* 可定義「 」，以停用預設的「HTML/文字」快取設定 `DISABLE_DEFAULT_CACHING` 變數 `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

例如，當您的業務邏輯需要微調年齡標題（具有以日曆日為基礎的值）時，這會很有用，因為預設情況下，年齡標題設定為0。 說了， **關閉預設快取時，請小心。**

* 可借由定義 `EXPIRATION_TIME` 變數 `global.vars` 使用AEMas a Cloud ServiceSDK Dispatcher工具。
* 可透過下列Apache，在更精細的層級上覆寫，包括獨立控制CDN和瀏覽器快取 `mod_headers` 指令：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >代理控制標題適用於Adobe管理的CDN。 若使用 [客戶管理的CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN)，視您的CDN提供者而定，可能需要不同的標題。

   設定全域快取控制標題或符合寬規則運算式的標題時，請務必小心，以免這些標題套用至您需要保留為私密的內容。 請考慮使用多個指令，以確保以微調方式套用規則。 如此一來，如果AEM as a Cloud Service偵測到快取標題已套用至它偵測到的Dispatcher無法執行的項目（如Dispatcher檔案所述），則會移除該快取標題。 若要強制AEM一律套用快取標題，您可以新增 **always** 選項，如下所示：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   您必須確定 `src/conf.dispatcher.d/cache` 有下列規則（預設設定中）:

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* 防止快取特定內容 **在CDN**，將「快取控制」標題設為 *私人*. 例如，下列項目會防止名為 **secure** 從CDN快取：

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >其他方法，包括 [dispatcher-ttl AEM ACS公域專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)，將不會成功覆寫值。

   >[!NOTE]
   >請注意，Dispatcher可能仍會根據自己的內容來快取內容 [快取規則](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html?lang=zh-Hant). 若要讓內容真正私密，您應確保Dispatcher不會快取內容。

### 用戶端資料庫(js,css) {#client-side-libraries}

* 使用AEM用戶端程式庫架構時，會產生JavaScript和CSS程式碼，讓瀏覽器可無限快取，因為任何變更都會以唯一路徑顯示為新檔案。  換句話說，會視需要產生參考用戶端資料庫的HTML，讓客戶在發佈新內容時能體驗新內容。 對於不遵守「不可變」值的舊版瀏覽器，快取控制項會設為「不可變」或30天。
* 請參閱區段 [用戶端程式庫與版本一致性](#content-consistency) 以取得其他詳細資訊。

### 影像和任何大到可以儲存在blob儲存體中的內容 {#images}

2022年5月中旬後建立之程式的預設行為(具體而言，針對高於65000的程式ID)是依預設快取，同時遵循要求的驗證內容。 預設情況下，較舊的程式(程式ID等於或低於65000)不會快取blob內容。

在這兩種情況下，您都可以使用Apache，在Apache/Dispatcher層以更精細的粒度層級覆寫快取標題 `mod_headers` 指令，例如：

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

修改Dispatcher層的快取標頭時，請小心不要快取得太廣，請參閱HTML/文字區段中的討論 [abos](#html-text). 此外，請確定原本保留為私密（而非快取）的資產不屬於 `LocationMatch` 指令篩選器。

#### 新預設快取行為 {#new-caching-behavior}

AEM層會根據快取標題是否已設定及請求類型的值，來設定快取標題。 請注意，如果未設定快取控制標題，則會快取公共內容，並將驗證的流量設為私密。 如果已設定快取控制標題，則快取標題將保持不變。

| 快取控制頭存在嗎？ | 請求類型 | AEM會將快取標題設為 |
|------------------------------|---------------|------------------------------------------------|
| 否 | 公共 | 快取控制：public, max-age=600，不可變 |
| 否 | 已驗證 | 快取控制：private, max-age=600，不可變 |
| 是 | 任何 | 未變 |

雖然不建議使用，但您可以設定Cloud Manager環境變數，以遵循舊行為(程式ID等於或低於65000)來變更新的預設行為 `AEM_BLOB_ENABLE_CACHING_HEADERS` 為false。

#### 舊的預設快取行為 {#old-caching-behavior}

依預設，AEM層不會快取blob內容。

>[!NOTE]
>建議您將Cloud Manager環境變數AEM_BLOB_ENABLE_CACHING_HEADERS設為true，將舊的預設行為變更為與新行為(程式ID高於65000)一致。 如果程式已上線，請確定在變更後，內容會如預期般運作。

>[!NOTE]
>其他方法，包括 [dispatcher-ttl AEM ACS公域專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)，將不會成功覆寫值。

### 節點儲存區中的其他內容檔案類型 {#other-content}

* 無預設快取
* 預設值不能設定為 `EXPIRATION_TIME` 用於html/文字檔案類型的變數
* 可借由指定適當的規則運算式來使用html/text區段中所述的相同LocationMatch策略來設定快取過期時間

### 進一步最佳化 {#further-optimizations}

* 避免使用 `User-Agent` 作為 `Vary` 頁首。 舊版的預設Dispatcher設定（在原型版本28之前）包含此項目，建議您使用下列步驟將其移除。
   * 在中找出vhost檔案 `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * 移除或註解行： `Header append Vary User-Agent env=!dont-vary` 從所有vhost檔案，但default.vhost除外，它為只讀
* 使用 `Surrogate-Control` 控制CDN快取的標頭與瀏覽器快取無關
* 考慮應用 [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) 和 [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) 指示允許後台刷新並避免快取丟失，使用戶能夠快速、新鮮地保存內容。
   * 有許多方法可以應用這些指令，但添加30分鐘 `stale-while-revalidate` 對所有快取控制標題而言，這是一個良好的起點。
* 下列是各種內容類型的範例，可在設定您自己的快取規則時作為指南。 請仔細考慮並測試您的特定設定和需求：

   * 快取12h的可變客戶端庫資源，12h後進行後台刷新。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取不可變的客戶端庫資源，長期（30天），並進行後台刷新，以避免MISS。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取HTML頁面5分鐘，在瀏覽器上1小時重新整理後，在CDN上12小時重新整理後。 一律會新增快取控制標題，因此請務必確保/content/*下的相符html頁面為公用頁面。 否則，請考慮使用更具體的規則運算式。

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取內容服務/Sling模型匯出工具json回應5分鐘，瀏覽器上需1小時背景重新整理，CDN上需12小時。

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 長期（30天）快取核心影像元件中不可變的URL，並進行背景重新整理，以避免遺漏。

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取來自DAM的可變資源（例如影像和視訊）,24小時後重新整理背景，以避免發生遺漏

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### HEAD請求行為 {#request-behavior}

在HEADCDN收到Adobe請求時， **not** 快取時，Dispatcher和/或AEM例項會轉換並接收該要求作為GET要求。 如果回應可快取，則會從CDN提供後續的HEAD要求。 如果回應無法快取，則後續的HEAD請求會在一段視乎 `Cache-Control` TTL。

### 行銷活動參數 {#marketing-parameters}

網站URL常包含用來追蹤促銷活動成功的促銷活動參數。 為了有效使用Dispatcher的快取，建議您設定Dispatcher設定的 `ignoreUrlParams` 屬性為 [記錄](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters).

此 `ignoreUrlParams` 區段必須取消註解，且應參考檔案 `conf.dispatcher.d/cache/marketing_query_parameters.any`，可透過取消註解與行銷管道相關參數對應的行來修改此欄。 您也可以新增其他參數。

```
/ignoreUrlParams {
{{ /0001 { /glob "*" /type "deny" }}}
{{ $include "../cache/marketing_query_parameters.any"}}
}
```

## Dispatcher快取失效 {#disp}

一般而言，Dispatcher快取無需失效。 當內容重新發佈時，您應該仰賴Dispatcher重新整理其快取，並仰賴附有快取過期標題的CDN。

### 啟動/停用期間Dispatcher快取失效 {#cache-activation-deactivation}

與舊版AEM一樣，發佈或取消發佈頁面會清除Dispatcher快取中的內容。 如果懷疑發生快取問題，客戶應重新發佈相關頁面，並確保有符合 `ServerAlias` localhost ，這是Dispatcher快取失效的必要項目。

當發佈例項從作者收到新版本的頁面或資產時，會使用排清代理程式使其Dispatcher上的適當路徑無效。 更新的路徑會從Dispatcher快取及其父項中移除，直到達到某個層級(您可以使用 [statfilelevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level))。

## Dispatcher快取的明確失效 {#explicit-invalidation}

Adobe建議依賴標準快取標題來控制內容傳送生命週期。 不過，如有需要，可以直接使Dispatcher中的內容無效。

下列清單包含您可能想明確使快取失效（同時選擇性地監聽失效的完成）的情況：

* 發佈體驗片段或內容片段等內容後，會使參考這些元素的已發佈和快取內容失效。
* 當引用的頁成功失效時通知外部系統。

有兩種方法可明確使快取無效：

* 偏好的做法是使用作者的Sling Content Distribution(SCD)。
* 使用復寫API來叫用發佈Dispatcher排清復寫代理程式。

這些方法在層可用性、重複事件的刪除能力以及事件處理保證方面各不相同。 下表總結了以下選項：

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>N/A</th>
    <th>層可用性</th>
    <th>重複資料刪除 </th>
    <th>擔保 </th>
    <th>動作 </th>
    <th>影響 </th>
    <th>說明 </th>
  </tr>  
  <tr>
    <td>Sling內容分送(SCD)API</td>
    <td>作者</td>
    <td>可能使用Discovery API或啟用 <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">去重複化模式</a>.</td>
    <td>至少一次。</td>
    <td>
     <ol>
       <li>新增</li>
       <li>刪除</li>
       <li>無效</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>分層/統計級別</li>
       <li>分層/統計級別</li>
       <li>僅級別資源</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>發佈內容並使快取失效。</li>
       <li>移除內容，使快取失效。</li>
       <li>不發佈內容即會讓內容失效。</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>復寫API</td>
    <td>發佈</td>
    <td>不可能，會在每個發佈執行個體上引發事件。</td>
    <td>盡力而為。</td>
    <td>
     <ol>
       <li>啟動</li>
       <li>停用</li>
       <li>刪除</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>分層/統計級別</li>
       <li>分層/統計級別</li>
       <li>分層/統計級別</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>發佈內容並使快取失效。</li>
       <li>從製作/發佈層級 — 移除內容並讓快取失效。</li>
       <li><p><strong>從作者階層</strong>  — 移除內容並讓快取失效（如果是從發佈代理程式的AEM製作層級觸發）。</p>
           <p><strong>從發佈層</strong>  — 僅讓快取失效（如果是從排清或僅限資源排清代理程式的AEM Publish層級觸發）。</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

請注意，與快取失效直接相關的兩個動作是Sling Content Distribution(SCD)API Invalidate和Replication API Deactivate。

此外，從桌上，我們觀察到：

* 每個事件都必須得到保證時，都需要SCD API，例如與需要精確知識的外部系統同步。 如果在無效呼叫時有發佈層級上調事件，則會在每個新發佈處理無效時引發額外的事件。

* 使用復寫API不是常見的使用案例，但應用於快取失效的觸發器來自發佈層級，而非製作層級的情況。 如果已設定Dispatcher TTL，此功能可能會很實用。

最後，如果您想要使Dispatcher快取失效，建議的選項是使用「作者」的「SCD API無效」動作。 此外，您也可以監聽事件，以便接著觸發進一步的下游動作。

### Sling內容分送(SCD) {#sling-distribution}

>[!NOTE]
>使用下列指示時，請注意，您應在AEM Cloud Service開發環境中測試自訂程式碼，而非在本機測試。

使用來自作者的SCD動作時，實作模式如下：

1. 在作者中撰寫自訂程式碼以叫用Sling內容分送 [API](https://sling.apache.org/documentation/bundles/content-distribution.html)，使用路徑清單傳遞無效動作：

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* （選擇性）接聽會反映所有Dispatcher例項已失效的資源的事件：


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

* （可選）在 `invalidated(String[] paths, String packageId)` 方法。

>[!NOTE]
>
>當Dispatcher失效時，不會清除AdobeCDN。 由Adobe管理的CDN會遵循TTL，因此不需要將其清除。

### 復寫API {#replication-api}

以下呈現使用復寫API停用動作時的實作模式：

1. 在發佈層級上，呼叫復寫API以觸發發佈Dispatcher排清復寫代理程式。

排清代理端點不可設定，而是預先設定為指向Dispatcher，與排清代理旁邊執行的發佈服務相符。

排清代理程式通常可由根據OSGi事件或工作流程的自訂程式碼觸發。

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals(“flush”);
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
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache isn't clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## 用戶端程式庫與版本一致性 {#content-consistency}

頁面由HTML、Javascript、CSS和影像組成。 鼓勵客戶利用 [用戶端程式庫(clientlibs)架構](/help/implementing/developing/introduction/clientlibs.md) 將Javascript和CSS資源匯入至HTML頁面，並考慮到JS程式庫之間的相依性。

clientlibs架構提供自動版本管理，這表示開發人員可以在原始碼控制中籤入JS程式庫的變更，而當客戶推播其版本時，將會提供最新版本。 若無此項功能，開發人員將需要手動變更HTML，並參考新版程式庫，如果許多HTML範本共用相同的程式庫，這特別麻煩。

當新版本的程式庫發行至生產環境時，會更新參考的HTML頁面，並附上這些更新程式庫版本的新連結。 指定HTML頁面的瀏覽器快取過期後，無論從瀏覽器快取載入舊程式庫，因為重新整理的頁面(從AEM)現在必定會參考新版本的程式庫。 換句話說，重新整理的HTML頁面將包含所有最新的程式庫版本。

此機制為序列化雜湊，會附加至用戶端程式庫連結，確保瀏覽器有唯一的版本化URL來快取CSS/JS。 只有當用戶端程式庫的內容變更時，才會更新序列化雜湊。 這表示即使是新部署，如果發生不相關的更新（即用戶端程式庫的基礎css/js未變更），參照仍會維持不變，確保減少瀏覽器快取的中斷。

### 啟用用戶端程式庫的長快取版本 — AEMas a Cloud ServiceSDK快速入門 {#enabling-longcache}

預設的clientlib包含在HTML頁面上，如下列範例所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

啟用嚴格的clientlib版本設定時，會新增長期雜湊金鑰作為選取器至用戶端程式庫。 因此，clientlib參考如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

所有AEMas a Cloud Service環境預設會啟用嚴格的clientlib版本設定。

若要在本機SDK快速入門中啟用嚴格的clientlib版本設定，請執行下列動作：

1. 導覽至OSGi Configuration manager `<host>/system/console/configMgr`
1. 尋找AdobeGraniteHTML程式庫管理員的OSGi設定：
   * 勾選核取方塊以啟用嚴格版本設定
   * 在標示為Long term用戶端快取金鑰的欄位中，輸入/值。*；雜湊
1. 儲存變更。不必將此配置保存在原始碼控制中，因為AEM as a Cloud Service會自動在開發、預備和生產環境中啟用此配置。
1. 每次變更用戶端程式庫的內容時，都會產生新的雜湊金鑰，並更新HTML參考。
