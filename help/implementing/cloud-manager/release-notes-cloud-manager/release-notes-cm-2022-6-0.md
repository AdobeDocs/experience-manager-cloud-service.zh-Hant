---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.6.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2022.6.0 的發行說明。
feature: Release Information
exl-id: 0a348836-74cd-4fd4-aef4-6ffbd6483c24
source-git-commit: e05c2fa2cfb035ed363e2c80d4aac33b022bd435
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.6.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 2022.6.0 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2022.6.0 發行日期是 2022 年 6 月 9 日。下一版本計劃於 2022 年 6 月 30 日發行。

## 新增功能 {#what-is-new}

* Cloud Manager 登錄頁面上的新歡迎卡讓使用者可以快速存取和租用戶相關的上線教學課程和進度量度。
   * 此功能將在 2022.06.0 版發行後的一週內分階段推出。
* 具有必要權限的使用者可以存取新的[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)在 Cloud Manager 登入頁面上查看租使用者可用權利的詳細資訊。
   * AEM Sites 是第一個透過 Cloud Manage 儀表板提供可用性和使用量消耗的解決方案。
   * 此功能將在 2022.06.0 版發行後的一週內分階段推出。
* [New Relic 子帳號和自助使用者管理](/help/implementing/cloud-manager/user-access-new-relic.md)現在可透過 Cloud Manager UI 使用。
   * 此功能將在 2022.06.0 版發行後的一週內分階段推出。
* Cloud Service 生產計劃主頁上的新 Go Live 小工具現在提供了為成功上線體驗做準備的指導。
* 使用 Git 鏡像時，[現在可重複使用組建成品](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)。

## API 變更 {#api-changes}

* 此 [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API 已過時，並應改用 [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant)。
   * `List Programs` 會持續運作，但其使用方式將在紀錄中產生警告訊息。
   * 三個月後將不再受支援。
