---
title: AEM as a Cloud Service 2022.4.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2022.4.0版中移轉工具的發行說明
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 3%

---

# AEM as a Cloud Service 2022.4.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2022.4.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.28的發行日期為2022年4月22日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測及報告不受支援的Asset Manager API使用情形。 AEM as a Cloud Service不再支援四個API。 客戶應確保不再使用這些API，並應使用新的資產上傳方法。

* 能夠偵測內容片段範本的使用情況。 AEM as a Cloud Service上不再支援內容片段範本來建立新的內容片段。 客戶需要建立內容片段模型，以取代內容片段範本。

* 能夠偵測存放庫的資產中繼資料節點下具有超過100個子系的資產。 建議移除載入包含這類資產的資料夾時，不需要用來改善效能的中繼資料節點。

* 能夠偵測和報告所使用的資料存放區型別。

* AEM表單入口網站的模式已更新。

### 錯誤修正 {#bug-fixes-bpa}

* BPA會報告核心元件的發現，而非僅報告客戶元件。 此問題已修正。
