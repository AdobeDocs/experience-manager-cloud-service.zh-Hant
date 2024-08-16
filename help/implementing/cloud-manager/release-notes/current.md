---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.8.0 的發行說明
description: 瞭解AEM as a Cloud Service中Cloud Manager 2024.8.0的發行說明。
feature: Release Information
role: Admin
source-git-commit: a823bcd1461b847983d0243cd9abd59efd8d7b6f
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 26%

---


# Adobe Experience Manager as a Cloud Service中Cloud Manager 2024.8.0的發行說明 {#release-notes}

本頁面記錄 AEM as a Cloud Service 中 Cloud Manager 版本 2024.8.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager版本2024.8.0發行日期為2024年8月14日。 下一版本計畫於2024年9月14日發行。

## 新增功能 {#what-is-new}

* [其他發佈區域](/help/operations/additional-publish-regions.md)和[99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) （服務等級協定）現在可供AEM Formsas a Cloud Service使用。
   * 此增強功能可讓您透過增加連續運作時間及減少延遲，達成更高的SLA，確保為分散於全球的使用者提供同級最佳的體驗。

## 早期採用計畫 {#early-adoption}

若想要有機會測試一些即將推出的功能，請參加 Adobe 的早期採用者計劃。

### Cloud Manager中的Edge Delivery Services支援 {#edge-delivery-services}

如果您已將Edge Delivery Services授權為AEM Sites的一部分，[您現在可以直接在Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md)中使用Edge Delivery Services上線網站，並使用引導式自助服務體驗上線。

此功能可為您的所有AEM屬性提供統一的體驗。 它可確保關鍵工作流程的一致性，例如網域名稱管理、SSL憑證管理和CDN對應。

如果您有興趣測試這項新功能並分享您的回饋意見，請從與您的Adobe ID相關聯的電子郵件地址傳送電子郵件至`aemcs-cmedgedelsvs-program-adopter@adobe.com`。

### 網域驗證(DV)憑證

透過Cloud Manager，您現在可以[自助式產生和管理網域已驗證(DV) SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)。 此功能為您提供最快、最簡單且最具成本效益的解決方案，為您的線上業務建立安全的網站。

如果您想要測試這項新功能並提供您的回饋意見，請使用連結至您Adobe ID的電子郵件地址傳送電子郵件至`Grp-aemcs-dv-dert-adopter@adobe.com`。

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板使用 Google Lighthouse，這是一種開放原始碼自動化工具，可提升網頁應用程式的品質。您可以使用它來稽核任何網頁，無論是公開或需要驗證。 它提供效能、協助工具、漸進式網頁應用程式、SEO等評估。

想要試用新儀表板嗎？ 若要開始，請使用連結至您Adobe ID的電子郵件傳送電子郵件至`aem-lighthouse-pilot@adobe.com`。

## 錯誤修正

* 已修正刪除管道後發現管道步驟正在執行的一個罕見問題。
* 已修正組態管道在極少數情況下錯誤顯示`FAILED`狀態的問題。
