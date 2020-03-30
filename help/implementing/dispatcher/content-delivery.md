---
title: 內容傳送
description: '內容傳送 '
translation-type: tm+mt
source-git-commit: 663d3c35f9b7f01d5036e852a5afb61a032bd964

---


# AEM中的「雲端服務」內容傳送 {#content-delivery}

目前的頁面詳細資訊會在AEM中以Cloud Service的形式發佈服務內容傳送。 發佈服務內容傳送包括：

* CDN（通常由Adobe管理）
* AEM Dispatcher
* AEM發佈

資料流程如下：

1. URL會新增至瀏覽器
1. 對DNS中對應至該網域的CDN提出請求
1. 如果內容已完全快取到CDN,CDN會將內容提供給瀏覽器
1. 如果內容未完全快取，CDN會呼叫（反向proxy）給分派程式
1. 如果內容已完全快取在Dispatcher上，則Dispatcher會將其提供給CDN
1. 如果內容未完全快取，則分派程式會呼叫（反向proxy）至AEM發佈
1. 內容由瀏覽器轉譯，瀏覽器也會快取內容，視標題而定

內容類型HTML/text設定為在分派程式層的300秒（5分鐘）後過期，分派程式快取和CDN都會遵守此臨界值。 在重新部署發佈服務期間，會清除調度器快取，然後在新的發佈節點接受通信之前預熱。

以下各節提供內容傳送的更詳細資訊，包括CDN設定和快取。

有關從作者服務複製到發佈服務的資訊，請參 [閱](/help/operations/replication.md)。

## CDN {#cdn}

AEM as Cloud Service隨附內建CDN。 其主要目的是透過從邊緣的CDN節點（在瀏覽器附近）傳送可快取的內容，來減少延遲。 它已完全管理並設定，以提供最佳的AEM應用程式效能。

AEM總共提供兩個選項：

1. AEM Managed CDN - AEM的現成可用CDN。 它是緊密整合的選項，不需要大量客戶投資來支援與AEM的CDN整合。
1. 客戶管理的CDN指向AEM Managed CDN —— 客戶將自己的CDN指向AEM的現成可用的CDN。 客戶仍需要管理其自己的CDN，但是與AEM整合的投資並不大。

第一個選項應滿足大多數客戶效能和安全性要求。 此外，它需要客戶的最小努力。

第二個選項將逐個允許。 此決定是基於符合某些先決條件，包括但不限於與其CDN廠商舊有整合且難以放棄的客戶。

以下是比較兩個選項的決策矩陣。 詳細資訊請參閱下列章節。

| 詳細資料 | AEM Managed CDN | 客戶管理的CDN指向AEM CDN |
|---|---|---|
| **客戶工作** | 沒有，它完全整合。 只需將CNAME指向AEM Managed CDN。 | 適度的客戶投資。 客戶必須管理自己的CDN。 |
| **先決條件** | 無 | 需要替換的現有CDN十分繁雜。 上線前必須先示範成功的負載測試。 |
| **CDN專業知識** | 無 | 需要至少一次兼職的工程資源及能夠設定客戶CDN的詳細CDN知識。 |
| **安全性** | 由 Adobe 管理. | 由Adobe管理（也可由客戶在自己的CDN管理）。 |
| **效能** | 由Adobe最佳化。 | 將受益於某些AEM CDN功能，但由於額外的跳數，可能會造成小幅效能點擊。 **注意**:從客戶CDN跳至Emply CDN可能會很有效)。 |
| **快取** | 支援在調度器上應用的快取標頭。 | 支援在調度器上應用的快取標頭。 |
| **影像和視訊壓縮功能** | 可與Adobe Dynamic Media搭配使用。 | 可搭配Adobe Dynamic Media或客戶管理的CDN影像／視訊解決方案使用。 |

### AEM Managed CDN {#aem-managed-cdn}

使用Adobe現成可用的CDN來準備內容傳送很簡單，如下所述：

1. 您將透過共用包含此資訊之安全表單的連結，將已簽署的SSL憑證和機密金鑰提供給Adobe。 請與客戶支援協調此項工作。
   **注意：** Aem作為雲端服務不支援「已驗證網域(DV)」憑證。
1. 您應通知客戶支援：
   * 哪個自定義域應與給定環境關聯，如程式ID和環境ID所定義。
   * 如果需要任何IP白名單來限制特定環境的流量。
1. 然後，客戶支援將與您協調CNAME DNS記錄的時間，並將其FQDN指向 `adobe-aem.map.fastly.net`。
1. 當SSL憑證即將到期時，您會收到通知，因此您可以重新提交新的SSL憑證。

