---
title: Adobe Experience Manager as a Cloud Service中Cloud Manager 2022.3.0發行說明
description: 以下是AEM as a Cloud Service中Cloud Manager 2022.3.0的發行說明。
feature: Release Information
exl-id: d09d48c5-6e0a-4a6a-85e9-1a60fdd6e5bf
source-git-commit: 68586304724530f83649cffee76cefef3e1c8627
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service中Cloud Manager 2022.3.0發行說明 {#release-notes}

本頁記錄AEM as a Cloud Service中Cloud Manager 2022.3.0的發行說明。

>[!NOTE]
>
>請參閱 [本頁](/help/release-notes/release-notes-cloud/release-notes-current.md) Adobe Experience Manager as a Cloud Service的最新發行說明。

## 發行日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2022.3.0版的發行日期為2022年3月10日。 下一版預計於2022年4月7日發行。

## 新增功能 {#what-is-new}

* 您可以使用開發人員角色來存取AEM環境記錄。

## 錯誤修正 {#bug-fixes}

* 手動建立的Git存放庫子集的名稱值不正確，導致建置工件重複使用功能無法有效運作。 這些存放庫的名稱已變更，使用者可在Cloud Manager API/UI中看到更正的名稱。
* 來自非生產管道的成品在生產完全堆棧管道上被不當重複使用。
* 新增或編輯程式碼品質管道時，不再顯示處理量度失敗的選項。
* 在建置步驟中可能會造成某些非預期的管道變數設定。
