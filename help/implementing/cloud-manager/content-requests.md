---
title: 了解雲端服務內容請求
description: 如果您已向Adobe購買內容請求授權，請瞭解Adobe Experience Cloud as a Service測量的內容請求型別，以及組織與分析報告工具的差異。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: dc01da4c85b37f21deb169b941c0cf2a958298b8
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 10%

---

# Cloud Service內容請求

## Cloud Service內容請求的差異{#content-requests-variances}

內容請求可能與組織的Analytics報告工具不同，如下表所述。 一般而言，Analytics工具會透過使用者端檢測收集資料 <b>不應使用</b> 來報告特定網站的內容請求數量，原因很簡單，這些請求通常取決於要觸發的一般使用者同意，因此會遺漏相當一部分的流量。 收集記錄檔中資料伺服器端的Analytics工具，或為在AEMas a Cloud Service上新增自己CDN的客戶提供CDN報告，可提供較佳的計數。 若要報告頁面檢視及其相關效能，AdobeRUM資料服務是Adobe的建議選項。

| 差異原因 | 解釋 |
|---|---|
| 一般使用者同意 | 依賴使用者端工具的Analytics工具通常取決於一般使用者同意觸發。 這可能代表大多數未受追蹤的流量。 如果客戶希望自行測量內容請求，建議依賴分析工具來收集資料伺服器端或CDN報告。 |
| 標記 | 作為Adobe Experience Manager (AEM)內容請求跟蹤的所有頁面或API呼叫可能不會使用Analytics跟蹤進行標籤。 |
| Tag Management 規則 | Tag Management規則設定可能會導致頁面上的各種資料收集設定，從而導致與內容請求追蹤的某些差異組合。 |
| 機器人 | AEM 未預先識別和刪除的未知機器人可能會導致跟踪差異。 |
| 報表套裝 | 屬於同一 AEM 實例和域的頁面可能會將資料發送到不同的 Analytics 報表包。 |
| 第三方監控和安全工具 | 監控和安全掃描工具可能會為 AEM 生成未在 Analytics 報告中跟踪的內容請求。 |
| API存取 | 以程式設計方式存取頁面或Adobe Experience Manager API，可能會為AEM產生未在Analytics報表中追蹤的內容請求。 |
| 預取請求 | 使用預取服務來預加載頁面以提高速度可能會導致內容請求流量顯著增加。 |
| DDOS | 雖然Adobe會嘗試自動偵測並過濾掉來自DDOS攻擊的流量，但無法保證偵測到所有可能的DDOS攻擊。 |
| 流量攔截器 | 在瀏覽器中使用跟踪器阻止程序可能會選擇不跟踪某些請求。 |
| 防火牆 | 防火牆可能會阻止 Analytics 跟踪。這種情況在公司防火牆中更為常見。 |

另請參閱 [授權儀表板](/help/implementing/cloud-manager/license-dashboard.md).

## 了解雲端服務內容請求 {#about-content-request}

透過自動分析源自AEM CDN的記錄檔、從CDN隔離傳回HTML（文字/html）或JSON （應用程式/json）內容的請求，以及根據以下詳述的若干包含和排除規則，在Adobe Experience Manager (AEM as a Cloud Service)as a Cloud Service邊緣自動追蹤內容請求。 內容請求會與CDN快取提供的傳回內容無關，或會回到CDN的來源(AEM傳送器)。

對於在AEMas a Cloud Service之上自有CDN的客戶，此追蹤將導致無法與授權內容請求進行比較的數字，而必須由位於外部CDN邊緣的客戶測量。

有現行規則可排除知名機器人，包括定期造訪網站以重新整理其搜尋索引或服務的知名服務。

### 包含的內容請求型別{#included-content-requests}

