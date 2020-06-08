---
title: 2020.3.0 版發行說明
description: 2020.3.0 版發行說明
translation-type: tm+mt
source-git-commit: 27225bf4b918f39892ac9ab6f46deb97479f08e8
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 100%

---


# AEM 雲端服務 2020.3.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.3.0 版的一般發行說明。


## 發行日期 {#release-date}

Experience Manager 雲端服務的 2020.3.0 的發行日期為 2020 年 3 月 5 日。

## Cloud Manager {#cloud-manager}

請詳閱本節，瞭解 AEM 雲端服務 2020.3.0 版中 Cloud Manager 的新增功能和更新。

### 新功能 {#what-is-new}

* 現在建置步驟執行時，建置步驟記錄可供同時使用。
* 管道執行詳細資訊頁面上的部分訊息經過編輯，以更明確說明。

### 錯誤修正 {#bug-fixes}

* 無法透過 UI 下載自訂和產品功能測試步驟的記錄檔。
* 雲端服務程式的 git 存放庫建立失敗時，部署管理員角色中的使用者有時無法從此故障中恢復。
* 沙箱程式建立期間，某些使用者活動可能會導致程式建立作業在建立非生產管道之前失敗。
* 在設定的逾時期限內，建置步驟中使用的短暫 SonarQube 例項偶爾會無法啟動。
* 在同一個雲端服務程式中同時建立多個開發環境時，可能會發生只能成功建立一個環境的情況。
* 未能穩定收到雲端服務程式的 Experience Cloud 通知。
* 特定專案中，*ResourceResolver 物件應一律關閉*，這會產生 Null 指標異常，但不會影響管道執行。

