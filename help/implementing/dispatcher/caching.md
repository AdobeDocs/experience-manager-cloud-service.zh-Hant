---
title: 在AEM中快取為雲端服務
description: '在AEM中快取為雲端服務 '
translation-type: tm+mt
source-git-commit: 18c2f70acd33c83a0d98ccb658d3e9be18b34c8b
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---


# 簡介 {#intro}

流量會透過CDN傳遞至apache Web伺服器層，此層支援包括分派器的模組。 為了提高效能，調度器主要用作快取以限制對發佈節點的處理。
規則可套用至分派器設定，以修改任何預設的快取到期設定，從而在CDN處快取。 請注意，如果在分發程式配置中啟用了 `enableTTL` ，則分發程式也會遵守生成的快取過期標題，這意味著它將刷新特定內容，即使在重新發佈的內容之外。

本頁還介紹如何使調度程式快取失效，以及如何在瀏覽器級別對客戶端庫進行快取。

## 快取 {#caching}

### HTML/文字 {#html-text}

* 依預設，會根據apache圖層所發出的快取控制標題，由瀏覽器快取5分鐘。 CDN也尊重此值。
* 可以在使用AEM做為Cloud Service SDK Dispatcher工具中定義變數， `EXPIRATION_TIME` 覆寫所 `global.vars` 有HTML/Text內容的變數。
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

* 若要防止快取特定內容，請將「快取控制」標題設為「私用」。 例如，下列項目會防止快取名為&quot;myfolder&quot;的目錄下的html內容：

```
<LocationMatch "\/myfolder\/.*\.(html)$">.  // replace with the right regex
    Header set Cache-Control “private”
</LocationMatch>
```

* 請注意，其他方法(包括 [dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))將無法成功覆寫值。

### 用戶端程式庫(js,css) {#client-side-libraries}

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

## Dispatcher快取失效 {#disp}

通常，不需要使調度程式快取失效。 相反，當內容重新發佈時，您應依賴Dispatcher重新整理其快取，而CDN則會包含快取到期標題。

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
1. 儲存變更。請注意，不需將此組態儲存在原始碼控制項中，因為AEM將會自動在開發、階段和生產環境中啟用此組態。
1. 每當用戶端程式庫的內容變更時，就會產生新的雜湊金鑰，並更新HTML參考。
