---
title: AEM as aCloud Service中Cloud Manager的發行說明2021.7.0版
description: AEM as aCloud Service中Cloud Manager的發行說明2021.7.0版
feature: 發行資訊
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: e24610cef6d134ddf9ce8abe9a5893deac08eeb6
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# Adobe Experience Manager as aCloud Service2021.7.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM as a 2021.7.0Cloud Service中Cloud Manager的發行說明。

>[!NOTE]
>若要查看Adobe Experience Manager as aCloud Service的最新發行說明，請按一下[here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html)。

## 發行日期 {#release-date}

AEM as aCloud Service2021.7.0中的Cloud Manager發行日期為2021年7月15日。
下一版預計於2021年8月12日發行。

### 新增功能 {#what-is-new}

* 客戶現在可以將Azul 8和11 JDK用於其Cloud Manager構建進程，並且可以選擇將其中一個JDK用於與工具鏈相容的Maven插件&#x200B;*或*&#x200B;整個Maven進程執行。

* 傳出輸出IP現在將記錄在建置步驟記錄檔中。

* 執行舊版AEM的預備和生產環境現在會回報&#x200B;**可用更新**&#x200B;狀態。

* 支援的SSL憑證上限已提高至每個程式20個。

* 每個環境可配置的域數上限已增加到500個。

* **管理Git**&#x200B;按鈕已重新命名為&#x200B;**存取Git資訊**，對話方塊也已視覺化重新整理。

* Cloud Manager使用的AEM專案原型版本已更新為28版。

### 錯誤修正 {#bug-fixes}

* 在某些情況下，將IP允許清單系結至環境時，「預覽」不是可用選項。

* 手動導覽至非現有執行的執行詳細資訊頁面時未顯示錯誤，只是無休止的載入畫面。

* 達到最大SSL憑證數時顯示的錯誤訊息並無幫助。

* 在某些情況下，**概述**&#x200B;頁面上的管道卡片所顯示的發行版本可能會不一致。

* 添加程式嚮導未正確說明建立後無法更改名稱。

### 已知問題 {#known-issues}

切換使用Azul JDK的客戶應注意，並非所有現有應用程式都會在Azul JDK上編譯，且不會出現錯誤。 強烈建議您在切換前先在本機測試。

