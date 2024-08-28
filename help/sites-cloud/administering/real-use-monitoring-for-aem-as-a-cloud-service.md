---
title: AEM as a Cloud Service 的真實使用監控
description: 瞭解如何使用即時監控(RUM)來即時擷取和分析網站或應用程式的數位使用者體驗。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 2515bc51fd54b014ffb701a8aef38cd08d6725b3
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 1%

---

# AEM as a Cloud Service的Real Use Monitoring服務 {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Real Use Monitoring服務（資料的使用者端集合）是一項自動化服務。 不需要客戶設定。

>[!INFO]
>
>使用者端監視僅適用於具有AEM (Adobe Experience Manager)Cloud Service版本&#x200B;**2024.5.16461**&#x200B;及更高版本的客戶。

## 概觀 {#overview}

RUM （即時監控）服務是一種效能監控技術，可即時擷取和分析網站或應用程式的數位使用者體驗。 它提供網頁應用程式即時效能的可見度，並深入分析一般使用者體驗。 此服務著重於透過監控網站參與來最佳化效能，而非使用者本身。

透過RUM，系統會從URL起始一直追蹤關鍵效能量度，直到將請求傳回瀏覽器為止。 它可協助開發人員增強應用程式，讓使用者輕鬆使用。

>[!INFO]
>
>「Real User Monitoring」已更名為「Real Use Monitoring」，因為它更能反映服務的真實本質。

## 誰能從「即時使用監控」服務中受益？ {#who-can-benefit-from-rum-service}

AEM已開發RUM來協助客戶和Adobe瞭解訪客如何與AEM網站互動。 RUM可用來協助診斷效能問題，以及測量實驗的成效。 RUM透過取樣來保留訪客的隱私權 — 僅監控所有頁面檢視的一小部分 — 並且不會收集任何個人識別資訊(PII)。


## 瞭解實際使用監控服務的運作方式 {#understand-how-the-rum-service-works}

AEM使用RUM來協助客戶和Adobe瞭解訪客如何與AEM網站互動。 它可協助他們診斷效能問題，並測量實驗的成效。 RUM透過取樣來保留訪客的隱私權 — 僅監控所有頁面檢視的一小部分 — 並且不會收集任何個人識別資訊(PII)。

## Real Use Monitoring服務與隱私權 {#rum-service-and-privacy}

AEM中的「Real Use Monitoring」服務可保留訪客隱私權，並將資料收集降至最低。 身為訪客，這表示您造訪或可供Adobe使用的網站不會收集任何個人資訊。

作為網站操作員，您不需要其他選擇加入即可透過此功能啟用監視。 使用者不需額外快顯視窗或同意表單，即可接受啟用RUM。

## Real Use Monitoring服務資料抽樣 {#rum-service-data-sampling}

傳統的網站分析解決方案會嘗試收集每位訪客的資料。 AEM RUM服務只會從一小部分的頁面檢視中擷取資訊。 此服務的用途是取樣和匿名處理，而非取代分析。 依預設，頁面的取樣比例為1:100。 網站運運算元目前無法增加或減少取樣速率。 為了準確估計總流量，每100次頁面檢視會從1收集資料，從而提供整體流量的可靠近似值。

在決定是否收集資料時，會依頁面檢視來決定，幾乎無法追蹤多個頁面上的互動。 在設計上，RUM沒有訪客或工作階段的概念，只有頁面檢視。

## 會收集哪些資料？ {#what-data-is-being-collected}

Real Use Monitoring服務可防止收集個人識別資訊。 RUM收集的完整資訊集列示如下：

