---
title: 遷移指南，以Experience Manager合作夥伴的as a Cloud Service
description: 遷移指南，以Experience Manager合作夥伴的as a Cloud Service
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: 595eff9c259208754ac62ea27dfc6be7d74b79d3
workflow-type: tm+mt
source-wordcount: '2126'
ht-degree: 11%

---

# 《Adobe Experience Manager as a Cloud Service合作夥伴遷移指南》 {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="遷移AEM到雲服務"
>abstract="概括介紹建議的分階段方法，將客戶從各種Experience Manager部署過渡到Experience Manageras a Cloud Service，並幫助現有客戶提供連接、連續的體驗"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="什麼是新的和不同的？"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="AEM as a Cloud Service 簡介."

Adobe Experience Manager(AEM)as a Cloud Service為Experience Manager提供了重新構建的基礎，它基於基於容器的基礎架構、API驅動的開發和指導DevOps流程，使營銷人員和開發人員能夠始終領先於客戶體驗管理創新。

Cloud Service將Adobe Experience Manager豐富的現成功能和可擴充性與現代雲本地架構的靈活性結合在一起，使品牌能夠滿足不斷變化的消費者需求。

此一頁的內容概括介紹了建議的分階段方法，以將客戶從各種Experience Manager部署過渡到Experience Manageras a Cloud Service，並幫助現有客戶在這個專門構建的現代化平台上提供連接、連續的體驗，以便進行體驗管理。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

有關遷移過程的一般說明，請參閱下圖。

![影像](/help/journey-migration/assets/migration-process.png)

## Adobe Experience Manager as a Cloud Service入門 {#getting-started}

