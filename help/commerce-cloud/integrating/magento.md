---
title: 商AEM務整合框架與Adobe Commerce
description: 而AEMAdobe Commerce則利用商業整合框架(CIF)進行無縫整合。 CIF使AEM得能夠訪問Adobe Commerce實例並通過GraphQL與Adobe Commerce通信。 它還允許AEM作者使用產品和類別選擇器以及產品控制台瀏覽從Adobe Commerce按需獲取的產品和類別資料。 此外，CIF還提供了一個現成的店面，可以加快商業項目。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: e304b49b44cf871f3c47120fad7899407c573234
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 6%

---

# 利用AEM商務整合框架實現Adobe Commerce整合 {#aem-framework}

該Experience Manager和Adobe Commerce利用商業整合框架(CIF)進行無縫整合。 CIF使AEM用Adobe Commerce的 [GraphQLAPI](https://devdocs.magento.com/guides/v2.4/graphql/)。

>[!NOTE]
>
> 支援的最低GraphQLAPI版本為2.3.5。某些功能僅在較新版本或僅在Adobe Commerce版中受支援。

>[!NOTE]
>
>GraphQL 目前在 Adobe Experience Manager (AEM) as a Cloud Service 中用於兩個 (獨立) 情況：
>
>* 這種情形是CIF公司通過GraphQL與商業進行溝通。
>* [內AEM容片段與GraphQLAPIAEM(基於標準GraphQL的自定義實現)協作，以提供結構化內容供您的應用程式使用](/help/headless/graphql-api/content-fragments.md)。


## 架構概述 {#overview}

總體體系結構如下：

![CIF體系結構概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支援伺服器端和客戶端通信模式。
伺服器端API調用是使用內置的通用 [GraphQL客戶](https://github.com/adobe/commerce-cif-graphql-client) 與 [生成的資料模型集](https://github.com/adobe/commerce-cif-magento-graphql) 商業GraphQL模式。 另外，可以使用任何GQL格式的GraphQL查詢或變異。

對於客戶端元件，使用 [反應](https://reactjs.org/)，也請參見Wiki頁。 [阿波羅客戶](https://www.apollographql.com/docs/react/) 的子菜單。

## CIF核AEM心元件體系結構 {#cif-core-components}

![CIF核AEM心元件體系結構](../assets/cif-component-architecture.jpg)

[AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components) 遵循非常相似的設計模式和最佳做法 [AEMWCM核心元件](https://github.com/adobe/aem-core-wcm-components)。

CIF核心元件與Adobe Commerce的業務邏輯和後AEM端通信在Sling模型中實現。 如果需要自定義此邏輯以滿足項目特定要求，則可以使用Sling模型的委託模式。

>[!TIP]
>
>的 [自定義AEMCIF核心元件](../customizing/customize-cif-components.md) 頁面提供了有關如何自定義CIF核心元件的詳細示例和最佳實踐。

在項目中，AEM CIF核心元件和定制項目元件可以通過Sling Context-Aware配置輕鬆檢索與頁面關聯的Adobe Commerce儲存的AEM配置客戶端。
