---
title: AEM as a Cloud Service 版本 2024.09 中移轉工具的發行說明
description: AEM as a Cloud Service 版本 2024.09.0 中移轉工具的發行說明
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: ht
source-wordcount: '230'
ht-degree: 100%

---

# AEM as a Cloud Service 版本 2024.09.0 中移轉工具的發行說明 {#release-notes}

本頁面概述 AEM as a Cloud Service 2024.09.0 中移轉工具的發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具 v3.0.20 的發行日期為 2024 年 8 月 28 日。

### 新增功能 {#what-is-new-ctt}

* 此版本將不再擷取使用者，因此選用的使用者對應功能已移除。
* 新增 OSGI 設定選項，用於在摘取和擷取過程中停用或啟用主體移轉 (預設設定為啟用)

### 錯誤修正 {#bug-fixes-ctt}

* 改進 CTT，以防止在 azcopy 設定中取消保護祕密金鑰時出現錯誤
* 現在起，CTT 可在驗證階段複製 AzCopy 記錄時，正常地處理的任何錯誤
* 變更摘取過程中建立的 azcopy 記錄目錄

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析工具 v2.1.52 的發行日期為 2024 年 9 月 4 日

### 新增功能 {#what-is-new-bpa}

* 引進新模式來偵測 AEM 中的 JCR 型事件

### 錯誤修正 {#bug-fixes-bpa}

* 修正誤報
* 提升處理 Dispatcher 重新導向回應的穩健性
* 修正 /apps/wcm/core/resources/linguals/ 下所有語言的 NCC 發現結果未報告問題
* 新增檢查以偵測節點的多重屬性是否沒有值

