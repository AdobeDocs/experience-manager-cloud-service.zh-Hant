---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.4.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2022.4.0 的發行說明。
feature: Release Information
exl-id: e7ff623b-aeca-40a6-bf48-98af270a4117
source-git-commit: 458d63c27bb2ab4d09237aa3ecb96c0f6d5e67ed
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.4.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 2022.4.0 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2022.4.0 發行日期是 2022 年 4 月 7 日。下一個版本計劃於 2022 年 5 月 5 日發行。

## 新增功能 {#what-is-new}

* 已經實作對管道建置步驟持續時間和成功率的改進，並將在 4 月份逐步推出至所有客戶。
* 您現在可在新增和編輯管道精靈的輸入欄位中鍵入名稱的前幾個字元，然後從建議的相符結果中選取[生產](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)和[非生產](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)管道，即可輕鬆找到 Git 分支。
* 在 4 月發布後不久，在環境建立期間定義雲端區域時，印度將可供選擇。
* 此&#x200B;**管道**&#x200B;頁面現在具有分頁功能，以提高包含大量管道的方案的可用性。
   * 表格中每頁將顯示 50 行。
* Cloud Manager 使用的 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)版本已更新至版本 36。
* Oracle JDK 現在成為 AEM 應用計劃開發和操作的預設 JDK。此 Cloud Manager 建置流程將自動切換成使用 Oracle JDK，即使在 Maven 工具鏈中明確選取了替代選項。
   * 若要了解如何切換至 Oracle JDK 的詳細資訊，請參閱[此「組建環境」文件。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)
   * 若要解決此變更的常見問題，請參閱[適用於 Adobe Experience Manager 常見問題的 Java 支援政策](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf)。
* 透過在驗證步驟中檢測較舊的 AEM 版本，管道執行現在將更快地失敗。使用者將在 UI 中看到一條消息來指導他們。

## 錯誤修正 {#bug-fixes}

* 在 UI 測試步驟中建立的記錄現在可以透過 UI 下載。
* Web 層配置管道現在只能重用來自 Web 層配置執行的套件。
* UI 中有關如何在過時的環境中更新 AEM 的消息更加清晰。
