---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.7.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2024.7.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 12e19fe771c0b70ec471949944141f4d6858cbfd
workflow-type: ht
source-wordcount: '633'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.7.0 的發行說明 {#release-notes}

本頁面記錄 AEM as a Cloud Service 中 Cloud Manager 版本 2024.7.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2024.7.0 版發行日期為 2024 年 7 月 18 日。下一版本計畫於 2024 年 8 月 8 日發行。

## 新增功能 {#what-is-new}

* [生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)和[非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)觸發器「**在 Git 變更**」現在可用於[私人存放庫](/help/implementing/cloud-manager/managing-code/private-repositories.md)，在提交時啟動管道。
   * 這將分階段推出，並於 8 月中旬完成。
* 當您新增「[Adobe 管理的 DV 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md)」時，您現在可以新增涵蓋多個網域的單一憑證，而不是為每個網域都建立憑證。
* 現在，只要程式至少有一個適用的 Sites 或 Forms 解決方案，就可以將沒有[其他發佈區域](/help/operations/additional-publish-regions.md)的解決方案新增至該程式。
* 現在，只要程式至少有一個適用的 Sites 或 Forms 解決方案，就可以將不具有 [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) 的解決方案新增至該程式。
* 「[體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)」已透過多種方式增強。
   * 現在透過 CDN 針對 `.com` 端點執行稽核，取代了先前的 `.net` 方法。
      * 此變更可以更準確地模擬真實的使用者體驗，並幫助您在管理和最佳化網站方面做出更明智的決策。
   * 體驗稽核 UI 進行了多項增強，包括：
      * 新增了效能、最佳實務、SEO 和可存取性的趨勢檢視。
      * 現在，可以直接在掃描快照詳細資料面板中以更直觀的方式查看 Lighthouse 原始報告連結。
      * 增強了 Lighthouse 推薦區段。
   * 根據 Lighthouse 版本 12.0.0 移除了 PWA 指標，該版本已刪除該指標。
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 已更新至[版本 49](https://github.com/adobe/aem-project-archetype/tree/aem-project-archetype-49)。

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
