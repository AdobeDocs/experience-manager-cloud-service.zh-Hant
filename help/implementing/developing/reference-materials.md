---
title: API參考資料
description: 具AEM有廣泛而強大的API，您可以利用這些API進行數字型驗項目。
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# API參考資料 {#api-reference-materials}

Adobe Experience Manager(AEM)為開發應用和擴展提供了許多APIAEM。 AEM建立在許多開源技術之上，這些技術也可以利用。

## 核AEM心API {#core-aem-apis}

以下API是核AEM心。

| API | 說明 |
|---|---|
| [Adobe Experience Manager as a Cloud Service ](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 產品抽象，如頁面、資產、工作流等。 |
| [花崗岩UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobe的Open Web堆棧，提供各種基本元件（請注意，6.5花崗岩材料適用於AEMaaCS） |
| [珊瑚UI](https://opensource.adobe.com/coral-spectrum/documentation/) | Adobe的雲UI視覺樣式，旨在提供用戶體驗的一致性 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## 附加框架 {#additional-apis}

AEM依賴於許多其他開源API。

| API | 說明 |
|---|---|
| [阿帕奇斯林](https://sling.apache.org/apidocs/sling11/) | 使用Java內容儲存庫(JCR)儲存和管理內容的Web框架 |
| [阿帕奇長兔橡樹](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 實現可擴展的高效能分層Java內容儲存庫(JCR)，以用作現代世界級網站的基礎 |
| [Java內容儲存庫](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR 2.0版的規範 |
| [阿帕奇費利克斯](https://felix.apache.org) | 開放服務網關倡議(OSGi)框架和服務平台的實施 |

## API首選項指導 {#guidelines}

以下AEM四個主要Java API集按首選項的降序順序構建。

| 優先順序 | API | 說明 |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service ](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 產品抽象，如頁面、資產、工作流等。 |
| 2 | [阿帕奇斯林](https://sling.apache.org/apidocs/sling11/) | REST和基於資源的抽象，如資源、值映射和HTTP請求。 |
| 3 | [阿帕奇長兔橡樹](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 資料和內容抽象，如節點、屬性和會話。 |
| 4 | [阿帕奇費利克斯](https://felix.apache.org/) | OSGi應用容器抽象，如服務和(OSGi)元件。 |

如果API是由提供AEM的，則比Sling、JCR和OSGi更好。 如AEM果不提供API，則選擇Sling而不是JCR和OSGi。

>[!TIP]
>
>有關這些指南的詳細資訊，請參閱文檔 [瞭解Java API最佳實踐。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## 交AEM付和內容管理服務和API {#delivery-apis}

提AEM供可定製的元件和內容交付選項。

| 功能 | 說明 |
|---|---|
| [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) | 標準化的Web內容管理(WCM)元件AEM，可加快網站開發時間並降低網站維護成本 |
| [JSON導出器](/help/implementing/developing/components/json-exporter.md) | 以JSON資料模型格AEM式傳遞任何頁的內容 |
| [為元件啟用JSON導出](/help/implementing/developing/components/enabling-json-exporter.md) | 基於建模器框架生成元件內容的JSON導出 |
| [資產API](/help/assets/mac-api-assets.md) | 允許對資產執行建立 — 讀取 — 更新 — 刪除(CRUD)操作，包括二進位、元資料、格式副本和注釋。 請參見AEM AssetsHTTP API |
| [內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | 通過CRUD操作直接通過HTTP API訪問內容片段內容 |
| [內容片段GraphQL API](/help/headless/graphql-api/content-fragments.md) | 在無頭CMS實現中，允許將內容片段高效地傳遞到JavaScript客戶端 |
| [內容片段資產HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | 支援的HTTP資產請求的準確格式 |

## 特SPA定API {#spa-apis}

AEM單頁應用程式(SPA)Editor SDK框架提供特定的JavaScript API引用。

| API | 說明 |
|---|---|
| [元件映射](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | 為單頁應用程式將前端元件映射到Adobe Experience Manager資源類型(元件AEM)提供方法 |
| [頁面模型管理器](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager編輯器與Adobe Experience Manager單頁應用程式(SPA)編輯器之間的解釋器 |
| [反應可編輯元件](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | 提供React元件和整合層，以便您開始使用Adobe Experience Manager網站編輯器 |
| [Angular可編輯元件](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | 提供Angular元件和整合層，以便您開始使用Adobe Experience Manager站點編輯器 |

>[!TIP]
>
>查看 [介SPA紹和漫遊](/help/implementing/developing/hybrid/introduction.md) 的子菜單。
