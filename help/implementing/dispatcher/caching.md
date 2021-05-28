---
title: AEM as a Cloud Service 中的快取
description: 'AEM as a Cloud Service 中的快取 '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 1%

---

# 簡介 {#intro}

流量會透過CDN傳遞至Apache Web伺服器層，該層支援模組，包括Dispatcher。 為了提高效能，Dispatcher主要用作快取，以限制發佈節點上的處理作業。
規則可套用至Dispatcher設定，以修改任何預設的快取過期設定，進而導致CDN快取。 請注意，如果在Dispatcher設定中啟用`enableTTL`，則Dispatcher也會遵照產生的快取過期標題，這表示即使在重新發佈的內容之外，也會重新整理特定內容。

本頁也說明Dispatcher快取失效的情形，以及快取在瀏覽器層級如何與用戶端程式庫搭配運作。

## 快取 {#caching}

### HTML/文字{#html-text}

* 依預設，會根據apache層發出的`cache-control`標題，由瀏覽器快取5分鐘。 CDN也會遵循此值。
* 在`global.vars`中定義`DISABLE_DEFAULT_CACHING`變數，即可停用預設的HTML/文字快取設定：

```
Define DISABLE_DEFAULT_CACHING
```

例如，當您的業務邏輯需要微調年齡標題（具有以日曆日為基礎的值）時，這會很有用，因為預設情況下，年齡標題設定為0。 也就是說，**在關閉預設快取時請小心。**

* 在`global.vars`中定義`EXPIRATION_TIME`變數，以使用AEM作為Cloud ServiceSDK Dispatcher工具，即可覆寫所有HTML/Text內容。
* 可透過下列apache mod_headers指示，在更精細的粒度層級上覆寫：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   設定全域快取控制標題或符合寬規則運算式的標題時，請務必小心，這樣就不會將這些標題套用至您可能想保留為私密的內容。 請考慮使用多個指令，以確保以微調方式套用規則。 如此一來，如果AEM as aCloud Service偵測到快取標題已套用至其偵測到的Dispatcher無法執行的項目，則會移除快取標題，如Dispatcher檔案所述。 若要強制AEM一律套用快取，您可以新增「always」選項，如下所示：

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

* 為防止快取特定內容，請將「快取控制」標頭設定為&#x200B;*private*。 例如，以下操作會阻止快取名為&#x200B;**myfolder**&#x200B;的目錄下的html內容：

   ```
      <LocationMatch "/content/myfolder/.*\.(html)$">.  // replace with the right regex
      Header set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >其他方法(包括[dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))將無法成功覆寫值。

### 用戶端程式庫(js,css){#client-side-libraries}

* 使用AEM用戶端程式庫架構時，會產生JavaScript和CSS程式碼，讓瀏覽器可無限快取，因為任何變更都會以唯一路徑顯示為新檔案。  換句話說，會視需要產生參考用戶端資料庫的HTML，讓客戶在發佈新內容時能體驗新內容。 對於不遵守「不可變」值的舊版瀏覽器，快取控制項會設為「不可變」或30天。
* 如需其他詳細資訊，請參閱[用戶端程式庫和版本一致性](#content-consistency)一節。

### 影像和任何儲存在blob儲存空間中且足夠大的內容 {#images}

* 預設情況下，不快取
* 可透過下列apache `mod_headers`指示在更精細的層級上設定：

   ```
      <LocationMatch "^/content/.*\.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   請參閱上方html/text一節中的討論，提醒不要過快取太廣，以及如何強制AEM一律使用「一律」選項套用快取。

   必須確保`src/conf.dispatcher.d/`快取下的檔案具有以下規則（預設配置中）:

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   請確定原本要保持為私密（而非快取）的資產不屬於LocationMatch指令篩選器。

   >[!NOTE]
   >其他方法(包括[dispatcher-ttl AEM ACS Commons專案](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))將無法成功覆寫值。

### 節點儲存區{#other-content}中的其他內容檔案類型

* 無預設快取
* 預設值無法使用用於html/text檔案類型的`EXPIRATION_TIME`變數進行設定
* 可借由指定適當的規則運算式，以html/text區段中所述的相同LocationMatch策略來設定快取過期時間

## Dispatcher快取失效 {#disp}

一般而言，Dispatcher快取無需失效。 當內容重新發佈時，您應該仰賴Dispatcher重新整理其快取，並仰賴附有快取過期標題的CDN。

### 啟用/停用{#cache-activation-deactivation}期間Dispatcher快取失效

與舊版AEM一樣，發佈或取消發佈頁面也會從Dispatcher快取中清除內容。 如果懷疑發生快取問題，客戶應重新發佈相關頁面。

