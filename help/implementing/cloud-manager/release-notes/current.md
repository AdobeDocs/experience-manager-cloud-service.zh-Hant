---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的發行說明
description: 了解 AEM as a Cloud Service 中 Cloud Manager 2025.1.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f6c1aa32647bcabeb0781973f81b75c11edc6a5d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 18%

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

* **「CDN設定」已重新命名為「網域對應」：**&#x200B;隨著AEM Cloud Manager的使用者介面改善，標籤「CDN設定」現在已重新命名為「網域對應」，以改善術語與功能的對應。<!-- CMGR-64738 -->

  ![「CDN設定」在使用者介面](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)中重新命名為「網域對應」


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
