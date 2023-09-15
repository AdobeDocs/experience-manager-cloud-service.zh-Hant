---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.9.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.9.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 8bf2ffe8b1d3780f4ad3f6972fea4f8281945abb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 76%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.9.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2023.9.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2023.9.0 發行日期是 2023 年 9 月 14 日。下一版本計畫於 2023 年 10 月 5 日發行。

## 新增功能 {#what-is-new}

* CDN記錄檔（若有）可透過Cloud Manager UI下載。
* 使用者現在可以選擇加入，將Google Lighthouse支援的體驗稽核測試納入非生產用的完整棧疊管道中。

## 早期採用計劃 {#early-adoption}

參加我們的早期採用計劃，即有機會測試一些即將推出的功能。

### 自助服務內容還原 {#content-restore}

[新的自助服務內容還原功能](/help/operations/restore.md)現在會提供最長達 7 天的備份還原，並可供早期採用者用於評估目的，其中包括：

* 前 24 小時的時間點備份還原
* 固定時間還原最長可達 7 天

如果您有興趣測試此新功能並分享您的意見反應，請使用和您的 Adob&#x200B;&#x200B;e ID 相關聯的電子郵件傳送電子郵件至 `aemcs-restorefrombackup-adopter@adobe.com`。請注意：

* 早期採用者計劃僅適用於開發環境。
* 此功能可使用的早期採用者計劃很有限。
* 此功能用於恢復意外刪除的內容，不適用於災難復原。

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板會利用 Google Lighthouse，這是一種開放原始碼自動化工具，用於提高網頁應用程式的品質。您可以用於在任何網頁 (公用網頁或需要身份驗證的網頁) 上執行。可用於對效能、協助工具、漸進式網頁應用程式、SEO 等進行稽核。

有興趣測試新儀表板嗎？請使用和您的 Adob&#x200B;&#x200B;e ID 相關聯的電子郵件傳送電子郵件至 `aem-lighthouse-pilot@adobe.com`，我們就會協助您開始使用。

## 錯誤修正 {#bug-fixes}

* 刪除程式時，也會刪除任何相關聯且正在執行的管道，以確保管道不會錯誤指定為失敗狀態。
* 上線完成按鈕已停用，並通知使用者管道正在進行的原因。
* 有時，當管道執行的所有步驟都是「已完成」時，管道的狀態會視為「執行中」，使其看起來像是處於卡住狀態。 它現在會視為「完成」。
