---
title: AEMas a Cloud Service版2023.03.0中移轉工具發行說明
description: AEMas a Cloud Service版2022.03.0中移轉工具發行說明
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 5815dacd2806cc7886aa0c7c5c9fd329306b3e1b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 6%

---

# AEMas a Cloud Service版2023.03.0中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2022.03.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.40的發行日期為2023年3月3日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以檢測並報告發生衝突的節點 — 具有相同的節點 `jcr:uuid`. 這類發現被標為重要，因為在將內容移至AEMas a Cloud Service時，這可能導致內容擷取失敗。
* BPA現在可以偵測事件接聽程式的使用情況並製作報表。 建議您在移至AEM as a Cloud Service時，將此類型的事件處理機制重新調整為sling工作。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告誤判 `grouprendercondition`. 此問題已修正。