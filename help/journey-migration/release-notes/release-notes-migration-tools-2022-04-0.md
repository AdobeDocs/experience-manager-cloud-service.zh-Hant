---
title: AEM as a Cloud Service2022.4.0版中移轉工具發行說明
description: AEM as a Cloud Service2022.4.0版中移轉工具發行說明
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
source-git-commit: 717b2c851a18ef5171d64a462509ce08fb87a59c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---

# AEM as a Cloud Service2022.4.0版中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2022.4.0中移轉工具的發行說明。

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.28的發行日期為2022年4月22日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測到不支援的Asset Manager API的使用情況並製作報表。 AEM as a Cloud Service中不再支援4個API。 客戶應確定不再使用這些API，且應使用新的資產上傳方法。

* 偵測內容片段範本使用情形的功能。 在AEM as a Cloud Service上建立新內容片段時不再支援內容片段範本。 客戶需要建立內容片段模型來取代內容片段範本。

* 能夠偵測存放庫中資產之中繼資料節點底下有超過100個子系的資產。 建議您移除載入包含這類資產的資料夾時，不需要改善效能的中繼資料節點。

* 偵測所使用資料存放區類型並製作報表的功能。

* AEM表單入口網站模式已更新。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告核心元件的調查結果，而非僅報告客戶元件。 此問題已修正。
