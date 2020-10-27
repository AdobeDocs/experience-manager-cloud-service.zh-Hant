---
title: AEM中Cloud Manager的Cloud Manager版本注意事項2020.3.0版
description: AEM中Cloud Manager的Cloud Manager版本注意事項2020.3.0版
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 73%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.3.0 {#release-notes}

本頁概述AEM中Cloud Manager的發行說明，即Cloud Service 2020.3.0。

## 發行日期 {#release-date}

AEM中Cloud Manager作為Cloud Service 2020.3.0的發行日期為2020年3月05日。

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