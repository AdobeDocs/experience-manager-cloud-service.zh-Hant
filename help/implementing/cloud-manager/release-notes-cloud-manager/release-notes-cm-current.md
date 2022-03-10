---
title: Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.3.0發行說明
description: 以下是Cloud Manager 2022.3.0在as a Cloud Service中的發行說明AEM。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---


# Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.3.0發行說明 {#release-notes}

本頁記錄了Cloud Manager 2022.3.0在as a Cloud Service中的發行說明AEM。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

2022年3月10日Cloud Manager版本2022.3.0AEM的發佈日期。 下一版計畫於2022年4月7日發行。

## 新增功能 {#what-is-new}

* 具有 **開發人員** 角色現在可以訪問環AEM境日誌。
* [的 `reliability_rating` 臨界度量](/help/implementing/cloud-manager/code-quality-testing.md) 已禁用。
* 用戶現在可以對 **管線** 的子菜單。

## 錯誤修正 {#bug-fixes}

* 手動建立的Git儲存庫的子集具有不正確的名稱值，這影響了 [生成項目重用功能。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 這些資料庫的名稱已更改，用戶將在Cloud Manager API/UI中看到更正的名稱。
* [添加或編輯代碼質量管道時，](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 這樣 **重要度量故障行為** 選項不再顯示。
* 意外的管道變數配置不再導致生成步驟中的錯誤。
