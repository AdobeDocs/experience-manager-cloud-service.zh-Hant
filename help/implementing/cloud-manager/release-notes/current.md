---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的發行說明
description: 了解 AEM as a Cloud Service 中 Cloud Manager 2025.1.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: ee01e5a2b805330f47af7ff563ca1ac90036f0bf
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 10%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.1.0 的發行資訊。

>[!NOTE]
>
>請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.1.0發行日期是2025年1月22日星期三。

下一個預計發行日期為2025年2月13日星期四。


## 新增功能 {#what-is-new}

* **程式碼品質規則 — SonarQube伺服器升級：** Cloud Manager程式碼品質步驟將開始使用SonarQube Server 9.9搭配Cloud Manager 2025.2.0版，預計於2025年2月13日星期四執行。

  若要準備，更新的SonarQube規則現在可在[程式碼品質規則](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)取得。

  您可以設定下列管道文字變數，以「提前檢查」新規則：

  `CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

  此外，設定下列變數，以確保程式碼品質步驟會針對相同的認可執行（通常針對相同的`commitId`略過）：

  `CM_DISABLE_BUILD_REUSE` = `true`

![變數設定頁面](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe建議建立新的CI/CD程式碼品質管道，並設定至與您的主要生產管道相同的分支。 在2025年2月13日發行版本之前&#x200B;*設定適當的變數*，以驗證新的強制規則不會引入封鎖程式。

* **Java 17和Java 21版本支援：**&#x200B;客戶現在可以使用Java 17或Java 21版本進行版本建立，以取得效能增強功能和新的語言功能。 如需設定步驟，包括更新您的Maven專案和程式庫版本，請參閱[組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)。 當組建版本設定為Java 17或Java 21時，部署的執行階段為Java 21。

   * **功能啟用**
      * 此功能將在2025年2月13日星期四對所有客戶啟用，同時預設推出新的SonarQube版本。
      * 客戶可以設定上述升級SonarQube 9.9版的兩個變數設定，立即&#x200B;*啟用*。

   * **Java 21執行階段部署**
      * 使用Java 17或Java 21建置時，會部署Java 21執行階段。
      * Cloud Manager沙箱和開發環境的逐步推出將於2月開始，並持續到4月的生產環境。
      * 使用Java 11建置的客戶若想採用Java 21執行階段&#x200B;*較早*，可以透過[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)聯絡Adobe。

* **「CDN設定」已重新命名為「網域對應」：**&#x200B;隨著AEM Cloud Manager的使用者介面改善，標籤「CDN設定」現在已重新命名為「網域對應」。 這項變更可改善術語與功能的協調性。<!-- CMGR-64738 -->

  ![「CDN設定」在使用者介面](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)中重新命名為「網域對應」

* **只要按一下即可布建Edge Delivery網站：** Cloud Manager現在可讓具有適當許可權和授權的使用者只要按一下即可建立範例Edge Delivery Services網站。 此簡化程式提供下列自動化功能：

   * **GitHub整合** — 在現有組織內自動建立GitHub存放庫，並預先設定Edge Delivery Services的樣板範本。
   * **AEM Code Sync App安裝** — 在存放庫上安裝AEM Code Sync App，確保順暢的同步和部署。
   * **內容Collaboration安裝程式** — 連結指定的Google磁碟機資料夾以儲存內容，提供內容管理的協同合作環境。
   * **內容發佈** — 使用者現在可以直接從Cloud Manager使用者介面發佈已布建網站的內容，簡化工作流程並提升效率。
   * **增強型Collaboration** — 此平台可讓使用者將多位共同作業人員新增至Google Drive內容儲存資料夾，以利團隊合作及貢獻內容。

  這些增強功能旨在改善自動化、簡化設定流程，並增強Edge Delivery Services使用者的共同作業。<!-- CMGR-59362 -->

  ![布建Edge Delivery網站](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

  ![布建Edge Delivery網站對話方塊](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)

* **Edge Delivery Services網站的增強支援：** Cloud Manager現在支援加入最新的Edge Delivery Services網站。 此更新包含了CDN和傳遞棧疊的全面重構，進而改善了健全性和可維護性。

* **早期採用者程式更新 — Bitbucket和GitLab的PR驗證支援：** Cloud Manager現在同時支援Bitbucket和GitLab的雲端和自控版本的提取請求(PR)驗證。 此功能可讓客戶在合併PR之前，根據Adobe的程式碼品質臨界值測試其程式碼變更。 透過在合併之前確保更高的計畫碼品質，此增強功能可大幅改善生產管道中計畫碼變更的成功率，縮短上市時間並簡化開發工作流程。


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
