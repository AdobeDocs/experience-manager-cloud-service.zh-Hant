---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.6.0 的發行說明
description: 以下是AEMas a Cloud Service中Cloud Manager 2024.6.0的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 8d5d8910a906e2adf17fa9c75f17634602c2e0b9
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 47%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.6.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2024.6.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.6.0 版發行日期為 2024 年 6 月 6 日。下一版本預計於 2024 年 7 月 11 日發行。

## 新增功能 {#what-is-new}

* 您現在可以 [使用您自己的GitHub存放庫](/help/implementing/cloud-manager/managing-code/private-repositories.md) 作為完整棧疊和前端管道的來源。
   * 此外，您還可以充分利用GitHub存放庫， [Git子模組，](/help/implementing/cloud-manager/managing-code/git-submodules.md) 提供對用於提取請求驗證的自動產生管道的增強控制，並允許您在計畫碼掃描階段定義關鍵量度的行為。
   * [您也可以選擇](/help/implementing/cloud-manager/managing-code/github-check-config.md) 若要保留GitHub上的報表歷史記錄，請命名管道，並設定管道變數以符合您的需求。
* [自助內容還原](/help/operations/restore.md) 提供長達7天的備份還原功能，以及下列功能：
   * 前 24 小時的時間點備份還原
   * 固定時間還原最長可達 7 天
* [新OakPal規則](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) 已新增到Cloud Manager程式碼品質掃描。
   * 自2024年6月起新增的每個新規則都是不中斷的變更。
   * 強烈建議您儘快解決這些問題，因為從2024年8月發行的Cloud Manager版本開始，這些新規則會導致管道失敗。

## 早期採用計劃 {#early-adoption}

若想要有機會測試一些即將推出的功能，請參加 Adobe 的早期採用者計劃。

### Cloud Manager中的Edge Delivery Services支援 {#edge-delivery-services}

如果您已將授權Edge Delivery Services當作Adobe Experience Manager Sites的一部分， [您現在可以直接在Cloud Manager中使用Edge Delivery Services載入您的網站](/help/implementing/cloud-manager/edge-delivery-services.md) 使用引導式自助服務體驗上線。

這可讓您的所有AEM屬性獲得統一的體驗，確保所有關鍵工作流程的一致性，包括網域名稱管理、SSL憑證管理和CDN對應。

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `aemcs-cmedgedelsvs-program-adopter@adobe.com` 來自與您的Adobe ID相關聯的電子郵件地址。

### 網域驗證(DV)憑證

Cloud Manager現在可讓您 [自助服務會產生並管理網域已驗證(DV) SSL憑證。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) 這為您提供最快、最簡單且最具成本效益的解決方案，為您的線上業務建立安全的網站。

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `Grp-aemcs-dv-dert-adopter@adobe.com` 來自與您的Adobe ID相關聯的電子郵件地址。

### 透過實際使用監控(RUM)進行使用者端收集 {#rum}

您可以善用 [Real Use Monitoring (RUM)資料服務](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) 啟用AEMas a Cloud Service的使用者端集合。

Real Use Monitoring (RUM) Data Service提供使用者互動的更精確反映，確保網站參與的可靠測量。 這是深入了解頁面效能的絕佳機會。這對於使用 Adobe 管理 CDN 或非 Adobe 管理 CDN 的客戶很有幫助。對於使用非 Adobe 管理 CDN 的客戶，現在可以啟用自動流量報告，而無需與 Adobe 共享任何流量報告。

如果您有興趣測試此新功能並分享意見反應，請使用與您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `aemcs-rum-adopter@adobe.com`。請在電子郵件中附上生產、階段和開發環境的網域名稱。此功能可使用的早期採用者計劃有限。

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板使用 Google Lighthouse，這是一種開放原始碼自動化工具，可提升網頁應用程式的品質。您可以用於在任何網頁 (公用網頁或需要身份驗證的網頁) 上執行。可用於對效能、協助工具、漸進式網頁應用程式、SEO 等進行稽核。

有興趣測試新儀表板嗎？若要開始，請使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aem-lighthouse-pilot@adobe.com`。
