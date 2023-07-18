---
title: AEMas a Cloud Service2023.07.0版中移轉工具的發行說明
description: AEMas a Cloud Service2022.07.0版中移轉工具的發行說明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 88227693b7dfc3cbd30751718dc85e55ee67bb96
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 7%

---

# AEMas a Cloud Service2023.07.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.07.0中移轉工具發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.42的發行日期為2023年7月6日。

### 新增功能 {#what-is-new-bpa}

* 此版本的Best Practices Analyzer已新增多個最佳實務模式。 這些類別包括：
   * 識別最低維護任務設定
   * 偵測長時間執行/大量查詢
   * 偵測大量處於執行中或過時狀態的作者工作流程
   * 偵測OSGI Apache sling作業設定
   * 偵測自訂Guava快取

### 錯誤修正 {#bug-fixes-bpa}

* BPA已經過改良，以防止產生含有大量結果之報告的記憶體不足報告失敗。
* BPA已經過改良，可偵測路徑中的逸出字元，以防止將內容移轉至AEMas a Cloud Service時發生內容擷取失敗。


