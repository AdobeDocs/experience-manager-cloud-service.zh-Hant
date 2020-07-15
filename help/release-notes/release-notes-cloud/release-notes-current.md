---
title: Adobe Experience Manager 雲端服務 2020.7.0 版發行說明
description: Experience Manager 2020.7.0 版發行說明
translation-type: tm+mt
source-git-commit: 74abf1c4cc6ae449a81e3e40d073bfcb23b056e8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 29%

---


# AEM 雲端服務 2020.7.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.7.0 版的一般發行說明。

## Cloud Manager 新增功能 {#cloud-manager}

請詳閱本節，了解 AEM 雲端服務 2020.7.0 版中 Cloud Manager 的新增功能和更新。

### 發行日期 {#release-date}

Cloud Manager  2020.7.0版的發行日期為2020年7月9日。

### 新功能 {#what-is-new-cloud-manager}

* 環境頁面已重新設計。

* 休眠的環境現在在Cloud Manager中，當休眠時會顯示離散狀態。

* Cloud Manager組建容器現在支援Java 8和Java 11。

### 錯誤修正 {#bug-fixes-cm}

* 從Cloud Manager到Developer Console的連結在完全建立環境之前未正確啟用。

* 直接從Cloud Manager連結至「開發人員主控台」時，不會顯示沙盒程式環境的解除休眠／休眠選項。

* 「非 **生產管線** 」(Non-Production Pipeline)編輯頁面上的「取消」(Cancel)和「保存 **** 」(Save)選項並不總是可見。

* 程式碼品質處理中的某些失敗可能會導致記錄檔無法正確產生。

* 建立新程式時，建議的名稱有時會返回現有程式名稱的副本。

* 有些大型管線步驟記錄無法一貫地透過使用者介面下載。

* 驗證環境名稱時會出現一個逐項錯誤。

* 「環境」頁面有時會在無顯示時顯示發佈和分派器區段。