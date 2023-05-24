---
title: AEMas a Cloud Service2022.3.0版中移轉工具的發行說明
description: AEMas a Cloud Service2022.3.0版中移轉工具的發行說明
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 4%

---

# AEMas a Cloud Service2022.3.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.3.0中移轉工具發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26的發行日期為2022年3月16日。

### 新增功能 {#what-is-new-bpa}

* 可偵測未處理的資產。 如果偵測到未處理的資產，則需要將這些資產設定為已處理，或在內容轉移期間從移轉集移除，以避免在內容擷取期間遇到問題。
* 可偵測內容是否超過1000個虛名URL。 使用大量虛名URL不是最佳做法，因為它會讓Dispatcher和Publish伺服器承受負載。
* 能夠識別Oak索引定義相關問題並偵測與AEMas a Cloud Service的不相容性。
* 能夠偵測並報告外部器設定的使用狀況。 在AEM中，as a Cloud Service的外部化工具設定是由Cloud Manager設定，因此，需要重構現有的外部化工具設定以保持相容性。

### 錯誤修正 {#bug-fixes-bpa}

* 在某些情況下，BPA無法執行，因為FormsSelectiveFeaturesAnalysis擲回判斷提示錯誤。 此問題已修正。
* BPA將與WRK模式相關的發現回報為MAJOR而非CRITICAL。 此問題已修正。
* BPA錯誤地將ui.apps中與OAK索引定義相關的發現回報為CRITICAL。 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.9.0的發行日期為2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 檢查大小護欄 — 內容轉移工具檢查大小功能有助於減少失敗的內容轉移。  使用「檢查大小」功能，使用者可以1)判斷是否有足夠的磁碟空間 `crx-quickstart` 子目錄（擷取之前），以及2)預估移轉集大小並驗證其是否受支援。 如果違反了其中一項或兩項檢查，使用者將在CTT UI中看到警告。 有了這道護欄，您可以避免內容轉移失敗，並主動與Adobe客戶服務討論移轉選項。 請參閱 [決定移轉集大小和磁碟空間](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) 以取得更多詳細資料。
