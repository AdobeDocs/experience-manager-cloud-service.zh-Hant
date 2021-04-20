---
sub-product: AEM as a Cloud Service 實作
user-guide-title: AEM as a Cloud Service 實作
breadcrumb-title: 實作指南
user-guide-description: 了解如何自訂 Experience Manager as a Cloud Service 部署作業，包括開發和部署主題。
feature-set: Experience Manager
feature: Developer Tools
role: Developer, Architect
translation-type: tm+mt
source-git-commit: cef4c40a0a4af7b3cc7cbe696ceb1a197bbef56a
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 36%

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
   + 管理SSL證書{#manage-ssl-certificates}
      + [簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
      + [取得SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)
      + [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
      + [查看、更新和替換SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
      + [檢查SSL證書的狀態](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md)
      + [刪除SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
   + 管理自定義域名{#custom-domain-names}
      + [簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
      + [取得自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/get-custom-domain-name.md)
      + [新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
      + [添加TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)
      + [檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)
      + [配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)
      + [檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md)
      + [查看、更新和替換自定義域名](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)
      + [更新自訂網域名稱的SSL憑證](/help/implementing/cloud-manager/custom-domain-names/update-cdn-ssl-certificate.md)
      + [刪除自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)
   + 管理IP允許清單{#ip-allow-lists}
      + [簡介](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)
      + [新增IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
      + [查看和更新IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
      + [套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
      + [取消應用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/unapply-ip-allow-list.md)
      + [刪除IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)
      + [檢查IP允許清單狀態](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md)
   + [Cloud Manager常見問答集](/help/implementing/cloud-manager/cloud-manager-cs-faqs.md)
+ 管理程式碼 {#managing-code}
   + [Maven 專案版本處理](cloud-manager/project-version-handling.md)
   + [存取 Git](cloud-manager/accessing-git.md)
   + [整合 Git 與 Adobe Cloud Manager](cloud-manager/integrating-with-git.md)
   + [使用多源Git儲存庫](/help/implementing/cloud-manager/working-with-multiple-source-git-repositories.md)
   + [企業團隊開發設AEM置(作為Cloud Service)](/help/implementing/cloud-manager/enterprise-team-dev-setup.md)
+ 為 AEM as a Cloud Service 開發 {#developing}
   + [AEM 專案結構](developing/introduction/aem-project-content-package-structure.md)
   + [AEM 專案存放庫結構套件](developing/introduction/repository-structure-package.md)
   + [AEM as a Cloud Service SDK](developing/introduction/aem-as-a-cloud-service-sdk.md)
   + [AEM as a Cloud Service 開發方針](developing/introduction/development-guidelines.md)
   + [記錄](developing/introduction/logging.md)
   + [配置和配置瀏覽器](developing/introduction/configurations.md)
   + [技AEM術基礎](/help/implementing/developing/introduction/aem-technologies.md)
   + [AEM as a Cloud Service API](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/ref/javadoc/index.html)
   + [產生伺服器端API的存取Token](developing/introduction/generating-access-tokens-for-server-side-apis.md)
   + [Headful and Headless in AEM](developing/headful-headless.md)
   + 完整AEM堆疊開發{#full-stack}
      + [開始開發 AEM Sites - WKND 教學課程](developing/introduction/develop-wknd-tutorial.md)
      + [UI的結AEM構](developing/introduction/ui-structure.md)
      + [Sling 速查表](developing/introduction/sling-cheatsheet.md)
      + [使用 Sling 介面卡](developing/introduction/sling-adapters.md)
      + [在 AEM as a Cloud Service 中使用 Sling Resource Merger](developing/introduction/sling-resource-merger.md)
      + [AEM as a Cloud Service 中的覆蓋](developing/introduction/overlays.md)
      + [使用用戶端端程式庫](developing/introduction/clientlibs.md)
      + [頁面差異](/help/implementing/developing/introduction/page-diff.md)
      + [編輯器限制](/help/implementing/developing/introduction/editor-limitations.md)
      + [命名慣例](/help/implementing/developing/introduction/naming-conventions.md)
      + 元件和模板{#components-templates}
         + [元件概觀](developing/components/overview.md)
         + [範本](developing/components/templates.md)
         + [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)
         + [樣式系統](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html)
         + [內容服務的JSON匯出器](developing/components/json-exporter.md)
         + [為元件啟用JSON匯出](developing/components/enabling-json-exporter.md)
         + [影像編輯器](developing/components/image-editor.md)
         + [裝飾標籤](developing/components/decoration-tag.md)
         + [使用隱藏條件](developing/components/hide-conditions.md)
         + [元件參考指南](developing/components/reference.md)
      + [標籤AEM框架](/help/implementing/developing/introduction/tagging-framework.md)
      + [在應用程式中建AEM立標籤](/help/implementing/developing/introduction/tagging-applications.md)
      + 搜尋 {#search}
         + [查詢產生器 API](/help/implementing/developing/introduction/query-builder-api.md)
         + [Query Builder Predicate Reference](/help/implementing/developing/introduction/query-builder-predicates.md)
         + [實作自訂謂詞評估器](/help/implementing/developing/introduction/query-builder-custom-predicate.md)
      + [自訂錯誤頁面](/help/implementing/developing/introduction/custom-error-page.md)
      + [節AEM點類型](/help/implementing/developing/introduction/node-types.md)
      + [Java API准則](/help/implementing/developing/introduction/java-api-guidelines.md)
   + 混AEM合開發{#hybrid}
      + [混合SPA式和AEM](https://www.adobe.com/content/dam/www/us/en/marketing/experience-manager-sites/headless-content-management-system/pdfs/aem-hybrid-architecture-wp-1-18-19.pdf)
      + [為元件啟用JSON匯出](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/components-templates/enabling-json-exporter.html)
      + [簡SPA介與逐步說明](developing/hybrid/introduction.md)
      + [WKND教SPA學課程](developing/hybrid/wknd-tutorial.md)
      + [開始使用React](developing/hybrid/getting-started-react.md)
      + [開始使用Angular](developing/hybrid/getting-started-angular.md)
      + [深SPA潛](developing/hybrid/deep-dives.md)
      + [開SPA發AEM](developing/hybrid/developing.md)
      + [編SPA輯器概述](developing/hybrid/editor-overview.md)
      + [BlueprintSPA](developing/hybrid/blueprint.md)
      + [頁SPA面元件](developing/hybrid/page-component.md)
      + [動態模型到元件映射](developing/hybrid/model-to-component-mapping.md)
      + [型號路由](developing/hybrid/routing.md)
      + [RemotePage元件](developing/hybrid/remote-page.md)
      + [在中編SPA輯外AEM部](developing/hybrid/editing-external-spa.md)
      + [複合元SPA件](developing/hybrid/composite-components.md)
      + [伺服器端演算](developing/hybrid/ssr.md)
      + [為元件啟用JSON匯出](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/components-templates/enabling-json-exporter.html)
      + [啟動整合](developing/hybrid/launch-integration.md)
      + [參SPA考檔案](developing/hybrid/reference-materials.md)
   + 無頭式體驗管理 {#headless}
      + [無頭AEM和](developing/headless/introduction.md)
      + 快速入門手冊{#getting-started}
         + [建立配置](developing/headless/getting-started/create-configuration.md)
         + [建立內容片段模型](developing/headless/getting-started/create-content-model.md)
         + [建立資產資料夾](developing/headless/getting-started/create-assets-folder.md)
         + [建立內容片段](developing/headless/getting-started/create-content-fragment.md)
         + [存取和傳送內容片段](developing/headless/getting-started/create-api-request.md)
      + 內容片段 {#content-fragments}
         + [使用內容片段和GraphQL進行無頭傳送](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-graphql.html)
         + [使用內容片段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments.html)
         + [為實例啟用內容片段功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-configuration-browser.html)
         + [內容片段模型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-models.html)
         + [管理內容片段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-managing.html)
         + [變化 - 編寫片段內容](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-variations.html)
         + [Markdown](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-markdown.html)
         + [使用關聯的內容](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-assoc-content.html)
         + [中繼資料 - 片段屬性](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-metadata.html)
         + [樹狀結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-structure-tree.html)
         + [預覽- JSON表示法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/content-fragments/content-fragments-json-preview.html)
      + 傳送API {#delivery-api}
         + [內容片段REST API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/assets-api-content-fragments.html)
         + [內容片段GraphQL API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html)
         + [含內AEM容片段的GraphQL API —— 內容與查詢範例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/content-fragments-graphql-samples.html)
         + [內容片段的AEM遠程GraphQL查詢驗證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-authentication-content-fragments.html)
+ 開發人員工具 {#developer-tools}
   + [EclipseAEM的開發人員工具](/help/implementing/developing/tools/eclipse.md)
   + [Content Package Maven Plugin](/help/implementing/developing/tools/maven-plugin.md)
   + [AEM Repo Tool](/help/implementing/developing/tools/repo-tool.md)
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
   + [使用ContextHub設定區段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/personalization/contexthub-segmentation.html)
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