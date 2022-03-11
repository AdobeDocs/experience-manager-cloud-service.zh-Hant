---
title: Cloud Manager在as a Cloud Service版AEM2021.2.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2021.2.0中的發行說明
exl-id: 281f9523-dec2-44f1-9459-5a45d48489d9
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.2.0 {#release-notes}

本頁概述了as a Cloud Service2021.2.0中Cloud Manager的發行說明AEM。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年2月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 資產客戶現在可以通過Cloud Manager UI選擇何時以自助服務方式部署其Brand Portal實例以及在何處部署。 對於具有資產解決方案的常規（非沙箱）計畫，現在可以在生產環境中配置Brand Portal。 在生產環境上只能進行一次設定。

* 在項AEM目和沙盒建立中使用的項目原型已更新為版本25。

* 代碼掃描期間識別的已過時API清單已細化，以包括最新Cloud ServiceSDK版本中已棄用的其他類和方法。

* SonarQube雲管理器的配置檔案已更新，以刪除Sonar規則squid:S2142。 這將不再與線程中斷檢查衝突。

* Cloud Manager UI將通知暫時無法添加/更新域名的用戶，因為關聯環境有一個正在運行的管道附加到它，或者當前正在等待批准步驟。

* 客戶中設定的屬性 `pom.xml` 現在將動態刪除以聲納為前置詞的檔案，以避免生成和質量掃描失敗。

* 如果SSL證書正由當前正在部署的域名使用，Cloud Manager UI將通知暫時無法選擇該證書的用戶。

* 已添加其他代碼質量規則以涵蓋Cloud Service相容性問題。

### 錯誤修正  {#bug-fixes}

* 與域名匹配的SSL證書不再區分大小寫。

* 如果證書私鑰不滿足2048位限制，Cloud Manager UI將立即通知用戶，並顯示相應的錯誤消息。

* 如果SSL證書正由當前正在部署的域名使用，Cloud Manager UI將通知暫時無法選擇該證書的用戶。

* 在某些情況下，內部問題可能導致環境刪除停滯。

* 某些管道故障錯誤地報告為管道錯誤。
