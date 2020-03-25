---
title: 內容傳送
description: '內容傳送 '
translation-type: tm+mt
source-git-commit: 91005209eaf0fe1728940c414e28e24960df9e7f

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

以下各節提供內容傳送的更詳細資訊，包括CDN設定和Dispatcher快取。

有關從作者服務複製到發佈服務的資訊，請參 [閱](/help/operations/replication.md)。

>[!NOTE]
>流量會通過apache Web伺服器，該伺服器支援包括調度器在內的模組。 調度器主要用作快取，以限制對發佈節點的處理，以提高效能。

## CDN {#cdn}

AEM提供三個選項：

1. Adobe Managed CDN - AEM的現成可用CDN。 這是建議的選項，因為它已完全整合。
1. 客戶CDN指向Adobe Managed CDN —— 客戶將自己的CDN指向AEM的現成可用CDN。 如果第一個選項不可行，這是下一個偏好的選項，因為它仍會運用AEM與其預設CDN的整合。 客戶仍須負責管理其CDN。
1. 客戶管理的CDN —— 客戶自行攜帶CDN，並負責管理它。

>[!CAUTION]
>強烈建議使用第一個選項。 如果您選擇第二個選項，Adobe不能因任何錯誤設定而負責。

第二和第三種選擇將逐案允許。 這包括滿足某些先決條件，包括但不限於與其CDN廠商舊有整合且難以復原的客戶。

### Adobe Managed CDN {#adobe-managed-cdn}

使用Adobe現成可用的CDN來準備內容傳送很簡單，如下所述：

1. 您將透過共用包含此資訊之安全表單的連結，將已簽署的SSL憑證和機密金鑰提供給Adobe。 請與客戶支援協調此項工作。
注意：Aem作為雲端服務不支援「已驗證網域(DV)」憑證。
1. 然後，客戶支援將與您協調CNAME DNS記錄的時間，並將其FQDN指向 `adobe-aem.map.fastly.net`。
1. 當SSL憑證即將到期時，您會收到通知，因此您可以重新提交新的SSL憑證。

依預設，對於Adobe Managed CDN設定，所有公開流量都可以進入發佈服務，適用於生產與非生產（開發與階段）環境。 如果您希望限制特定環境的發佈服務流量（例如，限制IP位址範圍的轉移），您應與客戶支援合作設定這些限制。

### 客戶CDN指向Adobe Managed CDN {#point-to-point-CDN}

如果您想要使用現有的CDN，但無法滿足客戶管理的CDN的需求，則支援此功能。 在這種情況下，您可以管理自己的CDN，但指向Adobe的受管CDN。

請注意，您必須：

1. 您必須有現有的CDN。
1. 你會搞定的。
1. 您必須能夠設定CDN以搭配Aem做為雲端服務使用——請參閱下方的設定指示。
1. 您有工程CDN專家隨時待命，以防相關問題出現。
1. 您必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 使用網 `X-Forwarded-Host` 域名稱設定標題。
1. 使用原始網域（即Adobe的CDN入口）設定主機標題。 價值應來自Adobe。
1. 將SNI報頭髮送到源。 與主機標頭一樣， sni標頭必須是源域。
1. 設定 `X-Edge-Key`要將流量正確路由至AEM伺服器所需的。 價值應來自Adobe。

### 客戶管理的CDN {#customer-managed-cdn}

如果您需要使用現有的CDN，則支援此功能。  在這種情況下，您會管理自己的CDN，並將它指向AEM。

您可以管理自己的CDN，但需：

1. 您有現有的CDN。
1. 它必須是支援的CDN。 目前支援Akamai。 如果您的組織想要管理目前不支援的CDN，請聯絡客戶支援。
1. 你會搞定的。
1. 您必須能夠設定CDN以搭配Aem做為雲端服務使用——請參閱下方的設定指示。
1. 您有工程CDN專家隨時待命，以防相關問題出現。
1. 您必須依設定指示中所述，將CDN節點的白名單提供給Cloud Manager。
1. 您必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 借由呼叫環境建立／更新API，將CIDR清單加入白名單，將CDN廠商的白名單提供給Adobe。
1. 使用網 `X-Forwarded-Host` 域名稱設定標題。
1. 使用原始網域（即Aem為雲端服務入口）設定主機標題。 價值應來自Adobe。
1. 將SNI報頭髮送到源。 SNI標頭必須是源域。
1. 設定 `X-Edge-Key` 將流量正確路由至AEM伺服器所需的項目。 價值應來自Adobe。

在接受即時流量之前，您應向Adobe客戶支援驗證端對端流量路由是否正常運作。

### 快取 {#caching}

快取程式遵循下列規則。

### HTML/文字 {#html-text}

* 依預設，會根據apache圖層所發出的快取控制標題，由瀏覽器快取5分鐘。 CDN也尊重此值。
* 可以在使用AEM做為Cloud Service SDK Dispatcher工具中定義變數， `EXPIRATION_TIME` 覆寫所 `global.vars` 有HTML/Text內容的變數。

