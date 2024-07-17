---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.6.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2024.6.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 6ca376bda8055d62e35e13053ff21f861c12b292
workflow-type: ht
source-wordcount: '548'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.6.0 的發行說明 {#release-notes}

本頁面記錄 AEM as a Cloud Service 中 Cloud Manager 版本 2024.6.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.6.0 版發行日期為 2024 年 6 月 6 日。下一版本預計於 2024 年 7 月 18 日發行。

## 新增功能 {#what-is-new}

* 您現在可以[使用自己的 GitHub 存放庫](/help/implementing/cloud-manager/managing-code/private-repositories.md)，做為完整堆疊和前端管道的來源。
   * 此外，您還可以透過有 [Git 子模組](/help/implementing/cloud-manager/managing-code/git-submodules.md)的 GitHub 存放庫，對用於驗證提取請求的自動產生的管道增強控制，並定義程式碼掃描階段中關鍵指標的行為。
   * [您也可以選擇](/help/implementing/cloud-manager/managing-code/github-check-config.md)在 GitHub 上保留報告歷史記錄、命名管道，以及按照您的需求設定管道變數。
* [自助內容還原](/help/operations/restore.md)提供最多 7 天的備份還原，並具備下列功能：
   * 前 24 小時的時間點備份還原
   * 固定時間還原最長可達 7 天
* [新的 OakPal 規則](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package)已新增至 Cloud Manager 程式碼品質掃描。
   * 截至 2024 年 6 月新增的每項新規則都是非重大變更。
   * 建議您盡快解決這些問題，因為這些新規則將會導致 Cloud Manager 2024 年 8 月版本無法啟動管道。

## 早期採用計劃 {#early-adoption}

若想要有機會測試一些即將推出的功能，請參加 Adobe 的早期採用者計劃。

### Cloud Manager 中的 Edge Delivery Services Support {#edge-delivery-services}

如果您已獲得 Edge Delivery Services 授權，成為 Adobe Experience Manager Sites 的一部分，[現在可以直接在 Cloud Manager 中使用 Edge Delivery Services 讓您的網站上線](/help/implementing/cloud-manager/edge-delivery-services.md)，並使用引導式自助服務體驗來啟用網站。

這樣一來，所有 AEM 屬性均能提供統一的體驗，確保與所有關鍵工作流程 (包括網域名稱管理、SSL 憑證管理和內容傳遞網路對應) 保持一致。

如果您有興趣測試此新功能並分享回饋意見，請使用與您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `aemcs-cmedgedelsvs-program-adopter@adobe.com`。

### 網域驗證 (DV) 憑證

您現在可透過 Cloud Manager [以自助方式產生和管理網域驗證 (DV) SSL 憑證。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) 您要為線上業務建立安全的網站，這便是最快、最簡單且成本效益最高的解決方案。

如果您有興趣測試此新功能並分享回饋意見，請使用與您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `Grp-aemcs-dv-dert-adopter@adobe.com`。

<!-- RICK: REMOVED THIS SECTION AS PER EMAIL REQUEST TO DL-AEM-DOCS FROM SHWETA DUA, WEDNESDAY, JUNE 12, 2024 ### Client-Side Collection via Real Use Monitoring (RUM) {#rum}

You can leverage the [Real Use Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) to enable client-side collection for AEM as a Cloud Service.

Real Use Monitoring (RUM) Data Service offers a more precise reflection of user interactions, ensuring a reliable measure of website engagement. It is a great opportunity to gain advanced insights into your page performance. This is beneficial for customers who use either Adobe-managed CDN or non-Adobe managed CDN. For customers using a non-Adobe managed CDN, automated traffic reporting can now be enabled for them, thus removing the need to share any traffic report with Adobe.

If you are interested in testing this new feature and sharing your feedback, please send an email to `aemcs-rum-adopter@adobe.com` from the email address associated with your Adobe ID. Please include the domain name for production, stage, and dev environments in your email.  Availability of the early adopter program of this feature is limited.-->

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板使用 Google Lighthouse，這是一種開放原始碼自動化工具，可提升網頁應用程式的品質。您可以用於在任何網頁 (公用網頁或需要身份驗證的網頁) 上執行。可用於對效能、協助工具、漸進式網頁應用程式、SEO 等進行稽核。

有興趣測試新儀表板嗎？若要開始，請使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aem-lighthouse-pilot@adobe.com`。
