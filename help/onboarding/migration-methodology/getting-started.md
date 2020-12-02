---
title: 將Experience Manager轉換為雲端服務的單頁機
description: 將Experience Manager轉換為雲端服務的單頁機
translation-type: tm+mt
source-git-commit: 02e6581ec5a922d71c53e99212a1f8aecc405f6f
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 8%

---


# 移轉至Adobe Experience Manager作為雲端服務{#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration-overview"
>title="將AEM移轉至雲端服務"
>abstract="概述建議的分階段方法，將客戶從各種Experience Manager部署過渡到Experience Manager，成為雲端服務，並協助現有客戶提供連通、連續的體驗"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="新增功能與不同功能？"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="AEM as a Cloud Service 簡介."

Adobe Experience Manager(AEM)作為雲端服務，為Experience Manager提供重新架構的基礎，以容器為基礎的基礎架構、API導向的開發以及引導式DevOps流程為基礎，讓行銷人員和開發人員在客戶體驗管理創新方面始終領先於潮流。

雲端服務結合了Adobe Experience Manager的豐富現成功能和擴充性，以及現代雲端原生架構的靈活性，讓品牌能夠滿足不斷變化的消費者需求。

此單頁機概述了將客戶從各種Experience Manager部署過渡到Experience Manager作為雲端服務的建議分階段方法，並幫助現有客戶在這個專為體驗管理而打造的現代化平台上提供連通、持續的體驗。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## 以雲端服務形式開始使用Adobe Experience Manager {#getting-started}

