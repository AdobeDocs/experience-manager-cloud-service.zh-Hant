---
title: AEM與第三方商務整合使用Commerce Integration Framework
description: 企業可能需要額外的第三方商務解決方案來支撐其店面。 商務整合架構(CIF)可用於此類整合案例，將協力廠商商務解決方案與使用I/O Runtime的Adobe Experience Manager連結。
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# AEM與第三方商務整合使用Commerce Integration Framework {#aem-third-party}

企業可能需要額外的第三方商務解決方案來支撐其店面。 商務整合架構(CIF)可用於此類整合案例，除了Magento外，協力廠商商務解決方案也需要與AEM整合。 CIF提供加速器參考店面、AEM CIF核心元件和製作工具等元素，可與Magento現成可用。 若要整合AEM和協力廠商商務解決方案並重複使用這些CIF元素，則需要進行一些額外的開發。

## 架構 {#architecture}

總體架構如下：

![AEM非Magento/第三方架構概觀](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

AEM - Magento和AEM —— 協力廠商商務的整合架構主要不同之處，在於新增整合與資料轉換層，如上圖所示。 整合層必須裝載在Adobe的無伺服器平台Adobe I/O Runtime上。 您可以在這裡進一步瞭解Adobe I/O Runtime [](https://www.adobe.io/apis/experienceplatform/runtime.html)。

此整合層的目的是將非Magento或協力廠商的API對應至Adobe Commerce API(Magento GraphQL API)。 此對應可讓 [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 和CIF製作工具從非Magento解決方案擷取資料。 透過此方法，整合層封裝整合邏輯，並在AEM和協力廠商解決方案之間建立分離關注點。 這允許以不可知的方式使用CIF元素和各種第三方解決方案。 介紹了在項目中使用CIF元素的優 [點](/help/commerce-cloud/overview.md)。

## 開發整合 {#develop-integration}

為協助您開始建立必要的整合層，將非Magento/第三方解決方案與AEM整合，我們建立了參考實 [作](https://github.com/adobe/commerce-cif-graphql-integration-reference) ，以展示此點。 此參考可作為專案的起點。
