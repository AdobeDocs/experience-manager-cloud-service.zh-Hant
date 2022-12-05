---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.8.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2022.8.0 的發行說明。
feature: Release Information
exl-id: df31673a-0ffd-4ea8-a6da-fbf75318b915
source-git-commit: 83e49215eff975300f263dcf0215081b02260e70
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.8.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 2022.8.0 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2022.8.0 發行日期是 2022 年 8 月 11 日。下一個版本計劃於 2022 年 9 月 9 日發行。

## 新增功能 {#what-is-new}

* [新增環境工作流程](/help/implementing/cloud-manager/manage-environments.md)中的全新 UI 體驗
* Cloud Manager 中包含的 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)已更新為版本 37。

## 錯誤修正 {#bug-fixes}

* 更正了 Cloud Manager UI 中未建立或刪除 New Relic 使用者的情況。
* 已使得某些不常見的建立存放庫失敗案例能更快復原。
* 由於引進了重試機制，罕見的 VSTS 組織設定錯誤現在已減少。
* 在 New Relic 子帳戶使用者建立期間改善的驗證現在可以防止某些錯誤。
