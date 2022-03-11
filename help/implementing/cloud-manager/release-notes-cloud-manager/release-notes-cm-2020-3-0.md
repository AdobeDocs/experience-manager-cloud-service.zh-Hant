---
title: Cloud Manager在as a Cloud Service版AEM2020.3.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2020.3.0中的發行說明
feature: Release Information
exl-id: 2ff62ba5-a657-4739-b646-1e948332bf79
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 73%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2020.3.0 {#release-notes}

本頁概述了as a Cloud Service2020.3.0中Cloud Manager的發行說明AEM。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的發AEM布日期為2020年3月5日。

### 新增功能 {#what-is-new}

* 現在建置步驟執行時，建置步驟記錄可供同時使用。
* 管道執行詳細資訊頁面上的部分訊息經過編輯，以更明確說明。

### 錯誤修正  {#bug-fixes}

* 無法透過 UI 下載自訂和產品功能測試步驟的記錄檔。
* 雲端服務程式的 git 存放庫建立失敗時，部署管理員角色中的使用者有時無法從此故障中恢復。
* 沙箱程式建立期間，某些使用者活動可能會導致程式建立作業在建立非生產管道之前失敗。
* 在設定的逾時期限內，建置步驟中使用的短暫 SonarQube 例項偶爾會無法啟動。
* 在同一個雲端服務程式中同時建立多個開發環境時，可能會發生只能成功建立一個環境的情況。
* 未能穩定收到雲端服務程式的 Experience Cloud 通知。
* 特定專案中，*ResourceResolver 物件應一律關閉*，這會產生 Null 指標異常，但不會影響管道執行。
