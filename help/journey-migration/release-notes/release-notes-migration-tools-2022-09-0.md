---
title: 《 2022.9.0版中遷移工具AEM發行說明》
description: 《 2022.9.0版中遷移工具AEM發行說明》
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
source-git-commit: dd4515bdbba81dcec0868c3058c7745775cc80ff
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 5%

---

# 《 2022.9.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.9.0中遷移工具的AEM發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.34版的發佈日期為2022年9月12日。

### 新增功能 {#what-is-new-bpa}

* BPA現在可以檢測並報告客戶是否添加了自定義記錄器配置。 AEMas a Cloud Service不支援自定義日誌檔案。 所有日誌檔案都需要管道連接到 `error.log`
* BPA現在可以報告客戶儲存庫中存在的不同二進位MIME類型以及與它們關聯的計數。

### 錯誤修正 {#bug-fixes-bpa}

* 當在單個模式下顯示大量查找結果時，BPA UI出現呈現問題。 這個已經修復了。
* BPA錯誤地將某些發現報告為嚴重性不相容的更改。 這個已經修復了。
