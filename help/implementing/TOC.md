---
sub-product: AEM 雲端服務實作
user-guide-title: AEM 雲端服務實作
breadcrumb-title: Implementing Guide
user-guide-description: Learn how to customize your Experience Manager as a Cloud Service deployment, including development and deployment topics.
translation-type: tm+mt
source-git-commit: fa7d271a047277afe0a4bad709d1223224c92fb8
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 65%

---


# 實作 {#implementing}

+ [為 AEM 雲端服務實作應用程式](/help/implementing/home.md)
+ 使用 Cloud Manager {#using-cloud-manager}
   + [管理環境](cloud-manager/manage-environments.md)
   + [設定 CI/CD 管道](cloud-manager/configure-pipeline.md)
   + [部署程式碼](cloud-manager/deploy-code.md)
   + 了解測試結果 {#test-results}
      + [概覽](/help/implementing/cloud-manager/overview-test-results.md)
      + [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)
      + [自訂程式碼品質規則](cloud-manager/custom-code-quality-rules.md)
      + [功能測試](/help/implementing/cloud-manager/functional-testing.md)
      + [體驗審核測試](/help/implementing/cloud-manager/experience-audit-testing.md)
   + [存取和管理記錄檔](cloud-manager/manage-logs.md)
   + [了解通知](cloud-manager/notifications.md)
+ 管理程式碼 {#managing-code}
   + [Maven 專案版本處理](cloud-manager/project-version-handling.md)
   + [存取 Git](cloud-manager/accessing-git.md)
   + [整合 Git 與 Adobe Cloud Manager](cloud-manager/integrating-with-git.md)
+ 為 AEM 雲端服務開發 {#developing}
   + [AEM 專案結構](developing/introduction/aem-project-content-package-structure.md)
   + [AEM 專案存放庫結構套件](developing/introduction/repository-structure-package.md)
   + [AEM 雲端服務 SDK](developing/introduction/aem-as-a-cloud-service-sdk.md)
   + [AEM 雲端服務開發方針](developing/introduction/development-guidelines.md)
   + [開始開發 AEM Sites - WKND 教學課程](developing/introduction/develop-wknd-tutorial.md)
   + [AEM UI的結構](developing/introduction/ui-structure.md)
   + [Sling 速查表](developing/introduction/sling-cheatsheet.md)
   + [使用 Sling 介面卡](developing/introduction/sling-adapters.md)
   + [在 AEM 雲端服務中使用 Sling Resource Merger](developing/introduction/sling-resource-merger.md)
   + [AEM 雲端服務中的覆蓋](developing/introduction/overlays.md)
   + [記錄](developing/introduction/logging.md)
   + [AEM 雲端服務 API](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/index.html)
   + [頁面差異](/help/implementing/developing/introduction/page-diff.md)
   + [編輯器限制](/help/implementing/developing/introduction/editor-limitations.md)
   + [命名慣例](/help/implementing/developing/introduction/naming-conventions.md)
+ 元件與範本 {#components-templates}
   + [元件概觀](developing/components/overview.md)
   + [範本](developing/components/templates.md)
   + [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)
   + [樣式系統](/help/sites-cloud/authoring/features/style-system.md)
   + [內容服務的JSON匯出器](developing/components/json-exporter.md)
   + [為元件啟用JSON匯出](developing/components/enabling-json-exporter.md)
   + [影像編輯器](developing/components/image-editor.md)
   + [裝飾標籤](developing/components/decoration-tag.md)
   + [使用隱藏條件](developing/components/hide-conditions.md)
+ 無頭體驗管理 {#headless}
   + [無頭與AEM混合](https://www.adobe.com/content/dam/www/us/en/marketing/experience-manager-sites/headless-content-management-system/pdfs/aem-hybrid-architecture-wp-1-18-19.pdf)
   + [為元件啟用JSON匯出](developing/components/enabling-json-exporter.md)
   + 單頁應用程式 {#spa}
      + [SPA簡介與逐步說明](developing/spa/introduction.md)
      + [SPA WKND教學課程](developing/spa/wknd-tutorial.md)
      + [開始使用React](developing/spa/getting-started-react.md)
      + [開始使用Angular](developing/spa/getting-started-angular.md)
      + [SPA深潛](developing/spa/deep-dives.md)
      + [開發AEM的SPA](developing/spa/developing.md)
      + [SPA編輯器概述](developing/spa/editor-overview.md)
      + [SPA藍圖](developing/spa/blueprint.md)
      + [SPA頁面元件](developing/spa/page-component.md)
      + [動態模型到元件映射](developing/spa/model-to-component-mapping.md)
      + [型號路由](developing/spa/routing.md)
      + [啟動整合](developing/spa/launch-integration.md)
      + [伺服器端演算](developing/spa/ssr.md)
      + [SPA參考檔案](developing/spa/reference-materials.md)
+ 個性化 {#personalization}
   + [ContextHub](developing/personalization/contexthub.md)
   + [設定ContextHub](developing/personalization/configuring-contexthub.md)
   + [將ContextHub新增至頁面](developing/personalization/adding-contexthub.md)
   + [商店候選人範例](developing/personalization/sample-stores.md)
   + [儲存模組示例](developing/personalization/sample-modules.md)
   + [ContextHub診斷](developing/personalization/contexthub-diagnostics.md)
   + [擴充ContextHub](developing/personalization/extending-contexthub.md)
   + [ContextHub API](developing/personalization/contexthub-api.md)
   + [整合 Adobe Target](/help/sites-cloud/integrating/adobe-target.md)
   + [使用ContextHub設定區段](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
+ 設定和擴充 AEM 雲端服務 {#configuring-and-extending}
   + [擴充體驗片段](developing/extending/experience-fragments.md)
   + [自訂和擴充內容片段](developing/extending/content-fragments-customizing.md)
   + [轉譯專用內容片段設定元件](developing/extending/content-fragments-configuring-components-rendering.md)
   + [設定搜尋表單](developing/extending/search-forms.md)
   + [設定 RTF 編輯器](/help/implementing/developing/extending/rich-text-editor.md)
   + [設定 RTE 外掛程式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md)
   + [設定 RTE 以建立可存取的網站](/help/implementing/developing/extending/rte-accessible-content.md)
+ 部署至 AEM 雲端服務 {#deploying}
   + [部署至 AEM 雲端服務](deploying/overview.md)
   + [AEM版本更新](deploying/aem-version-updates.md)
   + [為 AEM 雲端服務設定 OSGi](deploying/configuring-osgi.md)
+ 作者階層 {#author-tier}
   + [存取作者階層](/help/implementing/author-tier/accessing-the-author-tier.md)
   + [保護作者階層](/help/implementing/author-tier/securing-the-author-tier.md)
+ 內容傳遞概覽 {#content-delivery}
   + [內容傳遞流程](dispatcher/overview.md)
   + [雲端中的 Dispatcher](dispatcher/disp-overview.md)
   + [AEM 雲端服務中的 CDN](dispatcher/cdn.md)
   + [AEM 雲端服務中的快取](dispatcher/caching.md)
