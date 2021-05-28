---
title: 移轉至Experience Manager作為Cloud Service
description: 移轉至Experience Manager作為Cloud Service
exl-id: 4d1addcf-b22d-41a3-ba5c-e5c42244e5cd
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 10%

---

# 移轉至Adobe Experience Manager作為Cloud Service {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="移轉至AEM as a Cloud Service"
>abstract="概述建議的分階段方法，將客戶從各種Experience Manager部署移轉為以Cloud Service形式Experience Manager，並協助現有客戶提供連線、連續的體驗"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="新增功能與不同之處？"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="AEM as a Cloud Service 簡介."

Adobe Experience Manager(AEM)as a Cloud Service提供重新架構的Experience Manager基礎，以容器為基礎的基礎架構、API導向的開發以及引導式DevOps程式為基礎，讓行銷人員和開發人員隨時都能領先於客戶體驗管理創新的趨勢。

Cloud Service將Adobe Experience Manager的豐富現成可用功能和擴充性與現代雲端原生架構的靈活性結合在一起，讓品牌可以應付不斷變化的消費者需求。

這個單頁機概述了建議的分階段方法，可將客戶從各種Experience Manager部署，轉變為以Cloud Service形式Experience Manager，並協助現有客戶在這個專為特定用途而打造的現代化平台上提供連線、持續的體驗，以便管理體驗。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## 開始使用Adobe Experience Manager as aCloud Service{#getting-started}

