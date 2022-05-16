---
title: Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.3.0發行說明
description: 以下是Cloud Manager 2022.3.0在as a Cloud Service中的發行說明AEM。
feature: Release Information
exl-id: d09d48c5-6e0a-4a6a-85e9-1a60fdd6e5bf
source-git-commit: 68586304724530f83649cffee76cefef3e1c8627
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service的Cloud Manager 2022.3.0發行說明 {#release-notes}

本頁記錄了Cloud Manager 2022.3.0在as a Cloud Service中的發行說明AEM。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中2022.3.0版的AEM發佈日期為2022年3月10日。 下一版計畫於2022年4月7日發行。

## 新增功能 {#what-is-new}

* 可以AEM使用開發人員角色訪問環境日誌。

## 錯誤修正 {#bug-fixes}

* 手動建立的Git儲存庫的子集具有不正確的名稱值，這防止了生成項目重用功能的有效性。 這些資料庫的名稱已更改，用戶將在Cloud Manager API/UI中看到更正的名稱。
* 來自非生產管道的生成工件在生產完整堆棧管道上被不恰當地重複使用。
* 添加或編輯代碼質量管道時，不再顯示處理度量失敗的選項。
* 生成步驟中可能會導致某些意外的管道變數配置。
