---
title: AEM as a Cloud Service 版本 2021.2.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2021.2.0 中 Cloud Manager 的發行說明
exl-id: 281f9523-dec2-44f1-9459-5a45d48489d9
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.2.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.2.0 中 Cloud Manager 的發行說明

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.2.0 中 Cloud Manager 的發行日期為 2021 年 2 月 11 日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* Assets 客戶現在可以透過 Cloud Manager UI 以自助方式選擇何時何地部署其 Brand Portal 執行個體。對於具有 Assets 解決方案的一般 (非沙箱) 計畫，現在可以在生產環境中佈建品牌入口網站。佈建只能在生產環境中進行一次。

* 專案和沙箱建立中使用的 AEM Project 原型已更新至版本 25。

* 計劃碼掃描期間識別的已棄用 API 清單已細化，加入最新 Cloud Service SDK 版本中棄用的其他類別和方法。

* 已更新 Cloud Manager 的 SonarQube 設定檔，以移除 Sonar 規則 squid:S2142。這將不再與執行緒中斷檢查衝突。

* Cloud Manager UI 將通知可能暫時無法新增/更新網域名稱的使用者，因為相關環境已附加執行中的管道，或目前正在等候核准步驟。

* 客戶中設定的屬性 `pom.xml` 前置詞為「聲納」的檔案現在會動態移除，以避免建置和品質掃描失敗。

* 如果目前部署的網域名稱正在使用 SSL 憑證，Cloud Manager UI 將通知暫時無法選擇該憑證的使用者。

* 已新增其他計劃碼品質規則，以涵蓋 Cloud Service 相容性問題。

### 錯誤修正  {#bug-fixes}

* 比對 SSL 憑證與網域名稱不再區分大小寫。

* 如果憑證私密金鑰不符合 2048 位元限制，Cloud Manager UI 現在會通知使用者，並顯示適當的錯誤訊息。

* 如果目前部署的網域名稱正在使用 SSL 憑證，Cloud Manager UI 將通知暫時無法選擇該憑證的使用者。

* 在某些情況下，內部問題可能會導致環境刪除卡住。

* 某些管道故障錯誤報告為管道錯誤。
