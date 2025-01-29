---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的發行說明
description: 了解 AEM as a Cloud Service 中 Cloud Manager 2025.1.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 17f6c359a0396c3ee68b43d0140d637856f7f502
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 19%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.1.0 的發行資訊。

>[!NOTE]
>
>請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.1.0發行日期是2025年1月22日星期三。

下一個版本預計於 2025 年 2 月 13 日星期四發行。


## 新增功能 {#what-is-new}

* **程式碼品質規則 — SonarQube伺服器升級：** Cloud Manager程式碼品質步驟將開始使用SonarQube Server 9.9搭配Cloud Manager 2025.2.0版，預計於2025年2月13日星期四執行。

  為了做好準備，更新的 SonarQube 規則現已在 [程式碼品質規則中提供](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)。

  您可以設定下列管道文字變數，以「提前檢查」新規則：

  `CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

  此外，設定以下變數以確保程式碼品質步驟執行相同認可 (通常會跳過相同`commitId`)：

  `CM_DISABLE_BUILD_REUSE` = `true`

![設定變數頁面](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe 建議建立一個新的 CI/CD 程式碼品質管道，並將其配置到與主生產管道相同的分支。在 *2025 年 2 月 13 日發布之前設定適當的變數* ，以驗證新的強制規則不會引入阻止程序。

* **Java 17和Java 21版本支援：**&#x200B;客戶現在可以使用Java 17或Java 21版本進行版本建立，以取得效能增強功能和新的語言功能。 如需設定步驟，包括更新您的Maven專案和程式庫版本，請參閱[組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)。 當組建版本設定為Java 17或Java 21時，部署的執行階段為Java 21。

   * **功能啟用**
      * 此功能將在2025年2月13日星期四對所有客戶啟用，同時預設推出新的SonarQube版本。
      * 客戶可以設定上述升級SonarQube 9.9版的兩個變數設定，立即&#x200B;*啟用*。

   * **Java 21執行階段部署**
      * 使用Java 17或Java 21建置時，會部署Java 21執行階段。
      * Cloud Manager沙箱和開發環境的逐步推出將於2月開始，並持續到4月的生產環境。
      * 使用Java 11建置的客戶若想採用Java 21執行階段&#x200B;*較早*，可以透過[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)聯絡Adobe。

* **「CDN設定」已重新命名為「網域對應」：**&#x200B;隨著AEM Cloud Manager的使用者介面改良專案，「CDN設定」標籤現在已重新命名為「網域對應」。 這項變更可改善術語與功能的協調性。<!-- CMGR-64738 -->

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

* **管道的進階篩選選項：** Cloud Manager現在在管道頁面上提供進階篩選選項，讓您快速存取相關資料並提高部署效率。 幾項主要功能包括：

   * **多重條件篩選：**&#x200B;使用管道名稱、環境和部署程式碼之類的篩選條件來調整搜尋結果。
   * **簡化的管道搜尋：**&#x200B;輕鬆找到特定管道，以加快導覽速度並改善工作流程管理。

  總之，這些增強功能使管道的管理和部署更有效率且更方便使用。

  ![管道篩選器功能](/help/implementing/cloud-manager/release-notes/assets/pipeline-filters.png)

* **Edge Delivery服務的自助服務CDN設定：** Edge Delivery服務的新採用者現在可以透過Cloud Manager獨立設定其CDN。 此更新將支援從`.hlx.page/live`延伸至新的`.aem.page/live`，提供更大的彈性並簡化使用者的設定。

## 早期採用方案 {#early-adoption}

成為 Cloud Manager 早期採用方案的一部分，並有機會測試即將推出的功能。

* **早期採用者程式更新 — Bitbucket和GitLab的PR驗證支援：** Cloud Manager現在同時支援Bitbucket和GitLab的雲端和自控版本的提取請求(PR)驗證。 此功能可讓客戶在合併PR之前，根據Adobe的程式碼品質臨界值測試其程式碼變更。 透過在合併之前確保更高的計畫碼品質，此增強功能可大幅改善生產管道中計畫碼變更的成功率，縮短上市時間並簡化開發工作流程。

如需有關「自攜Git」（現在支援GitLab和Bitbucket）以及註冊為早期採用者的詳細資訊，請參閱[Cloud Manager 2024年10月發行說明](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md##gitlab-bitbucket)。

* **進階測試環境：**&#x200B;專門建置的解決方案，旨在縮短開發及生產之間的差距。 此環境針對企業需求量身打造，可複製生產層級的規格，以支援精確的使用者驗收測試(UAT)和完整的效能評估。

如果您有興趣加入Early Adopter計畫，請[完成此表單](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Furldefense.com%2Fv3%2F__https%3A%2Fwww.feedbackprogram.adobe.com%2Fh%2Fs%2F6N425LYG1jQ1Nc0F20Zllt__%3B!!OgNkHJCYlf_CHg！fIp-QrZ9si3kcUIjRCniEzqAAa8FcU1iN34SGQFtlcQ36eUQXOZWbDHP7oZajqdgpuOMAVL5CQpkZ6ths76A qks8%24&amp;data=05%7C02%7Cpanchapa%40adobe.com%7Cf81bcaa4b20544f1818b08dccd07c78c%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638610680502164019%7CUnknown%7CTWFpbGZsb3d8eyJWIawMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=aGo6zz2ldPrta4lpvo3CLNENR5ghHDDCPbG1adUaNZQ%3D&amp;reserved=0)，並傳送電子郵件至[earlyadopter_cs_advtestenvironment@adobe.com](mailto:earlyadopter_cs_advtestenvironment@adobe.com) （含您的`OrgID`）。



<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
