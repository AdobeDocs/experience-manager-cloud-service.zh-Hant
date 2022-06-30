---
title: Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.6.0發行說明
description: 以下是Cloud Manager 2022.6.0在as a Cloud Service中的發行說明AEM。
feature: Release Information
source-git-commit: 5200ee315ad88dae4b52c0ea904489e73f62a8a0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 1%

---


# Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.6.0發行說明 {#release-notes}

本頁記錄了Cloud Manager 2022.6.0在as a Cloud Service中的發行說明AEM。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中2022.6.0版的AEM發佈日期為2022年6月9日。 下一版計畫於2022年6月30日發行。

## 新增功能 {#what-is-new}

* Cloud Manager UI現在允許 [自服務內容恢復](/help/operations/backup.md) 到已知良好的雲環境AEM狀態。
   * 此功能將在發佈後的幾週內分階段2022.06.0出。
* Cloud Manager登錄頁上的新歡迎卡使用戶能夠快速訪問與租戶相關的入門教程和進度度量。
   * 此功能將在發佈後的一週內分階段2022.06.0出。
* 具有必要權限的用戶可以訪問新 [許可證儀表板](/help/implementing/cloud-manager/license-dashboard.md) 在雲管理器登錄頁上查看租戶可用權利的詳細資訊。
   * AEM Sites是第一個通過雲管理儀表板提供可用性和使用消耗的解決方案。
   * 此功能將在發佈後的幾週內分階段2022.06.0出。
* [New Relic子帳戶和自助服務用戶管理](/help/implementing/cloud-manager/user-access-new-relic.md) 現在可通過雲管理器UI訪問。
   * 此功能將在發佈後的幾週內分階段2022.06.0出。
* Cloud Service製作程式首頁上的新Go Live小部件現在提供了指導，為成功的go Live體驗做好準備。
* [現在可以重用生成對象](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 使用git鏡像時。

## API更改 {#api-changes}

* 的 [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API已棄用， [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) 應改為使用。
   * `List Programs` 繼續工作，但其使用將在日誌中生成警告消息。
   * 三個月後，它將不再得到支援。

