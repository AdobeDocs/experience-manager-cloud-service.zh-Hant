---
sub-product: AEM as a Cloud Service 實作
user-guide-title: AEM as a Cloud Service 實作
breadcrumb-title: 實作指南
user-guide-description: 了解如何自訂 Experience Manager as a Cloud Service 部署作業，包括開發和部署主題。
translation-type: tm+mt
source-git-commit: b927992107d7e7e4df5511a366c71449ff73ec93
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 52%

---


# 實作 {#implementing}

+ [為 AEM as a Cloud Service 實作應用程式](/help/implementing/home.md)
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
      + [UI測試](/help/implementing/cloud-manager/ui-testing.md)
   + [存取和管理記錄檔](cloud-manager/manage-logs.md)
   + [了解通知](cloud-manager/notifications.md)
+ 管理程式碼 {#managing-code}
   + [Maven 專案版本處理](cloud-manager/project-version-handling.md)
   + [存取 Git](cloud-manager/accessing-git.md)
   + [整合 Git 與 Adobe Cloud Manager](cloud-manager/integrating-with-git.md)
   + [使用多源Git儲存庫](/help/implementing/cloud-manager/working-with-multiple-source-git-repositories.md)
+ 為 AEM as a Cloud Service 開發 {#developing}
   + [AEM 專案結構](developing/introduction/aem-project-content-package-structure.md)
   + [AEM 專案存放庫結構套件](developing/introduction/repository-structure-package.md)
   + [AEM as a Cloud Service SDK](developing/introduction/aem-as-a-cloud-service-sdk.md)
   + [AEM as a Cloud Service 開發方針](developing/introduction/development-guidelines.md)
   + [記錄](developing/introduction/logging.md)
   + [配置和配置瀏覽器](developing/introduction/configurations.md)
   + [AEM技術基礎](/help/implementing/developing/introduction/aem-technologies.md)
   + [AEM as a Cloud Service API](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/index.html)
   + 完整堆疊AEM開發{#full-stack}
      + [開始開發 AEM Sites - WKND 教學課程](developing/introduction/develop-wknd-tutorial.md)
      + [AEM UI的結構](developing/introduction/ui-structure.md)
      + [Sling 速查表](developing/introduction/sling-cheatsheet.md)
      + [使用 Sling 介面卡](developing/introduction/sling-adapters.md)
      + [在 AEM as a Cloud Service 中使用 Sling Resource Merger](developing/introduction/sling-resource-merger.md)
      + [AEM as a Cloud Service 中的覆蓋](developing/introduction/overlays.md)
      + [使用用戶端程式庫](developing/introduction/clientlibs.md)
      + [頁面差異](/help/implementing/developing/introduction/page-diff.md)
      + [編輯器限制](/help/implementing/developing/introduction/editor-limitations.md)
      + [命名慣例](/help/implementing/developing/introduction/naming-conventions.md)
      + 元件和模板{#components-templates}
         + [元件概觀](developing/components/overview.md)
         + [範本](developing/components/templates.md)
         + [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)
         + [樣式系統](/help/sites-cloud/authoring/features/style-system.md)
         + [內容服務的JSON匯出器](developing/components/json-exporter.md)
         + [為元件啟用JSON匯出](developing/components/enabling-json-exporter.md)
         + [影像編輯器](developing/components/image-editor.md)
         + [裝飾標籤](developing/components/decoration-tag.md)
         + [使用隱藏條件](developing/components/hide-conditions.md)
      + [AEM標籤架構](/help/implementing/developing/introduction/tagging-framework.md)
      + [建立標籤至AEM應用程式](/help/implementing/developing/introduction/tagging-applications.md)
      + 搜尋 {#search}
         + [Query Builder API](/help/implementing/developing/introduction/query-builder-api.md)
         + [Query Builder Predicate Reference](/help/implementing/developing/introduction/query-builder-predicates.md)
         + [實作自訂謂詞評估器](/help/implementing/developing/introduction/query-builder-custom-predicate.md)
      + [自訂錯誤頁面](/help/implementing/developing/introduction/custom-error-page.md)
      + [AEM節點類型](/help/implementing/developing/introduction/node-types.md)
      + [Java API准則](/help/implementing/developing/introduction/java-api-guidelines.md)
   + Hybrid AEM Development {#hybrid}
      + [Hybrid與SPA搭配AEM](https://www.adobe.com/content/dam/www/us/en/marketing/experience-manager-sites/headless-content-management-system/pdfs/aem-hybrid-architecture-wp-1-18-19.pdf)
      + [為元件啟用JSON匯出](developing/components/enabling-json-exporter.md)
      + [SPA簡介與逐步說明](developing/hybrid/introduction.md)
      + [SPA WKND教學課程](developing/hybrid/wknd-tutorial.md)
      + [開始使用React](developing/hybrid/getting-started-react.md)
      + [開始使用Angular](developing/hybrid/getting-started-angular.md)
      + [SPA深潛](developing/hybrid/deep-dives.md)
      + [開發AEM的SPA](developing/hybrid/developing.md)
      + [SPA編輯器概述](developing/hybrid/editor-overview.md)
      + [SPA藍圖](developing/hybrid/blueprint.md)
      + [SPA頁面元件](developing/hybrid/page-component.md)
      + [動態模型到元件映射](developing/hybrid/model-to-component-mapping.md)
      + [型號路由](developing/hybrid/routing.md)
      + [啟動整合](developing/hybrid/launch-integration.md)
      + [伺服器端演算](developing/hybrid/ssr.md)
      + [SPA參考檔案](developing/hybrid/reference-materials.md)
   + 無頭體驗管理{#headless}
      + [無頭與AEM](developing/headless/introduction.md)
      + 快速入門手冊{#getting-started}
         + [建立配置](developing/headless/getting-started/create-configuration.md)
         + [建立內容片段模型](developing/headless/getting-started/create-content-model.md)
         + [建立資產資料夾](developing/headless/getting-started/create-assets-folder.md)
         + [建立內容片段](developing/headless/getting-started/create-content-fragment.md)
         + [存取和傳送內容片段](developing/headless/getting-started/create-api-request.md)
      + 內容片段 {#content-fragments}
         + [使用內容片段和GraphQL進行無頭傳送](/help/assets/content-fragments/content-fragments-graphql.md)
         + [使用內容片段](/help/assets/content-fragments/content-fragments.md)
         + [為實例啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
         + [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
         + [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)
         + [變化 - 編寫片段內容](/help/assets/content-fragments/content-fragments-variations.md)
         + [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
         + [使用關聯的內容](/help/assets/content-fragments/content-fragments-assoc-content.md)
         + [中繼資料 - 片段屬性](/help/assets/content-fragments/content-fragments-metadata.md)
         + [樹狀結構](/help/assets/content-fragments/content-fragments-structure-tree.md)
         + [預覽- JSON表示法](/help/assets/content-fragments/content-fragments-json-preview.md)
      + 傳送API {#delivery-api}
         + [內容片段REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
         + [內容片段GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)
         + [含內容片段的AEM GraphQL API —— 範例內容與查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md)
+ 開發人員工具 {#developer-tools}
   + [AEM Developer Tools for Eclipse](/help/implementing/developing/tools/eclipse.md)
   + [Content Package Maven Plugin](/help/implementing/developing/tools/maven-plugin.md)
   + [AEM Repo工具](/help/implementing/developing/tools/repo-tool.md)
   + [使用CRXDE Lite](/help/implementing/developing/tools/crxde.md)
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
+ 設定和擴充 AEM as a Cloud Service {#configuring-and-extending}
   + [擴充體驗片段](developing/extending/experience-fragments.md)
   + [自訂和擴充內容片段](developing/extending/content-fragments-customizing.md)
   + [轉譯專用內容片段設定元件](developing/extending/content-fragments-configuring-components-rendering.md)
   + [設定搜尋表單](developing/extending/search-forms.md)
   + [設定 RTF 編輯器](/help/implementing/developing/extending/rich-text-editor.md)
   + [設定 RTE 外掛程式](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md)
   + [設定 RTE 以建立可存取的網站](/help/implementing/developing/extending/rte-accessible-content.md)
+ 部署至 AEM as a Cloud Service {#deploying}
   + [部署至 AEM as a Cloud Service ](deploying/overview.md)
   + [AEM版本更新](deploying/aem-version-updates.md)
   + [為 AEM as a Cloud Service 設定 OSGi](deploying/configuring-osgi.md)
+ 作者階層 {#author-tier}
   + [存取作者階層](/help/implementing/author-tier/accessing-the-author-tier.md)
   + [保護作者階層](/help/implementing/author-tier/securing-the-author-tier.md)
+ 內容傳遞概覽 {#content-delivery}
   + [內容傳遞流程](dispatcher/overview.md)
   + [雲端中的 Dispatcher](dispatcher/disp-overview.md)
   + [AEM as a Cloud Service 中的 CDN](dispatcher/cdn.md)
   + [AEM as a Cloud Service 中的快取](dispatcher/caching.md)