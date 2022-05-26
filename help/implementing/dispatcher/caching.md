---
title: AEM as a Cloud Service 中的快取
description: 'AEM as a Cloud Service 中的快取 '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 58999e2aec2f9decaa55554c9488967b70701522
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 簡介 {#intro}

流量通過CDN傳遞到apache Web伺服器層，該層支援包括調度程式的模組。 為了提高效能，調度器主要用作快取以限制對發佈節點的處理。
規則可應用於調度程式配置以修改任何預設快取過期設定，從而導致在CDN中快取。 請注意，如果 `enableTTL` 在調度程式配置中啟用，這意味著即使在重新發佈的內容之外，它也會刷新特定內容。

本頁還介紹如何使調度程式快取無效，以及在瀏覽器級別對客戶端庫的快取工作。

## 快取 {#caching}

### HTML/文本 {#html-text}

* 預設情況下，由瀏覽器快取5分鐘，基於 `cache-control` apache層發出的標頭。 CDN也尊重此值。
* 可通過定義以下項來禁用預設HTML/文本快取設定 `DISABLE_DEFAULT_CACHING` 變數 `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

例如，當您的業務邏輯需要對帳齡標題（具有基於日曆日的值）進行微調時，這可能很有用，因為預設情況下帳齡標題設定為0。 也就是說， **關閉預設快取時，請小心。**

* 可通過定義所有HTML/文本內容來覆蓋 `EXPIRATION_TIME` 變數 `global.vars` 使用AEMas a Cloud ServiceSDK Dispatcher工具。
* 可以在更精細的粒度級別上覆蓋，包括使用以下apache mod_headers指令獨立控制CDN和瀏覽器快取：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >Surgote-Control標頭應用於Adobe管理的CDN。 如果使用 [客戶管理的CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN)，根據您的CDN提供程式，可能需要不同的標頭。

   在設定全局快取控制標頭或與寬規則運算式匹配的標頭時，請小心謹慎，以使這些標頭不會應用於您可能希望保持私有的內容。 考慮使用多個指令來確保以細粒度方式應用規則。 使用這種方法AEM，如果as a Cloud Service檢測到快取報頭已應用到它檢測到的調度程式無法執行的內容，則它將刪除快取報頭，如調度程式文檔中所述。 為了強制始終AEM應用快取頭，您可以添加 **總是** 選項：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   必須確保檔案 `src/conf.dispatcher.d/cache` 具有以下規則（預設配置中）:

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* 防止快取特定內容 **在CDN**，將Cache-Control頭設定為 *私*。 例如，以下操作會阻止名為的目錄下的html內容 **安全** 從CDN快取：

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >其他方法，包括 [dispatcher-ttl AEM ACS Commons項目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)，將無法成功覆蓋值。

   >[!NOTE]
   >請注意，調度程式可能仍會根據其自己的內容快取內容 [快取規則](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html)。 要使內容真正私有，您應確保該內容不由調度程式進行快取。

### 客戶端庫(js,css) {#client-side-libraries}

* 通過使用AEM客戶端庫框架，JavaScript和CSS代碼的生成方式使瀏覽器可以無限期地快取它，因為任何更改都以具有唯一路徑的新檔案的形式顯示。  換句話說，將根據需要生成引用客戶端庫的HTML，以便客戶在發佈新內容時能夠體驗新內容。 對於不尊重「不可變」值的較舊瀏覽器，快取控制設定為「不可變」或30天。
* 請參閱一節 [客戶端庫和版本一致性](#content-consistency) 的雙曲餘切值。

### 影像和任何大到可以儲存在blob儲存中的內容 {#images}

預設情況下，2022年5月中旬後建立的程式（具體來說，對於高於65000的程式ID）的預設行為是快取，同時也尊重請求的驗證上下文。 預設情況下，較舊的程式（程式ID等於或低於65000）不快取blob內容。

在這兩種情況下，可以使用apache在apache/dispatcher層的更細粒度級別上覆蓋快取頭 `mod_headers` 指令，例如：

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

在調度器層修改快取標頭時，請小心不要快取太廣，請參閱HTML/文本部分中的討論 [上](#html-text)。 另外，確保本應保持私有（而非快取）的資產不屬於 `LocationMatch` 指令篩選器。

#### 新建預設快取行為 {#new-caching-behavior}

層AEM將根據是否已設定快取標頭和請求類型的值來設定快取標頭。 請注意，如果未設定快取控制標頭，則公共內容將被快取，並且已驗證的通信將設定為專用。 如果已設定快取控制標頭，則快取標頭將保持不變。

| 是否存在快取控制標頭？ | 請求類型 | AEM將快取頭設定為 |
|------------------------------|---------------|------------------------------------------------|
| 否 | 公共 | 快取控制：public, max-age=600，不可變 |
| 否 | 已驗證 | 快取控制：private,max-age=600，不可變 |
| 是 | 任何 | 不變 |

雖然不推薦，但可以通過設定Cloud Manager環境變數來更改新預設行為以遵循較舊行為（程式ID等於或低於65000） `AEM_BLOB_ENABLE_CACHING_HEADERS` 錯誤。

#### 較舊的預設快取行為 {#old-caching-behavior}

預設AEM情況下，該層不會快取blob內容。

>[!NOTE]
>建議通過將Cloud Manager環境變數AEM_BLOB_ENABLE_CACHING_HEADERS設定為true，將舊預設行為更改為與新行為（程式ID高於65000）一致。 如果程式已在運行，請確保在更改後內容的行為與預期一致。

>[!NOTE]
>其他方法，包括 [dispatcher-ttl AEM ACS Commons項目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)，將無法成功覆蓋值。

### 節點儲存中的其他內容檔案類型 {#other-content}

* 無預設快取
* 不能使用 `EXPIRATION_TIME` 用於html/text檔案類型的變數
* 通過指定適當的regex，可以使用html/text節中描述的相同LocationMatch策略來設定快取過期

### 進一步優化 {#further-optimizations}

* 避免使用 `User-Agent` 作為 `Vary` 標題。 預設調度程式設定的較舊版本（早於原型版本28）包括了這一點，我們建議您使用以下步驟刪除該設定。
   * 在中查找vhost檔案 `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * 刪除或注釋掉行： `Header append Vary User-Agent env=!dont-vary` 從所有vhost檔案中，預設為vhost，該值為只讀
* 使用 `Surrogate-Control` 控制獨立於瀏覽器快取的CDN快取的報頭
* 考慮應用 [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) 和 [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) 指令，允許後台刷新並避免快取未命中，使用戶能夠保持內容快速、新鮮。
   * 應用這些指令有多種方法，但需要添加30分鐘 `stale-while-revalidate` 到所有快取控制標頭是一個良好的起點。
* 下面是各種內容類型的一些示例，在設定自己的快取規則時，這些內容可作為指南。 請仔細考慮並test您的特定設定和要求：

   * 快取可變客戶端庫資源，12h後進行後台刷新。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取不可變的客戶端庫資源，具有後台刷新，可長期（30天），以避免MISS。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取HTML頁面5分鐘，後台刷新1h（在瀏覽器上）,CDN上刷新12h。 始終會添加Cache-Control標頭，因此必須確保/content/*下的匹配html頁面是公開的。 否則，請考慮使用更具體的規則運算式。

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取內容服務/Sling模型導出器json響應，時間為5分鐘，後台刷新時間為瀏覽器1h,CDN為12h。

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 通過後台刷新，從核心映像元件中長期（30天）快取不可變的URL，以避免MISS。

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 快取DAM中可變資源（如影像和視頻）,24小時後進行背景刷新，以避免MISS

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### HEAD請求行為 {#request-behavior}

當在HEADCDN上接收到Adobe請求時， **不** 快取，該請求被調度器和/或實例轉換和接AEM收作為GET請求。 如果響應是可快取的，則將從CDN提供後續HEAD請求。 如果響應不可快取，則後續HEAD請求將在一段時間內被傳遞AEM給調度程式和/或實例，該時間段取決於 `Cache-Control` TTL。

## Dispatcher快取無效 {#disp}

通常，不必使調度程式快取無效。 相反，在內容重新發佈時，您應依靠調度程式刷新其快取，而CDN則遵守快取過期報頭。

### 激活/停用期間Dispatcher快取無效 {#cache-activation-deactivation}

與以前版本的AEM頁面一樣，發佈或取消發佈頁面將從調度程式快取中清除內容。 如果懷疑存在快取問題，客戶應重新發佈有問題的頁面，並確保虛擬主機與ServerAlias localhost匹配，而ServerAlias localhost是調度程式快取失效所必需的。


當發佈實例從作者處收到頁面或資產的新版本時，它使用刷新代理使其調度程式上的適當路徑無效。 更新的路徑將從調度程式快取及其父快取中刪除到一個級別(您可以使用 [statfilesel（狀態檔案級）](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)。

### 顯式調度程式快取失效 {#explicit-invalidation}

通常，不需要手動使調度程式中的內容無效，但如果需要，可能會使其無效。

>[!NOTE]
>在AEMas a Cloud Service之前，有兩種方法使調度程式快取無效。
>
>1. 調用複製代理，指定發佈調度程式刷新代理
>2. 直接調用 `invalidate.cache` API(例如， `POST /dispatcher/invalidate.cache`)

>
>調度員的 `invalidate.cache` 不再支援API方法，因為它只針對特定的調度程式節點。 AEMas a Cloud Service在服務級別運行，而不是單個節點級別，因此 [取消驗證快取頁AEM面](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) 頁面對AEMas a Cloud Service無效

應使用複製刷新代理。 可以使用 [複製API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html)。 刷新代理終結點不可配置，但已預配置為指向調度程式，與運行刷新代理的發佈服務匹配。 刷新代理通常可由OSGi事件或工作流觸發。

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 
-->

下圖說明了這一點。

![CDN](assets/cdnd.png "CDN")

如果擔心調度程式快取未清除，請與 [客戶支援](https://helpx.adobe.com/support.ec.html) 如果需要，可以刷新調度程式快取。

Adobe管理的CDN考慮TTL，因此不需要刷新它。 如果有問題， [聯繫客戶支援](https://helpx.adobe.com/support.ec.html) 支援，他們可以根據需要刷新Adobe管理的CDN快取。

## 客戶端庫和版本一致性 {#content-consistency}

頁面由HTML、Javascript、CSS和影像組成。 鼓勵客戶利用 [客戶端庫（客戶端庫）框架](/help/implementing/developing/introduction/clientlibs.md) 將Javascript和CSS資源導入到HTML頁中，同時考慮JS庫之間的依賴關係。

客戶端庫框架提供自動版本管理，這意味著開發人員可以在原始碼管理中籤入對JS庫的更改，並且當客戶推送其版本時，將提供最新版本。 如果沒有這一點，開發人員將需要手動更改引用新版本庫的HTML，如果許多HTML模板共用同一庫，則這一點特別困難。

當將庫的新版本發佈到生產版本時，將使用指向這些更新的庫版本的新連結更新引用HTML頁。 一旦給定HTML頁的瀏覽器快取已過期，就不會擔心舊庫將從瀏覽器快取中載入，因為現在保證刷新頁面(從AEM)引用庫的新版本。 換句話說，刷新的HTML頁將包括所有最新的庫版本。

這種機制是序列化散列，附加到客戶端庫連結，確保瀏覽器有一個唯一的版本化URL來快取CSS/JS。 僅當客戶端庫的內容更改時才更新序列化哈希。 這意味著，如果發生不相關的更新（即對客戶端庫的基礎css/js沒有更改），即使進行新部署，引用也保持不變，確保減少對瀏覽器快取的中斷。

### 啟用客戶端庫的長快取版本 — AEMas a Cloud ServiceSDK快速啟動 {#enabling-longcache}

預設客戶端庫包括在HTML頁上，如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

當啟用嚴格的客戶端庫版本控制時，會將長期哈希鍵作為選擇器添加到客戶端庫。 因此，客戶端庫引用如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

預設情況下，在所有as a Cloud Service環境中都啟用嚴格AEM的客戶端庫版本控制。

要在本地SDK快速啟動中啟用嚴格客戶端庫版本控制，請執行以下操作：

1. 導航到OSGi配置管理器 `<host>/system/console/configMgr`
1. 查找Adobe花崗岩HTML庫管理器的OSGi配置：
   * 選中複選框以啟用嚴格版本控制
   * 在標有「Long term client side cache key（長期客戶端快取鍵）」的欄位中，輸入值/。*；散列
1. 儲存變更。請注意，無需在原始碼管理中保存此配置，AEM因為as a Cloud Service將在開發、階段和生產環境中自動啟用此配置。
1. 每當客戶端庫的內容被更改時，都會生成新的哈希鍵，並更新HTML引用。