| 請求型別 | 內容要求 | 說明 |
| --- | --- | --- |
| HTTP代碼100-299 | 已包含 | 這些是傳送所有或部分內容的一般請求。 |
| 用於自動化的HTTP程式庫 | 已包含 | 範例：<br>· Amazon CloudFront<br>· Apache Http使用者端<br>·非同步Http使用者端<br>· Axios<br>·蔚藍色<br>· Curl<br>· GitHub節點擷取<br>·龜甲<br>· Go-http-client<br>· Headless鉻黃<br>· Java™使用者端<br>·澤西島<br>·節點內嵌<br>· okhttp<br>· Python要求<br>· Reactor Netty<br>· Wget<br>· WinHTTP |
| 監視和健康狀態檢查工具 | 已包含 | 這些是由客戶設定的，用來監控網站的特定方面。 例如，可用性或真實世界的使用者效能。 使用 `/system/probes/health` 端點，而不是來自網站的實際HTML頁面。<br>範例：<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+ (相容；UptimeRobot/2.0； [https://uptimerobot.com/](https://uptimerobot.com/))<br>·千眼蜻蜓 — x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` 請求 | 已包含 | 若要加快載入下一頁的速度，客戶可在使用者按一下連結前，讓瀏覽器載入一組頁面，讓這些頁面已位於快取中。 *請注意：這會大幅增加流量* — 取決於預先擷取的頁面數量。 |
| 封鎖Adobe Analytics或Google Analytics報表的流量 | 已包含 | 網站訪客安裝隱私權軟體（廣告封鎖程式等）較為常見，這些軟體會影響Google Analytics或Adobe Analytics的正確性。 AEMas a Cloud Service會計算Adobe操作之基礎結構的第一個進入點上的請求，而非使用者端。 |

另請參閱 [授權儀表板](/help/implementing/cloud-manager/license-dashboard.md).

### 排除的內容請求型別{#excluded-content-request}

| 請求型別 | 內容要求 | 說明 |
| --- | --- | --- |
| HTTP代碼500+ | 已排除 | AEMas a Cloud Service或客戶自訂程式碼發生錯誤時，會傳回錯誤給訪客。 |
| HTTP程式碼400-499 | 已排除 | 內容不存在(404)或存在其他內容或請求相關問題時傳回給訪客的錯誤。 |
| HTTP程式碼300-399 | 已排除 | 這些是很好的要求，可檢查伺服器上是否有某些專案變更，或將要求重新導向至其他資源。 它們本身不包含內容，因此不計費。 |
| 要求移至/libs/* | 已排除 | AEM內部JSON請求，例如不可計費的CSRF權杖。 |
| 來自DDOS攻擊的流量 | 已排除 | DDOS保護。 AEM會自動偵測部分DDOS攻擊並加以封鎖。 偵測到的DDOS攻擊無法計費。 |
| AEMas a Cloud ServiceNewRelic監控 | 已排除 | AEMas a Cloud Service全域監視。 |
| 供客戶監控其Cloud Service計畫的URL | 已排除 | 建議用於外部監視可用性的URL。<br><br>`/system/probes/health` |
| AEMas a Cloud ServicePod熱身服務 | 已排除 | 使用者代理： skyline-service-warmup/1.* |
| 著名的搜尋引擎、社交網路和HTTP資料庫（由Fastly標籤） | 已排除 | 定期造訪網站以重新整理其搜尋索引或服務的知名服務：<br><br>範例：<br>· AddSearchBot<br>· AhrefsBot<br>·應用程式機器人<br>·向Jeeves Corporate Spider詢問<br>·賓格機器人<br>·必應預覽<br>·邊界點<br>·建置方式<br>·位元組資料片<br>·編目程式昆高<br>· Facebookexternalhit<br>· Google AdsBot<br>· Google AdsBot Mobile<br>·谷歌機器人<br>· Googlebot Mobile<br>·爬蟲程式<br>· LucidWorks<br>· MJ12bot<br>· Pingdom<br>·Pinterest<br>· SemrushBot<br>· SiteEffect<br>·隱藏機器人<br>· StatusCake<br>· YandexBot |
| 排除Commerce integration framework呼叫 | 已排除 | 這些是向AEM提出並轉送至Commerce integration framework的請求 — URL開頭為 `/api/graphql` — 為了避免重複計算，這些量度不針對Cloud Service計費。 |
| 排除 `manifest.json` | 已排除 | 資訊清單不是API呼叫，而是提供如何在案頭或行動電話上安裝網站的資訊。 Adobe不應將JSON請求計算為 `/etc.clientlibs/*/manifest.json` |
| 排除 `favicon.ico` | 已排除 | 雖然傳回的內容不應是HTML或JSON，但根據我們的觀察，在某些案例中（例如SAML驗證流程），favicon可以傳回為HTML，因此會明確從計數中排除。 |
