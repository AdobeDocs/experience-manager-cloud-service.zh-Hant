---
title: Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.3.0發行說明
description: 以下是Cloud Manager 2022.3.0在as a Cloud Service中的發行說明AEM。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 0749099acf98b09d0f83bfe86c2cc4558261c029
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---


# Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.3.0發行說明 {#release-notes}

本頁記錄了Cloud Manager 2022.3.0在as a Cloud Service中的發行說明AEM。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

2022年3月10日Cloud Manager版本2022.3.0AEM的發佈日期。 下一版計畫於2022年4月7日發行。

## 新增功能 {#what-is-new}

* 可以AEM使用開發人員角色訪問環境日誌。

## 錯誤修正 {#bug-fixes}

* 手動建立的Git儲存庫的子集具有不正確的名稱值，這防止了生成項目重用功能的有效性。 這些資料庫的名稱已更改，用戶將在Cloud Manager API/UI中看到更正的名稱。
* 來自非生產管道的生成工件在生產完整堆棧管道上被不恰當地重複使用。
* 添加或編輯代碼質量管道時，不再顯示處理度量失敗的選項。
* 生成步驟中可能會導致某些意外的管道變數配置。