**限制流量**

依預設，對於Adobe Managed CDN設定，所有公開流量都可以進入發佈服務，適用於生產與非生產（開發與階段）環境。 如果您希望限制特定環境的發佈服務流量（例如，限制IP位址範圍的轉移），您應與客戶支援合作設定這些限制。

### 客戶CDN指向AEM Managed CDN {#point-to-point-CDN}

如果您想要使用現有的CDN，但無法滿足客戶管理的CDN的需求，則支援此功能。 在這種情況下，您可以管理自己的CDN，但指向Adobe的受管CDN。

請注意：

1. 您必須有現有的CDN。
1. 你必須管好它。
1. 您必須能夠設定CDN以搭配Aem做為雲端服務使用——請參閱下方的設定指示。
1. 您必須有工程CDN專家隨時待命，以防相關問題出現。
1. 您必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 使用網 `X-Forwarded-Host` 域名稱設定標題。
1. 使用原始網域（即Adobe的CDN入口）設定主機標題。 價值應來自Adobe。
1. 將SNI報頭髮送到源。 與主機標頭一樣， sni標頭必須是源域。
1. 設定 `X-Edge-Key`要將流量正確路由至AEM伺服器所需的。 價值應來自Adobe。

在接受即時流量之前，您應向Adobe客戶支援驗證端對端流量路由是否正常運作。

## 快取 {#caching}

您可使用Dispatcher規則來設定CDN的快取。 請注意，如果在分派器配置中啟用，則分派器也會遵守產生的快取過期標 `enableTTL` 題，這表示即使在重新發佈內容以外，也會重新整理特定內容。

### HTML/文字 {#html-text}

* 依預設，會根據apache圖層所發出的快取控制標題，由瀏覽器快取5分鐘。 CDN也尊重此值。
* 可以覆寫所有HTML/Text內容，方法是在使用AEM `EXPIRATION_TIME` 做 `global.vars` 為Cloud Service SDK Dispatcher工具中定義變數。

您必須確保檔案下 `src/conf.dispatcher.d/cache` 有以下規則：

```
/0000
{ /glob "*" /type "allow" }
```

* 可以由以下apache mod_headers指令在更精細的級別上覆蓋：

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
</LocationMatch>
```

您必須確保檔案下 `src/conf.dispatcher.d/cache` 有以下規則（預設配置中）:

```
/0000
{ /glob "*" /type "allow" }
```

* 請注意，其他方法(包括 [dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))將無法成功覆寫值。

### 用戶端程式庫(js、css) {#client-side-libraries}

* 借由使用AEM的用戶端程式庫架構，JavaScript和CSS程式碼的產生方式，讓瀏覽器可以無限期地快取它，因為任何變更都會以具有唯一路徑的新檔案的形式顯示。  換言之，將視需要產生參照用戶端程式庫的HTML，讓客戶在發佈新內容時可體驗新內容。 對於不尊重「不可變」值的舊版瀏覽器，快取控制項會設為「不可變」或30天。
* 如需詳細資 [訊，請參閱「用戶端程式庫與版本一致性](#content-consistency) 」一節。

### 影像和任何儲存在點滴儲存空間中的大型內容 {#images}

* 依預設，未快取
* 可以通過以下apache指令在更精細的級別上 `mod_headers` 設定：

```
<LocationMatch "^.*.jpeg$">
    Header set Cache-Control "max-age=222"
