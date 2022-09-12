---
title: AEM as a Cloud Service2022.3.0版中移轉工具發行說明
description: AEM as a Cloud Service2022.3.0版中移轉工具發行說明
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# AEM as a Cloud Service2022.3.0版中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2022.3.0中移轉工具的發行說明。

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26的發行日期為2022年3月16日。

### 新增功能 {#what-is-new-bpa}

* 偵測未處理資產的功能。 如果偵測到未處理的資產，這些資產需要設為已處理，或需在內容轉移期間從移轉集中移除，以避免在內容擷取期間遇到問題。
* 偵測內容是否超過1000個虛名URL的功能。 使用大量虛名URL並非最佳作法，因為這會對Dispatcher和Publish伺服器造成負載。
* 能識別Oak索引定義相關問題，並偵測與AEMas a Cloud Service不相容。
* 能夠檢測並報告外部化程式配置的使用情況。 在AEMas a Cloud Service外部化程式設定中，由Cloud Manager設定，因此需重構現有外部化程式設定以維持相容性。

### 錯誤修正 {#bug-fixes-bpa}

* 在某些情況下，BPA無法運行，因為FormsSelectiveFeaturesAnalysis擲回斷言錯誤。 此問題已修正。
* BPA將與工作模式有關的結果報告為MAJOR，而非CRITICAL。 此問題已修正。
* BPA在ui.apps中以CRITICAL形式錯誤報告與OAK索引定義相關的發現。 此問題已修正。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具1.9.0版的發行日期為2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 檢查大小護欄 — 「內容轉移工具檢查大小」功能有助於減少失敗的內容轉移。  使用「檢查大小」功能，用戶可以1)確定他們在 `crx-quickstart` 子目錄，提取前，和2)預估移轉集大小並確認是否支援。 如果違反上述一項或兩項檢查，使用者在CTT UI中會看到警告。 透過此護欄，您可以避免內容傳輸失敗，並主動與Adobe客戶服務討論移轉選項。 請參閱 [確定遷移集大小和磁碟空間](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) 以取得更多詳細資訊。
