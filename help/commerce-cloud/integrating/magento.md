---
title: 利用AEMCommerce Integration Framework實現Adobe商務(Magento)整合
description: 以AEM及Adobe商務(Magento)使用商務整合框架(CIF)完美整合。 CIF可AEM以訪問Magento實例，並通過GraphQL與Magento通信。 此外，還可讓AEM作者使用「產品與類別挑選器」和「產品主控台」來瀏覽從Magento中隨選擷取的產品與類別資料。 此外，CIF還提供了一個現成的店面，可以加快商業項目。
thumbnail: aem-magento-architecture.jpg
exl-id: 1cdfda88-a728-432f-b24a-f81347572bcf
translation-type: tm+mt
source-git-commit: a4e53fdcb33eab8afabcb13d651155cd247bda1f
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# 使用AEMCommerce Integration Framework {#aem-magento-framework}的Adobe商務(Magento)整合

Experience Manager和Adobe商務(Magento)使用商務整合框架(CIF)無縫整合。 CIF使AEM用Adobe商務的[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)直接訪問並與通用實例通信。

>[!NOTE]
>
>GraphQL目前用於Adobe Experience Manager()的兩個（單獨）情AEM形中作為Cloud Service:
>
>* 在這種情況下，CIF通過GraphQL與商務進行通信。
>* [內AEM容片段與AEMGraphQL API（以標準GraphQL為基礎的自訂實作）搭配運作，以提供結構化內容供您的應用程式使用](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## 體系結構概述{#overview}

總體架構如下：

![CIF體系結構概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支援伺服器端和客戶端通信模式。
伺服器端API調用是使用內建的通用[GraphQL客戶端](https://github.com/adobe/commerce-cif-graphql-client)與商務GraphQL模式的[一組生成的資料模型](https://github.com/adobe/commerce-cif-magento-graphql)組合實現的。此外，可以使用任何GQL格式的GraphQL查詢或變異。

對於使用[React](https://reactjs.org/)構建的客戶端元件，使用[Apollo Client](https://www.apollographql.com/docs/react/)。

## CIFAEM核心元件體系結構{#cif-core-components}

![AEMCIF核心元件架構](../assets/cif-component-architecture.jpg)

[CIF核心組](https://github.com/adobe/aem-core-cif-components) 件遵循與WCM核心元件非常相似的設 [計AEM模式和最佳實踐](https://github.com/adobe/aem-core-wcm-components)。

CIF核心元件與Adobe商務的商AEM業邏輯及後端通訊是在Sling Models中實作。 如果需要自訂此邏輯以符合專案特定需求，則可使用Delegation Pattern for Sling Models。

>[!TIP]
>
>[自定義AEMCIF核心元件](../customizing/customize-cif-components.md)頁提供了如何自定義CIF核心元件的詳細示例和最佳做法。

在專案中，AEMCIF核心元件和自訂專案元件可透過Sling Context-Aware設定，輕鬆擷取與頁面相關之Adobe商務商店AEM的設定用戶端。
