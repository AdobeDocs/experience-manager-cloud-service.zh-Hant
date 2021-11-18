---
title: AEM與Adobe Commerce(Magento)使用Commerce Integration Framework整合
description: AEM和Adobe Commerce(Magento)可透過Commerce Integration Framework(CIF)順暢整合。 CIF可讓AEM存取Magento執行個體，並透過GraphQL與Magento通訊。 此外，AEM作者也可使用產品和類別選擇器，以及產品主控台來瀏覽從Magento依需求擷取的產品和類別資料。 此外，CIF提供現成可加速商業項目的店面。
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: 96e7a7c38dd1275c9b0d291d12a0f768ab183c38
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# AEM與Adobe Commerce(Magento)使用Commerce Integration Framework整合 {#aem-magento-framework}

Experience Manager和Adobe Commerce(Magento)可透過商務整合架構(CIF)順暢整合。 CIF可讓AEM使用Adobe Commerce直接存取商務執行個體並與其通訊 [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> 最低支援的GraphQL API版本為2.3.5。某些功能僅在較新版本或Adobe Commerce版本中受支援。

>[!NOTE]
>
>Adobe Experience Manager(AEM)as a Cloud Service中，GraphQL目前用於兩種（個別）的情況：
>
>* 此情境中，CIF會透過GraphQL與商務通訊。
>* [AEM內容片段可與AEM GraphQL API（以標準GraphQL為基礎的自訂實作）搭配使用，提供結構化內容以供您的應用程式使用](/help/assets/content-fragments/graphql-api-content-fragments.md).


## 架構概述 {#overview}

整體架構如下：

![CIF架構概觀](../assets/AEM_Magento_Architecture.png)

CIF內支援伺服器端和用戶端通訊模式。
伺服器端API呼叫是使用內建的一般實作 [GraphQL客戶端](https://github.com/adobe/commerce-cif-graphql-client) 與 [生成的資料模型集](https://github.com/adobe/commerce-cif-magento-graphql) （商務GraphQL架構）。 此外，還可以使用GQL格式的任何GraphQL查詢或變異。

針對用戶端元件，使用 [React](https://reactjs.org/), [阿波羅客戶](https://www.apollographql.com/docs/react/) 中所有規則的URL區段。

## AEM CIF核心元件架構 {#cif-core-components}

![AEM CIF核心元件架構](../assets/cif-component-architecture.jpg)

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 遵循與 [AEM WCM核心元件](https://github.com/adobe/aem-core-wcm-components).

AEM CIF核心元件與Adobe Commerce的商業邏輯和後端通訊是在Sling模型中實作。 如果您需要自訂此邏輯以符合專案特定需求，則可使用Sling模型的委派模式。

>[!TIP]
>
>此 [自訂AEM CIF核心元件](../customizing/customize-cif-components.md) 頁面提供自訂CIF核心元件的詳細範例和最佳實務。

在專案中，AEM CIF核心元件和自訂專案元件可透過Sling內容感知設定，輕鬆擷取與AEM頁面相關聯的Adobe Commerce存放區所設定的用戶端。
