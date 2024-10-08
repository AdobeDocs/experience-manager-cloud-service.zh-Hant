---
title: AEM as a Cloud Service 2024.05.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2024.05.0版中移轉工具的發行說明
feature: Release Information
role: Admin
exl-id: f50a74fa-ad7d-4837-b0a1-9945c32af02f
source-git-commit: 3b2ed44b438fe8587a9b9603ddfacc41111fb903
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 6%

---

# AEM as a Cloud Service 2024.05.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2024.05.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.50的發行日期為2024年5月。

### 新增功能 {#what-is-new-bpa}

* Best Practices Analyzer (BPA)現在支援將BPA產生的報告直接自動上傳到Cloud Acceleration Manager (CAM)。 使用者不再需要手動下載報告並將其上傳到CAM。 如需詳細資訊，請參閱[使用最佳做法分析工具](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)

### 錯誤修正 {#bug-fixes-bpa}

* Best Practices Analyzer現在會偵測大於16MB的所有節點
* 造成NCC發現點偶爾發生的競爭條件已修正。

## Cloud Acceleration Manager {#cam-release}

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager (CAM)現在支援將BPA產生的報表直接自動上傳至CAM。 若要深入瞭解，請參閱Cloud Acceleration Manager中的[整備階段 — 使用最佳實務分析卡](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

* Cloud Acceleration Manager現在會根據節點數、資料存放區大小等因素，提供擷取可能需要多久的預估值。 透過[將內容擷取到Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)瞭解更多資訊
