---
title: Universal Editor 2024.11.13發行說明
description: 這些是2024.11.13版通用編輯器的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 98795cab471470442cf5c424a67ce2846cfe85dc
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 5%

---


# Universal Editor 2024.11.13發行說明 {#release-notes}

以下是2024年11月13日發行的Universal Editor的發行說明。

>[!TIP]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **CORS逾時上的[重試選項]：**&#x200B;隨著[版本2024.09.26，](/help/release-notes/universal-editor/2024/2024-09-26.md)編輯器無法建立與已載入頁面的連線，導致無法無休止地載入狀態，因此引入錯誤面板。
   * 在此版本中，編輯器會自動不斷重試，連線建立後，即可繼續編輯。
   * 這對於需要超過一分鐘逾時才能初始化的頁面特別有用。
* **開發人員的擴充性增強功能：** Universal Editor現在支援將事件廣播到擴充功能，讓擴充功能開發人員可以訂閱[個事件。](/help/implementing/universal-editor/events.md)
   * 如此可讓開發人員在其自訂擴充功能中[回應編輯器事件。](/help/implementing/universal-editor/customizing.md#extending)
* **持續性元件選擇：**&#x200B;編輯器中選取的元件現在會持續存在，即使在重新整理瀏覽器之後也是如此。
   * 這可確保在重新載入頁面時，使用者可以繼續工作而不會失去內容。
* **本地化的快速連結：**&#x200B;首頁畫面上的&#x200B;**快速連結**&#x200B;區段現在提供檔案的本地化連結，讓使用者根據其語言偏好設定輕鬆存取相關的指南。
* **進階偵錯的要求ID：**&#x200B;錯誤通知現在在詳細資訊區段中包含&#x200B;**要求ID**，這與`x-request-id header`相關。
   * 這可讓Adobe工程團隊更輕鬆地透過將這些錯誤與內部記錄進行比對來追蹤和診斷問題。

## 其他改善專案 {#other-improvements}

* **修正長內容樹狀結構標籤：**&#x200B;解決&#x200B;**內容樹狀結構**&#x200B;面板中的長標籤被截斷的問題
   * 這可確保在內容重新排序時始終顯示拖放控點。
* **修正長屬性標籤：**&#x200B;解決&#x200B;**屬性**&#x200B;面板中的長欄位標籤與欄位驗證資訊重疊的錯誤
* **屬性面板中的水準捲動：**&#x200B;修正&#x200B;**屬性**&#x200B;面板中的寬元素導致水準捲動的問題
* **已修正通知期間的非使用中工具列：**&#x200B;顯示[快顯通知](https://spectrum.adobe.com/page/toast/)時，頂端&#x200B;**Adobe Experience Cloud**&#x200B;工具列已完全運作。
* **改善穩定性：**&#x200B;新增錯誤界限以處理非預期的值，避免單一轉譯器或驗證器失敗時整個UI損毀，提高健全性
