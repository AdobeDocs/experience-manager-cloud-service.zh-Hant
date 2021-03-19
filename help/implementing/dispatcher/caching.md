---
title: AEM as a Cloud Service 中的快取
description: 'AEM as a Cloud Service 中的快取 '
feature: Dispatcher
translation-type: tm+mt
source-git-commit: 69c865dbc87ca021443e53b61440faca8fa3c4d4
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 1%

---


# 簡介 {#intro}

流量會透過CDN傳遞至apache Web伺服器層，此層支援包括分派器的模組。 為了提高效能，調度器主要用作快取以限制對發佈節點的處理。
規則可套用至分派器設定，以修改任何預設的快取到期設定，從而在CDN處快取。 請注意，如果在分發程式配置中啟用了`enableTTL`，則分發程式也會遵守生成的快取過期標題，這意味著即使在重新發佈內容以外，它也會刷新特定內容。

本頁還介紹如何使調度程式快取失效，以及如何在瀏覽器級別對客戶端庫進行快取。

## 快取{#caching}

### HTML/Text {#html-text}

* 依預設，會根據apache圖層所發出的`cache-control`標題，由瀏覽器快取5分鐘。 CDN也尊重此值。
* 在`global.vars`中定義`DISABLE_DEFAULT_CACHING`變數，可停用預設的HTML/Text快取設定：

```
Define DISABLE_DEFAULT_CACHING
```

例如，當您的商業邏輯需要微調年齡頁首（含根據日曆日的值），因為預設年齡頁首設定為0時，這就很有用。 也就是說，**在關閉預設快取時請格外小心。**

* 可以覆寫所有HTML/Text內容，方法是使用作為Cloud ServiceSDK Dispatcher工具的`global.vars`AEM變數來定義`EXPIRATION_TIME`變數。
* 可以由以下apache mod_headers指令在更精細的級別上覆蓋：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   設定全域快取控制標題或符合寬規則運算式的標題時，請格外小心，以免套用至您可能想要保持私密的內容。 請考慮使用多個指令，以確保以更精細的方式套用規則。 如此一來AEM，如果Cloud Service檢測到快取標頭已應用到它檢測到的由調度程式執行的功能，則該標頭將被刪除，如調度程式文檔中所述。 為了強制AEM一律套用快取，您可以新增「一律」選項，如下所示：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   您必須確保`src/conf.dispatcher.d/cache`下的檔案具有以下規則（預設配置中）:

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* 為防止特定內容被快取，請將「快取控制」標題設為&#x200B;*private*。 例如，下列項目會防止快取名為&#x200B;**myfolder**&#x200B;之目錄下的html內容：

   ```
      <LocationMatch "/content/myfolder/.*\.(html)$">.  // replace with the right regex
      Header set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >其他方法(包括[dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))將無法成功覆寫值。

### 用戶端程式庫(js,css){#client-side-libraries}

* 使用AEM用戶端程式庫架構產生JavaScript和CSS程式碼，讓瀏覽器可以無限期快取它，因為任何變更都會以具有唯一路徑的新檔案的形式顯示。  換言之，將視需要產生參照用戶端程式庫的HTML，讓客戶在發佈新內容時可體驗新內容。 對於不尊重「不可變」值的舊版瀏覽器，快取控制項會設為「不可變」或30天。
* 如需詳細資訊，請參閱[用戶端程式庫和版本一致性](#content-consistency)一節。

### 影像和任何儲存在點滴儲存空間{#images}中的大型內容

* 依預設，未快取
* 可以通過以下apache `mod_headers`指令在更精細的級別上設定：

   ```
      <LocationMatch "^/content/.*\.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   請參閱上述html/text章節中的討論，以注意不要過度快取，以及如何強制AEM一律使用「always」選項套用快取。

   必須確保`src/conf.dispatcher.d/`cache下的檔案具有以下規則（預設配置中）:

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   請確定要保留為私密而非快取的資產不屬於LocationMatch指令篩選器。

   >[!NOTE]
   >其他方法(包括[dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))將無法成功覆寫值。

### 節點儲存{#other-content}中的其他內容檔案類型

* 無預設快取
* default cannot set with `EXPIRATION_TIME` variable used for html/text file types
* 透過指定適當的regex，可使用html/text區段中所述的相同LocationMatch策略來設定快取到期時間

## Dispatcher Cache Invalidation {#disp}

通常，不需要使調度程式快取失效。 相反，當內容重新發佈時，您應依賴Dispatcher重新整理其快取，而CDN則會包含快取到期標題。

### 啟動／停用期間的Dispatcher快取失效{#cache-activation-deactivation}

