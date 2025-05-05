---
title: API 參考資料
description: AEM 擁有廣泛而強大的 API，可用于您的數位體驗專案。
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
feature: Developing
role: Admin, Architect, Developer
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 6%

---

# API 參考資料 {#api-reference-materials}

Adobe Experience Manager (AEM)提供許多API來開發應用程式和延伸AEM。 AEM是以數種開放原始碼技術為基礎所建置，這些技術也可供使用。

## AEM Core APIs {#core-aem-apis}

下列API是AEM的核心。

| API | 描述 |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 產品抽象概念，例如頁面、資產、工作流程等。 |
| [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobe的Open Web棧疊，提供各種基本元件（6.5 Granite資料適用於AEMaaCS） |
| [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) | Adobe Systems 雲端 UI 的視覺樣式，旨在提供使用者體驗的一致性 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>如需 Experience Manager API 的最新資訊，另請造訪「[Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)」。

## 其他的框架 {#additional-apis}

AEM 依賴於其他幾個開源 API。

| 應用程式介面 | 描述 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | 使用Java Content Repository (JCR)儲存和管理內容的網頁架構 |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 實作可擴充的高效能階層Java內容存放庫(JCR)，以作為現代世界級網站的基礎 |
| [Java 內容儲存庫](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR 2.0版的規格 |
| [Apache Felix](https://felix.apache.org) | 實作Open Services Gateway Initiative (OSGi)架構和服務平台 |

## API偏好設定准則 {#guidelines}

AEM是以下列四個主要Java API集為基礎，依偏好設定以遞減順序建置。

| 優先順序 | 應用程式介面 | 描述 |
|---|---|---|
| 1 | [Adobe Experience Manager為Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 產品抽象，如页面、資產、工作流程等。 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST和以資源為基礎的抽象，例如資源、值對應和HTTP要求。 |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 資料和內容抽象概念，例如，節點、屬性和工作階段。 |
| 4 | [Apache Felix](https://felix.apache.org/) | OSGi應用程式容器抽象概念，例如服務和(OSGi)元件。 |

如果API是由AEM提供，則偏好使用API，而非Sling、JCR和OSGi。 如果AEM不提供API，則偏好使用Sling，而非JCR和OSGi。

>[!TIP]
>
>如需這些准則的詳細資訊，請參閱檔案[瞭解Java API最佳實務](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=zh-Hant)。

## AEM傳遞與內容管理服務與API {#delivery-apis}

AEM提供可自訂的元件和內容傳送選項。

| 功能 | 描述 |
|---|---|
| [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hant) | 標準化的 Web 內容管理 （WCM） 元件，可AEM加快開發時間並降低網站的維護成本 |
| [JSON 匯出工具](/help/implementing/developing/components/json-exporter.md) | 在 JSON 數據模型格式中傳遞任何AEM頁面的內容 |
| [為元件啟用 JSON 匯出](/help/implementing/developing/components/enabling-json-exporter.md) | 根據建模器框架生成元件內容的 JSON 導出 |
| [內容片段和內容片段模型OpenAPI](/help/headless/content-fragment-openapis.md) | 內容片段和內容片段模型OpenAPI |
| [使用OpenAPI的AEM內容片段傳送](/help/headless/aem-content-fragment-delivery-with-openapi.md) | AEM Edge Delivery Services上的HTTP REST API，旨在從JSON格式的內容片段傳送結構化內容。 |
| [內容片段 GraphQL API](/help/headless/graphql-api/content-fragments.md) | 實現內容片段的高效傳遞，以在無頭 CMS 實施中JavaScript用戶端 |
|  |  |
| [Assets API](/help/assets/mac-api-assets.md) | 允許對資產執行建立 — 讀取 — 更新 — 刪除(CRUD)操作，包括二進位、中繼資料、轉譯和註解。 See AEM Assets HTTP API |
| [內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | 透過CRUD作業，直接透過HTTP API存取內容片段內容 |
| [內容片段Assets HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html?lang=zh-Hant) | 支援的HTTP資產請求的確切格式 |

>[!NOTE]
>
>請參閱[結構化內容傳遞與管理的AEM API](/help/headless/apis-headless-and-content-fragments.md)，以取得各種可用API的概觀，以及所涉及概念的比較。

## SPA專屬的API {#spa-apis}

AEM單頁應用程式(SPA)編輯器SDK架構提供特定的JavaScript API參考資料。

| API | 描述 |
|---|---|
| [元件映像](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | 為單頁面應用程式提供了一種將前端元件映射到Adobe Experience Manager資源類型（AEM元件）的方法 |
| [頁面模型管理器](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager编辑器和Adobe Experience Manager單頁面應用程式 （SPA） 編輯器之間的解釋器 |
| [React 可編輯元件](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | 提供React元件和整合層，讓您開始使用Adobe Experience Manager網站編輯器 |
| [Angular可編輯元件](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Provides the Angular components and integration layer to get you started with the Adobe Experience Manager Site Editor |

>[!TIP]
>
>如需單頁應用程式的詳細資訊，請參閱[SPA簡介和逐步說明](/help/implementing/developing/hybrid/introduction.md)。
