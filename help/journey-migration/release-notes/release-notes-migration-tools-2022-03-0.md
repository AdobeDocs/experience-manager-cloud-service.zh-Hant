---
title: AEM as a Cloud Service 2022.3.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2022.3.0版中移轉工具的發行說明
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# AEM as a Cloud Service 2022.3.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2022.3.0中移轉工具的發行說明。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26的發行日期為2022年3月16日。

### 新增功能 {#what-is-new-bpa}

* 可偵測未處理的資產。 如果偵測到未處理的資產，這些資產必須設定為已處理，或在內容轉移期間從移轉集移除，以避免在內容擷取期間遇到問題。
* 能夠偵測內容是否超過1000個虛名URL。 使用大量虛名URL並非最佳實務，因為這會在Dispatcher和Publish伺服器上增加負載。
* 可識別Oak索引定義相關問題，並偵測與AEM as a Cloud Service不相容。
* 能夠偵測和報告外部器設定的使用情況。 在AEM as a Cloud Service Externalizer中，設定是由Cloud Manager所設定。 因此，必須重構現有的外部器設定以保持相容性。

### 錯誤修正 {#bug-fixes-bpa}

* 在某些情況下，BPA無法執行，因為FormsSelectiveFeaturesAnalysis擲回宣告錯誤。
* BPA將與WRK模式相關的發現回報為MAJOR而非CRITICAL。
* BPA錯誤地將ui.apps中與Oak索引定義相關的發現回報為CRITICAL。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

「內容轉移工具v1.9.0」的發行日期為2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 檢查大小護欄 — 內容轉移工具檢查大小功能有助於減少失敗的內容轉移。 使用檢查大小功能，使用者可以在擷取前先判斷在`crx-quickstart`子目錄中是否有足夠的磁碟空間。 此外，他們可以估計移轉集大小，並驗證其是否受支援。 如果違反了其中一項或兩項檢查，使用者會在CTT使用者介面中看到警告。 有了這道護欄，您可以避免內容轉移失敗，並主動與Adobe客戶服務討論移轉選項。 如需詳細資訊，請參閱[決定移轉集大小和磁碟空間](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hant#migration-set-size)。
