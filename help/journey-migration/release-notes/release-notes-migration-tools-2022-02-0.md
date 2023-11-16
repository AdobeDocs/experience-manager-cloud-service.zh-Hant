---
title: AEMas a Cloud Service版本2022.2.0中移轉工具的發行說明
description: AEMas a Cloud Service版本2022.2.0中移轉工具的發行說明
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 7%

---

# AEMas a Cloud Service版本2022.2.0中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.2.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24的發行日期為2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測和報告使用和不使用智慧標籤的資產數量。
* 能夠偵測和報告所使用的核心元件版本。
* 能夠偵測和報告執行BPA的來源層型別（製作或發佈）。

### 錯誤修正 {#bug-fixes-bpa}

* BPA大小調整邏輯變得更快速、更有效率。
* 在某些情況下，BPA在執行時沒有增加分析的計數。 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.8.6的發行日期為2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 內容驗證 — 使用者能夠可靠地判斷「內容轉移工具」擷取的所有內容是否已成功擷取至目標例項。 若要使用此功能，請在 `System Console` 來源AEM環境的。 另請參閱 [驗證內容轉移 — 快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) 以取得更多詳細資料。

### 錯誤修正 {#bug-fixes-ctt}

* 部分使用者未對應，因為使用者對應區分大小寫。 此問題已修正。 使用者對應不再區分大小寫。
