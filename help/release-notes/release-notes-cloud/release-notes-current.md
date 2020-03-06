---
title: 版本2020.3.0的發行說明
description: 版本2020.3.0的發行說明
translation-type: tm+mt
source-git-commit: bcbb50f467a0e3b3047e2bb872a8fe39a9f02a1a

---


# Release Notes for AEM as a Cloud Service 2020.3.0 {#release-notes}

以下章節概述Experience Manager的雲端服務2020.3.0一般發行說明。

## Cloud Manager {#cloud-manager}

Cloud Manager 2020.3.0版的發行日期為2020年3月05日。

請依照本節瞭解Cloud Manager 2020.3.0版的新增功能和更新。

### 新功能 {#what-is-new}

* 現在，在運行生成步驟時，生成步驟的日誌可用。
* 已編輯管線執行詳細資訊頁面上的部分消息以明確說明。

### 錯誤修正 {#bug-fixes}

* 無法透過UI下載自訂和產品功能測試步驟的記錄檔。
* 當Cloud Service程式的git儲存庫建立失敗時，部署管理員角色中的用戶有時無法從此故障中恢復。
* 建立沙盒程式期間的某些用戶活動可能導致程式建立在建立非生產管線之前失敗。
* 建置步驟中使用的短暫SonarQube實例偶爾在配置的超時內無法啟動。
* 在同一Cloud Service程式中同時建立開發環境時，可能會遇到只能成功建立一個環境的情況。
* Experience Cloud的雲端服務方案通知未一致收到。
* 在特定項目中， *ResourceResolver對象應始終關閉* ，將產生Null指針異常；但是，這不會影響管線執行。

