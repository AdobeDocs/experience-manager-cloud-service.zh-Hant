---
title: 使用商AEM務整合框架進行Magento整合
description: 而AEMMagento則使用商務整合框架(CIF)完美整合。 CIF可AEM以訪問Magento實例，並通過GraphQL與Magento通信。 此外，還可讓AEM作者使用「產品與類別挑選器」和「產品主控台」來瀏覽從Magento中隨選擷取的產品與類別資料。 此外，CIF還提供了一個現成的店面，可以加快商業項目。
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# 使用AEMCommerce Integration Framework {#aem-magento-framework}進行Magento整合

而AEMMagento則使用商務整合框架(CIF)完美整合。 CIF可AEM以訪問Magento實例，並通過GraphQL與Magento通信。 此外，還可讓AEM作者使用「產品與類別挑選器」和「產品主控台」來瀏覽從Magento中隨選擷取的產品與類別資料。 此外，CIF還提供了一個現成的店面，可以加快商業項目。

>[!NOTE]
>
>GraphQL目前用於Adobe Experience Manager()的兩個（單獨）情AEM形中作為Cloud Service:
>
>* 商AEM務會透過GraphQL從商務平台取用資料。
>* [內AEM容片段與AEMGraphQL API（以標準GraphQL為基礎的自訂實作）搭配運作，以提供結構化內容供您的應用程式使用](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## 體系結構概述{#overview}

總體架構如下：

![CIF體系結構概述](../assets/AEM_Magento_Architecture.JPG)

CIF以GraphQL支援為基礎。 與Magento之AEM間的主通信通道是Magento的[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/) API。 有不同的方式可將通訊設AEM定為Cloud Service和Magento，如需詳細資訊，請參閱[快速入門](../getting-started.md)頁面。

在CIF中，支援伺服器端和客戶端通信模式。
伺服器端API呼叫是使用內建的通用[GraphQL用戶端](https://github.com/adobe/commerce-cif-graphql-client)，並結合用於MagentoGraphQL架構的一組[產生的資料模型](https://github.com/adobe/commerce-cif-magento-graphql)來實作。 此外，還可以使用任何GQL格式的GraphQL查詢或變異。

對於使用[React](https://reactjs.org/)構建的客戶端元件，使用[Apollo Client](https://www.apollographql.com/docs/react/)。

## CIFAEM核心元件體系結構{#cif-core-components}

![AEMCIF核心元件架構](../assets/cif-component-architecture.jpg)

[CIF核心](https://github.com/adobe/aem-core-cif-components) 元件與WCM核心元件的設計模式和 [實AEM踐非常相似](https://github.com/adobe/aem-core-wcm-components)。

CIF核心元件的商業邏輯和後端通AEM訊是在Sling Models中建置的。 如果需要自訂此邏輯，以符合專案特定需求，則可使用Delegation Pattern for Sling Models。

>[!TIP]
>
>[自定義AEMCIF核心元件](../customizing/customize-cif-components.md)頁提供了如何自定義CIF核心元件的詳細示例和最佳做法。

在專案中，AEMCIF核心元件和自訂專案元件可透過Sling Context-Aware設定，輕鬆擷取與頁面相關之Magento商店的AEM設定用戶端。
