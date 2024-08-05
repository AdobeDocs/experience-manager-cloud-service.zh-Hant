---
title: AEM as a Cloud Service 2024.07版中移轉工具的發行說明
description: AEM as a Cloud Service 2024.07.0版中移轉工具的發行說明
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 4f01ca0076248442fe93161bbc8b98bffb64551b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 8%

---

# AEM as a Cloud Service 2024.07.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2024.07.0中移轉工具的發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v3.0.16的發行日期為2024年7月。

### 新增功能 {#what-is-new-ctt}

* 發生失敗時自動上傳CTT擷取記錄。
* 使用者現在可以在更新擷取金鑰後成功執行內嵌。
* 新增支援透過AzureDataStore使用Azure存取金鑰和秘密金鑰執行CTT擷取。
* 現在，當使用無效的金鑰建立移轉集時，使用者會收到正確的錯誤訊息。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.50的發行日期為2024年5月。

### 錯誤修正 {#bug-fixes-bpa}

* Best Practices Analyzer現在會偵測大於16MB的所有節點
* 造成NCC發現點偶爾發生的競爭條件已修正。
