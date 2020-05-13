---
title: Adobe Experience Manager 雲端服務 2020.5.0 版發行說明
description: Experience Manager 2020.5.0 版發行說明
translation-type: tm+mt
source-git-commit: 94a732f56929ad4af23855152e258f82ad61ee2c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 29%

---


# AEM 雲端服務 2020.5.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.5.0 版的一般發行說明。

## Cloud Manager {#cloud-manager}

請詳閱本節，瞭解 AEM 雲端服務 2020.5.0 版中 Cloud Manager 的新增功能和更新。

### 新功能 {#what-is-new}

* 已新增6個額外的程式碼品質規則，以協助客戶在規劃移轉至雲端服務時找出潛在問題。
* 已新增新 *的「雲端服務相容性* 」度量，以總結相容性相關問題的數目。
* 未能建立的環境現在將在建立失敗大約24小時後自動刪除，除非已刪除。
* 「活動」頁和「管線執行清單」API的效能已改進。
* 程式碼品質記錄現在包含完整的堆疊追蹤以找出例外。

### 錯誤修正 {#bug-fixes}

* 在生產管線執行期間，總覽頁面上會顯示誤導性資訊卡。
* DontImplementOrExtendProviderTypesPomCheck代碼質量規則有時可能會產生Null指標異常。 **
* 概述頁面中的某些檔案連結無法正常運作。
* 「建立環境」對話方塊無法在Safari中正確呈現。
* 概述頁面上的某些卡片無法正確顯示實體名稱。
* 在某些情況下，「建置映像」無法成功下載客戶包。

