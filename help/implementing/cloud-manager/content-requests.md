---
title: 了解 Cloud Service 內容要求
description: 如果您已向Adobe購買內容請求授權，請瞭解Adobe Experience Cloud as a Service測量的內容請求型別，以及與組織分析報告工具的差異。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 2%

---

# 瞭解Cloud Service內容請求

## 簡介 {#introduction}

內容請求包括傳送至AEM Sites的請求。 這些請求可能會透過Edge Delivery Services或客戶提供的快取系統(例如內容傳遞網路(CDN))路由。 這些請求會以HTML或JSON格式傳送結構化資料，並支援頁面檢視（例如頁面和體驗片段）或JSON以Headless方式透過API傳回。

當使用者使用HTML或JSON檢視頁面時，系統會計算內容請求。 它會在第一快取系統收到請求的位置測量請求。 出於計算內容請求的目的，包含或排除某些HTTP請求。 檢視HTTP [包含的內容要求](#included-content-requests)和[排除的內容要求](#excluded-content-request)的完整清單。

>[!NOTE]
>
>內容請求檢視中顯示的資料每24小時會重新整理一次。

## 關於Cloud Service內容請求 {#understanding-cloud-service-content-requests}

*頁面要求*&#x200B;參考的HTTP要求會擷取轉譯首頁面體驗所需的核心結構化內容(例如HTML或JSON)。 其中不包含對資產的請求，例如影像或指令碼。

對於使用現成CDN的客戶，AEM as a Cloud Service會以伺服器端層級的測量來計算內容請求。 此測量會自動進行，不依賴使用者端分析追蹤。

AEM (Adobe Experience Manager) as a Cloud Service會根據AEM執行個體產生並在CDN收到的回應型別來識別內容請求。 具體來說，會計算傳回HTML (`text/html`)或JSON (`application/json`)的請求。 這些格式通常會針對傳統網站呈現或Headless傳送來傳送主要頁面內容。

對靜態資產(例如JavaScript檔案、CSS樣式表和影像)的請求不會計為內容請求。

>[!NOTE]
>如果API請求傳回作為頁面層級內容的HTML或JSON （例如，在Headless傳送中），根據其內容，它可能仍會計為內容請求。

測量內容請求，無論回應是從CDN快取提供，還是轉送至原始AEM環境。

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Cloud Service內容請求的差異 {#content-requests-variances}

內容請求在組織的分析報告工具中可能有差異，如下表所述。 一般而言，請避免使用依賴使用者端工具來報告網站內容請求數量的分析工具。 這些工具通常遺漏大部分流量，因為它們取決於使用者同意啟用。 收集記錄檔中資料伺服器端的Analytics工具，或為在AEM as a Cloud Service上新增自己CDN的客戶提供CDN報告，可提供較佳的計數。

| 差異原因 | 解釋 |
|---|---|
| 一般使用者同意 | 依賴使用者端工具的Analytics工具通常取決於使用者同意觸發。 此工作流程可能代表未追蹤的大部分流量。 如果客戶想自行測量內容請求，Adobe建議您仰賴分析工具從伺服器端或CDN報表收集資料。 |
| 標記 | 作為Adobe Experience Manager內容請求跟蹤的所有頁面或API呼叫可能不會使用Analytics跟蹤進行標籤。 |
| Tag Management 規則 | Tag Management規則設定可能會導致頁面上的各種資料收集設定，從而導致與內容請求追蹤的某些差異組合。 |
| 機器人 | AEM未預先識別和移除的未知機器人可能會導致追蹤差異。 |
| 報表套裝 | 同一AEM例項中的頁面可報告至不同的Analytics報表套裝。 此程式可依設定將資料分割至多個套裝。 |
| 第三方監控和安全工具 | 監控和安全掃描工具（例如正常運行時間檢查程式或弱點掃描器）可能會請求頁面，從而產生分析報表中不可見的伺服器端內容請求。 |
| API存取 | 透過API (例如，透過Adobe Experience Manager as a Headless CMS)對AEM頁面或內容的請求仍會計為內容請求，但不會觸發Analytics追蹤。 |
| 預取請求 | 預先擷取（例如使用Service Worker或Edge函式）可以透過預先請求頁面來增加流量。 這些要求會在伺服器端計算，但不會執行使用者端分析程式碼。 |
| DDOS | Adobe會使用篩選功能來偵測及封鎖許多DDoS攻擊。 不過，在套用篩選器之前，部分攻擊請求可能仍會被計為內容請求。 |
| 流量攔截器 | 瀏覽器中的隱私權功能或企業防火牆可能會阻擋分析指令碼載入。 這些使用者仍會產生伺服器端內容請求。 |
| 防火牆 | 公司或地區防火牆可能會阻止分析呼叫到達Adobe伺服器，導致分析中出現報告不足的情況，而伺服器端計數則不受影響。 |

請參閱[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)，以取得檢視及追蹤內容要求使用量是否符合授許可權制的資訊。

## 伺服器端收集規則 {#serverside-collection}

AEM as a Cloud Service會套用伺服器端收集規則來計數內容請求。 這些規則會排除已知機器人（例如搜尋引擎編目程式）和一組定期偵測網站的監控服務。 此排除清單上沒有的其他綜合或監控型別流量，則計為計費內容請求。

下表列出包含和排除的內容請求型別，以及每種請求的簡短說明。

### 包含的內容請求型別 {#included-content-requests}

>[!NOTE]
>如果API要求傳回HTML回應，則可能會根據其使用內容分類為內容要求。 通常會排除傳回非UI資料的API請求。

| 請求型別 | 內容要求 | 說明 |
| --- | --- | --- |
| HTTP代碼100-299 | 已包含 | 包括傳回完整或部分HTML或JSON內容的成功請求。<br>HTTP程式碼206：這些要求只會傳遞完整內容的一部分。 例如，視訊或大型影像。 部分內容請求會在其傳送轉譯頁面內容中所使用的HTML或JSON回應的一部分時納入。 |
| 用於自動化的HTTP程式庫 | 已包含 | 擷取頁面內容的工具或程式庫提出的請求。 範例包含下列專案： <br>· Amazon CloudFront<br>· Apache Http Client<br>·非同步HTTP使用者端<br>· Axios<br>· Azureus<br>· Curl<br>· GitHub節點擷取<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™ Client<br>· Jersey<br>· Node Oembed<br>· Okhttp<br>· python請求<br>· Reactor Netty<br>· Wget<br>· WinHTTP<br>· Fast HTTP<br>· GitHub節點提取<br>· Reactor Netty |
| 監視和健康狀態檢查工具 | 已包含 | 用來監督頁面健康狀態或可用性的要求。<br>檢視[排除的內容要求型別](#excluded-content-request)。<br>範例包含下列專案：<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+ (相容； UptimeRobot/2.0； [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">`個請求 | 已包含 | 當客戶預先載入或預先擷取內容（例如，使用`<link rel="prefetch">`）時，系統會計算這些伺服器端請求。 請注意，此方法可能會增加流量，端視預先擷取的頁面數量而定。 |
| 封鎖Adobe Analytics或Google Analytics報告的流量 | 已包含 | 網站訪客安裝隱私權軟體（廣告封鎖程式等）而影響Google Analytics或Adobe Analytics正確性的現象較為常見。 AEM as a Cloud Service會計算Adobe運作之基礎結構的第一個進入點上的請求，而非使用者端。 |

另請參閱[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)。

### 排除的內容請求型別 {#excluded-content-request}

| 請求型別 | 內容要求 | 說明 |
| --- | --- | --- |
| HTTP代碼500+ | 已排除 | AEM as a Cloud Service或客戶自訂程式碼發生錯誤時，會傳回錯誤給訪客。 |
| HTTP程式碼400-499 | 已排除 | 內容不存在(404)或存在其他內容或請求相關問題時傳回給訪客的錯誤。 |
| HTTP程式碼300-399 | 已排除 | 要求檢查伺服器上是否有任何變更或將要求重新導向至其他資源的良好要求。 它們本身不包含內容，因此不計費。 |
| 要求將傳送至`/libs/`* | 已排除 | AEM內部JSON請求，例如不可計費的CSRF權杖。 |
| 來自DDOS攻擊的流量 | 已排除 | DDOS保護。 AEM會自動偵測部分DDOS攻擊並加以封鎖。 偵測到的DDOS攻擊無法計費。 |
| AEM as a Cloud Service New Relic監控 | 已排除 | AEM as a Cloud Service全球監控。 |
| 供客戶監控其Cloud Service程式的URL | 已排除 | Adobe建議您使用URL來監視外部可用性或健康狀態檢查。<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod熱身服務 | 已排除 |
| 代理程式： skyline-service-warmup/1.* |
| 著名的搜尋引擎、社交網路和HTTP資料庫（由Fastly標籤） | 已排除 | 定期造訪網站以重新整理其搜尋索引或服務的知名服務： <br><br>範例： <br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Ask Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuildWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsAdsAds機器人<br>· Google AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteImprovement<br>· StatusCake<br>· YandexBot<br>· ContentKing<br>克勞德博特<br> |
| 排除Commerce integration framework呼叫 | 已排除 | 向AEM提出且轉送至Commerce integration framework的請求（URL開頭為`/api/graphql`）為避免重複計算，Cloud Service不為這些請求記帳。 |
| 排除`manifest.json` | 已排除 | 資訊清單不是API呼叫。 此處提供如何在桌上型電腦或行動電話上安裝網站的資訊。 Adobe不應將JSON請求計算為`/etc.clientlibs/*/manifest.json` |
| 排除`favicon.ico` | 已排除 | 雖然傳回的內容不應是HTML或JSON，但已觀察到某些情況（例如SAML驗證流程）會傳回favicon作為HTML。 因此，Favicon會明確從計數中排除。 |
| 體驗片段(XF) — 相同網域重複使用 | 已排除 | 從託管於相同網域上的頁面向XF路徑（例如`/content/experience-fragments/...`）提出的請求（由符合請求主機的Referer標頭識別）。<br><br>範例： `aem.customer.com`的首頁從相同網域提取橫幅或卡片的XF。<br><br>· URL符合/content/experience-fragments/...<br>· Referer網域符合&#x200B;`request_x_forwarded_host`<br><br>**注意：**&#x200B;如果自訂體驗片段路徑（例如使用`/XFrags/...`或`/content/experience-fragments/`之外的任何路徑），則不會排除請求並可能計入請求中，即使請求是相同網域亦然。 建議您使用Adobe的標準XF路徑結構，以確保排除邏輯可正確套用。 |

## 管理內容請求 {#managing-content-requests}

如上面小節[Cloud Service內容要求的差異](#content-requests-variances)中所述，由於多種原因，內容要求可能會高於預期，常見的執行緒是點選CDN的流量。  身為AEM客戶，您可以根據授權預算，監控及管理內容要求，這對您有利。  管理內容要求通常是實作技巧與[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)的組合。

### 管理內容請求的實作技術 {#implementation-techniques-to-manage-crs}

* 確保任何「找不到頁面」回應皆會以HTTP狀態404傳送。  如果以200狀態傳回，則會計入內容請求。
* 將健康情況檢查或監控工具路由至/systems/probes/health URL，或使用HEAD方法而非GET以避免發生內容請求。
* 針對您與網站整合的任何自訂搜尋編目程式，在內容新鮮度的需求與AEM授權成本之間取得平衡。  過於激進的編目程式可能會使用許多內容請求。
* 以伺服器端（狀態301或302）而非使用者端（狀態200含javascript重新導向）的方式處理任何重新導向，以避免兩個不同的內容請求。
* 合併或減少API呼叫，這些是來自AEM的JSON回應，可載入以轉譯頁面。

### 管理內容請求的流量篩選規則 {#traffic-filter-rules-to-manage-crs}

* 常見的機器人模式是使用空的使用者代理。  您將需要檢閱實作和流量模式，以檢視空白的使用者代理程式是否有用。  若要封鎖此流量，建議的[語法](/help/security/traffic-filter-rules-including-waf.md#rules-syntax)為：

```
trafficFilters:
  rules:
    - name: block-missing-user-agent
      when:
        anyOf:
          - { reqHeader: user-agent, exists: false }
          - { reqHeader: user-agent, equals: '' }
      action: block
```

* 有些機器人一天對某個網站點選非常多，第二天就消失了。  這可能會讓封鎖特定IP位址或使用者代理的嘗試受挫。  一種通用方法是引入[速率限制規則](/help/security/traffic-filter-rules-including-waf.md#rate-limit-rules)。  檢閱[範例](/help/security/traffic-filter-rules-including-waf.md#ratelimiting-examples)，並製作符合您快速要求率允差的規則。  請檢閱[條件結構](/help/security/traffic-filter-rules-including-waf.md#condition-structure)語法，瞭解您可能想要允許一般速率限制的任何例外狀況。
