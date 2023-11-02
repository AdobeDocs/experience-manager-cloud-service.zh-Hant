---
title: Experience Manager as a Cloud Service 合作夥伴移轉指南
description: Experience Manager as a Cloud Service 合作夥伴移轉指南
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 22%

---

# Adobe Experience Manager as a Cloud Service 合作夥伴移轉指南 {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="移轉至 AEM as a Cloud Service"
>abstract="概述建議的分階段方法，將客戶從各種 Experience Manager 部署轉變到 Experience Manager as a Cloud Service，並協助現有客戶實現連線而持續的體驗"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=zh-Hant" text="有哪些新增的不同功能？"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html?lang=zh-Hant" text="AEM as a Cloud Service 簡介."

Adobe Experience Manager (AEM) as a Cloud Service以容器式基礎架構、API導向式開發和引導式DevOps流程為基礎，提供重新架構的Experience Manager基礎，讓行銷人員和開發人員在客戶體驗管理創新中永遠保持領先。

Cloud Service結合了Adobe Experience Manager豐富的現成可用功能及擴充性，以及現代雲端原生架構的靈活性，讓品牌能夠滿足不斷變化的消費者需求。

此單一頁面會概述建議的分階段方法，以用於將客戶從各種 Experience Manager 部署轉變到 Experience Manager as a Cloud Service，並協助現有客戶在此專門建置的新式體驗管理平台上實現連線而持續的體驗。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

請參閱下圖，以取得移轉歷程的一般表示法。

![影像](/help/journey-migration/assets/migration-process.png)

## Adobe Experience Manager as a Cloud Service快速入門 {#getting-started}

