---
title: AEM的Real Use Monitoringas a Cloud Service
description: 瞭解如何使用即時監控(RUM)來即時擷取和分析網站或應用程式的數位使用者體驗。
source-git-commit: a15f973c21044e16751401bd0ffb256a4d0fb17d
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---


>[!NOTE]
>我們很高興在此宣佈 [GA推出](/help/release-notes/release-notes-cloud/release-notes-current.md#real-use-monitoring) 對於Real Use Monitoring服務，是指使用者端資料收集。 這是自動化服務，不需要客戶設定。

# AEMas a Cloud Service的Real Use Monitoring Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!INFO]
>
>使用者端監控僅適用於擁有AEM Cloud Service版本的客戶 **2024.5.16461** 及更高版本。

## 概觀 {#overview}

Real Use Monitoring (RUM)服務是一種效能監視技術，可即時擷取和分析網站或應用程式的數位使用者體驗。 它提供網頁應用程式即時效能的可見度，並深入分析一般使用者體驗。 「Real User Monitoring」已更名為「Real Use Monitoring」，因為它更能反映服務的真正本質，其重點在於透過監控網站參與而最佳化效能，而非使用者本身。

透過RUM，系統會從URL起始一直追蹤關鍵效能量度，直到將請求傳回瀏覽器為止，所有這一切都有助於開發人員增強應用程式，讓一般使用者易於使用。

## 誰能從實際使用監控服務中獲益？ {#who-can-benefit-from-rum-service}

Real Use Monitoring服務對所有客戶都有好處。 它可提供使用者互動的有代表性反映，透過擷取使用者端頁面檢視數量，確保可靠衡量網站的參與度。

對於所有Adobe客戶，此服務可提供使用者互動的重要深入分析。 使用自己CDN的客戶可受益於簡化的流量報告，因為Adobe現在直接整合資料收集，消除在續約週期期間需要單獨報告的需求。

您是否要使用Adobe的早期採用者RUM Explorer視覺化工具，針對您的網站互動獲得有用的深入分析，以釋放您網站的完整潛能？ 此工具可提供頁面效能的深入分析，包括點按次數、核心網頁生命(CWV)、轉換和客戶歷程圖等量度。 運用這些強大的深入分析，您可以微調數位體驗，更有效滿足使用者的需求。 如果您想深入瞭解並取得存取權，請傳送電子郵件至： `rum-explorer@adobe.com`.

## 瞭解實際使用監控服務的運作方式 {#understand-how-the-rum-service-works}

Adobe Experience Manager使用即時監控(RUM)來協助客戶和Adobe瞭解訪客如何與Adobe Experience Manager網站互動、診斷效能問題，以及衡量實驗的成效。 RUM透過取樣來保留訪客的隱私權 — 僅監控所有頁面檢視的一小部分 — 並且不會收集任何個人識別資訊(PII)。

## Real Use Monitoring Service與隱私權 {#rum-service-and-privacy}

Adobe Experience Manager中的「Real Use Monitoring」服務可保留訪客隱私權，並將資料收集降至最低。 身為訪客，這表示您造訪的網站不會收集任何個人資訊，也不會提供給Adobe使用。

作為網站操作員，您不需要其他選擇加入即可透過此功能啟用監視。 使用者不需額外快顯視窗或同意表單，即可接受啟用RUM。

## Real Use Monitoring Service資料抽樣 {#rum-service-data-sampling}

傳統的網站分析解決方案會嘗試收集每位訪客的資料。 Adobe Experience Manager的RUM服務只會從一小部分頁面檢視中擷取資訊。 此服務的用途是取樣和匿名處理，而非取代分析。 依預設，頁面的取樣比例為1:100。 網站運運算元目前無法增加或減少取樣速率。 為了準確估計總流量，每100次頁面檢視會從1收集資料，從而提供整體流量的可靠近似值。

由於系統是以逐頁檢視為基礎，決定是否收集資料，因此幾乎無法追蹤多個頁面上的互動。 在設計上，RUM沒有訪客或工作階段的概念，只有頁面檢視。

## 正在收集哪些資料 {#what-data-is-being-collected}

Real Use Monitoring服務可防止收集個人識別資訊。 RUM可收集的完整資訊集列示如下：

* 正在造訪的網站的主機名稱，例如： `experienceleague.adobe.com`
* 用來顯示頁面的廣泛使用者代理程式型別和作業系統，例如： `desktop:windows` 或 `mobile:ios`
* 資料收集的時間，例如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 例如，被瀏覽頁面的URL： `https://experienceleague.adobe.com/docs`
* 反向連結URL （連結至目前頁面的頁面URL，如果使用者依循連結）
* 隨機產生的頁面檢視ID，格式類似： `2Ac6`
* 取樣速率的加權或反值，例如： `100`. 這表示只記錄一百分之一的頁面檢視
* 查核點，或載入頁面或以訪客身分與頁面互動順序中的特定事件名稱
* 使用者針對上述查核點與之DOM元素的來源或識別碼。 例如，這可能是影像
* 使用者與上述查核點互動的外部頁面或資源的目標或連結。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 核心Web Vitals (CWV)效能量度，包括最大內容繪製(LCP)、首次輸入延遲(FID)、累計版面位移(CLS)以及說明訪客體驗品質的首次位元組時間(TTFB)。

## 客戶真實使用監控的運作方式 {#how-rum-works-for-a-customer}

Real Use Monitoring會自動監控使用者端流量，為您提供有價值的深入分析。 身為Adobe客戶，您無需執行任何其他步驟，因為此服務已順暢整合至您現有的設定。 透過「一般可用性」(GA)的推出，您將自動受益於這項新功能。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## 如何使用實際使用監控服務資料 {#how-rum-service-data-is-being-used}

RUM資料有利於以下用途：

* 找出並修正客戶地點的效能瓶頸
* 簡化包含頁面檢視的自動化流量查詢。
* 為了瞭解Adobe Experience Manager如何與相同頁面上的其他指令碼（例如分析、鎖定目標或外部程式庫）互動，以提高相容性。

## 限制和瞭解頁面檢視與效能度量中的差異 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

由於您將分析RUM資料，頁面檢視和其他效能量度可能會有差異。 這些差異可歸因於即時使用者端監視中固有的數個因素。 以下是客戶在解譯其RUM資料時應牢記的主要考量事項：

1. **追蹤器封鎖程式**

   * 終端使用者若使用追蹤器封鎖程式或隱私權擴充功能，可能會阻礙RUM資料收集，因為這些工具會限制追蹤指令碼的執行。 此限制可能會導致報告頁面檢視和使用者互動不足，造成實際網站活動與RUM擷取的資料之間有所出入。

1. **擷取Headless API/JSON呼叫的限制**

   * RUM資料服務著重於使用者端體驗，目前不會擷取從非AEM Headless應用程式進行的後端API或JSON呼叫。 若將這些呼叫從RUM服務資料中排除，將會從CDN Analytics測量的內容請求中造成差異。

## 常見問題集 {#faq}


1. **客戶是否能夠將RUM服務指令碼與Dynatrace等協力廠商系統整合？**

   是。

1. **是否正在收集「互動至下一次繪製」、「第一位元組時間」和「首次有內容的繪製」網頁量度？**

   系統會收集下一個繪圖的互動(INP)和第一個位元組的時間(TTFB)。  目前不會收集第一個內容繪製。

1. **此 `/.rum` 我的網站封鎖路徑，該如何修正？**

   此 `/.rum` 需要RUM集合的路徑才能運作。  如果您的AEMas a Cloud Service中包含CDN (Adobe提供)，則需確保 `/.rum` 路徑轉寄給與其他AEM內容相同的AEM來源。

1. **RUM集合是否會計入合約目的的內容請求？**

   RUM資料庫和RUM集合都不會計為內容請求，也不會增加報告的頁面檢視或API呼叫數量。 此外，對於透過AEMas a Cloud Service使用現成可用CDN的客戶， [伺服器端集合](#serverside-collection) 是內容要求的基礎。

1. **我如何選擇退出？**

我們強烈建議使用即時監控(RUM)，因為其顯著優點，並且可讓您最佳化數位體驗。 此服務提供有價值的深入分析，有助於改善網站效能。此服務的設計目的是順暢無縫，不會影響您網站的效能。

選擇退出表示遺漏這些深入分析。 不過，如果您遇到任何問題，請聯絡Adobe支援。
