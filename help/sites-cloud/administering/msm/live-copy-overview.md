---
title: Live Copy 概觀主控台
description: 瞭解Live Copy概述控制檯的基本概念，以快速瞭解要同步內容的即時副本的狀態。
feature: Multi Site Manager
role: Admin
exl-id: 3ef7fbce-10a1-4b21-8486-d3c3706e537c
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 90%

---

# Live Copy 概觀主控台 {#live-copy-overview-console}

**Live Copy 概觀**&#x200B;主控台使您能夠：

* 檢視/管理整個網站的繼承。
   * 檢視藍圖樹和對應的 Live Copy 結構，以及它們的繼承狀態
   * 變更暫停和恢復等繼承狀態
   * 檢視藍圖和 Live Copy 屬性
* 執行推出動作。

## 開啟 Live Copy 概觀 {#opening-the-live-copy-overview}

您可以從以下位置開啟 Live Copy 概觀：

* [藍圖頁面的參考側面板 (Sites 主控台)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [藍圖頁面的屬性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 藍圖頁面的參考 {#references-to-a-blueprint-page}

**Live Copy 概觀**&#x200B;可以從 **Sites** 主控台的&#x200B;**參考**&#x200B;側面板開啟：

1. 在 **網站** 主控台， [導覽至您的Blueprint頁面並加以選取](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. 開啟&#x200B;**[參考](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**&#x200B;邊欄並選擇 **Live Copy**。

   ![來自參考邊欄的 Live Copy](../assets/live-copy-references.png)

   >[!TIP]
   >
   >您也可以先開啟參考，然後選擇藍圖。

1. 選擇 **Live Copy 概觀**&#x200B;以顯示和使用與所選藍圖相關的所有 Live Copy 的概觀。
1. 使用&#x200B;**關閉**&#x200B;以退出並返回 **Sites** 主控台。

### 藍圖頁面的屬性 {#properties-of-a-blueprint-page}

**Live Copy 概觀**&#x200B;可以在檢視藍圖頁面的屬性時開啟：

1. 開啟相關藍圖頁面的&#x200B;**屬性**。
1. 開啟 **Blueprint** 標籤 —  **即時副本概觀** 選項會顯示在頂端工具列中：

   ![藍圖屬性索引標籤](../assets/live-copy-blueprint-tab.png)

1. 選擇 **Live Copy 概觀**&#x200B;以顯示和使用與目前藍圖相關的所有 Live Copy 的概觀。

1. 使用&#x200B;**關閉**&#x200B;以退出並返回 **Sites** 主控台。

## 使用 Live Copy 概觀 {#using-the-live-copy-overview}

**Live Copy 概觀**&#x200B;視窗概要顯示與所選頁面相關之 Live Copy 的狀態。

![Live Copy 概觀視窗](../assets/live-copy-overview.png)

推出取決於特定推出設定中定義的同步動作。某些動作取決於對內容的修改。但是，也有很多動作並不取決於對內容的修改，而是取決於事件 (例如頁面啟動)。此類事件不會修改內容，但會修改與內容相關的內部屬性。

狀態欄位也取決於特定推出設定中定義的同步動作，並指示自上次成功推出後是否對藍圖或 Live Copy 進行了任何此類動作。狀態欄位將僅反映特定推出設定中的動作。如果從未對 Live Copy 執行過成功的推出，則狀態將始終顯示為最新。

例如，推出設定定義為 `targetActivate`。因此，推出將完全取決於啟動事件。狀態欄位將僅指示自上次成功推出以來是否發生任何啟動事件。

**Live Copy 概觀**&#x200B;也可用於對 Live Copy 執行動作：

1. 開啟 **Live Copy 概觀**。
1. 選取所需的Blueprint或即時副本頁面，然後工具列會更新以顯示可用的動作。 可用的[動作](overview.md#terms-used)取決於您選擇的是[藍圖](#actions-for-a-blueprint-page)還是 [Live Copy](#actions-for-a-live-copy-page) 頁面。

### 藍圖頁面的動作 {#actions-for-a-blueprint-page}

選擇藍圖頁面時，可以執行以下動作：

![藍圖的 Live Copy 概觀動作](../assets/live-copy-overview-actions-blueprint.png)

* **編輯** - 開啟藍圖頁面以進行編輯。
* **[推出](overview.md#rollout-and-synchronize)** - 執行推出以將變更從來源推送到 Live Copy。

### Live Copy 頁面的動作 {#actions-for-a-live-copy-page}

選擇 Live Copy 頁面時，可以執行以下動作：

![Live Copy 的 Live Copy 概觀動作](../assets/live-copy-overview-actions.png)

* **編輯** - 開啟 Live Copy 頁面進行編輯。
* **[關係狀態](#relationship-status)** - 檢視關於狀態和繼承的資訊。
* **[同步](overview.md#rollout-and-synchronize)** - 同步 Live Copy 以將變更從來源推送到 Live Copy。
* **[重設](creating-live-copies.md#resetting-a-live-copy-page)** - 重設 Live Copy 頁面以刪除所有繼承取消，並將頁面返回到與來源頁面相同的狀態。
* **[暫停](overview.md#suspending-and-cancelling-inheritance-and-synchronization)** - 暫時停用 Live Copy 與其藍圖頁面之間的即時關係。
* **[恢復](creating-live-copies.md#resuming-inheritance-for-a-page)** - 恢復允許您回復暫停的關係。
* **[分離](overview.md#detaching-a-live-copy)** - 永久移除 Live Copy 與其藍圖頁面之間的即時關係。

## 關係狀態 {#relationship-status}

**關係狀態**&#x200B;主控台有兩個索引標籤，提供一系列功能。

* [關係狀態](#relationship-status-tab)
* [Live Copy](#live-copy-tab)

### 關係狀態 {#relationship-status-tab}

此索引標籤提供藍圖和 Live Copy 之間關係狀態的詳細資訊。

![關係狀態索引標籤](../assets/live-copy-relationship-status.png)

### Live Copy {#live-copy-tab}

此索引標籤允許您檢視和編輯 Live Copy 設定。

![Live Copy 索引標籤](../assets/live-copy-relationship-status-live-copy.png)
