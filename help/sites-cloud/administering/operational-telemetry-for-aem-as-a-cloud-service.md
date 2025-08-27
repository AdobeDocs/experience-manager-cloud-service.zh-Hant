---
title: AEM as a Cloud Service 的操作遙測
description: 瞭解操作遙測，這是一項允許監控使用者端資料收集的自動化服務。
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 41d9fd628eec8ce757447bed13d50211e71785de
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 1%

---

# AEM as a Cloud Service的作業遙測服務 {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>作業遙測服務（使用者端資料收集）是一項自動化服務。 不需要客戶設定。

>[!INFO]
>
>使用者端監視僅適用於具有AEM (Adobe Experience Manager) Cloud Service **2024.5.16461**&#x200B;版及更高版本的客戶。

## 概觀 {#overview}

作業遙測服務是一種效能監視技術，可即時監視網站或應用程式上的使用者端流量。 此服務著重於收集透過監控網站參與（而非使用者本身）對最佳化效能至關重要的量度和資料。 使用作業遙測時，會從URL起始開始，一直追蹤關鍵效能量度，直到將請求傳回瀏覽器為止。

## 誰能從作業遙測服務中獲益？ {#who-can-benefit-from-operational-telemetry-service}

作業遙測可協助客戶和Adobe瞭解一般使用者與AEM網站的互動情形。 作業遙測透過有限的資料收集和取樣（只監視所有頁面檢視的一小部分）來保留訪客的隱私權。

## 操作遙測服務資料抽樣 {#operational-telemetry-service-data-sampling}

傳統的網站分析解決方案會嘗試收集每位訪客的資料。 AEM的作業遙測服務只會從一小部分的頁面檢視擷取資訊。 此服務的用途是取樣和匿名處理，而非取代分析。 依預設，頁面的取樣比率為1:100。 網站運運算元目前無法增加或減少取樣速率。 為了準確估計總流量，每100次頁面檢視會從1收集資料，從而提供整體流量的可靠近似值。

在決定是否收集資料時，會依頁面檢視來決定，幾乎無法追蹤多個頁面上的互動。 根據設計，「作業遙測」沒有訪客或工作階段的概念，只有頁面檢視。

## 會收集哪些資料？ {#what-data-is-being-collected}

操作遙測服務的設計目的是將資料收集減至最少。 操作遙測收集的完整資訊集列示如下：

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
* [核心Web Vitals (CWV)](https://web.dev/articles/lcp)效能量度[最大內容繪製(LCP)](https://web.dev/articles/lcp)、[與下一個繪製(INP)的互動](https://web.dev/articles/inp)以及描述訪客體驗品質的[累積版面配置轉換(CLS)](https://web.dev/articles/cls)。

## 作業遙測如何為客戶運作 {#how-operational-telemetry-works-for-a-customer}

作業遙測會自動監視使用者端流量。 身為Adobe客戶，您不需要執行任何其他步驟，因為此服務已順暢整合至您現有的設定。 運作遙測服務已正式推出，您將自動受益於這項新功能。 操作遙測服務目前未公開任何面對客戶的量度以進行監視。 我們正在努力儘快為您提供此功能。

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Adobe如何使用作業遙測 {#how-operational-telemetry-data-is-being-used}

作業遙測資料用於下列用途：

* 找出並修正客戶地點的效能瓶頸
* 若要瞭解AEM如何與相同頁面上的其他指令碼（例如分析、鎖定目標或外部程式庫）互動，以提高相容性。
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their Operational Telemetry data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede Operational Telemetry data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by Operational Telemetry.

1. **Limitations in capturing headless API/JSON calls**

   * Operational Telemetry data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from Operational Telemetry service data creates variances from the content requests measured by CDN Analytics.
-->

## 常見問題 {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the Operational Telemetry service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **是否正在收集「下一筆繪畫的互動」、「第一位元組的時間」和「第一筆內容繪畫」量度？**

   系統會收集下一個繪圖的互動(INP)和第一個位元組的時間(TTFB)。  目前不會收集第一個內容繪製。

1. **我的網站已封鎖`/.rum`路徑，該如何修正？**

   操作遙測集合需要`/.rum`路徑才能運作。 如果您在Adobe的AEM as a Cloud Service之前使用CDN，請確定`/.rum`路徑轉送至與您的其他AEM內容相同的AEM來源。 此外，請確定此維度沒有任何調整。 或者，您也可以將Cloud Manager`rum.hlx.page`中名為[的環境變數設定為值](/help/implementing/cloud-manager/environment-variables.md#add-variables)，將作業遙測使用的主機變更為`AEM_OPTEL_EXTERNAL`。 `true`如果您想稍後變更為相同的網域請求，只需再次移除該環境變數即可。

1. **作業遙測集合是否計入合約用途的內容要求？**

   作業遙測程式庫與作業遙測集合不會計為內容要求，也不會增加報告的頁面檢視或API呼叫數。 此外，對於透過AEM as a Cloud Service使用現成CDN的客戶，[伺服器端集合](#serverside-collection)是內容請求的基礎。

1. **如何停用作業遙測？**

   Adobe建議您使用作業遙測，因為其顯著優點，且將可讓Adobe透過改善網站效能來協助您最佳化數位體驗。 此服務的設計是順暢無縫，不會影響網站的效能。

   選擇退出可能代表您錯失了改善網站流量參與度的機會。 不過，如果您遇到任何問題，可以透過[將Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables)中名為`AEM_OPTEL_DISABLED`的環境變數設定為值`true`來停用作業遙測。 如果您想在稍後再次啟用作業遙測，只需再次移除該環境變數即可。
