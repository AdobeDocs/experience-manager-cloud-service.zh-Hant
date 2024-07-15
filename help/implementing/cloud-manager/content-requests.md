---
title: 了解雲端服務內容要求
description: 如果您已向Adobe購買內容請求授權，請瞭解Adobe Experience Cloud as a Service測量的內容請求型別，以及組織與分析報告工具的差異。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a1b0d37b2f2f4e58b491651cb8e6504a6909393e
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 10%

---

# Cloud Service內容請求

## 簡介 {#introduction}

內容請求是進入AEM Sites (包括與AEM SitesEdge Delivery Services相關的請求)或任何客戶提供的快取系統（例如內容傳遞網路）的請求，以透過頁面檢視（例如頁面和體驗片段）HTML格式或透過API呼叫（以Headless方式）JSON格式傳遞內容或資料。 內容請求會計為頁面檢視或5次API呼叫，並在第一個接收內容請求的快取系統入口計量。 出於計算內容請求的目的，包含或排除某些HTTP請求。 本檔案提供這類包含和排除HTTP要求的完整清單，及其技術定義。

## 了解雲端服務內容要求 {#understanding-cloud-service-content-requests}

對於使用現成CDN的客戶，Cloud Service內容請求是透過伺服器端資料收集來測量。 系統會透過CDN記錄分析啟用此集合。 透過自動分析源自Adobe Experience Manager as a Cloud Service CDN的記錄檔，可在AEM as a Cloud Service邊緣的伺服器端自動收集內容請求。 這是透過從CDN隔離傳回HTML`(text/html)`或JSON `(application/json)`內容的要求來完成的，其基礎為下文詳述的幾個包含和排除規則。 內容請求會與從CDN快取提供的傳回內容或回到CDN原始來源(AEM傳送器)的內容分開進行。

對於使用自己CDN的客戶，使用者端集合可提供更精確的互動反映，以確保透過[即時使用監控](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md)服務取得可靠的網站參與度測量。 這可提供客戶對其頁面流量和效能的進階深入分析。 雖然此功能對所有客戶都有好處，但可提供使用者互動的有代表性反映，從使用者端擷取頁面檢視次數，確保可靠衡量網站參與度。

對於在AEM as a Cloud Service基礎上自備CDN的客戶，伺服器端報表會產生數字，而無法與授權內容請求進行比較。 透過[即時監控](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md)，Adobe可反映可靠的網站參與度量。


### Cloud Service內容請求的差異 {#content-requests-variances}

內容請求在組織的Analytics報告工具中可能有差異，如下表所述。 一般而言，*不要*&#x200B;使用透過使用者端檢測收集資料的分析工具，來報告特定網站的內容要求數目，因為通常要視使用者同意而觸發，因此遺漏了相當部分的流量。 收集記錄檔中資料伺服器端的Analytics工具，或為在AEM as a Cloud Service上新增自己CDN的客戶提供CDN報告，可提供較佳的計數。 若要報告頁面檢視及其相關效能，[AdobeRUM資料服務](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md)是Adobe的建議選項。

| 差異原因 | 解釋 |
|---|---|
| 一般使用者同意 | 依賴使用者端工具的Analytics工具通常取決於使用者同意觸發。 這可能代表大多數未受追蹤的流量。 如果客戶希望自行測量內容請求，建議依賴分析工具來收集資料伺服器端或CDN報告。 |
| 標記 | 作為Adobe Experience Manager內容請求跟蹤的所有頁面或API呼叫可能不會使用Analytics跟蹤進行標籤。 |
| Tag Management 規則 | Tag Management規則設定可能會導致頁面上的各種資料收集設定，從而導致與內容請求追蹤的某些差異組合。 |
| 機器人 | AEM 未預先識別和刪除的未知機器人可能會導致跟踪差異。 |
| 報表套裝 | 屬於同一 AEM 實例和域的頁面可能會將資料發送到不同的 Analytics 報表包。 |
| 第三方監控和安全工具 | 監控和安全掃描工具可能會為 AEM 生成未在 Analytics 報告中跟踪的內容請求。 |
| API存取 | 以程式設計方式存取頁面或Adobe Experience Manager API，可能會為AEM產生未在Analytics報表中追蹤的內容請求。 |
| 預取請求 | 使用預取服務來預加載頁面以提高速度可能會導致內容請求流量顯著增加。 |
| DDOS | 雖然Adobe會嘗試自動偵測並過濾掉來自DDOS攻擊的流量，但無法保證偵測到所有可能的DDOS攻擊。 |
| 流量攔截器 | 在瀏覽器中使用跟踪器阻止程序可能會選擇不跟踪某些請求。 |
| 防火牆 | 防火牆可能會阻止 Analytics 跟踪。這種情況在公司防火牆中更為常見。 |