| 有什麼不同？ | 架構概述 |
|--------------------------|--------------------------|
| <ul><li>[現代架構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)</li><li>[資產微服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[直接存取二進位檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=en)</li><li>[程式碼和內容的分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[復寫即服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=zh-Hant)</li><li>[Admin Console、群組/使用者成員資格和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[AEM架構簡介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[環境棧疊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[作者階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[發佈階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hant) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - 執行階段架構](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - 執行階段架構")

<br>

## Adobe Experience Manager as a Cloud Service中的開發人員歷程 {#developer-journey}

### 開發

相較於Adobe Experience Manager內部部署和Adobe Experience Manager as a Cloud Service解決方案，Managed Services中的程式碼開發基礎很類似。

開發人員撰寫程式碼並在本機進行測試，然後推送至遠端Adobe Experience Manager as a Cloud Service環境。

請參閱有關Experience Manageras a Cloud Service實作的自助資源，以瞭解如何自訂Experience Manageras a Cloud Service部署。

| 本機開發設定 | 開始前須知 |
|-----------|------------|
| <ol><li>檢閱 [ADOBE EXPERIENCE MANAGER SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en) 檔案以深入瞭解。</li><li>觀看 [安裝Dispatcher SDK](https://video.tv.adobe.com/v/30601) 瞭解如何安裝Dispatcher SDK</li><li>觀看 [設定Dispatcher SDK](https://video.tv.adobe.com/v/30602) 瞭解如何設定Dispatcher SDK</li><li>檢閱 [本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) 深入瞭解的檔案</li><li>設定Experience Manager的存取權 [逐步說明](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Development Essentials](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[開發指導方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)</li><li>[瞭解Experience Manager專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[Digital Foundation藍圖](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[樣式系統](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=en)</li><li>[覆蓋](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manageras a Cloud ServiceAPI參考](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> 請參閱教學課程，瞭解如何 [在本機Experience ManagerSDK上開發和部署WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)

### 部署

開發人員編寫程式碼並在本機進行測試，然後將程式碼推送到遠端 AEM as a Cloud Service 環境。

需要有 Cloud Manager，這是 Managed Services 的選用內容傳遞工具。現在，這是將程式碼部署到 AEM as a Cloud Service 環境的唯一機制。

請參閱自助資源，瞭解如何設定並部署至AEMas a Cloud Service環境。

1. [設定CM管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=en)
   * 生產管道
   * 非生產和僅限程式碼品質管道
2. [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en)
3. [瞭解測試結果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en)
4. **存取記錄檔**
   * [透過CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)
   * [透過Adobei/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [操作與維護](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=en)
   * [設定OSGI設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en)
   * [備份和還原](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en)

>[!TIP]
> 請參閱教學課程，瞭解如何 [將WKND部署至Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)

### 說明和資源

1. [偵錯提示與秘訣](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en) (僅適用於本機SDK和Experience Manager雲端開發環境)
4. [記錄檔和記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) （建置單元測試、程式碼掃描、建置影像、部署）
   * [Experience Manager Cloud Service記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpcaccess)
   * 本機SDK記錄（在host：port/crx-quickstart/logs下）

>[!NOTE]
> 如需其他說明，您可能需要：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索 [Experience Manager社群和論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

<br>

## 移至 Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="移至 Adobe Experience Manager as a Cloud Service"
>abstract="此單一頁面會概述建議的分階段方法，以用於將客戶從各種 Experience Manager 部署轉變到 Experience Manager as a Cloud Service，並協助現有客戶在此專門建置的新式體驗管理平台上實現連線而持續的體驗。"

**Experience Manageras a Cloud Service為Experience Manager Sites和Assets提供可擴充、安全且敏捷的技術基礎，讓行銷和IT人員專注於實現大規模具影響力的體驗。**

透過Experience Manageras a Cloud Service，您的團隊便能專注於創新而非規劃產品升級。 新產品功能會經過徹底測試，並持續傳送給您的團隊，讓團隊可以隨時存取最先進的應用程式。

轉換至雲端服務的過程包括三個階段：「規劃」、「執行」和「上線後」。為了順利成功轉換，您應該確保有正確規劃，並遵守本指南所綜覽的最佳作法。

下圖顯示建議的Cloud Service轉換歷程的高層級表示。

![影像](/help/journey-migration/assets/home-img1.png)

<br>

### 規劃

在開始轉換至Cloud Service的過程之前，您應該先熟悉Experience Manageras a Cloud Service，並檢閱已進行的重大變更，以及已遭取代或已棄用的功能。

<table>
<tr>
<td>專案探索與評估</td>
<td><ul><li>另請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=zh-Hant">Experience Manageras a Cloud Service重大變更</a> 來瞭解Adobe Experience Manager as a Cloud Service和Experience Manager 6.x之間的重要差異。</li><li>另請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">已棄用的功能</a> 以進一步瞭解已標示為過時的功能。</li><li>[僅適用於Cloud Service移轉]評估Cloud Service整備：執行 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">Best Practices Analyzer (BPA)</a> 在來源環境中 </li><li>針對Experience Manager CS中的重大變更和已棄用功能完成評估</li></ul></td>
</tr>
<tr>
<td>評論</td>
<td><ul><li>根據探索，執行工作量估計和資源配置練習</li></ul></td>
</tr>
<tr>
<td>測量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立專案KPI</a>，成功標準和專案時間表</li></ul></td>
</tr>
</table>

>[!NOTE]
>最佳實務分析報告提供了您原本必須手動收集和評估的資訊，有助於快速評估轉換為AEMas a Cloud Service所需的時間和成本。


<br>

### 執行

在開始專案的執行階段之前，您應該先開始Cloud Service。 您也需要熟悉Cloud Manager。 這是將專案程式碼部署至Experience Manager Cloud Service例項的機制。

Cloud Manager可讓組織在雲端中自行管理Experience Manager。 其中包括持續整合與持續傳遞([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=en))架構，可讓IT團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。

#### 內容移轉

1. [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) ：用於將現有內容從來源AEM例項（內部部署或AMS）移至目標AEM Cloud Service例項。
2. [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) ：用於匯入及匯出存放庫的可變內容。


#### 重構/最佳化

| 快速入門 | 檢閱並重構程式碼 | Dispatcher評論 |
|---|---|---|
| <ul><li>[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[本機Dispatcher設定](https://video.tv.adobe.com/v/30602/)</li><li>[使用SDK API jar編譯程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[檢閱AEM開發指導方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)<ul><li>背景工作與長時間執行的工作</li><li>Sling排程器</li><li>輸入資料流使用量和更多內容</li></ul></li></ul> | <ul><li>執行 [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) 在來源環境中。[**僅限移轉**]<ul><li>專案結構化考量事項(根據 [雲端原型](https://github.com/adobe/aem-project-archetype))<ul><li>程式碼和內容的分離（可變與不可變）</li><li>[自訂索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en)</li><li>[自訂執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en)</li></ul></li></ul></li><li>檢閱並執行必要的變更</li><li>[部署](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 它位在本機SDK上</li><li>透過AEM SDK執行煙霧測試</li></ul> | <ul><li>檢閱 [Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en) 用於重構</li><li>使用 [Dispatcher轉換工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en) 工具（如果適用）。 [**僅限移轉**]</li><li>可使用進行測試 [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> 資產客戶：使用檢閱和重構資產工作流程 [資產雲端移轉](https://github.com/adobe/aem-cloud-migration) 工具


#### 部署/上線

1. [部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=en) git
2. 透過 [Cloud Manager品質管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=en)
3. [部署至開發環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**僅限移轉**] 使用封裝或進行內容轉移 [內容轉移工具](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. 執行建議的測試週期（煙霧、QA等）
6. 提升至Cloud Manager生產管道
7. 煙霧測試驗證
8. 入門

<br>

### 上線後

在「上線後」階段中，您應該確保有清理暫存檔案，並回顧最佳作法以便持續開發及留下管理記錄。

>[!TIP]
> 有工具可針對AEMas a Cloud Service環境進行疑難排解
>1. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en)
>3. [管理記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)

<br>

### 工具和資源

| 評估 | 重構 | Experience Manager現代化 | 內容移轉 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[最佳做法分析工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en)</li></li> | <ul><li>[統一的Experience外掛程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=en)</li></ul> | <ul><li>[從靜態範本轉換為可編輯的範本](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[根據原則設計設定](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[從基礎元件轉換為核心元件](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[從傳統 UI 轉換為觸控式 UI](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en)</li><li>[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> 如需其他說明，您可能需要：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索 [Experience Manager社群和論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)
