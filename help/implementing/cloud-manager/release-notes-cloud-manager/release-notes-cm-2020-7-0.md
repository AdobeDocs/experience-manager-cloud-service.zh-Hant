---
title: AEM as a Cloud Service 版本 2020.7.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2020.7.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: b5ac4dd4-18c6-4867-b2df-53711555007f
source-git-commit: 596a7a41dac617e2fb57ba2e4891a2b4dce31fad
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.7.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2020.7.0 中 Cloud Manager 的發行說明

## 發行日期 {#release-date}

AEM as a Cloud Service 2020.7.0 中的 Cloud Manager 發行日期是 2020 年 7 月 9 日。

## 新增功能 {#whats-new-cloud-manager}

* 環境頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* 每個環境的環境變數數量提高至 200 個。

* Cloud Manager 管道現在支援客戶設定變數和機密。

   如需詳細資訊，請參閱管道變數。

* 現在支援身份驗證綁定的私有 Maven 存放庫。

* Cloud Manager 建置容器現可支援 Java 8 和 Java 11。有關更多詳細資訊，請參閱使用 Java 11 支援。

### 錯誤修正 {#bug-fixes-cm}

* 環境完全建立前，從 Cloud Manager 到開發人員控制台的連結未正確啟用。

* 直接從 Cloud Manager 連結至開發人員控制台時，系統未顯示將沙箱方案的環境解除休眠/休眠的選項。

* 非生產管道編輯頁面有時未顯示&#x200B;**取消**&#x200B;和&#x200B;**儲存**&#x200B;選項。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立新方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容的情況下，顯示發佈和發送器區段。

### 已知問題 {#known-issues}

* 由於計劃碼涵蓋範圍的計算方式有所變更，Jacoco 外掛計劃的&#x200B;*最低*&#x200B;版本現在是 0.7.5.201505241946 (2015 年 5 月發佈)。若客戶明確參考較舊版本，會在程式碼品質處理程序中收到錯誤訊息。
