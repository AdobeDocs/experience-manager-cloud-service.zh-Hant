---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.7.0 的發行說明
description: 以下是AEM as a Cloud Service中Cloud Manager 2024.7.0的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: a5cd55bcdc6044dd8db26f009b955216cda5daee
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 57%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.7.0 的發行說明 {#release-notes}

本頁面記錄 AEM as a Cloud Service 中 Cloud Manager 版本 2024.7.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager版本2024.7.0發行日期為2024年7月18日。 下一版本計畫於 2024 年 8 月 8 日發行。

## 新增功能 {#what-is-new}

* [生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)和[非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)在Git變更上&#x200B;**觸發**&#x200B;以在認可上啟動管道，現在可供[私人存放庫使用。](/help/implementing/cloud-manager/managing-code/private-repositories.md)
   * 我們將分階段推出，並於8月中旬前完成。
* 新增[Adobe管理的DV憑證時，](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)您現在可以新增單一憑證，其涵蓋多個網域，而非為每個網域建立憑證。
* 現在起，只要程式至少套用Sites或Forms解決方案，就可以將沒有[其他發佈區域](/help/operations/additional-publish-regions.md)的解決方案新增至程式。
* 現在可以將沒有[99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)的解決方案新增到計畫中，只要該計畫至少套用了Sites或Forms解決方案。
* [體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)已透過多種方式增強。
   * 現在會透過CDN針對`.com`端點執行稽核，取代之前的`.net`方法。
      * 這項變更可更精確地模擬真實的使用者體驗，並協助您針對管理和最佳化網站做出更明智的決策。
   * 已對體驗稽核UI進行多項增強，包括：
      * 新增效能、最佳實務、SEO和協助工具的趨勢檢視。
      * Lighthouse原始報表連結現在會以更直覺的方式顯示，直接顯示在掃描快照詳細資料面板中。
      * 改善燈塔建議區段。
   * 根據Lighthouse版本12.0.0移除PWA量度，因此消除此量度。

## 早期採用計劃 {#early-adoption}

若想要有機會測試一些即將推出的功能，請參加 Adobe 的早期採用者計劃。

### Cloud Manager 中的 Edge Delivery Services Support {#edge-delivery-services}

如果您已獲得 Edge Delivery Services 授權，成為 Adobe Experience Manager Sites 的一部分，[現在可以直接在 Cloud Manager 中使用 Edge Delivery Services 讓您的網站上線](/help/implementing/cloud-manager/edge-delivery-services.md)，並使用引導式自助服務體驗來啟用網站。

這樣一來，所有 AEM 屬性均能提供統一的體驗，確保與所有關鍵工作流程 (包括網域名稱管理、SSL 憑證管理和內容傳遞網路對應) 保持一致。

如果您有興趣測試此新功能並分享回饋意見，請使用與您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `aemcs-cmedgedelsvs-program-adopter@adobe.com`。

### 網域驗證 (DV) 憑證

您現在可透過 Cloud Manager [以自助方式產生和管理網域驗證 (DV) SSL 憑證。](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) 您要為線上業務建立安全的網站，這便是最快、最簡單且成本效益最高的解決方案。

如果您有興趣測試此新功能並分享回饋意見，請使用與您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `Grp-aemcs-dv-dert-adopter@adobe.com`。

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板使用 Google Lighthouse，這是一種開放原始碼自動化工具，可提升網頁應用程式的品質。您可以用於在任何網頁 (公用網頁或需要身份驗證的網頁) 上執行。可用於對效能、協助工具、漸進式網頁應用程式、SEO 等進行稽核。

有興趣測試新儀表板嗎？若要開始，請使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aem-lighthouse-pilot@adobe.com`。