當發佈例項從作者收到新版本的頁面或資產時，會使用排清代理程式使其Dispatcher上的適當路徑無效。 更新的路徑會從Dispatcher快取中及其父項中移除，直到達到某個層級(您可以使用[statfilelevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)來設定。

### 顯式Dispatcher快取失效{#explicit-invalidation}

一般而言，不需要手動使Dispatcher中的內容無效，但如有需要，則可以如下所述。

在AEM as aCloud Service之前，有兩種方式會使Dispatcher快取失效。

1. 叫用復寫代理，指定發佈調度程式刷新代理
2. 直接呼叫`invalidate.cache` API（例如`POST /dispatcher/invalidate.cache`）

不再支援Dispatcher的`invalidate.cache` API方法，因為它只處理特定的Dispatcher節點。 AEM as aCloud Service在服務層級運作，而非個別節點層級，因此[使來自AEM的快取頁面失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html)頁面中的失效指示對AEM as aCloud Service不再有效。
而應使用復寫刷新代理。 這可以使用復寫API來完成。 復寫API檔案可在[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/day/cq/replication/Replicator.html)取得，如需快取排清的範例，請參閱[ API範例頁面](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html)，具體為向所有可用代理髮出「啟動」類型復寫動作的`CustomStep`範例。 無法設定排清代理端點，但已預先設定為指向調度程式，與運行排清代理的發佈服務相匹配。 排清代理程式通常可由OSGi事件或工作流程觸發。

下圖說明此情況。

![](assets/cdnd.png "CDNCDN")

如果擔心調度程式快取未清除，請聯絡[客戶支援](https://helpx.adobe.com/support.ec.html)，如有需要，可以排清調度程式快取。

由Adobe管理的CDN會遵循TTL，因此不需要將其清除。 如果懷疑有問題，請[聯絡客戶支援](https://helpx.adobe.com/support.ec.html)支援，如有需要，可以排清Adobe管理的CDN快取。

## 用戶端程式庫與版本一致性{#content-consistency}

頁面由HTML、Javascript、CSS和影像組成。 建議客戶運用[用戶端資料庫(clientlibs)架構](/help/implementing/developing/introduction/clientlibs.md)，將Javascript和CSS資源匯入HTML頁面，同時考慮到JS資料庫之間的相依性。

clientlibs架構提供自動版本管理，這表示開發人員可以在原始碼控制中籤入JS程式庫的變更，而當客戶推播其版本時，將會提供最新版本。 若無此項功能，開發人員將需要手動變更HTML並參考新版程式庫，如果許多HTML範本共用相同的程式庫，這特別麻煩。

當新版本的程式庫發行至生產環境時，會更新參考的HTML頁面，並附上這些更新程式庫版本的新連結。 指定HTML頁面的瀏覽器快取過期後，無論從瀏覽器快取載入舊程式庫，因為重新整理的頁面(從AEM)現在必定會參考新版程式庫。 換言之，重新整理的HTML頁面將包含所有最新的程式庫版本。

此機制為序列化雜湊，會附加至用戶端程式庫連結，確保瀏覽器有唯一的版本化URL來快取CSS/JS。 只有當用戶端程式庫的內容變更時，才會更新序列化雜湊。 這表示即使是新部署，如果發生不相關的更新（即用戶端程式庫的基礎css/js未變更），參照仍會維持不變，確保減少瀏覽器快取的中斷。

### 啟用用戶端程式庫的長快取版本 — AEM as aCloud ServiceSDK快速入門{#enabling-longcache}

HTML頁面上的預設clientlib包含如下列範例所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

啟用嚴格的clientlib版本設定時，會新增長期雜湊金鑰作為選取器至用戶端程式庫。 因此，clientlib參考如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

所有AEM中預設會以Cloud Service環境的形式啟用嚴格的clientlib版本設定。

若要在本機SDK快速入門中啟用嚴格的clientlib版本設定，請執行下列動作：

1. 導覽至OSGi Configuration manager `<host>/system/console/configMgr`
1. 尋找AdobeGranite HTML程式庫管理員的OSGi設定：
   * 勾選核取方塊以啟用嚴格版本設定
   * 在標示為Long term用戶端快取金鑰的欄位中，輸入/值。*；雜湊
1. 儲存變更。請注意，不必將此配置保存在原始碼控制中，因為AEM as aCloud Service會自動在開發、預備和生產環境中啟用此配置。
1. 每次變更用戶端程式庫的內容時，都會產生新的雜湊金鑰，並更新HTML參考。
