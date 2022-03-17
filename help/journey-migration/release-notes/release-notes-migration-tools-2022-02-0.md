---
title: 《 2022.2.0版中遷移工具AEM發行說明》
description: 《 2022.2.0版中遷移工具AEM發行說明》
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 6%

---

# 《 2022.2.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.2.0中遷移工具的AEM發行說明。

## 最佳做法分析器 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.24版的發佈日期為2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠檢測和報告具有和不具有智慧標籤的資產數。
* 能夠檢測和報告所使用的核心元件版本。
* 能夠檢測並報告執行BPA的源層（作者或發佈）的類型。

### 錯誤修正 {#bug-fixes-bpa}

* BPA規模邏輯的製作更快、更高效。
* 在某些情況下，BPA在運行時未增加分析計數。 這個已經修復了。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.8.6的發佈日期為2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 內容驗證 — 用戶能夠可靠地確定內容傳輸工具提取的所有內容是否已成功地被引入目標實例。 要使用此功能，您需要在 `System Console` 來源環AEM境。 請參閱 [驗證內容傳輸 — 入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) 的子菜單。

### 錯誤修正 {#bug-fixes-ctt}

* 某些用戶未映射，因為用戶映射區分大小寫。 這個已經修復了。 用戶映射不再區分大小寫。
