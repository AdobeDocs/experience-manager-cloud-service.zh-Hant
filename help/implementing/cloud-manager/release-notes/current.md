---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.12.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.12.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 71ce915413cd968a78a33b7a52d02e09841e1707
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 54%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.12.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2023.12.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEMas a Cloud Service中的Cloud Manager版本2023.12.0發行日期是2023年12月14日。 下一個版本計畫於 2024 年 1 月 18 日發行。

## 新增功能 {#what-is-new}

* [Cloud Manager 自訂權限](/help/implementing/cloud-manager/custom-permissions.md)可讓您以可設定的權限建立自訂權限設定檔，以限制 Cloud Manager 使用者對方案、管道和環境的存取。
   * 此功能將分階段推出，預計2024年2月Cloud Manager版本完成。
   * 請傳送電子郵件至 `Grp-CloudManager-custom-permissions@adobe.com` 來自與您的Adobe ID相關聯的電子郵件地址（如果您希望更早啟用）。
* 建置容器現在支援的Node.js版本18 [前端管道。](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)
* 對於新建立的Cloud Manager計畫， [關聯的New Relic子帳戶](/help/implementing/cloud-manager/user-access-new-relic.md) 預設為未啟用。
   * 若現有方案的New Relic子帳戶超過90天未存取，則會將其停用。
   * 如果您想要使用New Relic子帳戶，則需要透過Cloud Manager選擇加入。
* Java 8和11次要版本的推出以及maven的更新 [宣佈並從10月版本的Cloud Manager開始](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) 已完成。
   * 為前端和完整棧疊管道新增了對節點18的支援。
   * Java 8次要版本已更新至 `jdk1.8.0_371`.
   * Java 11次要版本更新至 `jdk-11.0.20`.
   * Maven已更新至3.8.8版
      * Maven現在會停用所有不安全的專案 `http://*` 預設為映象。
      * [Adobe建議](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 使用者更新其Maven存放庫以使用HTTPS而不是HTTP。
   * 組建容器基礎影像已更新為Ubuntu 22.04。

## 早期採用計劃 {#early-adoption}

若想要有機會測試一些即將推出的功能，請參加 Adobe 的早期採用者計劃。

### 透過真實使用者監控(RUM)進行使用者端收集 {#rum}

您可以善用 [Real User Monitoring (RUM)資料服務](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) 啟用AEMas a Cloud Service的使用者端集合。

Real User Monitoring (RUM) Data Service提供更精確的使用者互動反映，確保可靠衡量網站參與度。 這是取得頁面效能進階深入分析的絕佳機會。 這對使用Adobe管理的CDN或非Adobe管理的CDN的客戶有好處。 對於使用非Adobe託管CDN的客戶，現在可為其啟用自動流量報表，因此無需與Adobe共用任何流量報表。

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `aemcs-rum-adopter@adobe.com` 來自與您的Adobe ID相關聯的電子郵件地址。 請在您的電子郵件中包含生產、中繼和開發環境的網域名稱。  此功能可使用的早期採用者計劃很有限。

### 帶著您自己的 GitHub {#byo-github}

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/implementing/cloud-manager/managing-code/byo-github.md)這種整合消除了始終將程式碼與 Adobe 存放庫保持同步的需要，並允許您先確認提取要求再將其合併到主要分支。

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
