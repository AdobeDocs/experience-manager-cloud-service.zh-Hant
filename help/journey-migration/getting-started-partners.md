---
title: Experience Manager as a Cloud Service 合作夥伴移轉指南
description: Experience Manager as a Cloud Service 合作夥伴移轉指南
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
feature: Migration
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 18%

---

# Adobe Experience Manager as a Cloud Service 合作夥伴移轉指南 {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="移轉至 AEM as a Cloud Service"
>abstract="概述建議的分階段方法，將客戶從各種 Experience Manager 部署轉變到 Experience Manager as a Cloud Service，並協助現有客戶實現連線而持續的體驗"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=zh-Hant" text="有哪些新增的不同功能？"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html?lang=zh-Hant" text="AEM as a Cloud Service 簡介。"

Adobe Experience Manager (AEM) as a Cloud Service提供Experience Manager的更新架構。 此基礎是建置在容器式基礎結構、API導向式開發和引導式DevOps程式上。 這可讓行銷人員和開發人員在客戶體驗管理創新中保持領先地位。

Cloud Service結合了Adobe Experience Manager豐富的現成可用功能及擴充性，以及現代雲端原生架構的靈活性，讓品牌能夠滿足不斷變化的消費者需求。

本頁面概述將客戶從舊版Experience Manager部署轉變為Experience Manager as a Cloud Service時建議的分階段方法。 全新的專門建置平台可協助您提供連線且持續的體驗。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

請參閱下圖，以取得移轉歷程的一般表示法。

![移轉歷程的一般表示法](/help/journey-migration/assets/migration-process.png)

## Adobe Experience Manager as a Cloud Service快速入門 {#getting-started}

