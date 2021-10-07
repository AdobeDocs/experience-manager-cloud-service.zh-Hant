---
title: API參考資料
description: AEM提供廣泛而強大的API，可供您運用於數位體驗專案。
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# API參考資料 {#api-reference-materials}

Adobe Experience Manager(AEM)提供許多API來開發應用程式和擴充AEM。 AEM以多種開放原始碼技術為基礎，也可加以運用。

## AEM核心API {#core-aem-apis}

下列API是AEM的核心。

| API | 說明 |
|---|---|
| [Adobe Experience Manager as a Cloud Service ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | 產品抽象化，例如頁面、資產、工作流程等。 |
| [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobe的Open Web堆疊，提供各種基本元件（請注意，6.5 Granite材料適用於AEMaaCS） |
| [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) | Adobe的雲端UI視覺樣式，旨在提供使用者體驗的一致性 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## 其他框架 {#additional-apis}

AEM需仰賴許多其他開放原始碼API。

| API | 說明 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | 使用Java內容存放庫(JCR)來儲存及管理內容的Web架構 |
| [阿帕奇傑克拉布特橡樹](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 實作可擴充且高效能的階層式Java內容存放庫(JCR)，以作為現代世界級網站的基礎 |
| [Java內容儲存庫](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR 2.0版規範 |
| [阿帕奇費利克斯](https://felix.apache.org) | 開放服務網關計畫(OSGi)框架和服務平台的實施 |

## API偏好設定准則 {#guidelines}

AEM是以下四個主要Java API集建置，依優先順序遞減。

| 優先順序 | API | 說明 |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) | 產品抽象化，例如頁面、資產、工作流程等。 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST和資源型抽象化，例如資源、值映射和HTTP要求。 |
| 3 | [阿帕奇傑克拉布特橡樹](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 資料和內容抽象化，例如節點、屬性和工作階段。 |
| 4 | [阿帕奇費利克斯](https://felix.apache.org/) | OSGi應用程式容器抽象化，例如服務和(OSGi)元件。 |

如果AEM提供API，則偏好使用它，而非Sling、JCR和OSGi。 如果AEM未提供API，則偏好Sling，而非JCR和OSGi。

>[!TIP]
>
>如需這些准則的詳細資訊，請參閱檔案[了解Java API最佳實務。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## AEM傳送與內容管理服務與API {#delivery-apis}

AEM提供可自訂的元件和內容傳遞選項。

| 功能 | 說明 |
|---|---|
| [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) | 針對AEM的標準化網頁內容管理(WCM)元件，可縮短開發時間並降低網站的維護成本 |
| [JSON匯出工具](/help/implementing/developing/components/json-exporter.md) | 以JSON資料模型格式傳送任何AEM頁面的內容 |
| [為元件啟用JSON匯出](/help/implementing/developing/components/enabling-json-exporter.md) | 根據建模器架構產生元件內容的JSON匯出 |
| [Assets API](/help/assets/mac-api-assets.md) | 允許對資產執行建立 — 讀取 — 更新 — 刪除(CRUD)操作，包括二進位、中繼資料、轉譯和註解。 請參閱AEM Assets HTTP API |
| [內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | 透過CRUD作業直接透過HTTP API存取內容片段內容 |
| [內容片段GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) | 在無頭式CMS實作中，可讓內容片段有效傳送至JavaScript用戶端 |
| [內容片段資產HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | 支援的HTTP資產要求的確切格式 |

## SPA專用API {#spa-apis}

AEM單頁應用程式(SPA)編輯器SDK架構提供特定的JavaScript API參考。

| API | 說明 |
|---|---|
| [元件對應](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | 提供單頁應用程式將前端元件對應至Adobe Experience Manager資源類型(AEM元件)的方式 |
| [頁面模型管理員](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager編輯器與Adobe Experience Manager單頁應用程式(SPA)編輯器之間的解譯器 |
| [React可編輯的元件](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | 提供React元件和整合層，協助您開始使用Adobe Experience Manager網站編輯器 |
| [Angular可編輯的元件](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | 提供Angular元件和整合層，協助您開始使用Adobe Experience Manager網站編輯器 |

>[!TIP]
>
>如需單頁應用程式的詳細資訊，請參閱[SPA簡介和逐步說明](/help/implementing/developing/hybrid/introduction.md)。