另請參閱[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)。

## 伺服器端收集規則 {#serverside-collection}

有現行規則可排除知名機器人，包括定期造訪網站以重新整理其搜尋索引或服務的知名服務。

### 包含的內容請求型別 {#included-content-requests}

| 請求型別 | 內容要求 | 說明 |
| --- | --- | --- |
| HTTP代碼100-299 | 已包含 | 這些是傳送所有或部分內容的一般請求。 |
| 用於自動化的HTTP程式庫 | 已包含 | 範例： <br>· Amazon CloudFront<br>· Apache Http使用者端<br>·非同步Http使用者端<br>· Axios<br>· Azureus<br>· Curl<br>· GitHub節點擷取<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™使用者端<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Python要求15}· Reactor Netty<br>· Wget<br>· WinHTTP<br> |
| 監視和健康狀態檢查工具 | 已包含 | 這些是由客戶設定的，用來監控網站的特定方面。 例如，可用性或真實世界的使用者效能。 使用`/system/probes/health`端點，而不是來自網站的實際HTML頁面。<br>範例：<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(相容； UptimeRobot/2.0；[https://uptimerobot.com/](https://uptimerobot.com/))<br>· TookEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">`個請求 | 已包含 | 若要加快載入下一頁的速度，客戶可在使用者按一下連結前，讓瀏覽器載入一組頁面，讓這些頁面已位於快取中。 *請注意：這會顯著增加流量* — 取決於預先擷取的頁面數量。 |
| 封鎖Adobe Analytics或Google Analytics報表的流量 | 已包含 | 網站訪客安裝隱私權軟體（廣告封鎖程式等）較為常見，這些軟體會影響Google Analytics或Adobe Analytics的正確性。 AEM as a Cloud Service會計算Adobe運作之基礎結構的第一個進入點上的請求，而非使用者端。 |

另請參閱[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)。

### 排除的內容請求型別 {#excluded-content-request}

| 請求型別 | 內容要求 | 說明 |
| --- | --- | --- |
| HTTP代碼500+ | 已排除 | AEM as a Cloud Service或客戶自訂程式碼發生錯誤時，會傳回錯誤給訪客。 |
| HTTP程式碼400-499 | 已排除 | 內容不存在(404)或存在其他內容或請求相關問題時傳回給訪客的錯誤。 |
| HTTP程式碼300-399 | 已排除 | 這些是很好的要求，可檢查伺服器上是否有某些專案變更，或將要求重新導向至其他資源。 它們本身不包含內容，因此不計費。 |
| 要求移至/libs/* | 已排除 | AEM內部JSON請求，例如不可計費的CSRF權杖。 |
| 來自DDOS攻擊的流量 | 已排除 | DDOS保護。 AEM會自動偵測部分DDOS攻擊並加以封鎖。 偵測到的DDOS攻擊無法計費。 |
| AEM as a Cloud Service New Relic監控 | 已排除 | AEM as a Cloud Service全球監控。 |
| 供客戶監控其Cloud Service計畫的URL | 已排除 | 建議的URL可供外部監視可用性。<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod熱身服務 | 已排除 |
| 代理程式： skyline-service-warmup/1.* |
| 著名的搜尋引擎、社交網路和HTTP資料庫（由Fastly標籤） | 已排除 | 定期造訪網站以重新整理其搜尋索引或服務的已知服務： <br><br>範例： <br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Ask Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuildWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBotBotBot <br>· Google AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· MJ12bot<br>· Pingdom<br>· Pinterest<br>· SemrushBot<br>· SiteEnprovement<br>· StashBot<br>· StatusCake<br>· Yek{YandexBot |
| 排除Commerce integration framework呼叫 | 已排除 | 這些是向AEM提出並轉送至Commerce integration framework的請求（URL以`/api/graphql`開頭）以避免重複計算，因此不對Cloud Service計費。 |
| 排除`manifest.json` | 已排除 | 資訊清單不是API呼叫，而是提供如何在案頭或行動電話上安裝網站的資訊。 Adobe不應將JSON請求計為`/etc.clientlibs/*/manifest.json` |
| 排除`favicon.ico` | 已排除 | 雖然傳回的內容不應是HTML或JSON，但根據我們的觀察，在某些案例中（例如SAML驗證流程），favicon可以傳回為HTML，因此會明確從計數中排除。 |
