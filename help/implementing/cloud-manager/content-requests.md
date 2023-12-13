---
title: 了解雲端服務內容要求
description: 如果您已向Adobe購買內容請求授權，請瞭解Adobe Experience Cloud as a Service測量的內容請求型別，以及組織與分析報告工具的差異。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: e31b05f0cef6c5ca3a1c00b757eac013aa43bb90
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 4%

---

# Cloud Service內容請求

## 簡介 {#introduction}

Cloud Service內容請求是透過伺服器端的資料收集來測量。 集合會透過CDN記錄分析啟用。

>[!NOTE]
>此外，對於有限數量的 [早期採用者客戶](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter)，使用者端收集功能也會透過RUM (Real User Monitoring)測量啟用。 如需詳細資訊，請參閱以下檔案： [本文](#real-user-monitoring-for-aem-as-a-cloud-service).

## 了解雲端服務內容要求 {#understaing-cloud-service-content-requests}

透過自動分析源自AEMas a Cloud ServiceCDN的記錄檔，可在Adobe Experience Manager as a Cloud Service邊緣的伺服器端自動收集內容請求。 這是透過隔離傳回HTML的請求來完成的 `(text/html)` 或JSON `(application /Json)` 來自CDN的內容以及以下詳述的幾個包含和排除規則為基礎。 內容請求會與從CDN快取提供的傳回內容或回到CDN原始來源(AEM Dispatchers)的內容分開進行。

Real User Monitoring (RUM) Data Service是使用者端集合，可更準確地反映使用者互動，以確保可靠的網站參與測量。 這可提供客戶對其頁面流量和效能的進階深入分析。 這對使用Adobe託管CDN或非Adobe託管CDN的客戶都有好處。 此外，現在可以為使用非Adobe管理的CDN的客戶啟用自動流量報告，因此無需與Adobe共用任何流量報告。

對於在AEMas a Cloud Service之上自有CDN的客戶，伺服器端報告會導致數字無法用於與授權內容請求進行比較。 這些數字必須由位於外部CDN邊緣的客戶測量。 對於這些客戶、使用者端報表和相關效能， [AdobeRUM資料服務](#real-user-monitoring-for-aem-as-a-cloud-service) 是Adobe建議的選項。 請參閱 [發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter) 以取得關於如何選擇加入的資訊。

## 伺服器端集合 {#serverside-collection}

有現行規則可排除知名機器人，包括定期造訪網站以重新整理其搜尋索引或服務的知名服務。

### Cloud Service內容請求的差異 {#content-requests-variances}

內容請求可能與組織的Analytics報告工具不同，如下表所述。 一般而言， *不要* 使用透過使用者端檢測收集資料的分析工具，報告指定網站的內容請求數量，原因很簡單，這些請求通常取決於要觸發的使用者同意，因此會遺漏相當一部分的流量。 收集記錄檔中資料伺服器端的Analytics工具，或為在AEMas a Cloud Service上新增自己CDN的客戶提供CDN報告，可提供較佳的計數。 若要報告頁面檢視及其相關效能，AdobeRUM資料服務是Adobe的建議選項。

| 差異原因 | 解釋 |
|---|---|
| 一般使用者同意 | 依賴使用者端工具的Analytics工具通常取決於使用者是否同意觸發。 這可能代表大多數未受追蹤的流量。 如果客戶希望自行測量內容請求，建議依賴分析工具來收集資料伺服器端或CDN報告。 |
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

### 包含的內容請求型別 {#included-content-requests}

| 請求型別 | 內容要求 | 說明 |
| --- | --- | --- |
| HTTP代碼100-299 | 已包含 | 這些是傳送所有或部分內容的一般請求。 |
| 用於自動化的HTTP程式庫 | 已包含 | 範例：<br>· Amazon CloudFront<br>· Apache Http使用者端<br>·非同步Http使用者端<br>· Axios<br>·蔚藍色<br>· Curl<br>· GitHub節點擷取<br>·龜甲<br>· Go-http-client<br>· Headless鉻黃<br>· Java™使用者端<br>·澤西島<br>·節點內嵌<br>· okhttp<br>· Python要求<br>· Reactor Netty<br>· Wget<br>· WinHTTP |
| 監視和健康狀態檢查工具 | 已包含 | 這些是由客戶設定的，用來監控網站的特定方面。 例如，可用性或真實世界的使用者效能。 使用 `/system/probes/health` 端點，而不是來自網站的實際HTML頁面。<br>範例：<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+ (相容；UptimeRobot/2.0； [https://uptimerobot.com/](https://uptimerobot.com/))<br>·千眼蜻蜓 — x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` 請求 | 已包含 | 若要加快載入下一頁的速度，客戶可在使用者按一下連結前，讓瀏覽器載入一組頁面，讓這些頁面已位於快取中。 *請注意：這會大幅增加流量* — 取決於預先擷取的頁面數量。 |
| 封鎖Adobe Analytics或Google Analytics報表的流量 | 已包含 | 網站訪客安裝隱私權軟體（廣告封鎖程式等）較為常見，這些軟體會影響Google Analytics或Adobe Analytics的正確性。 AEMas a Cloud Service會計算Adobe操作之基礎結構的第一個進入點上的請求，而非使用者端。 |

另請參閱 [授權儀表板](/help/implementing/cloud-manager/license-dashboard.md).

### 排除的內容請求型別 {#excluded-content-request}

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

## 使用者端集合 {#cliendside-collection}

### 適用於AEM的Real User Monitoring (RUM)as a Cloud Service {#real-user-monitoring-for-aem-as-a-cloud-service}

>[!INFO]
>
>此功能僅供早期採用者程式使用。
>您需要使用AEM Cloud Service版本 **2023.11.14227** 以上以啟用RUM資料服務。

### 概觀 {#overview}

Real User Monitoring (RUM)是一種效能監視技術，可即時擷取和分析網站或應用程式的數位使用者體驗。 它提供網頁應用程式即時效能的可見度，並提供了對一般使用者體驗的精確洞察。

Real User Monitoring (RUM)提供從URL起始到將請求傳回瀏覽器為止的關鍵效能量度的深入分析，這一切都有助於開發人員增強應用程式，使其更容易為一般使用者使用。

### 誰可以受益於RUM資料監控服務？ {#who-can-benefit-from-rum-data-monitoring-service}

RUM Data Service對使用AdobeCDN的人有好處，因為它可提供使用者互動的更精確反映，透過反映使用者端的頁面檢視次數（可與現有的伺服器端CDN記錄頁面檢視次數比較），確保網站參與度的可靠測量。 此外，對於使用自己CDN的客戶，Adobe現在可以簡化包含頁面檢視的自動流量報告，這表示他們不必與Adobe共用任何流量報告。

這也是一個絕佳機會，讓您對使用Adobe CDN的客戶和使用自己CDN的客戶取得頁面效能的進階深入分析。

### 瞭解Real User Monitoring (RUM)資料服務的運作方式 {#understand-how-the-rum-data-service-works}

Adobe Experience Manager使用Real User Monitoring (RUM)來協助客戶和Adobe瞭解、訪客如何與Adobe Experience Manager支援的網站互動、診斷效能問題，以及評估實驗的成效。 RUM透過取樣來保留訪客的隱私權 — 僅會監視所有頁面檢視的一小部分 — 並明智地排除所有個人識別資訊(PII)。

### Real User Monitoring (RUM)與隱私權 {#rum-and-privacy}

Adobe Experience Manager中的「即時使用者監控」可保留訪客隱私權，並將資料收集降至最低。 身為訪客，這表示您造訪的網站不會收集任何個人資訊，也不會提供給Adobe使用。

作為網站操作員，這表示透過此功能啟用監視不需要額外的選擇加入。因此，使用者將不接受額外的快顯視窗來啟用RUM監視。

### RUM資料抽樣 {#rum-data-sampling}

傳統的網站分析解決方案會嘗試收集每位訪客的資料。 Adobe Experience Manager的Real User Monitoring僅擷取一小部分頁面檢視中的資訊。 Real User Monitoring (RUM)旨在進行抽樣和匿名處理，而非取代分析。 依預設，頁面會有1:100的取樣比例。 站台運運算元無法設定這個數字，以增加或減少目前為止的取樣率。 為了準確估計總流量，我們每100次頁面檢視就會收集一次的詳細資料，讓您可靠地估計整體流量。」

由於系統是以逐頁檢視為基礎，決定是否收集資料，因此幾乎無法追蹤多個頁面上的互動。 RUM沒有造訪、訪客或工作階段等概念，只有頁面檢視數。 這是刻意設計。

### 正在收集哪些資料 {#what-data-is-being-collected}

Real User Monitoring (RUM)的設計目的是防止收集個人識別資訊。 以下列出了Adobe Experience Manager的「Real User Monitoring」可收集的完整資訊集：

* 正在造訪的網站的主機名稱，例如： `experienceleague.adobe.com`
* 用來顯示頁面的廣泛使用者代理程式型別，例如：桌上型電腦或行動裝置
* 資料收集的時間，例如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 例如，被瀏覽頁面的URL： `https://experienceleague.adobe.com/docs`
* 反向連結URL （連結至目前頁面的頁面URL，如果使用者依循連結）
* 隨機產生的頁面檢視ID，格式類似： `2Ac6`
* 取樣速率的加權或反值，例如： `100`. 這表示僅會記錄一百分之一的頁面檢視
* 查核點，或載入頁面或以訪客身分與頁面互動順序中的特定事件名稱
* 使用者針對上述查核點與之DOM元素的來源或識別碼。 例如，這可能是影像
* 使用者與上述查核點互動的外部頁面或資源的目標或連結。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 核心Web Vitals (CWV)效能量度、最大內容繪製(LCP)、首次輸入延遲(FID)以及描述訪客體驗品質的Cumulative Layout Shift (CLS)。

### 如何設定真實使用者監視(RUM)資料服務 {#how-to-set-up-them-rum-data-service}

* 如果您希望加入我們的早期採用者計畫，請傳送電子郵件至 `aemcs-rum-adopter@adobe.com`，以及您與Adobe ID相關聯之電子郵件地址中的生產、測試和開發環境網域名稱。 接著Adobe的產品團隊將為您啟用Real User Monitoring (RUM)資料服務。
* 完成此操作後，Adobe的產品團隊將建立客戶共同作業管道。
* Adobe的產品團隊會與您聯絡，提供您網域金鑰和資料控制面板URL，讓您在其中檢視「頁面檢視」和「頁面檢視」 [核心Web Vitals (CWV)](https://web.dev/vitals/) 由使用者端Real User Monitoring (RUM)收集所收集的量度。
* 接著，我們將引導您如何使用網域金鑰存取資料控制面板url並檢視量度。

### 如何使用實際使用者監控(RUM)資料 {#how-rum-data-is-being-used}

RUM資料有利於以下用途：

* 找出並修正客戶地點的效能瓶頸
* 簡化的自動流量報告，包括適用於使用自己CDN之客戶的頁面檢視，這表示他們不需要與Adobe共用任何流量報告。
* 為了瞭解Adobe Experience Manager如何與相同頁面上的其他指令碼（例如分析、鎖定目標或外部程式庫）互動，以提高相容性。

### 限制和瞭解頁面檢視與效能度量中的差異 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

由於您將分析此資料，因此實際使用者監控(RUM)報告的頁面檢視和其他效能度量可能會有也可能沒有差異。 這些差異可歸因於即時使用者端監視中固有的數個因素。 以下是客戶在解譯其RUM資料時應牢記的主要考量事項：

1. **追蹤器封鎖程式**

   * 終端使用者若使用追蹤器封鎖程式或隱私權擴充功能，可能會妨礙真實使用者監控(RUM)的資料收集，因為這些工具會限制追蹤指令碼的執行。 此限制可能會導致報告頁面檢視和使用者互動不足，造成實際網站活動與RUM擷取的資料之間有所出入。

1. **擷取API/JSON呼叫的限制**

   * RUM資料服務著重於使用者端體驗，目前不會擷取後端API或JSON呼叫。 若將這些呼叫排除在真實使用者監控(RUM)資料之外，將會從CDN Analytics測量的內容請求中建立差異。

### 常見問題集 {#faq}

1. **如何設定要在監視中包含或排除的路徑？**

   客戶將能在Cloud Manager中設定環境變數，藉此設定路徑以包含或排除要監視的URL，方法是使用這些變數： `AEM_WEBVITALS_EXCLUDE` 和 `AEM_WEBVITALS_INCLUDE_PATHS`

   請注意，依預設，「包含」設定是設定為目標「/content」。 請務必記住，您需要在這裡設定的路徑是系統內的內容路徑，而不是您在瀏覽器中看到的URL路徑。 這項區別是精確設定和自訂設定，以符合您特定需求的關鍵。

1. **在互動達到客戶管理的CDN之前或互動達到客戶管理的CDN時，Adobe能否追蹤所有頁面檢視？**

   是。

1. **客戶是否能夠將RUM資料服務指令碼與Dynatrace等協力廠商系統整合？**

   是。

1. **是否正在收集「互動至下一次繪製」、「第一位元組時間」和「首次有內容的繪製」網頁量度？**

   系統會收集下一個繪圖的互動(INP)和第一個位元組的時間(TTFB)。  目前不會收集第一個內容繪製。
