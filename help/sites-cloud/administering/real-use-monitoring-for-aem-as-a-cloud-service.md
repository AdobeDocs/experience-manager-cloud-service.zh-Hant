---
title: AEM as a Cloud Service 的真實使用監控
description: 了解如何使用真實用途監控 （RUM） 實時捕獲和分析網站或應用程式的数字使用者體驗。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 9a8adf777008b7a601abc8760cee67ec3c1816c6
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# AEM作為Cloud Service的實際使用監控服務 {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>實際使用監控服務，即數據的用戶端 集合，是一項自動化服務。 無需客戶設定。

>[!INFO]
>
>客戶端監控僅適用於版本 2024.5.16461 **及更高版本AEM Cloud Service**&#x200B;客戶。

## 概觀 {#overview}

真實使用監控 （RUM） 服務是一種性能監控技術，可即時捕獲和分析網站或應用程式的數位用戶體驗。 它提供了對網站應用程式即時性能的可見性，並提供了對最終使用者體驗的更深入分析。 該服務側重於通過監控網站參與度而不是使用者本身來優化性能。

使用 RUM，從URL開始一直跟蹤關鍵績效指標，直到將請求反饋給瀏覽器。 它可以幫助開發人員增強應用程式，使其易於最終使用者使用。

>[!INFO]
>
>“真實用戶監控”已更名為“真實使用監控”，因為它更好地反映了服務的真正本質。

## 誰可以從實際使用的監控服務中受益？ {#who-can-benefit-from-rum-service}

實際使用監控服務對所有客戶都有好處。 它提供了用戶互動的代表性反映，通過捕獲用戶端 頁面視圖的數量來確保網站參與的可靠測量。

對於所有Adobe Systems客戶，此服務提供了有關用戶交互的寶貴見解。 使用自己的 CDN 的客戶可以從簡化的流量 報告中受益，因為Adobe Systems現在直接集成了資料彙集，無需在續訂週期內提供單獨的報告。

## 了解實際使用監控服務的工作原理 {#understand-how-the-rum-service-works}

Adobe Experience Manager （AEM） 使用真實使用監控 （RUM） 來幫助客戶和Adobe Systems了解訪問者如何與AEM網站進行交互。 它可以幫助他們診斷性能問題，並測量實驗的有效性。 RUM 通過抽樣保護訪問者的隱私 - 僅監控所有頁面視圖中的一小部分 - 並且不會收集任何個人身份信息 （PII）。

## 真實使用監控服務和隱私 {#rum-service-and-privacy}

AEM 中的 Real Use 監控服務旨在保護訪客隱私並最大程度地減少資料彙集。 作為訪客，這意味著您正在訪問或提供給Adobe Systems的網站不收集任何個人資訊。

作為網站操作員，無需其他選擇加入即可通過此功能啟用監視。 沒有額外的快顯視窗或同意書供最終使用者接受啟用 RUM。

## 真實監控服務數據採樣 {#rum-service-data-sampling}

傳統的網站分析解决方案嘗試收集每個訪客的數據。 AEM 的 RUM 服務僅從一小部分頁面視圖中捕獲信息。 該服務旨在進行採樣和匿名化，而不是替代分析。 根據預設，頁面的抽樣比率為 1：100。 網站運營商目前無法提高或降低抽樣率。 為了準確估計總流量，對於每 100 個頁面視圖，從 1 開始收集數據，從而為您提供總體流量的可靠近似值。

作為是否收集数据的決定，它是在頁面檢視的基礎上頁面檢視做出的，並且幾乎不可能跟蹤跨多個頁面的交互。 根據設計，RUM 沒有訪問者或會話的概念，只有頁面視圖的概念。

## 正在收集哪些數據 {#what-data-is-being-collected}

真實使用監控服務旨在防止個人身份資訊的集合。 RUM 收集的完整資訊如下：

