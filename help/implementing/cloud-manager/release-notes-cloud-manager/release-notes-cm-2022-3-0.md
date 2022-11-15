---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.3.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2022.3.0 的發行說明。
feature: Release Information
exl-id: d09d48c5-6e0a-4a6a-85e9-1a60fdd6e5bf
source-git-commit: 68586304724530f83649cffee76cefef3e1c8627
workflow-type: ht
source-wordcount: '196'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2022.3.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 2022.3.0 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2022.3.0 發行日期是 2022 年 3 月 10 日。下一版本計劃於 2022 年 4 月 7 日發行。

## 新增功能 {#what-is-new}

* 可使用開發人員角色存取 AEM 環境紀錄。

## 錯誤修正 {#bug-fixes}

* 手動建立的 Git 存放庫子集的名稱值不正確，這會妨礙組建成品重複使用功能，使其無法生效。這些存放庫的名稱已變更，使用者將在 Cloud Manager API/UI 中看到更正後的名稱。
* 在生產完整堆疊管道上以不適當的方式重複使用了來自非生產管道的組建成品。
* 新增或編輯計劃碼品質管道時，不再顯示處理量度失敗的選項。
* 在組建步驟中可能會導致一些非預期的管道變數設定。
