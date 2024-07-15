---
title: AEM as a Cloud Service 2023.07.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2023.07.0版中移轉工具的發行說明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---

# AEM as a Cloud Service 2023.07.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2023.07.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.42的發行日期為2023年7月6日。

### 新增功能 {#what-is-new-bpa}

* 此版本的Best Practices Analyzer新增了多個最佳實務模式。 這些類別包括：
   * 識別最低維護任務設定
   * 偵測長時間執行/大量查詢
   * 正在偵測大量處於執行中或過時狀態的作者工作流程
   * 偵測OSGI Apache Sling作業設定
   * 偵測自訂Guava快取

### 錯誤修正 {#bug-fixes-bpa}

* BPA已改善，以防止針對發現大量問題的報告產生記憶體不足的報告失敗。
* BPA已經過改善，可偵測路徑中的逸出字元，以防止將內容移轉至AEM as a Cloud Service時內容擷取失敗。
