---
title: AEM as a Cloud Service2022.2.0版中移轉工具發行說明
description: AEM as a Cloud Service2022.2.0版中移轉工具發行說明
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 6%

---

# AEM as a Cloud Service2022.2.0版中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2022.2.0中移轉工具的發行說明。

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24的發行日期為2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測有智慧標籤和沒有智慧標籤的資產數量並製作報表。
* 偵測並報告所使用核心元件的版本。
* 能夠偵測並報告執行BPA的來源層級（製作或發佈）類型。

### 錯誤修正 {#bug-fixes-bpa}

* BPA調整邏輯的製作速度更快、效率更高。
* 在某些情況下，BPA在執行時沒有增加分析計數。 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具1.8.6版的發行日期為2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 內容驗證 — 使用者能可靠判斷內容轉移工具擷取的所有內容是否皆成功內嵌至目標例項。 若要使用此功能，您必須在 `System Console` 來源AEM環境。 請參閱 [驗證內容傳輸 — 快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) 以取得更多詳細資訊。

### 錯誤修正 {#bug-fixes-ctt}

* 有些使用者未對應，因為「使用者對應」須區分大小寫。 此問題已修正。 使用者對應不再區分大小寫。
