---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.2.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2024.2.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4a41de9da557be562bb2ff5773c7954f76a9acc7
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 83%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.2.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2024.2.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2024.2.0 發行日期是 2024 年 ２ 月 15 日。下一個版本計畫於 2024 年 3 月 16 日發行。

## 新增功能 {#what-is-new}

* Cloud Manager現在支援的自助服務管理 [管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) 透過Cloud Manager UI。
* [預覽服務](/help/implementing/cloud-manager/manage-environments.md#access-preview-sevice) 現在將會針對在預覽服務功能推出之前建立的環境啟用。
* [Cloud Manager 自訂權限](/help/implementing/cloud-manager/custom-permissions.md)可讓您以可設定的權限建立自訂權限設定檔，以限制 Cloud Manager 使用者對方案、管道和環境的存取。
   * 此功能開始以分階段方式推出 [2023年12月發行版本](/help/implementing/cloud-manager/release-notes/2023/2023-12-0.md) 並將於2024年2月20日完成。
* 針對所有新環境， [環境產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) 根據設定檔說明、環境型別、數字和計畫編號的組合，名稱將是更方便使用的格式。
* [組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 已更新至Maven 3.9.4版和JDK jdk-11.0.22版和jdk1.8.0_401版。

## 早期採用計劃 {#early-adoption}

若想要有機會測試一些即將推出的功能，請參加 Adobe 的早期採用者計劃。

### 透過真實使用者監控 (RUM) 進行用戶端彙集 {#rum}

您可以利用[真實使用者監控 (RUM) 資料服務](/help/implementing/cloud-manager/content-requests.md#cliendside-collection)為 AEM as a Cloud Service 啟用用戶端彙集。

真實使用者監控 (RUM) 資料服務可以更準確地反映使用者互動，確保可靠地測量網站參與度。這是深入了解頁面效能的絕佳機會。這對於使用 Adobe 管理 CDN 或非 Adobe 管理 CDN 的客戶很有幫助。對於使用非 Adobe 管理 CDN 的客戶，現在可以啟用自動流量報告，而無需與 Adobe 共享任何流量報告。

如果您有興趣測試此新功能並分享意見反應，請使用與您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `aemcs-rum-adopter@adobe.com`。請在電子郵件中附上生產、階段和開發環境的網域名稱。此功能可使用的早期採用者計劃有限。

### 帶著您自己的 GitHub {#byo-github}

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/implementing/cloud-manager/managing-code/byo-github.md)透過此一整合，便不再需要持續與 Adobe 存放庫進行程式碼同步化，並讓您可以先確認提取要求再將其合併到主要分支。這是公開 GitHub 的專屬功能。不支援自行託管的 GitHub。

如果您有興趣測試此新功能並分享您的意見反應，可使用和您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `Grp-CloudManager_BYOG@adobe.com`。

### 自助服務內容還原 {#content-restore}

[新的自助服務內容還原功能](/help/operations/restore.md)現在會提供最長達 7 天的備份還原，並可供早期採用者用於評估目的，其中包括：

* 前 24 小時的時間點備份還原
* 固定時間還原最長可達 7 天

如果您有興趣測試此新功能並分享您的意見反應，可使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aemcs-restorefrombackup-adopter@adobe.com`。

* 早期採用者計劃僅適用於開發環境。
* 此功能可使用的早期採用者計劃很有限。
* 此功能用於恢復意外刪除的內容，不適用於災難復原。

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板使用 Google Lighthouse，這是一種開放原始碼自動化工具，可提升網頁應用程式的品質。您可以用於在任何網頁 (公用網頁或需要身份驗證的網頁) 上執行。可用於對效能、協助工具、漸進式網頁應用程式、SEO 等進行稽核。

有興趣測試新儀表板嗎？若要開始，請使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aem-lighthouse-pilot@adobe.com`。

## 錯誤修正 {#bug-fixes}

* 組建容器的JDK已更新至可解決的版本 [JDK-8313765。](https://bugs.openjdk.org/browse/JDK-8313765)
