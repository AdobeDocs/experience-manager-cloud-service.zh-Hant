---
title: Cloud Manager的發行說明，作AEM為Cloud Service版本2021.2.0
description: Cloud Manager的發行說明，作AEM為Cloud Service版本2021.2.0
translation-type: tm+mt
source-git-commit: 32557b3f25e4d4f4cb652f19cff4dae58638e07b
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---


# Adobe Experience ManagerCloud Manager的發行說明，Cloud Service2021.2.0 {#release-notes}

本頁概述了Cloud Manager的發行說明，AEM作為Cloud Service2021.2.0。

## 發行日期 {#release-date}

Cloud Manager作為2021.2.0Cloud ServiceAEM的發行日期為2021年2月11日。

## Cloud Manager {#cloud-manager}

### 新功能 {#what-is-new}

* 資產客戶現在可以選擇透過Cloud Manager UI以自助方式部署其品牌入口網站實例的時間和地點。 對於具有資產解決方案的一般（非沙盒）方案，現在可在生產環境中布建品牌入口網站。 在生產環境上只能執行一次置備。

* 「專AEM案與沙盒建立」中使用的「專案原型」已更新為第25版。

* 在程式碼掃描期間識別的已過時API清單已經過改良，以包含最新版Cloud ServiceSDK中已過時的其他類別和方法。

* SonarQube的Cloud Manager設定檔已更新，以移除Sonar規則squid:S2142。 這將不再與「線程中斷檢查」衝突。

* Cloud Manager UI會通知暫時無法新增／更新網域名稱的使用者，因為相關環境會附加一個執行中的管道，或目前正在等待核准步驟。

* 現在會動態移除客戶`pom.xml`檔案中預先加上聲納的屬性，以避免建置和品質掃描失敗。

* Cloud Manager UI會通知使用者，如果目前部署的網域名稱正在使用SSL憑證，可能暫時無法選取該憑證。

* 已新增其他程式碼品質規則，以涵蓋Cloud Service相容性問題。

### 錯誤修正 {#bug-fixes}

* 比對SSL憑證與網域名稱不再區分大小寫。

* 如果憑證私密金鑰不符合2048位元限制，Cloud Manager UI現在會通知使用者並顯示適當的錯誤訊息。

* Cloud Manager UI會通知使用者，如果目前部署的網域名稱正在使用SSL憑證，可能暫時無法選取該憑證。

* 在某些情況下，內部問題可能導致環境刪除停滯。

* 某些管線故障錯誤報告為管線錯誤。
