---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.12.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2022.12.0 的發行說明。
feature: Release Information
source-git-commit: 5877f3c84ab6303520dd4697144e9b18d717b74f
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.12.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 2022.12.0 的發行說明。

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2022.12.0 發行日期是 2022 年 11 月 29 日。 下一個版本計劃於 2023 年 1 月 19 日發行。

## 新增功能 {#what-is-new}

* [AEM 維護更新](/help/overview/what-is-new-and-different.md#aem-updates) 的通知將顯示在 Cloud Manager UI 中。 此變更將在 2022.12.0 版發行後數週內分階段推出。
* 當透過[內容轉移工具 (CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md)的擷取作業進行時，開發人員控制台和 Cloud Manager 中的環境狀態將顯示為 `Ingestion in Progress`。
* 改善 [Cloud Manager 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)的可用性和可靠性。

## 錯誤修正 {#bug-fixes}

* 已進行變更以防止 [前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)在管道執行過程中在同一個環境中進行。
* 已進行變更以防止 `PATCH /program//environment//variables` 請求 `FAILED` 狀態的環境。
