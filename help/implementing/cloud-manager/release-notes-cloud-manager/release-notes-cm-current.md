---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.12.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2022.12.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: aa7f2175e2a43a318a6171e622d292ed3a8e958b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 55%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.12.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 2022.12.0 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2022.12.0 發行日期是 2022 年 11 月 29 日。下一個版本計劃於 2023 年 1 月 19 日發行。

## 新增功能 {#what-is-new}

* 通知 [AEM維護更新](/help/overview/what-is-new-and-different.md#aem-updates) 會在Cloud Manager UI中呈現。 此變更將在2022.12.0版發行後的數週內分階段推出。
* 透過 [內容轉移工具(CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) 進行中，開發人員主控台和Cloud Manager中的環境狀態都會顯示為 `Ingestion in Progress`.
* 改善 [Cloud Manager 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)的可用性和可靠性。

## 錯誤修正 {#bug-fixes}

* 已進行變更，以防止 [前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 在相同環境中執行管道時從執行。
* 已進行變更，以防止 `PATCH /program//environment//variables` 要求環境 `FAILED` 狀態。
