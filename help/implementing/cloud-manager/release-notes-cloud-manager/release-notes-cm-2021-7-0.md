---
title: Cloud Manager在as a Cloud Service版AEM2021.7.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2021.7.0中的發行說明
feature: Release Information
exl-id: 7ef738a5-4657-482d-848b-e95e4fb816f9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.7.0 {#release-notes}

本頁概述了as a Cloud Service2021.7.0中Cloud Manager的發行說明AEM。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的當前發行說明，請按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年7月15日。


### 新增功能 {#what-is-new}

* 客戶現在能夠將Azul 8和11 JDK用於其Cloud Manager生成過程，並可以選擇將其中一個JDK用於與工具鏈相容的Maven插件 *或* 整個Maven進程的執行。

* 出站出口IP現在將記錄在生成步驟日誌檔案中。

* 運行舊版本的階段和生產環AEM境現在將報告 **可用更新**。

* 支援的最大SSL證書已增加到每個程式20個。

* 可配置的最大域數已增加到每個環境的500個。

* 的 **管理Git** 按鈕已重新命名為 **訪問Git資訊** 對話框已直觀刷新。

* Cloud Manager使用的AEMProject Archetype版本已更新為版本28。

### 錯誤修正 {#bug-fixes}

* 在某些情況下，將IP允許清單綁定到環境時，「預覽」不可用。

* 手動導航到非現有執行的執行詳細資訊頁面未顯示錯誤，只顯示無休止的載入螢幕。

* 達到最大SSL證書數時顯示的錯誤消息無用。

* 在某些情況下，在上面的管道卡中顯示的版本版本可能不一致 **概述** 的子菜單。

* 添加程式嚮導錯誤地指出建立後無法更改名稱。

### 已知問題 {#known-issues}

切換使用阿祖爾JDK的客戶應該知道，並非所有現有應用程式都會在阿祖爾JDK上進行編譯，而且不會出錯。 強烈建議在切換前在本地test。
