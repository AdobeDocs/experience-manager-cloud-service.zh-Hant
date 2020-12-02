---
title: AEM與Magento整合的商務整合框架
description: AEM和Magento可使用Commerce Integration Framework(CIF)完美整合。 CIF可讓AEM存取Magento執行個體，並透過GraphQL與Magento通訊。 此外，還可讓AEM作者使用「產品與類別選擇器」和「產品主控台」來瀏覽從Magento隨選擷取的產品與類別資料。 此外，CIF還提供了一個現成的店面，可以加快商業項目。
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# 使用Commerce Integration Framework {#aem-magento-framework}進行AEM和Magento整合

AEM和Magento可使用Commerce Integration Framework(CIF)完美整合。 CIF可讓AEM存取Magento執行個體，並透過GraphQL與Magento通訊。 此外，還可讓AEM作者使用「產品與類別選擇器」和「產品主控台」來瀏覽從Magento隨選擷取的產品與類別資料。 此外，CIF還提供了一個現成的店面，可以加快商業項目。

## 體系結構概述{#overview}

總體架構如下：

![CIF體系結構概述](../assets/AEM_Magento_Architecture.JPG)

CIF以GraphQL支援為基礎。 AEM和Magento之間的主要通訊通道是Magento的[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/) API。 AEM的雲端服務與Magento通訊有不同的設定方式，如需詳細資訊，請參閱[快速入門](../getting-started.md)頁面。

在CIF中，支援伺服器端和客戶端通信模式。
伺服器端API呼叫是使用內建的通用[GraphQL用戶端](https://github.com/adobe/commerce-cif-graphql-client)與Magento GraphQL架構的一組[產生的資料模型](https://github.com/adobe/commerce-cif-magento-graphql)組合來實作。 此外，還可以使用任何GQL格式的GraphQL查詢或變異。

對於使用[React](https://reactjs.org/)構建的客戶端元件，使用[Apollo Client](https://www.apollographql.com/docs/react/)。

## AEM CIF核心元件架構{#cif-core-components}

![AEM CIF核心元件架構](../assets/cif-component-architecture.jpg)

[AEM CIF核心元](https://github.com/adobe/aem-core-cif-components) 件與 [AEM WCM核心元件的設計模式和最佳實](https://github.com/adobe/aem-core-wcm-components)務非常相似。

在Sling Models中實作與Magento的AEM CIF Core Components商業邏輯和後端通訊。 如果需要自訂此邏輯，以符合專案特定需求，則可使用Delegation Pattern for Sling Models。

>[!TIP]
>
>[自訂AEM CIF核心元件](../customizing/customize-cif-components.md)頁面提供如何自訂CIF核心元件的詳細範例和最佳實務。

在專案中，AEM CIF Core Components和自訂專案元件可透過Sling Context-Aware設定，輕鬆擷取與AEM頁面關聯之Magento商店的設定用戶端。