* 正在造訪的網站的主機名稱，例如： `experienceleague.adobe.com`
* 用來顯示頁面的廣泛使用者代理程式型別和作業系統，例如： `desktop:windows`或`mobile:ios`
* 資料收集的時間，例如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 正在瀏覽的頁面URL，例如： `https://experienceleague.adobe.com/docs`
* 反向連結URL （連結至目前頁面的頁面URL，如果使用者依循連結）
* 隨機產生的頁面檢視識別碼，格式類似於： `2Ac6`
* 取樣速率的加權或反向，例如： `100`。 這表示只記錄一百分之一的頁面檢視
* 載入頁面順序中特定事件的檢查點或名稱。 或者，以訪客身分與其互動
* 使用者與上述查核點互動的DOM元素來源或識別碼。 例如，它可能是影像
* 使用者與上述查核點互動的外部頁面或資源的目標或連結。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 核心Web Vitals (CWV)效能量度，包括最大內容繪製(LCP)、首次輸入延遲(FID)、累計版面位移(CLS)以及說明訪客體驗品質的首次位元組時間(TTFB)。

## Real Use Monitoring如何為客戶運作 {#how-rum-works-for-a-customer}

Real Use Monitoring會自動監控使用者端流量，為您提供有價值的深入分析。 身為Adobe客戶，您無需執行任何其他步驟，因為此服務已順暢整合至您現有的設定。 透過「一般可用性」(GA)推出功能，您將自動受益於這項新功能。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## 如何使用Real Use監控服務資料 {#how-rum-service-data-is-being-used}

RUM資料有利於以下用途：

* 找出並修正客戶地點的效能瓶頸
* 簡化包含頁面檢視的自動化流量查詢。
* 若要瞭解AEM如何與相同頁面上的其他指令碼（例如分析、鎖定目標或外部程式庫）互動，以提高相容性。

## 頁面檢視和效能度量中的限制和瞭解差異 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

當您分析RUM資料時，頁面檢視和其他效能量度可能會有差異。 這些差異可歸因於即時使用者端監視中固有的數個因素。 以下是客戶在解譯其RUM資料時應牢記的主要考量事項：

1. **追蹤器封鎖程式**

   * 終端使用者若使用追蹤器封鎖程式或隱私權擴充功能，可能會阻礙RUM資料收集，因為這些工具會限制追蹤指令碼的執行。 此限制可能會導致報告頁面檢視和使用者互動不足，造成實際網站活動與RUM擷取的資料之間有所出入。

1. **擷取Headless API/JSON呼叫的限制**

   * RUM資料服務著重於使用者端體驗，目前不會擷取從非AEM Headless應用程式進行的後端API或JSON呼叫。 從RUM服務資料中排除這些呼叫，會從CDN Analytics測量的內容請求中建立變異。

## 常見問題集 {#faq}


1. **客戶是否可將RUM服務指令碼與Dynatrace等協力廠商系統整合？**

   是。

1. **是否正在收集「下一筆繪畫的互動」、「第一位元組的時間」和「第一筆內容繪畫」網頁縮圖量度？**

   系統會收集下一個繪圖的互動(INP)和第一個位元組的時間(TTFB)。  目前不會收集第一個內容繪製。

1. **我的網站已封鎖`/.rum`路徑，該如何修正？**

   需要`/.rum`路徑才能使RUM集合運作。 如果您在Adobe的AEM as a Cloud Service之前使用CDN，請確定`/.rum`路徑轉送至與您的其他AEM內容相同的AEM來源。 此外，請確定此維度沒有任何調整。

1. **RUM集合是否計入合約用途的內容要求？**

   RUM程式庫和RUM集合不會計為內容請求，也不會增加報告的頁面檢視或API呼叫數量。 此外，對於透過AEM as a Cloud Service使用現成CDN的客戶，[伺服器端集合](#serverside-collection)是內容請求的基礎。

1. **我如何選擇退出？**

   Adobe建議您使用「實際使用監控」(RUM)，因為這樣不僅可帶來顯著的好處，而且可讓您將數位體驗最佳化。 它可提供有價值的深入分析，有助於改善網站效能。 此服務的設計是順暢無縫，不會影響網站的效能。

   選擇退出表示缺少這些深入分析。 不過，如果您遇到任何問題，請聯絡Adobe支援。
