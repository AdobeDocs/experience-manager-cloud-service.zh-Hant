---
title: AEM as a Cloud Service2022.9.0版中移轉工具發行說明
description: AEM as a Cloud Service2022.9.0版中移轉工具發行說明
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
source-git-commit: dd4515bdbba81dcec0868c3058c7745775cc80ff
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 5%

---

# AEM as a Cloud Service2022.9.0版中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2022.9.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.34的發行日期為2022年9月12日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可偵測客戶是否已新增自訂記錄器設定並製作報表。 AEMas a Cloud Service不支援自訂記錄檔。 所有日誌檔案都需要管道傳送到 `error.log`
* BPA現在可以報告客戶存放庫中存在的不同二進位MIME類型，以及與其相關聯的計數。

### 錯誤修正 {#bug-fixes-bpa}

* 在單一模式下顯示大量結果時，BPA UI出現轉譯問題。 此問題已修正。
* BPA錯誤地將某些發現報告為具有嚴重性的不相容更改。 此問題已修正。
