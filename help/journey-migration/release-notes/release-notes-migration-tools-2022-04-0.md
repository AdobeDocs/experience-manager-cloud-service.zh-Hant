---
title: AEMas a Cloud Service版本2022.4.0中移轉工具的發行說明
description: AEMas a Cloud Service版本2022.4.0中移轉工具的發行說明
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 3%

---

# AEMas a Cloud Service版本2022.4.0中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.4.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.28的發行日期為2022年4月22日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測及報告不受支援的Asset Manager API使用情形。 AEMas a Cloud Service不再支援四個API。 客戶應確保不再使用這些API，並應使用新的資產上傳方法。

* 能夠偵測內容片段範本的使用情況。 AEMas a Cloud Service上不再支援內容片段範本來建立新的內容片段。 客戶需要建立內容片段模型，以取代內容片段範本。

* 能夠偵測存放庫的資產中繼資料節點下具有超過100個子系的資產。 建議移除載入包含這類資產的資料夾時，不需要用來改善效能的中繼資料節點。

* 能夠偵測和報告所使用的資料存放區型別。

* AEM表單入口網站的模式已更新。

### 錯誤修正 {#bug-fixes-bpa}

* BPA會報告核心元件的發現，而非僅報告客戶元件。 此問題已修正。
