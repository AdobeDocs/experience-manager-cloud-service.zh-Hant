---
title: Cloud Manager的發行說明，作AEM為Cloud Service版本2020.5.0
description: Cloud Manager的發行說明，作AEM為Cloud Service版本2020.5.0
feature: 發行資訊
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 71%

---


# Adobe Experience ManagerCloud Manager的發行說明，Cloud Service2020.5.0 {#release-notes}

本頁概述了Cloud Manager的發行說明，AEM作為Cloud Service2020.5.0。

## 發行日期 {#release-date}

Cloud Manager作為2020.5.0版Cloud ServiceAEM的發行日期為2020年5月7日。

## 新功能 {#whats-new-cloud-manager}

* 新增 6 項額外的程式碼品質規則，協助客戶在規劃 Cloud Service 遷移作業時找出潛在問題。
* 加入最新的 *Cloud Service 相容性*&#x200B;指標，概述相容性相關問題的數目。
* 現在起，系統會在環境建立失敗後約 24 小時內，自動刪除無法建立的環境 (除非該環境已遭刪除)。
* 改善「活動」頁面和「管道執行清單 API」的效能。
* 程式碼品質記錄現已增加例外狀況的完整堆疊追蹤。

### 錯誤修正 {#bug-fixes}

* 執行生產管道時，概覽頁面顯示資訊不正確的卡片。
* *DontImplementOrExtendProviderTypesPomCheck* 程式碼品質規則有時可能產生「Null 指標例外狀況」。
* 概覽頁面中的部分文件連結無法正常運作。
* 「建立環境」對話框在 Safari 中無法正確顯示。
* 概覽頁面中的特定卡片未正確顯示實體名稱。
* 某些情況下，「建置影像」無法成功下載客戶封裝。
