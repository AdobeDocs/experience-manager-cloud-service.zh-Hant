---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.4.0 的版本注意事項
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.4.0 的版本注意事項。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be39b09b609cccff916db462af9a84149d23a698
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 50%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.4.0 的版本注意事項 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 發行 2023.4.0 的版本注意事項。

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前版本注意事項，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2023.4.0版的發行日期為2023年4月13日。 下一個版本計劃於 2023 年 11 月 5 日發行。

## 新增功能 {#what-is-new}

* [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) 已更新至41版。

## 錯誤修正 {#bug-fixes}

* 當 [憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 過期， [網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md) 和 [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) 與憑證相關聯的CDN將不再移除。  在這種情況下，該站點將繼續可以訪問。
* Cloud Manager UI會提供更清楚的預警，指出 [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 即將過期。
* 已修正客戶無法建立新環境或刪除環境的罕見情況。