</LocationMatch>
```

必須確保src/conf.dispatcher.d/cache下的檔案具有以下規則（預設配置中）:

```
/0000
{ /glob "*" /type "allow" }
```

請確定要保留為私密而非快取的資產不屬於LocationMatch指令篩選器。

* 請注意，其他方法(包括 [dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))將無法成功覆寫值。

### 節點儲存中的其他內容檔案類型 {#other-content}

* 無預設快取
* default cannot set with `EXPIRATION_TIME` variable used for html/text file types
* 透過指定適當的regex，可使用html/text區段中所述的相同LocationMatch策略來設定快取到期時間

## Dispatcher {#disp}

流量會通過apache Web伺服器，該伺服器支援包括調度器在內的模組。 調度器主要用作快取，以限制對發佈節點的處理，以提高效能。

如CDN的快取區段所述，規則可套用至分派器設定，以修改任何預設快取到期設定。

本節的其餘部分介紹與調度程式快取失效相關的注意事項。 對於大部分客戶，不必使分派器快取失效，而是依賴於在重新發佈內容時重新整理其快取的分派器，以及與快取到期標題相關的CDN。

### 啟動／停用期間的Dispatcher快取失效 {#cache-activation-deactivation}

和舊版AEM一樣，發佈或取消發佈頁面會清除分派程式快取中的內容。 如果懷疑發生快取問題，客戶應重新發佈相關頁面。

當發佈實例從作者處收到頁面或資產的新版本時，它使用刷新代理使其調度程式上的適當路徑失效。 更新的路徑將連同其父代一起從調度器快取中刪除，最高可達一個級別(您可以使用statfiles級別配置 [此路徑](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)。

### 顯式調度器快取失效 {#explicit-invalidation}

一般而言，不需要手動使調度程式中的內容無效，但如有需要，則可能如下所述。

在AEM成為雲端服務之前，有兩種方式會使分派程式快取失效。

1. 調用複製代理，指定發佈調度器刷新代理
2. 直接呼 `invalidate.cache` 叫API(例如 `POST /dispatcher/invalidate.cache`)

不再支援Dispatcher的 `invalidate.cache` API方法，因為它只處理特定的Dispatcher節點。 AEM作為Cloud Service會在服務層級運作，而非個別節點層級運作，因此「從AEM [](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) Pages取消驗證快取頁面」頁面中的失效指示對於AEM作為Cloud Service不再有效。
而應使用複製刷新代理。 這可以使用複製API完成。 此處提供複製API文 [檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) ，有關刷新快取的示例，請參見 [API示例頁](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) ，具體是 `CustomStep` 向所有可用代理髮出類型為ACTIVATE的複製操作的示例。 刷新代理端點不可配置，但已預先配置為指向與運行刷新代理的發佈服務匹配的調度程式。 刷新代理通常可由OSGi事件或工作流觸發。

下圖說明這一點。

![](assets/cdnd.png "CDNCDN")

如果擔心調度器快取未清除，請與客戶支援聯 [系](https://helpx.adobe.com/support.ec.html) ，如有需要，客戶支援可以刷新調度器快取。

Adobe管理的CDN會遵守TTL，因此不需要將它清除。 如果懷疑有問題，請聯 [絡客戶支援](https://helpx.adobe.com/support.ec.html) ，以視需要清除Adobe管理的CDN快取。

## 用戶端程式庫與版本一致性 {#content-consistency}

頁面由HTML、Javascript、CSS和影像組成。 建議客戶運用用戶端資料庫(clientlibs)架構，將Javascript和CSS資源匯入HTML頁面，並考慮到JS資料庫之間的相依性。

clientlibs架構提供自動版本管理，這表示開發人員可以在來源控制中籤入JS程式庫的變更，而且當客戶推出最新版本時，就會提供最新版本。 若沒有這個功能，開發人員將需要手動變更參照新版程式庫的HTML，如果許多HTML範本共用相同的程式庫，這特別麻煩。

當新版程式庫發佈至生產版本時，參考的HTML頁面會更新，並包含這些更新程式庫版本的新連結。 一旦指定HTML頁面的瀏覽器快取過期，就不必擔心舊程式庫會從瀏覽器快取載入，因為重新整理的頁面（從AEM）現在可保證會參照新版本的程式庫。 換言之，重新整理的HTML頁面將包含所有最新的程式庫版本。

其機制是序列化雜湊，會附加至用戶端程式庫連結，以確保瀏覽器有唯一、版本化的URL可快取CSS/JS。 序列化雜湊只會在用戶端程式庫的內容變更時更新。 這表示即使在新部署時，如果發生不相關的更新（即客戶程式庫的基礎css/js未變更），參考會維持不變，以確保減少瀏覽器快取的中斷。

### 啟用用戶端程式庫的長快取版本- AEM做為雲端服務SDK快速入門 {#enabling-longcache}

HTML頁面上的預設clientlib包含如下範例：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

啟用嚴格的clientlib版本控制時，會將長期雜湊金鑰新增為用戶端程式庫的選擇器。 因此，clientlib參考如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

在所有AEM中，預設會將嚴格的clientlib版本設定為雲端服務環境。

若要在本機SDK快速入門中啟用嚴格的clientlib版本控制，請執行下列動作：

1. 導覽至OSGi Configuration Manager `<host>/system/console/configMgr`
1. 尋找Adobe Granite HTML Library Manager的OSGi Config:
   * 勾選核取方塊以啟用「嚴格版本控制」
   * 在標有「長期客戶端快取密鑰」的欄位中，輸入值/。*；雜湊
1. 儲存變更。請注意，不需將此組態儲存在來源控制項中，因為AEM將會自動在開發、階段和生產環境中啟用此組態，因此AEM會是雲端服務。
1. 每當用戶端程式庫的內容變更時，就會產生新的雜湊金鑰，並更新HTML參考。
