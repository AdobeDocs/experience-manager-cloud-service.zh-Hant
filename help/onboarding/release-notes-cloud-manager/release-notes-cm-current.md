---
title: AEM中Cloud Manager的Cloud Manager版本注意事項2021.2.0版
description: AEM中Cloud Manager的Cloud Manager版本注意事項2021.2.0版
translation-type: tm+mt
source-git-commit: dc006d50d703a17a84e3dc6631bc423f5de37f88
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---


# Adobe Experience Manager中Cloud Manager的Cloud Manager版本說明：Cloud Service 2021.2.0 {#release-notes}

本頁概述AEM中Cloud Manager的Release Notes（Cloud Service 2021.2.0版）。

## 發行日期 {#release-date}

AEM中Cloud Manager作為Cloud Service 2021.2.0的發行日期為2021年2月11日。

## Cloud Manager {#cloud-manager}

### 新功能 {#what-is-new}

* 資產客戶現在可以選擇透過Cloud Manager UI以自助方式部署其品牌入口網站實例的時間和地點。 對於具有資產解決方案的一般（非沙盒）方案，現在可在生產環境中布建品牌入口網站。 在生產環境上只能執行一次置備。

* 「專案與沙盒建立」中使用的AEM專案原型已更新為版本25。

* 程式碼掃描期間識別的已過時API清單已改良，加入最新Cloud Service SDK版本中已淘汰的其他類別和方法。

* SonarQube的Cloud Manager設定檔已更新，以移除Sonar規則squid:S2142。 這將不再與「線程中斷檢查」衝突。

* Cloud Manager UI會通知暫時無法新增／更新網域名稱的使用者，因為相關環境會附加一個執行中的管道，或目前正在等待核准步驟。

* 現在會動態移除客戶`pom.xml`檔案中預先加上聲納的屬性，以避免建置和品質掃描失敗。

* Cloud Manager UI會通知使用者，如果目前部署的網域名稱正在使用SSL憑證，可能暫時無法選取該憑證。

* 已新增其他程式碼品質規則，以涵蓋雲端服務相容性問題。

### 錯誤修正 {#bug-fixes}

* 比對SSL憑證與網域名稱不再區分大小寫。

* 如果憑證私密金鑰不符合2048位元限制，Cloud Manager UI現在會通知使用者並顯示適當的錯誤訊息。

* Cloud Manager UI會通知使用者，如果目前部署的網域名稱正在使用SSL憑證，可能暫時無法選取該憑證。

* 在某些情況下，內部問題可能導致環境刪除停滯。

* 某些管線故障錯誤報告為管線錯誤。
