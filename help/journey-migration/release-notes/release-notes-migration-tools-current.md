---
title: AEM as a Cloud Service 2024.09版中移轉工具的發行說明
description: AEM as a Cloud Service 2024.09.0版中移轉工具的發行說明
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 7%

---

# AEM as a Cloud Service 2024.09.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2024.09.0中移轉工具的發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具3.0.20版的發行日期為2024年8月28日。

### 新增功能 {#what-is-new-ctt}

* 此版本不再內嵌使用者，因此，使用者對應選用功能已移除。
* 已新增OSGI設定選項，以在擷取和內嵌期間停用或啟用主體移轉（預設設定為啟用）

### 錯誤修正 {#bug-fixes-ctt}

* CTT已改善，以防止在azcopy設定中取消保護機密金鑰時發生錯誤
* CTT現在會在驗證階段複製AzCopy記錄檔時，妥善處理任何錯誤
* 變更在擷取程式期間建立的Azcopy記錄檔目錄

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.52的發行日期為2024年9月4日

### 新增功能 {#what-is-new-bpa}

* 引入新模式以偵測AEM中JCR型的事件

### 錯誤修正 {#bug-fixes-bpa}

* 修正誤判
* 改善處理來自Dispatcher的重新導向回應的穩健性
* 修正/apps/wcm/core/resources/languages/底下所有語言的NCC發現未回報的問題
* 已新增檢查以偵測節點的多重屬性是否沒有值

