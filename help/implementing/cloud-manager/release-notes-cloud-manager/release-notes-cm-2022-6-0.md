---
title: Adobe Experience Manager as a Cloud Service中Cloud Manager 2022.6.0發行說明
description: 以下是AEM as a Cloud Service中Cloud Manager 2022.6.0的發行說明。
feature: Release Information
exl-id: 0a348836-74cd-4fd4-aef4-6ffbd6483c24
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service中Cloud Manager 2022.6.0發行說明 {#release-notes}

本頁記錄AEM as a Cloud Service中Cloud Manager 2022.6.0的發行說明。

>[!NOTE]
>
>請參閱 [本頁](/help/release-notes/release-notes-cloud/release-notes-current.md) Adobe Experience Manager as a Cloud Service的最新發行說明。

## 發行日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2022.6.0版的發行日期為2022年6月9日。 下一版預計於2022年6月30日發行。

## 新增功能 {#what-is-new}

* Cloud Manager UI現在允許 [自助服務內容還原](/help/operations/backup.md) 至AEM雲端環境的已知良好狀態。
   * 此功能將在2022.06.0版後的數週內分階段推出。
* Cloud Manager登陸頁面上新增的歡迎卡，可讓使用者快速存取入門教學課程和與租用戶相關的進度量度。
   * 此功能將在2022.06.0版發行後的一週內分階段推出。
* 具有必要權限的使用者可以存取新 [授權控制面板](/help/implementing/cloud-manager/license-dashboard.md) 在Cloud Manager登陸頁面上，檢視租用戶可用權益的詳細資訊。
   * AEM Sites是透過「雲端管理」控制面板提供可用性和使用量耗用量的第一個解決方案。
   * 此功能將在2022.06.0版後的數週內分階段推出。
* [新Relic子帳戶與自助服務使用者管理](/help/implementing/cloud-manager/user-access-new-relic.md) 現在可透過Cloud Manager UI使用。
   * 此功能將在2022.06.0版後的數週內分階段推出。
* Cloud Service生產計畫首頁上的全新上線介面工具集現在提供指引，為成功上線體驗做好準備。
* [現在可以重複使用生成成品](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 使用git鏡像時。

## API變更 {#api-changes}

* 此 [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API已淘汰， [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) 的值。
   * `List Programs` 會繼續運作，但其使用情形會在記錄中產生警告訊息。
   * 三個月後將不再支援。
