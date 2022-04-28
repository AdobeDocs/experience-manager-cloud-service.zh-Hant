---
title: 《 2022.3.0版中遷移工具AEM發行說明》
description: 《 2022.3.0版中遷移工具AEM發行說明》
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# 《 2022.3.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.3.0中遷移工具的AEM發行說明。

## 最佳做法分析器 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.26版的發佈日期為2022年3月16日。

### 新增功能 {#what-is-new-bpa}

* 檢測未處理資產的能力。 如果檢測到未處理的資產，則這些資產要麼需要設定為已處理，要麼需要在內容傳輸期間從遷移集中刪除，以避免在內容接收期間遇到問題。
* 能夠檢測內容是否具有1000個以上虛擬URL。 使用大量虛擬URL不是最佳做法，因為它給Dispatcher和Publish伺服器載入了負載。
* 能夠識別與Oak索引定義相關的問題並檢測與AEMas a Cloud Service的不相容。
* 能夠檢測並報告外部化器配置的使用情況。 在AEMas a Cloud Service外部化器配置中，由雲管理器設定，因此需要重新構造現有外部化器配置，以保持相容性。

### 錯誤修正 {#bug-fixes-bpa}

* 在某些情況下，BPA無法運行，因為FormsSelectiveFeaturesAnalysis引發斷言錯誤。 這個已經修復了。
* 雙酚A以主要而非關鍵的方式報告與工作模式有關的調查結果。 這個已經修復了。
* BPA錯誤地將與ui.apps中的OAK索引定義相關的發現報告為CRITICAL。 這個已經修復了。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.9.0的發佈日期為2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 檢查大小護欄 — 內容傳輸工具檢查大小功能有助於減少失敗的內容傳輸。  使用「檢查大小」功能，用戶可以1)確定他們在 `crx-quickstart` 在提取之前，先為子目錄，然後2)估計遷移集大小並驗證是否支援遷移集大小。 如果違反了其中一項或兩項檢查，用戶將在CTT UI中看到警告。 通過此保證，您可以避免內容傳輸失敗，並主動與Adobe客戶服務部門討論遷移選項。 請參閱 [確定遷移集大小和磁碟空間](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) 的子菜單。
