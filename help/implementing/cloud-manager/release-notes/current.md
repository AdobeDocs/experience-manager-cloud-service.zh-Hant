---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.10.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.10.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: b760b3a65d89b0b4f924379fc460015a58e2ed3e
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 63%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.10.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2023.10.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2023.10.0 發行日期是 2023 年 10 月 5 日。下一個版本計畫於 2023 年 11 月 2 日發行。

## 新增功能 {#what-is-new}

* 改善以下功能 [索引](/help/operations/indexing.md) 縮短了部署新索引時的管道持續時間。
   * 改良功能會因內容設定檔而異。
* 自動 [開發環境的更新](/help/implementing/cloud-manager/manage-environments.md#updating-environments) 預設為新程式啟用，為您節省手動執行更新的時間。
   * 此更新將分階段推出。
* 在2023年10月發行的Cloud Manager中，Java版本正在透過分階段推出進行更新。
   * Java 8和11以及Maven的次要版本已更新，並將在未來2個月內分階段推出。 新版本包含多項安全性修正和錯誤修正。 新版本為：
   * *Maven： 3.8.8*
   * *Java 8版本： /usr/lib/jvm/jdk1.8.0_371*
   * *Java 11版本： /usr/lib/jvm/jdk-11.0.20*
   * [請參閱OpenJDK公告](https://openjdk.org/groups/vulnerability/advisories/) 瞭解這些JDK更新中的安全性和錯誤修正的詳細資訊。

## 早期採用計劃 {#early-adoption}

參加我們的早期採用計劃，即有機會測試一些即將推出的功能。

### 自訂許可權 {#custom-permissions}

[Cloud Manager自訂許可權](/help/implementing/cloud-manager/custom-permissions.md) 可讓您使用可設定的許可權來建立新的自訂許可權設定檔，以限制對Cloud Manager使用者的程式、管道和環境的存取。

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `Grp-CloudManager-custom-permissions@adobe.com` 來自與Adobe ID相關聯的電子郵件地址。

### 自助服務內容還原 {#content-restore}

[新的自助服務內容還原功能](/help/operations/restore.md)現在會提供最長達 7 天的備份還原，並可供早期採用者用於評估目的，其中包括：

* 前 24 小時的時間點備份還原
* 固定時間還原最長可達 7 天

如果您有興趣測試此新功能並分享您的意見反應，請使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aemcs-restorefrombackup-adopter@adobe.com`。請注意：

* 早期採用者計劃僅適用於開發環境。
* 此功能可使用的早期採用者計劃很有限。
* 此功能用於恢復意外刪除的內容，不適用於災難復原。

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板會利用 Google Lighthouse，這是一種開放原始碼自動化工具，用於提高網頁應用程式的品質。您可以用於在任何網頁 (公用網頁或需要身份驗證的網頁) 上執行。可用於對效能、協助工具、漸進式網頁應用程式、SEO 等進行稽核。

有興趣測試新儀表板嗎？請使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aem-lighthouse-pilot@adobe.com`，我們就會協助您開始使用。
