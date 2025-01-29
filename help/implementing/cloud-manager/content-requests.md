---
title: 了解 Cloud Service 內容請求
description: 如果您已向Adobe購買內容請求授權，請瞭解Adobe Experience Cloud as a Service測量的內容請求型別，以及組織與分析報告工具的差異。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f57d90078b5fc0e0c8a79ca60cbc19e7b37323cd
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 9%

---

# 瞭解Cloud Service內容請求

## 簡介 {#introduction}

內容請求是指向AEM Sites提出的請求，包括與Edge Delivery Services或客戶提供的快取系統（例如內容傳遞網路）相關的請求。 這些請求會透過頁面檢視（例如頁面和體驗片段）以HTML格式傳送內容或資料，或透過API呼叫以Headless格式傳送內容或資料。 內容請求會計為頁面檢視或五個API呼叫，並在第一個接收內容請求的快取系統入口計量。 出於計算內容請求的目的，包含或排除某些HTTP請求。 本檔案提供這類包含和排除HTTP要求的完整清單，及其技術定義。

## 關於Cloud Service內容請求 {#understanding-cloud-service-content-requests}

對於使用現成CDN的客戶，Cloud Service內容請求是透過伺服器端資料收集來測量。 系統會透過CDN記錄分析啟用此集合。 AEM (Adobe Experience Manager) as a Cloud Service會自動在邊緣伺服器端收集內容請求。 它會分析AEM as a Cloud Service CDN產生的記錄檔。 此程式是透過從CDN隔離傳回HTML`(text/html)`或JSON `(application/json)`內容的請求來完成，而且是以以下詳述的幾個包含和排除規則為基礎。 無論內容是從CDN快取中提供還是傳回CDN來源(AEM的傳送器)，都會發生內容請求。

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Cloud Service內容請求的差異 {#content-requests-variances}

內容請求在組織的Analytics報告工具中可能有差異，如下表所述。 一般而言，請避免使用依賴使用者端工具來報告網站內容請求數量的分析工具。 這些工具通常遺漏大部分流量，因為它們取決於使用者同意啟用。 收集記錄檔中資料伺服器端的Analytics工具，或為在AEM as a Cloud Service上新增自己CDN的客戶提供CDN報告，可提供較佳的計數。

| 差異原因 | 解釋 |
|---|---|
| 一般使用者同意 | 依賴使用者端工具的Analytics工具通常取決於使用者同意觸發。 此工作流程可能代表未追蹤的大部分流量。 如果客戶希望自行測量內容請求，建議依賴分析工具來收集資料伺服器端或CDN報告。 |
| 標記 | 作為Adobe Experience Manager內容請求跟蹤的所有頁面或API呼叫可能不會使用Analytics跟蹤進行標籤。 |
| Tag Management 規則 | Tag Management規則設定可能會導致頁面上的各種資料收集設定，從而導致與內容請求追蹤的某些差異組合。 |
| 機器人 | AEM尚未預先識別和移除的未知機器人可能會導致追蹤差異。 |
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
| HTTP代碼100-299 | 已包含 | 傳送全部或部分內容的一般請求。 |
| 用於自動化的HTTP程式庫 | 已包含 | 範例： <br>· Amazon CloudFront<br>· Apache Http Client<br>·非同步HTTP使用者端<br>· Axios<br>· Azureus<br>· Curl<br>· GitHub節點擷取<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™ Client<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Python請求<br>· Reactor Netty<br>· Wget<br>· WinHTTP<br>·快速HTTP<br>· GitHub節點獲取<br>· Reactor Netty |
| 監視和健康狀態檢查工具 | 已包含 | 由客戶設定以監控網站的特定方面。 例如，可用性或真實世界的使用者效能。 如果他們針對特定端點（例如`/system/probes/health`）進行健康情況檢查，Adobe建議您使用`/system/probes/health`端點，而不是來自網站的實際HTML頁面。 [請參閱以下](#excluded-content-request)<br>範例：<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+ (相容； UptimeRobot/2.0； [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEeyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">`個請求 | 已包含 | 若要加快載入下一頁的速度，客戶可在使用者按一下連結前，讓瀏覽器載入一組頁面，讓這些頁面已位於快取中。 *請注意：此方法會顯著增加流量*，視預先擷取的頁面數量而定。 |
| 封鎖Adobe Analytics或Google Analytics報表的流量 | 已包含 | 網站訪客安裝隱私權軟體（廣告封鎖程式等）較為常見，這些軟體會影響Google Analytics或Adobe Analytics的正確性。 AEM as a Cloud Service會計算Adobe運作之基礎結構的第一個進入點上的請求，而非使用者端。 |

另請參閱[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)。

### 排除的內容請求型別 {#excluded-content-request}

| 請求型別 | 內容要求 | 說明 |
| --- | --- | --- |
| HTTP代碼500+ | 已排除 | AEM as a Cloud Service或客戶自訂程式碼發生錯誤時，會傳回錯誤給訪客。 |
| HTTP程式碼400-499 | 已排除 | 內容不存在(404)或存在其他內容或請求相關問題時傳回給訪客的錯誤。 |
| HTTP程式碼300-399 | 已排除 | 要求檢查伺服器上是否有任何變更或將要求重新導向至其他資源的良好要求。 它們本身不包含內容，因此不計費。 |
| 要求移至/libs/* | 已排除 | AEM內部JSON請求，例如不可計費的CSRF權杖。 |
| 來自DDOS攻擊的流量 | 已排除 | DDOS保護。 AEM會自動偵測部分DDOS攻擊並加以封鎖。 偵測到的DDOS攻擊無法計費。 |
| AEM as a Cloud Service New Relic監控 | 已排除 | AEM as a Cloud Service全球監控。 |
| 供客戶監控其Cloud Service計畫的URL | 已排除 | Adobe建議您使用URL來監視外部可用性或健康狀態檢查。<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod熱身服務 | 已排除 |
| 代理程式： skyline-service-warmup/1.* |
| 著名的搜尋引擎、社交網路和HTTP資料庫（由Fastly標籤） | 已排除 | 定期造訪網站以重新整理其搜尋索引或服務的知名服務： <br><br>範例： <br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Ask Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuildWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsAdsAds機器人<br>· Google AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteImprovement<br>· StatusCake<br>· YandexBot<br>· ContentKing<br>克勞德博特<br> |
| 排除Commerce integration framework呼叫 | 已排除 | 向AEM提出且轉送至Commerce integration framework的請求（URL開頭為`/api/graphql`）為避免重複計算，不對Cloud Service計費。 |
| 排除`manifest.json` | 已排除 | 資訊清單不是API呼叫。 此處提供如何在桌上型電腦或行動電話上安裝網站的資訊。 Adobe不應將JSON請求計為`/etc.clientlibs/*/manifest.json` |
| 排除`favicon.ico` | 已排除 | 雖然傳回的內容不應是HTML或JSON，但已觀察到某些情況（如SAML驗證流程）會傳回favicon作為HTML。 因此，Favicon會明確從計數中排除。 |
