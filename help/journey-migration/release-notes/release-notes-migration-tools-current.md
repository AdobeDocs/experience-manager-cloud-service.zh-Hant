---
title: 《 2022.4.0版中遷移工具AEM發行說明》
description: 《 2022.4.0版中遷移工具AEM發行說明》
feature: Release Information
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---

# 《 2022.4.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.4.0中遷移工具的AEM發行說明。

## 最佳做法分析器 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.28版的發佈日期為2022年4月22日。

### 新增功能 {#what-is-new-bpa}

* 能夠檢測和報告不支援的Asset Manager API的使用情況。 as a Cloud Service中不再支援四個APIAEM。 客戶應確保不再使用這些API，並應使用新的資產上載方法。

* 能夠檢測內容片段模板的使用情況。 不再支援在as a Cloud Service上建立新內容片段的內容片段模AEM板。 客戶將需要建立內容片段模型以替換內容片段模板。

* 能夠在儲存庫中資產的元節點下檢測具有100個以上子體的資產。 建議在載入包含此類資產的資料夾時刪除不需要的元資料節點來提高效能。

* 能夠檢測和報告所使用的資料儲存類型。

* 已為窗體門戶AEM更新模式。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告的是核心元件的調查結果，而不是只報告客戶元件。 這個已經修復了。