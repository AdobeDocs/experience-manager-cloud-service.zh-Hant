---
title: API 參考資料
description: AEM具有廣泛而強大的API，您可用於數位體驗專案。
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: 3434d51c9b0bad02b0c3f0836341f671c9405182
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 4%

---

# API 參考資料 {#api-reference-materials}

Adobe Experience Manager (AEM)提供許多API來開發應用程式和擴充AEM。 AEM是以數種開放原始碼技術為基礎所建置，這些技術也可供使用。

## AEM Core API {#core-aem-apis}

下列API是AEM的核心。

| API | 說明 |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 產品抽象概念，例如頁面、資產、工作流程等。 |
| [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobe的Open Web棧疊，提供各種基本元件（6.5 Granite資料適用於AEMaaCS） |
| [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) | 適用於雲端UI的Adobe視覺樣式，旨在提供一致的使用者體驗 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>如需Experience Manager API的最新資訊，請造訪 [ADOBE EXPERIENCE MANAGER AS A CLOUD SERVICE API](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

## 其他的框架 {#additional-apis}

AEM需仰賴數個其他開放原始碼API。

| API | 說明 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | 使用Java Content Repository (JCR)儲存和管理內容的網頁架構 |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 實作可擴充的高效能階層Java內容存放庫(JCR)，以作為現代世界級網站的基礎 |
| [Java內容存放庫](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR 2.0版的規格 |
| [Apache Felix](https://felix.apache.org) | 實作Open Services Gateway Initiative (OSGi)架構和服務平台 |

## API偏好設定准則 {#guidelines}

AEM是以下列四個主要Java API集為基礎，依偏好設定以遞減順序建置。

| 優先順序 | API | 說明 |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 產品抽象概念，例如頁面、資產、工作流程等。 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST和以資源為基礎的抽象，例如資源、值對應和HTTP要求。 |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 資料和內容抽象概念，例如，節點、屬性和工作階段。 |
| 4 | [Apache Felix](https://felix.apache.org/) | OSGi應用程式容器抽象概念，例如服務和(OSGi)元件。 |

如果API是由AEM提供，則偏好使用API，而非Sling、JCR和OSGi。 如果AEM不提供API，則偏好使用Sling而非JCR和OSGi。

>[!TIP]
>
>如需這些指引的詳細資訊，請參閱檔案 [瞭解Java API最佳實務。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## AEM傳遞與內容管理服務與API {#delivery-apis}

AEM提供可自訂的元件和內容傳送選項。

| 功能 | 說明 |
|---|---|
| [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) | 適用於AEM的標準化網站內容管理(WCM)元件，可加快開發時間並降低網站的維護成本 |
| [JSON匯出工具](/help/implementing/developing/components/json-exporter.md) | 以JSON資料模型格式傳遞任何AEM頁面的內容 |
| [為元件啟用 JSON 匯出](/help/implementing/developing/components/enabling-json-exporter.md) | 根據模組化工具框架產生元件內容的JSON匯出 |
| [Assets API](/help/assets/mac-api-assets.md) | 允許對資產執行建立 — 讀取 — 更新 — 刪除(CRUD)操作，包括二進位、中繼資料、轉譯和註解。 請參閱AEM Assets HTTP API |
| [內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | 透過CRUD作業，直接透過HTTP API存取內容片段內容 |
| [內容片段GraphQL API](/help/headless/graphql-api/content-fragments.md) | 在Headless CMS實作中實現將內容片段有效傳送至JavaScript使用者端 |
| [內容片段資產HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | 支援的HTTP資產請求的確切格式 |

## SPA專屬的API {#spa-apis}

AEM單頁應用程式(SPA)編輯器SDK架構提供特定的JavaScript API參考。

| API | 說明 |
|---|---|
| [元件對應](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | 提供單頁應用程式將前端元件對應至Adobe Experience Manager資源型別(AEM元件)的方法 |
| [頁面模型管理員](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager編輯器和Adobe Experience Manager單頁應用程式(SPA)編輯器之間的解譯器 |
| [React可編輯元件](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | 提供React元件和整合層，讓您開始使用Adobe Experience Manager網站編輯器 |
| [angular可編輯元件](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | 提供Angular元件和整合層，讓您開始使用Adobe Experience Manager網站編輯器 |

>[!TIP]
>
>檢視 [SPA簡介和逐步解說](/help/implementing/developing/hybrid/introduction.md) 以取得單頁應用程式的詳細資訊。
