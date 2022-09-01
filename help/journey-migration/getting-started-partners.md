---
title: 移轉指南以Experience Manager合作夥伴的as a Cloud Service
description: 移轉指南以Experience Manager合作夥伴的as a Cloud Service
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 9%

---

# Adobe Experience Manager as a Cloud Service合作夥伴移轉指南 {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="移轉至AEM as a Cloud Service"
>abstract="概述建議的分階段方法，將客戶從各種Experience Manager部署轉變為Experience Manageras a Cloud Service，並協助現有客戶提供連線的連續體驗"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html" text="新增功能與不同之處？"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html" text="AEM as a Cloud Service 簡介."

Adobe Experience Manager(AEM)as a Cloud Service提供重新架構的Experience Manager基礎，以容器為基礎的基礎架構、API導向的開發，以及引導式DevOps程式為基礎，讓行銷人員和開發人員可隨時領先客戶體驗管理創新的潮流。

Cloud Service將Adobe Experience Manager的豐富現成可用功能和擴充性與現代雲端原生架構的靈活性結合在一起，讓品牌可以應付不斷變化的消費者需求。

這個單頁機概述了建議的分階段方法，可將客戶從各種Experience Manager部署移轉至Experience Manageras a Cloud Service，並協助現有客戶在這個專為特定用途打造的現代化平台上提供連線、持續的體驗，以進行體驗管理。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

請參閱下圖以取得移轉歷程的一般表示法。

![影像](/help/journey-migration/assets/migration-process.png)

## 開始使用Adobe Experience Manager as a Cloud Service {#getting-started}

