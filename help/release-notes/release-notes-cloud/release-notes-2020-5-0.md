---
title: Adobe Experience Manager 雲端服務 2020.5.0 版發行說明
description: Experience Manager 2020.5.0 版發行說明
translation-type: ht
source-git-commit: 06a56b0ca8000a41fe4e492206459b1525aae59d
workflow-type: ht
source-wordcount: '374'
ht-degree: 100%

---


# AEM 雲端服務 2020.5.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.5.0 版的一般發行說明。

## 發行日期 {#release-date}

[!DNL Experience Manager] 雲端服務 2020.5.0 版的發行日期為 2020 年 5 月 7 日。

## AEM Sites 新增功能 {#aem-sites}

請詳閱本節，了解 AEM 雲端服務 2020.5.0 版中 AEM Sites 的新增功能和更新。

* 現在起，以非同步工作型態移動及轉出大量頁面後，可取得詳細工作資訊。
* 現在複製/貼上頁面樹狀結構時，可選擇僅貼上根頁面或一併貼上樹狀結構的子頁面。
* 現在起，匯出至 Adobe Target 工作區的 AEM 體驗片段在 Target 中會顯示為不重複的選件類型和選件來源。
* MSM - 使用&#x200B;*發佈*&#x200B;觸發程序時，現在系統會成功轉出即時副本來源中元件的刪除事件，亦即將即時副本來源中已刪除的元件從即時副本中刪除。
* MSM - 從即時副本來源轉出即時副本元件後，同一元件現在會重新命名為 *_msm_moved*。


## Cloud Manager 新增功能 {#cloud-manager}

請詳閱本節，了解 AEM 雲端服務 2020.5.0 版中 Cloud Manager 的新增功能和更新。

### 新功能 {#what-is-new}

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


