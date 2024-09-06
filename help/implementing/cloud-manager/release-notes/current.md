---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.9.0 的發行說明
description: 瞭解AEM as a Cloud Service中Cloud Manager 2024.9.0的發行說明。
feature: Release Information
role: Admin
source-git-commit: cfaa3be31195929b80310610120a779a20537c61
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 15%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.9.0 的發行說明 {#release-notes}

本頁面記錄 AEM as a Cloud Service 中 Cloud Manager 版本 2024.9.0 的發行說明。

>[!NOTE]
>
>請參閱Adobe Experience Manager as a Cloud Service ](/help/release-notes/release-notes-cloud/release-notes-current.md)的[最新發行說明。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager版本2024.9.0發行日期是2024年9月5日。 下一版本計畫於2024年10月3日發行。

## 新增功能 {#what-is-new}

* **體驗稽核儀表板：**

  AdobeCloud Manager的[增強體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md) (採用Google Lighthouse技術)可評估核心Web重要功能、SEO和協助工具量度，以提供AEM Sites品質和效能的深入分析。 透過提供可操作建議、讓團隊增強使用者體驗、頁面載入時間和網站合規性，它有助於使用者識別需要改進的領域。 此儀表板可簡化關鍵網站量度的監控，並確保AEM應用程式符合高效能和協助工具標準。

* **Adobe產生並管理的網域驗證憑證：**

  透過Cloud Manager，您現在可以[自助Adobe產生和受管理的DV （網域驗證） SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 此功能為您提供最快、最簡單且最具成本效益的解決方案，為您的線上組織或企業建立安全的網站。<!-- CMGR-52403 -->

* Cloud Manager中的&#x200B;**Edge Delivery Services支援：**

  如果您擁有AEM Sites中的Edge Delivery Services授權，[您現在可以直接透過Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md)使用Edge Delivery Services加入您的網站。 此功能可啟用引導式自助上線體驗。 此外也統一所有AEM屬性中的網域名稱管理、SSL憑證和CDN對應等基本工作流程，確保一致性和效率。<!-- CMGR-49859 -->

* 使用GitHub存放庫的客戶現在能夠建立和使用網頁層級設定管道。<!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## 錯誤修正

* SSL憑證表格檢視的分頁現在可如預期運作。<!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* 使用執行中的&#x200B;**Promote Build**&#x200B;按鈕時，升級了錯誤的成品版本。<!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