| 有什麼不同？ | 架構概述 |
|--------------------------|--------------------------|
| <ul><li>[現代建築](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)</li><li>[資產微服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[直接存取二進位檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=en)</li><li>[程式碼與內容分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[復製作為服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=en)</li><li>[管理控制台、群組/使用者成員資格和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[AEM Architecture簡介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[環境堆疊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[作者階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[發佈層級](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - 執行階段架構](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - 執行階段架構")

<br>

## Adobe Experience Manager as a Cloud Service中的開發人員歷程 {#developer-journey}

### 開發

與Adobe Experience Manager On Premise和Managed Services解決方案相比，Adobe Experience Manager as a Cloud Service中程式碼開發的基礎知識類似。

開發人員編寫程式碼並在本機測試，然後推送至遠端Adobe Experience Manager as a Cloud Service環境。

請參閱實作的相關自助資源，以了解如何自訂您的Experience Manageras a Cloud Service部署，以Experience Manageras a Cloud Service。

| 本機開發設定 | 開始前須知 |
|-----------|------------|
| <ol><li>檢閱 [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en) 檔案以深入了解。</li><li>Watch [安裝Dispatcher SDK](https://video.tv.adobe.com/v/30601) 了解如何安裝Dispatcher SDK</li><li>Watch [設定Dispatcher SDK](https://video.tv.adobe.com/v/30602) 了解如何設定Dispatcher SDK</li><li>檢閱 [本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) 檔案以深入了解</li><li>配置訪問Experience Manager [逐步](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[開發要點](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[開發指導方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)</li><li>[了解Experience Manager專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[Digital Foundation Blueprint](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[樣式系統](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=en)</li><li>[覆蓋](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manageras a Cloud ServiceAPI參考](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> 請參閱如何 [在本機Experience ManagerSDK上開發和部署WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

### 部署

開發人員編寫程式碼並在本機測試，然後推送至遠端AEMas a Cloud Service環境。

需要Cloud Manager，這是Managed Services的選用內容傳送工具。 這現在是將程式碼部署至AEMas a Cloud Service環境的唯一機制。

請參閱自助資源，了解如何設定及部署至AEMas a Cloud Service環境。

1. [配置CM管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=en)
   * 生產管道
   * 僅限非生產和代碼品質的管道
2. [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en)
3. [了解測試結果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en)
4. **存取記錄檔**
   * [透過CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)
   * [通過Adobei/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [操作與維護](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=en)
   * [設定OSGI設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en)
   * [備份和還原](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en)

>[!TIP]
> 請參閱如何 [部署WKND以Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

### 說明和資源

1. [除錯提示與秘訣](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en) (僅適用於本機SDK和Experience Manager雲端開發環境)
4. [記錄和記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM日誌](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) （構建單元測試，代碼掃描，構建映像，部署）
   * [Experience Manager Cloud Service記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * 本機SDK記錄（位於host:port/crx-quickstart/logs底下）

>[!NOTE]
> 如需其他說明，您可能想要：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索 [Experience Manager社群和論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## 移至Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="移至Adobe Experience Manager as a Cloud Service"
>abstract="這個單頁機概述了建議的分階段方法，可將客戶從各種Experience Manager部署移轉至Experience Manageras a Cloud Service，並協助現有客戶在這個專為特定用途打造的現代化平台上提供連線、持續的體驗，以進行體驗管理。"

**Experience Manageras a Cloud Service為Experience Manager Sites和資產提供可擴充、安全且敏捷的技術基礎，讓行銷人員和IT人員專注於大規模提供具影響力的體驗。**

有了Experience Manageras a Cloud Service，您的團隊便能專注於創新，而非規劃產品升級。 新產品功能會經過徹底測試，並持續傳送給您的團隊，讓他們隨時都能存取最新的應用程式。

轉換至雲端服務的過程包括三個階段：「規劃」、「執行」和「上線後」。為了順利成功轉換，您應該確保有正確規劃，並遵守本指南所綜覽的最佳作法。

下圖以高階方式呈現建議的轉換歷程至Cloud Service。

![影像](/help/journey-migration/assets/home-img1.png)

<br>

### 規劃

開始轉換至Cloud Service的過程之前，請熟悉Experience Manageras a Cloud Service，並檢閱對其所做的重大變更，以及檢閱已取代或棄用的功能。

<table>
<tr>
<td>項目發現和評估</td>
<td><ul><li>請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=zh-Hant">Experience Manageras a Cloud Service的重大變更</a> 了解Adobe Experience Manager as a Cloud Service和Experience Manager6.x之間的重要差異。</li><li>請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">過時的功能</a> 若要進一步了解已標示為過時的功能。</li><li>[僅適用於Cloud Service遷移]評估Cloud Service就緒性：執行 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">Best Practices Analyzer(BPA)</a> 源環境 </li><li>完成對CS中重大變更和已棄用功能的評估Experience Manager</li></ul></td>
</tr>
<tr>
<td>評論</td>
<td><ul><li>基於發現，執行工作估計和資源調整練習</li></ul></td>
</tr>
<tr>
<td>測量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立項目KPI</a>、成功標準和專案時間表</li></ul></td>
</tr>
</table>

>[!NOTE]
>最佳實務分析器報表可提供原本必須手動收集和評估的資訊，以加速評估轉換為AEMas a Cloud Service所需的時間和成本。


<br>

### 執行

開始專案的「執行」階段之前，您應先上線以Cloud Service。 您也需要熟悉Cloud Manager。 這是將專案程式碼部署至Experience Manager Cloud Service例項的機制。

Cloud Manager可讓組織在雲端中自行管理Experience Manager。 它包含持續整合和持續傳送([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=en))架構，讓IT團隊和實作合作夥伴可加速提供自訂或更新，而不會影響效能或安全性。

#### 內容移轉

1. [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) :用於將現有內容從來源AEM例項（內部部署或AMS）移至目標AEM Cloud Service例項。
2. [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) :用於匯入和匯出存放庫的可變內容。


#### 重構/最佳化

| 快速入門 | 檢閱與重構程式碼 | Dispatcher審核 |
|---|---|---|
| <ul><li>[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[本機Dispatcher設定](https://video.tv.adobe.com/v/30602/)</li><li>[使用SDK API jar編譯程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[檢閱AEM開發准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)<ul><li>後台任務和長時間運行的作業</li><li>Sling排程器</li><li>輸入資料流使用情況等</li></ul></li></ul> | <ul><li>執行 [Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) 源環境中。[**僅移轉**]<ul><li>專案結構考量事項(根據 [雲端原型](https://github.com/adobe/aem-project-archetype))<ul><li>程式碼和內容的分離（可變與不可變）</li><li>[自定義索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en)</li><li>[自訂執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en)</li></ul></li></ul></li><li>檢查並執行必要的更改</li><li>[部署](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 在本機SDK上</li><li>透過AEM SDK執行煙霧測試</li></ul> | <ul><li>檢閱 [Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en) 重構</li><li>使用 [Dispatcher轉換工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en) 工具。 [**僅移轉**]</li><li>可使用 [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> 資產客戶：使用 [Asset Cloud移轉](https://github.com/adobe/aem-cloud-migration) 工具


#### 部署/上線

1. [部署至Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=en) git
2. 透過 [Cloud Manager品質管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=en)
3. [部署至開發環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**僅移轉**] 使用套件或 [內容轉移工具](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. 執行建議的測試週期（煙霧、QA等）
6. 提升至Cloud Manager生產管道
7. 煙霧測試驗證
8. 上線

<br>

### 上線後

在「上線後」階段中，您應該確保有清理暫存檔案，並回顧最佳作法以便持續開發及留下管理記錄。

>[!TIP]
> 工具可用於疑難排解AEMas a Cloud Service環境
>1. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en)
>3. [管理記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)


<br>

### 工具和資源

| 評估 | 重構 | Experience Manager現代化 | 內容移轉 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en)</li></li> | <ul><li>[Unified Experience Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=en)</li></ul> | <ul><li>[從靜態範本轉換為可編輯的範本](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[根據原則設計設定](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[從基礎元件轉換為核心元件](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[從傳統 UI 轉換為觸控式 UI](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en)</li><li>[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> 如需其他說明，您可能想要：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索 [Experience Manager社群和論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

