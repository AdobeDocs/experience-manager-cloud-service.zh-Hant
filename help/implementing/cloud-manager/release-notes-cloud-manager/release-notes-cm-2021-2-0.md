---
title: AEM as aCloud Service中Cloud Manager的發行說明2021.2.0版
description: AEM as aCloud Service中Cloud Manager的發行說明2021.2.0版
exl-id: 281f9523-dec2-44f1-9459-5a45d48489d9
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---

# Adobe Experience Manager as aCloud Service2021.6.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM as a 2021.2.0Cloud Service中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEM as aCloud Service2021.2.0中的Cloud Manager發行日期為2021年2月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* Assets客戶現在可以透過Cloud Manager UI以自助方式部署其Brand Portal執行個體，選擇時機和位置。 針對具有Assets解決方案的一般（非沙箱）方案，現在可在生產環境中布建Brand Portal。 布建只能在生產環境中執行一次。

* 專案和沙箱建立中使用的AEM專案原型已更新為25版。

* 程式碼掃描期間識別的已棄用API清單已經過細化，加入最新Cloud ServiceSDK版本中已棄用的其他類別和方法。

* 更新Cloud Manager的SonarQube設定檔，以移除Sonar規則squid:S2142。 這不再與執行緒中斷檢查衝突。

* Cloud Manager UI會通知暫時無法新增/更新網域名稱的使用者，因為相關環境已附加執行中的管道，或目前正在等候核准步驟。

* 以聲納為首碼的客戶`pom.xml`檔案中設定的屬性現在會動態移除，以避免建置和品質掃描失敗。

* 如果目前部署的網域名稱正在使用SSL憑證，Cloud Manager UI會通知暫時無法選取該憑證的使用者。

* 已新增其他程式碼品質規則，以涵蓋Cloud Service相容性問題。

### 錯誤修正  {#bug-fixes}

* 比對SSL憑證與網域名稱不再區分大小寫。

* 如果憑證私密金鑰不符合2048位元限制，Cloud Manager UI現在會通知使用者，並顯示適當的錯誤訊息。

* 如果目前部署的網域名稱正在使用SSL憑證，Cloud Manager UI會通知暫時無法選取該憑證的使用者。

* 在某些情況下，內部問題可能會導致環境刪除卡住。

* 某些管道故障錯誤報告為管道錯誤。