您必須確保檔案下 `src/conf.dispatcher.d/cache` 有以下規則：

```
/0000
{ /glob "*" /type "allow" }
```

* 可以通過apache mod_headers指令在更精細的級別上覆蓋。 例如：

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200 s-maxage=200"
</LocationMatch>
```

您必須確保檔案下 `src/conf.dispatcher.d/cache` 有以下規則：

```
/0000
{ /glob "*" /type "allow" }
```

* 請注意，其他方法(包括 [dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))將無法成功覆寫值。

### 用戶端程式庫(js、css) {#client-side-libraries}

* 借由使用AEM的用戶端程式庫架構，JavaScript和CSS程式碼的產生方式，讓瀏覽器可以無限期地快取它，因為任何變更都會以具有唯一路徑的新檔案的形式顯示。  換言之，將視需要產生參照用戶端程式庫的HTML，讓客戶在發佈新內容時可體驗新內容。 對於不尊重「不可變」值的舊版瀏覽器，快取控制項會設為「不可變」或30天。
* 如需詳細資 [訊，請參閱「用戶端程式庫與版本一致性](#content-consistency) 」一節。

### 影像 {#images}

* 未快取

### 其他內容類型 {#other-content}

* 無預設快取
* 可以由apache覆蓋 `mod_headers`。 例如：

```
<LocationMatch "\.(css|js)$">
    Header set Cache-Control "max-age=500 s-maxage=500"
</LocationMatch>
```

*其他設定快取標題的方法也可能奏效

在接受即時流量之前，客戶應向Adobe客戶支援驗證端對端流量路由是否正常運作。

## Dispatcher {#disp}

流量會通過apache Web伺服器，該伺服器支援包括調度器在內的模組。 調度器主要用作快取，以限制對發佈節點的處理，以提高效能。

HTML/文字類型的內容會以快取標題設定，對應於300秒（5分鐘）的過期。

本節的其餘部分介紹與調度程式快取失效相關的注意事項。

### 啟動／停用期間的Dispatcher快取失效 {#cache-activation-deactivation}

和舊版AEM一樣，發佈或取消發佈頁面會清除分派程式快取中的內容。 如果懷疑發生快取問題，客戶應重新發佈相關頁面。

當發佈實例從作者處收到頁面或資產的新版本時，它使用刷新代理使其調度程式上的適當路徑失效。 更新的路徑將連同其父代一起從調度器快取中刪除，最高可達一個級別(您可以使用statfiles級別配置 [此路徑](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)。

### 顯式調度器快取失效 {#explicit-invalidation}

一般而言，不需要手動使調度程式中的內容無效，但如有需要，則可能如下所述。

在AEM成為雲端服務之前，有兩種方式會使分派程式快取失效。

1. 調用複製代理，指定發佈調度器刷新代理
2. 直接呼 `invalidate.cache` 叫API(例如 `POST /dispatcher/invalidate.cache`)

此方 `invalidate.cache` 法不再受支援，因為它只處理特定的調度器節點。
AEM作為Cloud Service會在服務層級運作，而非個別節點層級運作，因此「從AEM [](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) Pages取消驗證快取頁面」頁面中的失效指示對AEM作為Cloud Service無效。
而應使用複製刷新代理。 這可以使用複製API完成。 此處提供複製API文 [檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) ，有關刷新快取的示例，請參見 [API示例頁](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) ，具體是 `CustomStep` 向所有可用代理髮出類型為ACTIVATE的複製操作的示例。 刷新代理端點不可配置，但已預先配置為指向與運行刷新代理的發佈服務匹配的調度程式。 刷新代理通常可由OSGi事件或工作流觸發。

下圖說明了這一點。

![](assets/cdnc.png "CDNCDN")

如果擔心調度程式快取未清除，請與客戶支援聯繫，如有必要，客戶支援可以刷新調度程式快取。

Adobe管理的CDN會遵守TTL，因此不需要將它清除。 如果懷疑有問題，請連絡客戶支援，以視需要清除Adobe管理的CDN快取。

## 用戶端程式庫與版本一致性 {#content-consistency}

網頁當然由HTML、Javascript、CSS和影像組成。 建議客戶運用用戶端資料庫(clientlibs)架構，將Javascript和CSS資源匯入HTML頁面，並考慮到JS資料庫之間的相依性。

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

1. 導覽至OSGi Configuration Manager <host>/system/console/configMgr
1. 尋找Adobe Granite HTML Library Manager的OSGi Config:
   * 勾選核取方塊以啟用「嚴格版本控制」
   * 在標有「長期客戶端快取密鑰」的欄位中，輸入值/。*；雜湊
1. 儲存變更。請注意，不需將此組態儲存在原始碼控制項中，因為AEM將會自動在開發、階段和生產環境中啟用此組態。
1. 每當用戶端程式庫的內容變更時，就會產生新的雜湊金鑰，並更新HTML參考。
