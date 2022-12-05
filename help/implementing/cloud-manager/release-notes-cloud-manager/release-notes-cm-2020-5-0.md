---
title: AEM as a Cloud Service 版本 2020.5.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2020.5.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: 9f534858-d18f-4224-8b94-9583a05aed95
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.5.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2020.5.0 中 Cloud Manager 的發行說明

## 發行日期 {#release-date}

AEM as a Cloud Service 2020.5.0 中的 Cloud Manager 發行日期是 2020 年 5 月 07 日。

## 新增功能 {#whats-new-cloud-manager}

* 新增 6 項額外的程式碼品質規則，協助客戶在規劃 Cloud Service 遷移作業時找出潛在問題。
* 加入最新的 *Cloud Service 相容性*&#x200B;指標，概述相容性相關問題的數目。
* 現在起，系統會在環境建立失敗後約 24 小時內，自動刪除無法建立的環境 (除非該環境已遭刪除)。
* 改善「活動」頁面和「管道執行清單 API」的效能。
* 程式碼品質記錄現已增加例外狀況的完整堆疊追蹤。

### 錯誤修正  {#bug-fixes}

* 執行生產管道時，概覽頁面顯示資訊不正確的卡片。
* *DontImplementOrExtendProviderTypesPomCheck* 程式碼品質規則有時可能產生「Null 指標例外狀況」。
* 概覽頁面中的部分文件連結無法正常運作。
* 「建立環境」對話框在 Safari 中無法正確顯示。
* 概覽頁面中的特定卡片未正確顯示實體名稱。
* 某些情況下，「建置影像」無法成功下載客戶封裝。
