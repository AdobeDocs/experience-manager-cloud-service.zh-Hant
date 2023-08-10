---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.8.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.8.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: d1640c14c796d7b7b6a7b236b38077e360559966
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 31%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.8.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2023.8.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2023.8.0 發行日期是 2023 年 8 月 10 日。下一個版本計畫於 2023 年 7 月 9 日發行。

## 新增功能 {#what-is-new}

* 設定內容集至 [複製內容，](/help/implementing/developing/tools/content-copy.md) [內容感知設定](/help/implementing/developing/introduction/configurations.md) 現在允許在UI的內容集中使用。
* 已進行增強功能，以改善Cloud Manager UI中錯誤訊息的可理解性和顯示性。

## 自助內容還原早期採用計畫 {#early-adoption}

[新的自助內容還原功能](/help/operations/restore.md) 現在提供長達七天的備份還原功能，以供早期採用者評估，其功能包括：

* 前24小時的時間點備份還原
* 固定時間還原最多七天

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `aemcs-restorefrombackup-adopter@adobe.com` 從與您的Adobe ID相關聯的電子郵件中。 請注意:

* 早期採用者計畫僅限於開發環境。
* 率先採用者方案的可用性有限。
* 此功能用於復原意外刪除的內容，並非用於災難復原。

## 錯誤修正 {#bug-fixes}

* 此 **環境** 功能表現在會在觸發 **[複製內容](/help/implementing/developing/tools/content-copy.md)** 強制回應視窗。
* [管道重新執行](/help/implementing/cloud-manager/deploy-code.md#reexecute-deployment) 如果先前執行沒有 `commitId` 在建置階段狀態上設定。
* 現在，當使用者按一下中的管道時，對於罕見錯誤，會顯示更易於理解的訊息 **活動** 或 **管道** 畫面。
* 此 `contentSetName` 值不再遺失在記錄中，現在在啟動時提供在輸入中 [內容複製](/help/implementing/developing/tools/content-copy.md) 作業。
* 在某些罕見情況下，不再可以從同一管道開始兩個執行，導致「卡住」狀態。
* 憑證過期時，與憑證關聯的網域名稱和IP允許清單將不再從CDN中移除。
   * 在這種情況下，網站將繼續接受訪客造訪。
   * [](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)Cloud Manager UI 將提供更明顯的事先警告：SSL 憑證即將到期。
* AEM無法存取發佈端點的問題已修正，其情況為將Sites新增為僅限Assets計畫的解決方案。
