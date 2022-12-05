---
title: AEM as a Cloud Service 版本 2021.7.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2021.7.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: 7ef738a5-4657-482d-848b-e95e4fb816f9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.7.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.7.0 中 Cloud Manager 的發行說明

>[!NOTE]
>若要閱讀 Adobe Experience Manager as a Cloud Service 的目前發行說明，請按一下[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.7.0 中的 Cloud Manager 發行日期是 2021 年 7 月 15 日。


### 新增功能 {#what-is-new}

* 客戶現在可以將 Azul 8 和 11 JDK 用於其 Cloud Manager 建置流程，也可以選擇將這些 JDK 之一用於與工具鏈相容的 Maven 外掛計劃&#x200B;*或*&#x200B;整個 Maven 流程執行。

* 輸出 IP 現在記錄於建置步驟記錄檔。

* 執行舊版 AEM 的階段和生產環境現在會回報「**有可用的更新**」的狀態。

* 支援的 SSL 憑證數量上限已增加到每個計劃 20 個。

* 可以設定的網域數量上限已增加到每個環境 500 個。

* 「**管理 Git**」按鈕已重新命名為「**存取 Git 資訊**」並更新此對話方塊。

* Cloud Manager 使用的 AEM 專案原型版本已更新至版本 28。

### 錯誤修正 {#bug-fixes}

* 在某些情況下，將 IP 允許清單繫結到環境時，預覽選項無法使用。

* 手動瀏覽到不存在執行的執行詳細資訊頁面不會顯示錯誤，只會不斷載入畫面。

* 達到最大 SSL 憑證數量時顯示的錯誤訊息沒有幫助。

* 在某些情況下，在&#x200B;**總覽**&#x200B;頁面中管道卡上顯示的發行版本可能存在差異。

* 新增計畫精靈誤指建立後無法變更名稱。

### 已知問題 {#known-issues}

改用 Azul JDK 的客戶應注意，並非所有現有應用計劃都能在 Azul JDK 上順利編譯。強烈建議切換前在本機測試。