| 有什麼不同？ | 架構概述 |
|--------------------------|--------------------------|
| <ul><li>[現代建築](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant)</li><li>[資產微服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[直接存取二進位檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[程式碼與內容分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[復製作為服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=zh-Hant)</li><li>[管理控制台、群組/使用者成員資格和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[AEM Architecture簡介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[環境堆疊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[作者階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[發佈層級](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) (CI/CD)</li><li>[透過](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) Admin Console進 [行身分管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - 執行階段架構](/help/core-concepts/assets/concepts-03.png "AEM as a Cloud Service - 執行階段架構")

<br>

## Adobe Experience Manager as aCloud Service中的Developer Journey {#developer-journey}

### 開發

與Adobe Experience Manager On Premise和Managed Services解決方案相比，Adobe Experience Manager中程式碼開發的基礎Cloud Service類似。

開發人員編寫程式碼並在本機測試，接著再將程式碼推送至遠端Adobe Experience Manager作為Cloud Service環境。

請參閱實作的相關自助資源，以Experience Manager為Cloud Service，了解如何將Experience Manager自訂為Cloud Service部署。

| 本機開發設定 | 開始前須知 |
|-----------|------------|
| <ol><li>請參閱[Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)檔案以深入了解。</li><li>觀看[安裝Dispatcher SDK](https://video.tv.adobe.com/v/30601)以了解如何安裝Dispatcher SDK</li><li>觀看[設定Dispatcher SDK](https://video.tv.adobe.com/v/30602)以了解如何設定Dispatcher SDK</li><li>查看[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)檔案以深入了解</li><li>配置對Experience Manager[逐步](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)的訪問</li></ol> | <ol><li>[開發要點](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[開發准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[了解Experience Manager專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)</li><li>[Digital Foundation Blueprint](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[樣式系統](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[覆蓋](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/overlays.html?lang=en#developing)</li><li>[Experience Manager作為Cloud ServiceAPI參考](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/)</li></ol> |

>[!TIP]
> 請參閱如何在本機Experience ManagerSDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)上[開發和部署WKND的教學課程

### 部署

開發人員編寫程式碼並在本機測試，接著再將程式碼推送至遠端AEM作為Cloud Service環境。

需要Cloud Manager，這是Managed Services的選用內容傳送工具。 這是現在將程式碼部署至AEM做為Cloud Service環境的唯一機制。

請參閱自助資源，了解如何設定及部署至AEM as aCloud Service環境。

1. [配置CM管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * 生產管道
   * 僅限非生產和代碼品質的管道
2. [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [了解測試結果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **存取記錄檔**
   * [透過CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [通過Adobei/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [操作與維護](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [設定OSGI設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [備份和還原](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> 請參閱有關如何[將WKND部署到Experience Manager Cloud Service的教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/develop-wknd-tutorial.html?lang=en)

### 說明和資源

1. [除錯提示與秘訣](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (僅適用於本機SDK和Experience Manager雲端開發環境)
4. [記錄和記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM日誌](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) （構建單元測試、代碼掃描、構建映像、部署）
   * [Experience Manager Cloud Service記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpaccess)
   * 本機SDK記錄（位於host:port/crx-quickstart/logs底下）

>[!NOTE]
> 如需其他說明，您可能想要：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索[Experience Manager社群和論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## 移至Adobe Experience Manager as aCloud Service{#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="移至Adobe Experience Manager as aCloud Service"
>abstract="這個單頁機概述了建議的分階段方法，可將客戶從各種Experience Manager部署，轉變為以Cloud Service形式Experience Manager，並協助現有客戶在這個專為特定用途而打造的現代化平台上提供連線、持續的體驗，以便管理體驗。"

**Experience Manager作為Cloud Service，為Experience Manager網站和資產提供可擴充、安全且敏捷的技術基礎，讓行銷人員和IT人員專注於大規模提供具影響力的體驗。**

以Experience Manager為Cloud Service，您的團隊可專注於創新，而非規劃產品升級。 新產品功能會經過徹底測試，並持續傳送給您的團隊，以供隨時存取最新版的應用程式。

轉換至雲端服務的過程包括三個階段：「規劃」、「執行」和「上線後」。為了順利成功轉換，您應該確保有正確規劃，並遵守本指南所綜覽的最佳作法。

下圖將以插圖呈現建議您用來轉換至雲端服務的過程。

![影像](/help/move-to-cloud-service/assets/home-img1.png)

<br>

### 規劃

開始轉換至Cloud Service的過程之前，您應熟悉Experience Manager作為Cloud Service，並檢閱對其所做的重大變更，以及檢閱已取代或棄用的功能。

<table>
<tr>
<td>項目發現和評估</td>
<td><ul><li>請參閱<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">將Experience Manager顯著變更為Cloud Service</a>以了解Adobe Experience Manager作為Cloud Service與Experience Manager6.x之間的重要差異。</li><li>請參考<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">已棄用的功能</a>深入了解已標示為已棄用的功能。</li><li>[僅適用於Cloud Service遷移]評估Cloud Service就緒性：在源環境中運行<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">Best Practices Analyzer(BPA)</a> </li><li>完成對CS中重大變更和已棄用功能的評估Experience Manager</li></ul></td>
</tr>
<tr>
<td>評論</td>
<td><ul><li>基於發現，執行工作估計和資源調整練習</li></ul></td>
</tr>
<tr>
<td>測量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立專案KPI</a>、成功標準和專案時間軸</li></ul></td>
</tr>
</table>

>[!NOTE]
>「最佳實務分析器報表」可提供您原本必須手動收集和評估的資訊，以加速評估轉換為AEM作為Cloud Service所需的時間和成本。


<br>

### 執行

開始專案的「執行」階段之前，您應先上線以Cloud Service。 您也需要熟悉Cloud Manager。 這是將專案程式碼部署至Experience Manager Cloud Service例項的機制。

Cloud Manager可讓組織在雲端中自行管理Experience Manager。 它包含持續整合和持續傳送([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview))架構，可讓IT團隊和實作合作夥伴加快自訂或更新的傳送速度，而不會影響效能或安全性。

#### 內容移轉

1. [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) :用於將現有內容從來源AEM例項（內部部署或AMS）移至target AEMCloud Service例項。
2. [套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) :用於匯入和匯出存放庫的可變內容。


#### 重構/最佳化

| 快速入門 | 檢閱與重構程式碼 | Dispatcher審核 |
|---|---|---|
| <ul><li>[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[本機Dispatcher設定](https://video.tv.adobe.com/v/30602/)</li><li>[使用SDK API jar編譯程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[檢閱AEM開發准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>後台任務和長時間運行的作業</li><li>Sling排程器</li><li>輸入資料流使用情況等</li></ul></li></ul> | <ul><li>在源環境中運行[Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)。[**僅移轉**]<ul><li>專案結構考量事項（根據[雲端原型](https://github.com/adobe/aem-project-archetype)）<ul><li>程式碼和內容的分離（可變與不可變）</li><li>[自定義索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[自訂執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>檢查並執行必要的更改</li><li>[](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 在本機SDK上部署</li><li>透過AEM SDK執行煙霧測試</li></ul> | <ul><li>檢閱[Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration)以進行重構</li><li>在適當的情況下，使用[Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher)工具。 [**僅移轉**]</li><li>您可以使用[Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)進行測試</li></ul> |

>[!TIP]
> 資產客戶：使用[Asset Cloud移轉](https://github.com/adobe/aem-cloud-migration)工具檢閱及重新調整資產工作流程


#### 部署/上線

1. [部署至Cloud ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) Managerit
2. 透過[Cloud Manager品質管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)執行客戶代碼
3. [部署至開發環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**僅限**] 移轉使用套件或內 [容轉移工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)(CTT)
5. 執行建議的測試週期（煙霧、QA等）
6. 提升至Cloud Manager生產管道
7. 煙霧測試驗證
8. 上線

<br>

### 上線後

在「上線後」階段中，您應該確保有清理暫存檔案，並回顧最佳作法以便持續開發及留下管理記錄。

>[!TIP]
> 工具可用於疑難排解AEM as aCloud Service環境
>1. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [管理記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### 工具和資源

| 評估 | 重構 | Experience Manager現代化 | 內容移轉 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[Unified Experience Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[從靜態範本轉換為可編輯的範本](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[根據原則設計設定](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[從基礎元件轉換為核心元件](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[從傳統 UI 轉換為觸控式 UI](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> 如需其他說明，您可能想要：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索[Experience Manager社群和論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

