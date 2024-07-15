---
title: AEM as a Cloud Service 2022.2.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2022.2.0版中移轉工具的發行說明
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 7%

---

# AEM as a Cloud Service 2022.2.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2022.2.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24的發行日期為2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測和報告使用和不使用智慧標籤的資產數量。
* 能夠偵測和報告所使用的核心元件版本。
* 能夠偵測並報告執行BPA的來源層級型別(製作或Publish)。

### 錯誤修正 {#bug-fixes-bpa}

* BPA大小調整邏輯變得更快速、更有效率。
* 在某些情況下，BPA在執行時沒有增加分析的計數。 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.8.6的發行日期為2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 內容驗證 — 使用者可以可靠地判斷「內容轉移工具」擷取的所有內容是否已成功擷取至目標例項。 若要使用此功能，請在來源AEM環境的`System Console`中啟用它。 如需詳細資訊，請參閱[驗證內容傳輸 — 快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html#getting-started)。

### 錯誤修正 {#bug-fixes-ctt}

* 部分使用者未對應，因為使用者對應區分大小寫。 此問題已修正。 使用者對應不再區分大小寫。