與舊版相AEM同，發佈或取消發佈頁面會清除發送器快取中的內容。 如果懷疑發生快取問題，客戶應重新發佈相關頁面。

當發佈實例從作者處收到頁面或資產的新版本時，它使用刷新代理使其調度程式上的適當路徑失效。 更新的路徑將連同其父代一起從調度器快取中刪除，最高級別為（可以使用[statfilelevel](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)配置此路徑）。

### 顯式調度器快取失效{#explicit-invalidation}

一般而言，不需要手動使調度程式中的內容無效，但如有需要，則可能如下所述。

在作為AEMCloud Service之前，有兩種方法可以使調度器快取失效。

1. 調用複製代理，指定發佈調度器刷新代理
2. 直接呼叫`invalidate.cache` API（例如`POST /dispatcher/invalidate.cache`）

不再支援調度程式的`invalidate.cache` API方法，因為它只處理特定的調度程式節點。 AEM因為Cloud Service在服務級別運行，而不是在單個節點級別運行，所以[「從](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html)頁中使快取頁無效」中的失效指示對於Cloud Service不再AEM有效。
而應使用複製刷新代理。 這可以使用複製API完成。 複製API文檔位於[此處](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/Replicator.html)，有關刷新快取的示例，請參見[API示例頁](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html)，具體是`CustomStep`示例，該示例對所有可用的代理髮出類型為ACTIVATE的複製操作。 刷新代理端點不可配置，但已預先配置為指向與運行刷新代理的發佈服務匹配的調度程式。 刷新代理通常可由OSGi事件或工作流觸發。

下圖說明這一點。

![](assets/cdnd.png "CDNCDN")

如果擔心調度器快取未清除，請與[客戶支援](https://helpx.adobe.com/support.ec.html)聯繫，如有需要，可以刷新調度器快取。

Adobe管理的CDN會遵守TTL，因此不需要將其刷新。 如果懷疑有問題，請[聯絡客戶支援](https://helpx.adobe.com/support.ec.html)支援，以視需要清除Adobe管理的CDN快取。

## 客戶端庫和版本一致性{#content-consistency}

頁面由HTML、Javascript、CSS和影像組成。 建議客戶運用[用戶端程式庫(clientlibs)架構](/help/implementing/developing/introduction/clientlibs.md)，將Javascript和CSS資源匯入HTML頁面，並考慮到JS程式庫之間的相依性。

clientlibs架構提供自動版本管理，這表示開發人員可以在來源控制中籤入JS程式庫的變更，而且當客戶推出最新版本時，就會提供最新版本。 若沒有這個功能，開發人員將需要手動變更參照新版程式庫的HTML，如果許多HTML範本共用相同的程式庫，這特別麻煩。

當新版程式庫發佈至生產版本時，參考的HTML頁面會更新，並包含這些更新程式庫版本的新連結。 一旦指定HTML頁面的瀏覽器快取過期，就不會擔心舊程式庫會從瀏覽器快取載入，因為重新整理的頁面(從AEM)現在保證會參照新版本的程式庫。 換言之，重新整理的HTML頁面將包含所有最新的程式庫版本。

其機制是序列化雜湊，會附加至用戶端程式庫連結，以確保瀏覽器有唯一、版本化的URL可快取CSS/JS。 序列化雜湊只會在用戶端程式庫的內容變更時更新。 這表示即使在新部署時，如果發生不相關的更新（即客戶程式庫的基礎css/js未變更），參考會維持不變，以確保減少瀏覽器快取的中斷。

### 啟用客戶端庫的長快取版本AEM-作為Cloud ServiceSDK快速入門{#enabling-longcache}

HTML頁面上的預設clientlib包含如下範例：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

啟用嚴格的clientlib版本控制時，會將長期雜湊金鑰新增為用戶端程式庫的選擇器。 因此，clientlib參考如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

嚴格的clientlib版本化在所有環境中都預設AEM為Cloud Service環境。

若要在本機SDK快速入門中啟用嚴格的clientlib版本控制，請執行下列動作：

1. 導航至OSGi Configuration Manager `<host>/system/console/configMgr`
1. 尋找Adobe花崗岩HTML程式庫管理員的OSGi設定：
   * 勾選核取方塊以啟用「嚴格版本控制」
   * 在標有「長期客戶端快取密鑰」的欄位中，輸入值/。*；雜湊
1. 儲存變更。請注意，不必將此配置保存在原始碼控制中，AEM因為Cloud Service將在開發、階段和生產環境中自動啟用此配置。
1. 每當用戶端程式庫的內容變更時，就會產生新的雜湊金鑰，並更新HTML參考。