| 有什麼不同？ | 體系結構概述 |
|--------------------------|--------------------------|
| <ul><li>[現代建築](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/architecture.html)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant)</li><li>[資產微服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[直接訪問二進位檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[代碼和內容的分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[複製為服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=zh-Hant)</li><li>[管理控制台、組/用戶成員資格和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[體系結構簡AEM介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[環境堆棧](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/architecture.html)</li><li>[作者階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[發佈層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) 通過 [管理控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - 執行階段架構](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - 執行階段架構")

<br>

## 開發商Adobe Experience Manager as a Cloud Service之旅 {#developer-journey}

### 開發

在Adobe Experience Manager as a Cloud Service，代碼開發的基本要素與Adobe Experience Manager本地和Managed Services解決方案相似。

開發人員編寫代碼並在本地test，然後將代碼推送到遠程Adobe Experience Manager as a Cloud Service環境。

查看有關Experience Manageras a Cloud Service實施的自助資源，瞭解如何自定義Experience Manageras a Cloud Service部署。

| 本地開發設定 | 開始前要知道的事 |
|-----------|------------|
| <ol><li>審閱 [Adobe Experience ManagerSDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing) 文檔以瞭解詳細資訊。</li><li>監視 [安裝Dispatcher SDK](https://video.tv.adobe.com/v/30601) 瞭解如何安裝Dispatcher SDK</li><li>監視 [配置Dispatcher SDK](https://video.tv.adobe.com/v/30602) 瞭解如何配置Dispatcher SDK</li><li>審閱 [本地開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) 文檔以瞭解詳細資訊</li><li>配置對Experience Manager的訪問 [穿行](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[開發要點](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[開發指導方針](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[瞭解Experience Manager項目結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)</li><li>[數字基礎藍圖](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[樣式系統](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[覆蓋](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manageras a Cloud ServiceAPI參考](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> 請參閱有關如何 [在本地Experience ManagerSDK上開發和部署WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)

### 部署

開發人員編寫代碼並在本地test，然後將代碼推送到遠AEM程as a Cloud Service環境。

Cloud Manager是Managed Services的可選內容交付工具，是必需的。 現在，這是將代碼部署到as a Cloud Service環境的AEM唯一機制。

請參閱有關如何配置和部署到as a Cloud Service環境的自AEM助資源。

1. [配置CM管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * 生產管道
   * 僅限非生產和代碼質量管道
2. [部署代碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [瞭解您的Test結果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **訪問日誌**
   * [通過CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [通過Adobei/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [運營和維護](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [配置OSGI配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [備份和還原](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> 請參閱有關如何 [將WKND部署到Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

### 幫助和資源

1. [調試技巧和技巧](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (僅在本地SDK和Experience Manager雲開發環境中可用)
4. [日誌和日誌記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM日誌](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) （構建單元測試、代碼掃描、構建映像、部署）
   * [Experience Manager Cloud Service日誌](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpaccess)
   * 本地SDK日誌（主機：port/crx-quickstart/logs下）

>[!NOTE]
> 要獲得其他幫助，您可能希望：
>1. [聯繫Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 瀏覽 [Experience Manager社區和論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## 搬到Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="搬到Adobe Experience Manager as a Cloud Service"
>abstract="此一頁的內容概括介紹了建議的分階段方法，以將客戶從各種Experience Manager部署過渡到Experience Manageras a Cloud Service，並幫助現有客戶在這個專門構建的現代化平台上提供連接、連續的體驗，以便進行體驗管理。"

**Experience Manageras a Cloud Service為Experience Manager Sites和資產提供了可擴展、安全和敏捷的技術基礎，使營銷人員和IT部門能夠專注於提供大規模的有影響的體驗。**

有了Experience Manageras a Cloud Service，您的團隊可以專注於創新，而不是規劃產品升級。 新產品功能會經過徹底測試，並持續傳送給您的團隊，以供隨時存取最新版的應用程式。

轉換至雲端服務的過程包括三個階段：「規劃」、「執行」和「上線後」。為了順利成功轉換，您應該確保有正確規劃，並遵守本指南所綜覽的最佳作法。

下圖顯示了建議的向Cloud Service過渡的高級代表。

![影像](/help/journey-migration/assets/home-img1.png)

<br>

### 規劃

在開始向Cloud Service過渡之前，您應熟悉Experience Manageras a Cloud Service，並查看對其所做的顯著更改，並查看已替換或棄用的功能。

<table>
<tr>
<td>項目發現和評估</td>
<td><ul><li>請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">對Experience Manageras a Cloud Service的顯著更改</a> 瞭解Adobe Experience Manager as a Cloud Service和Experience Manager6.x的重要區別。</li><li>請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">不建議使用的功能</a> 瞭解有關標籤為不建議使用的功能和功能的詳細資訊。</li><li>[僅適用於Cloud Service遷移]評估Cloud Service就緒性：運行 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">最佳實踐分析器(BPA)</a> 源環境 </li><li>針對Experience ManagerCS中的顯著更改和不建議使用的功能完成評估</li></ul></td>
</tr>
<tr>
<td>評論</td>
<td><ul><li>基於發現、執行工作量估計和資源調配練習</li></ul></td>
</tr>
<tr>
<td>度量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立項目KPI</a>、成功標準和項目時間表</li></ul></td>
</tr>
</table>

>[!NOTE]
>「最佳做法分析器報告」通過提供本來必須手動收集和評估的資訊，加快了估計過渡到AEMas a Cloud Service所需的時間和成本的過程。


<br>

### 執行

在開始項目的「執行」階段之前，您應已掛接至Cloud Service。 您還需要熟悉雲管理器。 這是將項目代碼部署到Experience Manager Cloud Service實例的機制。

Cloud Manager使組織能夠在雲中自我管理Experience Manager。 它包括連續整合和連續交付([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview))框架，使IT團隊和實施合作夥伴能夠加快定制或更新的交付，而不會影響效能或安全性。

#### 內容移轉

1. [內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) :用於將現有內容從源實AEM例（本地或AMS）移至目標AEM Cloud Service實例。
2. [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) :用於導入和導出儲存庫的可變內容。


#### 重構/優化

| 快速入門 | 審閱和重構代碼 | Dispatcher Review（Dispatcher審查） |
|---|---|---|
| <ul><li>[本地開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[本地調度程式設定](https://video.tv.adobe.com/v/30602/)</li><li>[使用SDK APIjar編譯代碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[查看開發AEM指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>後台任務和長時間運行的作業</li><li>Sling調度程式</li><li>輸入流使用率及更多</li></ul></li></ul> | <ul><li>運行 [最佳實踐分析器(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) 源環境。[**僅遷移**]<ul><li>項目結構考慮事項(基於 [雲原型](https://github.com/adobe/aem-project-archetype))<ul><li>代碼和內容的分離（Mutable與Immutable）</li><li>[自定義索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[自定義運行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>查看並執行必要的更改</li><li>[部署](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 在本地SDK上</li><li>通過AEMSDK執行煙霧測試</li></ul> | <ul><li>審閱 [調度程式配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration) 用於重構</li><li>利用 [調度器轉換器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher) 工具。 [**僅遷移**]</li><li>可以使用 [調度器SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> 資產客戶：使用 [資產雲遷移](https://github.com/adobe/aem-cloud-migration) 工具


#### 部署/投入使用

1. [部署到雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) 蠢
2. 通過 [Cloud Manager質量管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)
3. [部署到開發環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**僅遷移**] 使用包或 [內容傳輸工具](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. 執行建議的測試週期（煙霧、QA等）
6. 升級到Cloud Manager生產管道
7. 煙霧test驗證
8. 上線

<br>

### 上線後

在「上線後」階段中，您應該確保有清理暫存檔案，並回顧最佳作法以便持續開發及留下管理記錄。

>[!TIP]
> 工具可用於診斷AEMas a Cloud Service環境
>1. [開發人員控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [管理記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### 工具和資源

| 評估 | 重構 | Experience Manager現代化 | 內容移轉 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[最佳做法分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[統一體驗插件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[從靜態範本轉換為可編輯的範本](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[根據原則設計設定](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[從基礎元件轉換為核心元件](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[從傳統 UI 轉換為觸控式 UI](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> 要獲得其他幫助，您可能希望：
>1. [聯繫Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 瀏覽 [Experience Manager社區和論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