| 有什麼不同？ | 架構概觀 |
|--------------------------|--------------------------|
| <ul><li>[現代建築](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)</li><li>[Asset Microservices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[直接存取二進位檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[程式碼與內容分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[複製為服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=en)</li><li>[管理控制台、群組／使用者會籍和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[AEM架構簡介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[環境堆棧](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[作者階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[發佈層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) (CI/CD)</li><li>[身分識](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) 別管理透過 [管理控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[資產計算服務](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - 執行階段架構](/help/core-concepts/assets/concepts-03.png "AEM as a Cloud Service - 執行階段架構")

<br>

## Adobe Experience Manager雲端服務開發人員歷程{#developer-journey}

### 開發

與Adobe Experience Manager On Premise和Managed Services解決方案相比，Adobe Experience Manager的程式碼開發基礎與雲端服務類似。

開發人員可編寫程式碼並在本機進行測試，然後將程式碼推送至遠端的Adobe Experience Manager做為雲端服務環境。

檢視Experience Manager雲端服務實作的自助資源，瞭解如何將Experience Manager自訂為雲端服務部署。

| 本地開發設定 | 開始之前要知道的事 |
|-----------|------------|
| <ol><li>請檢閱[Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)檔案以瞭解詳細資訊。</li><li>觀看[安裝Dispatcher SDK](https://video.tv.adobe.com/v/30601?captions=chi_hant)以瞭解如何安裝Dispatcher SDK</li><li>觀看[配置Dispatcher SDK](https://video.tv.adobe.com/v/30602?captions=chi_hant)以瞭解如何配置Dispatcher SDK</li><li>檢閱[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)檔案，以進一步瞭解</li><li>設定對Experience Manager [逐步存取](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)的存取</li></ol> | <ol><li>[Development Essentials](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[開發指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[瞭解Experience Manager專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[數位基礎藍圖](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[樣式系統](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[覆蓋](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/overlays.html?lang=en#developing)</li><li>[Experience Manager做為雲端服務API參考](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/)</li></ol> |

>[!TIP]
> 請參閱如何[在本機Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)上開發和部署WKND的教學課程

### 部署

開發人員可編寫程式碼並在本機進行測試，然後將它推送至遠端AEM做為雲端服務環境。

Cloud Manager是Managed Services的選用內容傳送工具，是必要項。 現在，這是將程式碼部署至AEM做為雲端服務環境的唯一機制。

檢視如何將AEM設定為雲端服務環境並部署至AEM的自助資源。

1. [配置CM管線](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * 生產管線
   * 非生產和代碼純質量管道
2. [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [瞭解您的測試結果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **訪問日誌**
   * [透過CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [透過Adobe i/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [操作和維護](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [配置OSGI配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [備份和還原](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> 請參閱如何[將WKND部署至Experience Manager Cloud服務的教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/develop-wknd-tutorial.html?lang=en)

### 說明與資源

1. [除錯秘訣與訣竅](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) （僅適用於本機SDK和Experience Manager Cloud Dev環境）
4. [記錄和記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM Logs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) (build-unit-testing, code-scanning, build-image, deploy)
   * [Experience Manager Cloud服務記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpaccess)
   * 本機SDK記錄檔（位於host:port/crx-quickstart/logs下）

>[!NOTE]
> 如需其他協助，您可以：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索[Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## 以雲端服務的身分移轉至Adobe Experience Manager {#move-to-cloud}

**Experience Manager作為雲端服務，為Experience Manager Sites和Assets提供可擴充、安全且靈活的技術基礎，讓行銷人員和IT專注於大規模提供具影響力的體驗。**

有了Experience Manager作為雲端服務，您的團隊可以專注於創新，而非規劃產品升級。 新產品功能會經過徹底測試，並持續傳送給您的團隊，以供隨時存取最新版的應用程式。

轉換至雲端服務的過程包括三個階段：「規劃」、「執行」和「上線後」。為了順利成功轉換，您應該確保有正確規劃，並遵守本指南所綜覽的最佳作法。

下圖將以插圖呈現建議您用來轉換至雲端服務的過程。

![影像](/help/move-to-cloud-service/assets/home-img1.png)

<br>

### 規劃

在開始Cloud Service的過渡之前，您應先熟悉Experience Manager作為Cloud Service，並查看對Experience Manager所做的顯著變更，並查看已取代或已淘汰的功能。

<table>
<tr>
<td>項目發現和評估</td>
<td><ul><li>請參閱<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en"> Experience Manager作為雲端服務的顯著變更</a>，瞭解Adobe Experience Manager作為雲端服務與Experience Manager 6.x之間的重要差異。</li><li>請參閱<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">已過時的功能</a>以進一步瞭解已標示為已過時的功能。</li><li>[僅適用於雲服務遷移]評估雲服務就緒性：在源環境中運行<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">最佳實踐分析器(BPA)</a> </li><li>針對Experience Manager CS中顯著的變更和已過時功能完成評估</li></ul></td>
</tr>
<tr>
<td>評論</td>
<td><ul><li>基於發現、執行努力估計和資源化練習</li></ul></td>
</tr>
<tr>
<td>測量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立專案KPI</a>、成功標準和專案時間表</li></ul></td>
</tr>
</table>

>[!NOTE]
>「最佳實務分析器報告」提供必須手動收集和評估的資訊，以加速評估轉換為AEM（雲端服務）所需時間和成本的程式。


<br>

### 執行

在開始項目的「執行」階段之前，您應已登入雲端服務。 您還需要熟悉Cloud Manager。 這是將專案程式碼部署至Experience Manager Cloud服務例項的機制。

Cloud Manager可讓組織在Cloud中自行管理Experience Manager。 它包含持續整合和持續傳送([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview))架構，讓IT團隊和實施合作夥伴加速傳送自訂或更新，而不影響效能或安全性。

#### 內容移轉

1. [內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) :用於將現有內容從來源AEM例項（內部部署或AMS）移至目標AEM Cloud服務例項。
2. [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) :用於導入和導出儲存庫的可變內容。


#### 調整／最佳化

| 快速入門 | 審查與重新調整代碼 | Dispatcher Review |
|---|---|---|
| <ul><li>[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[本地調度程式設定](https://video.tv.adobe.com/v/30602/?captions=chi_hant)</li><li>[使用SDK API jar編譯程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[檢視AEM Dev准則](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>後台任務和長期運行的作業</li><li>Sling調度程式</li><li>輸入串流使用情況及更多</li></ul></li></ul> | <ul><li>在源環境中運行[最佳實踐分析器(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)。[**僅移轉**]<ul><li>專案結構考量（根據[雲端原型](https://github.com/adobe/aem-project-archetype)）<ul><li>程式碼與內容的分離（可變或不可變）</li><li>[自訂索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[自訂執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>審查並執行必要的更改</li><li>[在本](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 機SDK上部署</li><li>透過AEM SDK執行煙霧測試</li></ul> | <ul><li>查看[Dispatcher configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration)的重構功能</li><li>在適當的情況下使用[Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher)工具。 [**僅移轉**]</li><li>測試可使用[Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)進行</li></ul> |

>[!TIP]
> 資產客戶：使用[Asset Cloud移轉](https://github.com/adobe/aem-cloud-migration)工具審核和重新調整資產工作流程


#### 部署／上線

1. [部署至Cloud ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) Managerit
2. 透過[Cloud Manager Quality Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)執行客戶代碼
3. [部署至開發環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**僅移**] 轉使用套件或內容 [傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration(CTT)
5. 執行建議的測試週期（煙霧、QA等）
6. 升級至Cloud Manager生產管道
7. 煙霧測試驗證
8. 上線

<br>

### 上線貼文

在「上線後」階段中，您應該確保有清理暫存檔案，並回顧最佳作法以便持續開發及留下管理記錄。

>[!TIP]
> AEM為雲端服務環境疑難排解工具已推出
>1. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [管理記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### 工具與資源

| 評估 | 重構 | Experience Manager現代化 | 內容移轉 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[最佳實務分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[Unified Experience Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[從靜態範本轉換為可編輯的範本](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[根據原則設計設定](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[從基礎元件轉換為核心元件](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[從傳統 UI 轉換為觸控式 UI](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> 如需其他協助，您可以：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索[Experience Manager Communities &amp; Forums](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

