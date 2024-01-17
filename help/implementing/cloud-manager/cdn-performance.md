---
title: CDN效能儀表板
description: 瞭解Cloud Manager如何評估內容傳遞網路(CDN)效能，以及您可以從儀表板瞭解什麼。
source-git-commit: 0d60c19638707262dab7f290f84fa873b694bc22
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---


# CDN效能儀表板 {#cdn-performance}

瞭解Cloud Manager如何評估內容傳遞網路(CDN)效能，以及您可以從儀表板瞭解什麼。

## 概觀 {#overview}

每個Cloud Manager計畫都有一個CDN效能儀表板。 此儀表板提供CDN效能的整體分數，以及趨勢、警報和必要的改善建議。

![CDN效能儀表板](assets/cdn-performance-dashboard.png)

## 存取控制面板 {#accessing}

CDN控制面板可在每個計畫的概觀頁面上取得。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在 **[我的計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 頁面，點選或按一下您要檢視其CDN控制面板的程式。

   ![我的程式頁面](assets/my-programs.png)

1. 在 **計畫總覽** 第頁，向下捲動至 **環境** 和 **管道** 卡片以檢視 **效能** 卡片。

   ![效能](assets/cdn-performance-overview.png)

## 使用控制面板 {#using}

儀表板會提供CDN效能的整體分數，以及趨勢、警報和必要的改善建議。

![CDN效能儀表板](assets/cdn-performance-dashboard.png)

如需CDN效能的詳細資訊及改善建議，請點選或按一下 **檢視趨勢**.

![績效趨勢](assets/cdn-performance-trend.png)

點選或按一下 **檢視** 在圖表下方以變更圖表的時間範圍。

如需如何改善CDN效能的建議，請選取 **Recommendations** 標籤。

![CDN建議](assets/cdn-performance-recommendations.png)

點選或按一下清單中任何建議旁的>形箭號，可檢視關於採取哪些步驟改善及問題原因的詳細資訊。

## 快取點選定義 {#cache-hit}

快取命中率是測量快取可成功填入多少內容要求，以及接收多少要求。 快取命中率越高，CDN的執行效能就越好。

>[!TIP]
>
>Adobe建議使用者將快取命中率設為99%。

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **點選**  — 從快取要求資料，但找到資料。
* **未命中**  — 從快取要求資料，但找不到資料。
* **通過**  — 從快取要求資料，但無論如何，資料設定為不快取此資料。
* **其他**  — 快取中不符合任何其他大小寫的所有資料請求。

快取量度每24小時更新一次。

>[!TIP]
>
>如需Cloud Manager和CDN如何與Dispatcher互動的詳細資訊，請參閱檔案 [AEMas a Cloud Service中的快取。](/help/implementing/dispatcher/caching.md)
