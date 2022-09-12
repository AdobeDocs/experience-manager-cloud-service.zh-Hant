---
title: AEM as a Cloud Service2021.7.0版中Cloud Manager發行說明
description: AEM as a Cloud Service2021.7.0版中Cloud Manager發行說明
feature: Release Information
exl-id: 7ef738a5-4657-482d-848b-e95e4fb816f9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud Service 2021.7.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2021.7.0as a Cloud Service版中Cloud Manager的發行說明。

>[!NOTE]
>若要查看最新的Adobe Experience Manager as a Cloud Service發行說明，請按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## 發行日期 {#release-date}

AEM 2021.7.0中的Cloud Manageras a Cloud Service日期為2021年7月15日。


### 新增功能 {#what-is-new}

* 客戶現在可以將Azul 8和11 JDK用於其Cloud Manager構建過程，並且可以選擇使用其中一個JDK用於與工具鏈相容的Maven插件 *或* 整個Maven程式執行。

* 傳出輸出IP現在將記錄在建置步驟記錄檔中。

* 執行舊版AEM的預備和生產環境現在會回報 **可用更新**.

* 支援的SSL憑證上限已提高至每個程式20個。

* 每個環境可配置的域數上限已增加到500個。

* 此 **管理Git** 按鈕已重新命名為 **存取Git資訊** 對話框已刷新。

* Cloud Manager使用的AEM專案原型版本已更新為28版。

### 錯誤修正 {#bug-fixes}

* 在某些情況下，將IP允許清單系結至環境時，「預覽」不是可用選項。

* 手動導覽至非現有執行的執行詳細資訊頁面時未顯示錯誤，只是無休止的載入畫面。

* 達到最大SSL憑證數時顯示的錯誤訊息並無幫助。

* 在某些情況下，在上的管道卡片中顯示的發行版本可能會不一致 **概述** 頁面。

* 添加程式嚮導未正確說明建立後無法更改名稱。

### 已知問題 {#known-issues}

切換使用Azul JDK的客戶應注意，並非所有現有應用程式都會在Azul JDK上編譯，且不會出現錯誤。 強烈建議您在切換前先在本機測試。