* 所造訪網站的主機名稱，例如： `experienceleague.adobe.com`
* 用于顯示頁面的廣泛用戶代理類型和操作系統，例如： `desktop:windows` 或 `mobile:ios`
* 資料彙集的時間，如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 就下列執行個體而言，正在瀏覽的頁面URL： `https://experienceleague.adobe.com/docs`
* 反向鏈接URL （連結到目前頁面的頁面URL （如果用戶跟在連結之後）
* 隨機產生的頁面檢視 ID，其格式類似於： `2Ac6`
* 抽樣率的權重或反函數，例如： `100`。 這意味著僅記錄了一百頁面中的一次觀看次數
* 加載頁面序列中特定事件查核點或名稱。 或者，將其作為訪客與之交互
* 用戶為上述查核點與之交互的 DOM 元素的來源或標識符。 若為執行個體，則可能是影像
* 用戶為上述查核點與之交互的外部頁面或資源的目標或連結。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 核心 Web 指標 （CWV） 性能指標，包括描述訪客體驗品質的最大內容繪製 （LCP）、首次輸入延遲 （FID）、累積版面偏移 （CLS） 和到第一個字節的時間 （TTFB）。

## 實際使用監視如何為客戶工作 {#how-rum-works-for-a-customer}

實際使用監控會自動監控用戶端 流量，為您提供有價值的見解。 作為Adobe Systems 客戶，您無需採取任何其他步驟，因為此服務已無縫集成到您現有的設置中。 通過正式發佈 （GA） 轉出，您將自動受益於此新功能。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## 如何使用實際使用監視服務數據 {#how-rum-service-data-is-being-used}

RUM 數據有利於以下目的：

* 識別並修復客戶網站的性能瓶頸
* 簡化包含頁面檢視的自動化流量查閱。
* 了解AEM如何與同一頁面上的其他腳本（如分析、目標定位或外部資料庫）交互，以提高兼容性。

## 限制和了解頁面檢視與績效量度的差異 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

分析 RUM 数据時，頁面視圖和其他性能指標可能存在差異。 這些差異可歸因於即時用戶端監控固有的幾個因素。 以下是客戶在解釋其 RUM 數據時應牢記的關鍵注意事項：

1. **追蹤器攔截器**

   * 使用跟蹤器攔截器或隱私擴展的最終使用者可能會阻礙 RUM 資料彙集，因為這些工具會限制跟蹤腳本的執行。 此限制可能會銷售機會漏報頁面視圖和用戶交互，從而在實際網站活動與 RUM 捕獲的數據之間造成差異。

1. **捕獲無頭 API/JSON 調用的限制**

   * RUM 数据服務專注於用戶端 體驗，目前不會捕獲從非AEM無外設應用進行的後端 API 或 JSON 調用。 從 RUM 服務數據中排除這些調用會與 CDN Analytics測量的內容請求產生差異。

## 常見問題集 {#faq}


1. **客戶能否將 RUM 服務腳本與按讚 Dynatrace 協力廠商系統集成？**

   是的。

1. **是否蒐集「下一次繪畫的互動」、「到第一個字節的時間」和「第一個內容繪畫」Web 生命體征量度？**

   收集與下一個繪製的交互 （INP） 和到第一個字節的時間 （TTFB）。  此時不會收集第一個內容繪畫。

1. **`/.rum`我的網站上路徑被封鎖，我應該如何解決？**

   該 `/.rum` 路徑是 RUM 集合工作所必需的。 如果 Adobe Systems 提供的內容前面有 CDN，作為AEM作為Cloud Service的一部分，請確保路徑 `/.rum` 前進到與AEM 內容其餘部分相同的AEM 來源。 並且，確保不以任何方式對其進行調整。

1. **出於合同目的，RUM 集合計入內容請求嗎？**

   RUM 資料庫 和 RUM 集合不計為內容請求，也不會增加報告的頁面視圖或 API 調用数。 此外，對於使用現成的 CDN 和 AEM 作為Cloud Service的客戶， [伺服器端 集合](#serverside-collection) 是內容請求的基礎。

1. **如何選擇退出？**

   Adobe Systems建議使用真實使用監控 （RUM），因為它具有顯著的優勢，並且可以允許您優化數字體驗。 它可以優惠方案有價值的見解，有助於提高網站性能。 該服務設計為無縫的，不會影響您網站的性能。

   退出退出意味著錯過這些見解。 但是，如果您遇到任何問題，請聯繫Adobe Systems支援。
