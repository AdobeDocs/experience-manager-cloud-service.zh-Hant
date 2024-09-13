---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.9.0 的發行說明
description: 了解 AEM as a Cloud Service 中 Cloud Manager 2024.9.0 的發行說明。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 610ae004b6da2f7fc0dae2baa613cb363fe9fb00
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 83%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.9.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2024.9.0 的發行說明。

>[!NOTE]
>
>請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2024.9.0 發行日期是 2024 年 9 月 5 日。下一版本預計於 2024 年 10 月 3 日發行。

## 新增功能 {#what-is-new}

* **體驗稽核儀表板：**

  Adobe Cloud Manager 的[增強型體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)由 Google Lighthouse 提供技術支援，透過評估核心頁面指標、SEO 和可存取性指標，提供對 AEM Sites 品質和效能的分析。它透過提供可操作的建議協助使用者確定需改善的區域，使團隊能夠增強使用者體驗、頁面載入時間和網站遵循性。此儀表板簡化了關鍵網站指標的監測，並確保 AEM 應用程式符合高效能和可存取性標準。

* **新增由 Adobe 產生和管理的網域驗證憑證：**

  您現在能夠透過 Cloud Manager [自選由 Adobe 產生和管理的網域驗證 (DV) SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。若您要建立安全的線上組織或企業網站，此功能是最快、最簡單且成本效益最高的解決方案。<!-- CMGR-52403 -->

  >[!NOTE]
  >
  >[Content Hub](/help/assets/product-overview.md)客戶計劃分階段接收此功能，作為逐步推出的一部分。

* **Cloud Manager 的 Edge Delivery Services 支援：**

  如果您擁有AEM Sites中的Edge Delivery Services授權，現在可以直接透過Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md)使用Edge Delivery Services加入您的網站[。 此功能可提供引導式自助上線體驗。它還統一所有 AEM 屬性中的網域名稱管理、SSL 憑證和內容傳遞網路 (CDN) 對應等必要工作流程，確保一致性和效率。<!-- CMGR-49859 -->

  >[!NOTE]
  >
  >[Content Hub](/help/assets/product-overview.md)客戶計劃分階段接收此功能，作為逐步推出的一部分。

* 使用 GitHub 存放庫的客戶可立即建立和使用 Web 層級設定管道。<!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## 錯誤修正

* SSL 憑證表格視圖的分頁現在可以如預期運作。<!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* 在執行中使用「**提升組建版本**」按鈕時，導致錯誤的成品版本獲得升級。<!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