| 有什麼不同？ | 架構概觀 |
|--------------------------|--------------------------|
| <ul><li>[現代架構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=zh-Hant)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=zh-Hant)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=zh-Hant)</li><li>[資產微服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=zh-Hant)</li><li>[直接存取二進位檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=zh-Hant)</li><li>[程式碼與內容的分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant)</li><li>[復寫為服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=zh-Hant)</li><li>[Admin Console、群組/使用者成員資格和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hant)</li></ul> | <ul><li>[AEM架構簡介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=zh-Hant#underlying-technology)</li><li>[環境棧疊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=zh-Hant)</li><li>[作者階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=zh-Hant#underlying-technology)</li><li>[發佈階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=zh-Hant#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=zh-Hant)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=zh-Hant) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=zh-Hant) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hant) (透過[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hant))</li><li>[Asset Compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/home.html?lang=zh-Hant)</li></ul> |

![AEM as a Cloud Service - 執行階段架構](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - 執行階段架構")

<br>

## Adobe Experience Manager as a Cloud Service中的開發人員歷程 {#developer-journey}

### 開發

Adobe Experience Manager as a Cloud Service中的程式碼開發基礎類似於Adobe Experience Manager內部部署和Managed Services解決方案中的基礎。

開發人員撰寫程式碼並在本機進行測試，然後將其推送到遠端Adobe Experience Manager as a Cloud Service環境。

請參閱有關Experience Manager as a Cloud Service實作的自助資源，以瞭解如何自訂Experience Manager as a Cloud Service部署。

| 本機開發設定 | 開始前須知 |
|-----------|------------|
| <ol><li>請檢閱[Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=zh-Hant)檔案以深入瞭解。</li><li>觀看[安裝Dispatcher SDK](https://video.tv.adobe.com/v/30601)，瞭解如何安裝Dispatcher SDK</li><li>觀看[設定Dispatcher SDK](https://video.tv.adobe.com/v/30602)，瞭解如何設定Dispatcher SDK</li><li>請檢閱[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=zh-Hant#local-development-environment-set-up)檔案以深入瞭解</li><li>設定Experience Manager [逐步說明](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=zh-Hant#accessing)的存取權</li></ol> | <ol><li>[開發要點](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=zh-Hant)</li><li>[開發指導方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=zh-Hant)</li><li>[瞭解Experience Manager專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant)</li><li>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)</li><li>[數位基礎藍圖](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[樣式系統](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=zh-Hant)</li><li>[重疊](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manager as a Cloud Service API參考](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> 請參閱教學課程，瞭解如何[在本機Experience Manager SDK上](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)開發及部署WKND

### 部署中

開發人員撰寫程式碼並在本機進行測試，然後將其推送到遠端AEM as a Cloud Service環境。

Cloud Manager是Managed Services的選用內容傳送工具，現在需使用。 這是將程式碼部署至AEM as a Cloud Service環境的唯一機制。

請參閱自助資源，瞭解如何設定並部署至AEM as a Cloud Service環境。

1. [設定CM管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=zh-Hant)

   * 生產管道
   * 非生產和僅限程式碼品質管道

1. [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant)
1. [瞭解測試結果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=zh-Hant)
1. **存取記錄檔**

   * [透過CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=zh-Hant)
   * 透過Adobe i/o cli[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=zh-Hant#debugging)

1. [作業與維護](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=zh-Hant)

   * [正在設定OSGI設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=zh-Hant)
   * [備份和還原](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=zh-Hant)

>[!TIP]
> 請參閱教學課程，瞭解如何[將WKND部署至Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)

### 說明和資源

1. [偵錯提示與秘訣](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=zh-Hant#debugging-aem-as-a-cloud-service)
1. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=zh-Hant#debugging)
1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=zh-Hant) (僅適用於本機SDK和Experience Manager雲端開發環境)
1. [記錄檔和記錄檔](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=zh-Hant#debugging)

   * [CM記錄檔](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=zh-Hant#debugging) （建置單元測試、程式碼掃描、建置影像、部署）
   * [Experience Manager Cloud Service記錄檔](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=zh-Hant#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpcaccess)
   * 本機SDK記錄檔（在host:port/crx-quickstart/logs下）

>[!NOTE]
>
> 如需其他說明，您可能需要：
>
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=zh-Hant)
>1. 探索[Experience Manager社群與論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=zh-Hant)

<br>

## 移至 Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="移至 Adobe Experience Manager as a Cloud Service"
>abstract="此單一頁面會概述建議的分階段方法，以用於將客戶從各種 Experience Manager 部署轉變到 Experience Manager as a Cloud Service，並協助現有客戶在此專門建置的新式體驗管理平台上實現連線而持續的體驗。"

**Experience Manager as a Cloud Service為Experience Manager Sites和Assets提供可擴充、安全且敏捷的技術基礎，讓行銷和IT人員專注於大規模提供具影響力的體驗。**

有了Experience Manager as a Cloud Service，您的團隊便能專注於創新而非規劃產品升級。 新產品功能會經過徹底測試，並持續傳送給您的團隊，讓團隊可以隨時存取最先進的應用程式。

轉換至Cloud Service的過程包含三個階段：規劃、執行和上線後。
為了順利成功轉換，您應該確保有正確規劃，並遵守本指南所概觀的最佳作法。

下圖顯示建議的Cloud Service轉換歷程的高層級表示。

![建議的Cloud Service轉換歷程的高階呈現](/help/journey-migration/assets/home-img1.png)

<br>

### 規劃

在開始轉換至Cloud Service的歷程之前，您應該：

* 熟悉Experience Manager as a Cloud Service
* 檢閱對其進行的重大變更
* 檢閱已取代或已棄用的功能

<table>
<tr>
<td>專案探索與評估</td>
<td><ul><li>請參閱<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=zh-Hant">Experience Manager as a Cloud Service的重大變更</a>，瞭解Adobe Experience Manager as a Cloud Service與Experience Manager 6.x之間的重要差異。</li><li>請參閱<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=zh-Hant">已棄用的功能</a>，深入瞭解已標示為已棄用的功能。</li><li>[僅適用於Cloud Service移轉]評估Cloud Service整備：在來源環境中執行<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=zh-Hant">Best Practices Analyzer (BPA)</a> </li><li>針對Experience Manager CS中的重大變更和已棄用功能完成評估</li></ul></td>
</tr>
<tr>
<td>檢閱</td>
<td><ul><li>根據探索，執行工作量估計和資源配置練習</li></ul></td>
</tr>
<tr>
<td>測量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立專案KPI</a>、成功標準和專案時間表</li></ul></td>
</tr>
</table>

>[!NOTE]
>最佳實務分析報告提供了您原本必須手動收集和評估的資訊，有助於快速評估轉換至AEM as a Cloud Service所需的時間和成本。


<br>

### 執行

在開始專案的執行階段之前，您應該先加入Cloud Service。 您也需要熟悉Cloud Manager。 這是將專案程式碼部署至Experience Manager Cloud Service執行個體的機制。

Cloud Manager可讓組織在雲端中自行管理Experience Manager。 它包含持續整合與持續傳遞([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=zh-Hant))架構，可讓IT團隊與實作夥伴加快自訂或更新的傳遞，而不會影響效能或安全性。

#### 內容移轉

1. [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=zh-Hant#migration) ：用於將現有內容從來源AEM執行個體（內部部署或AMS）移至目標AEM雲端服務執行個體。
1. [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant#package-manager) ：用於匯入及匯出存放庫的可變內容。


#### 重構/最佳化

| 快速入門 | 檢閱並重構程式碼 | Dispatcher評論 |
|---|---|---|
| <ul><li>[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=zh-Hant#local-development-environment-set-up)</li><li>[本機Dispatcher安裝程式](https://video.tv.adobe.com/v/30602/)</li><li>[使用SDK API jar編譯程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=zh-Hant)</li><li>[檢閱AEM Dev Guidelines](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=zh-Hant)<ul><li>背景工作與長時間執行的工作</li><li>Sling排程器</li><li>輸入資料流使用量和更多內容</li></ul></li></ul> | <ul><li>在來源環境中執行[Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=zh-Hant)。[**僅移轉**]<ul><li>專案結構化考量事項（根據[雲端原型](https://github.com/adobe/aem-project-archetype)）<ul><li>程式碼和內容的分離（可變與不可變）</li><li>[自訂索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=zh-Hant)</li><li>[自訂執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=zh-Hant)</li></ul></li></ul></li><li>檢閱並執行必要的變更</li><li>[在本機SDK上部署](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)</li><li>透過AEM SDK執行煙霧測試</li></ul> | <ul><li>檢閱[Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=zh-Hant)以進行重構</li><li>請視需要使用[Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=zh-Hant)工具。 [**僅移轉**]</li><li>可使用[Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=zh-Hant#prerequisites)進行測試</li></ul> |

>[!TIP]
> Assets客戶：使用[Asset Cloud Migration](https://github.com/adobe/aem-cloud-migration)工具檢閱和重構Assets工作流程


#### 部署/上線

1. [部署至Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=zh-Hant) Git
2. 透過[Cloud Manager品質管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=zh-Hant)執行客戶程式碼
3. [部署至開發環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=zh-Hant#debugging)
4. **僅移轉**&#x200B;使用封裝或[內容轉移工具](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)的內容轉移
5. 執行建議的測試週期（煙霧、QA等）
6. 提升至Cloud Manager生產管道
7. 煙霧測試驗證
8. 上線

<br>

### 上線後

在「上線後」階段中，您應該確保有清理暫存檔案，並回顧最佳作法以便持續開發及留下管理記錄。

>[!TIP]
>
> 提供AEM as a Cloud Service環境疑難排解工具
>
>1. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=zh-Hant)
>1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=zh-Hant)
>1. [管理記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=zh-Hant)

<br>

### 工具和資源

| 評估 | 重構 | Experience Manager現代化 | 內容移轉 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[最佳做法分析工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=zh-Hant)</li></li> | <ul><li>[整合式Experience外掛程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=zh-Hant)</li></ul> | <ul><li>[靜態範本至可編輯範本](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[設計原則組態](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[基礎元件至核心元件](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[傳統UI至觸控式UI](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hant)</li><li>[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant#contentmanagement)</li></ul> |

>[!NOTE]
>
> 如需其他說明，您可能需要：
>
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=zh-Hant)
>1. 探索[Experience Manager社群與論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=zh-Hant)
