---
title: AEM與Adobe商務(Magento)整合（使用Commerce Integration Framework）
description: AEM和Adobe商務(Magento)可透過Commerce Integration Framework(CIF)順暢地整合。 CIF可讓AEM存取Magento執行個體，並透過GraphQL與Magento通訊。 此外，AEM作者也可使用產品和類別選擇器，以及產品主控台來瀏覽從Magento依需求擷取的產品和類別資料。 此外，CIF提供現成可加速商業項目的店面。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: b6a9b515724b0a950fc399bec0d746fe273cfd33
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# AEM與Adobe商務(Magento)整合使用Commerce Integration Framework {#aem-magento-framework}

Experience Manager與Adobe商務(Magento)可透過商務整合架構(CIF)順暢整合。 CIF可讓AEM使用Commerce的[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)直接存取和與通訊執行個體。

>[!NOTE]
>
> 最低支援的GraphQL API版本為2.3.5。某些功能僅在較新版本中或僅在Adobe商務版中受支援。

>[!NOTE]
>
>Adobe Experience Manager(AEM)中目前有兩個（個別）案例使用GraphQL作為Cloud Service:
>
>* 此情境中，CIF會透過GraphQL與商務通訊。
>* [AEM內容片段可與AEM GraphQL API（以標準GraphQL為基礎的自訂實作）搭配使用，提供結構化內容以供您的應用程式使用](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## 架構概述 {#overview}

整體架構如下：

![CIF架構概觀](../assets/AEM_Magento_Architecture.png)

CIF內支援伺服器端和用戶端通訊模式。
伺服器端API呼叫是使用內建的通用[GraphQL用戶端](https://github.com/adobe/commerce-cif-graphql-client)結合商務GraphQL架構的[一組產生的資料模型](https://github.com/adobe/commerce-cif-magento-graphql)來實作。此外，任何GQL格式的GraphQL查詢或變異都可使用。

對於使用[React](https://reactjs.org/)建立的用戶端元件，會使用[Apollo Client](https://www.apollographql.com/docs/react/)。

## AEM CIF核心元件架構 {#cif-core-components}

![AEM CIF核心元件架構](../assets/cif-component-architecture.jpg)

[AEM CIF核心元](https://github.com/adobe/aem-core-cif-components) 件遵循與AEM WCM核心元件非常類似的設計 [模式和最佳實務](https://github.com/adobe/aem-core-wcm-components)。

AEM CIF核心元件的商業邏輯和與Adobe商務的後端通訊會在Sling模型中實作。 如果您需要自訂此邏輯以符合專案特定需求，則可使用Sling模型的委派模式。

>[!TIP]
>
>[自訂AEM CIF核心元件](../customizing/customize-cif-components.md)頁面提供如何自訂CIF核心元件的詳細範例和最佳實務。

在專案中，AEM CIF核心元件和自訂專案元件可透過Sling內容感知設定，輕鬆擷取與AEM頁面相關聯的Adobe商務存放區所設定的用戶端。
