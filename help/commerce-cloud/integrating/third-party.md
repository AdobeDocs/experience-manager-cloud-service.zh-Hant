---
title: 使用Commerce Integration Framework進行AEM和協力廠商商務整合
description: 企業可能需要額外的協力廠商商業解決方案來強化店面。 Commerce Integration Framework (CIF)可用於這類整合案例，以使用I/O Runtime將協力廠商商務解決方案連結至Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---

# 使用Commerce Integration Framework進行AEM和協力廠商商務整合 {#aem-third-party}

整合非Adobe Commerce解決方案是CIF的常見案例。 透過整合層，可連結具有不同API和結構描述的協力廠商解決方案。

## 架構 {#architecture}

整體架構如下：

![AEM非Magento/協力廠商架構概述](../assets//AEM_nonMagento_Architecture.png)

此整合層的用途是將第三方API和結構描述對應至Experience Manager外部支援的Adobe Commerce GraphQL API和結構描述。 有了此封裝，整合邏輯和系統可以更新，而不需要變更Experience Manager內的程式碼。

## 整合的解決方案需求

當Experience Manager隨選擷取資料時，需要產品目錄的即時API。

>[!TIP]
>
>如果沒有可用的即時API，則應使用具有API的外部產品快取進行整合。 範例 [Adobe Commerce Open Source](https://business.adobe.com/products/magento/open-source.html).

不需要實作完整的GraphQL結構描述，只需要結構描述的物件即可啟用所需的使用案例。

## 後端使用案例

CIF透過即時產品目錄存取和產品體驗管理工具來擴充Experience Manager。 這種緊密整合可讓作者在需要時使用內嵌UI存取商務資料，而不需離開內容內容。

需要產品目錄API的整合才能解鎖這些使用案例。

## 前端使用案例

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) 透過CIF支援的Adobe Commerce API擷取和交換資料。 若要重複使用元件，必須實作個別API。

對於效能關鍵的使用者端元件，建議直接與協力廠商解決方案通訊，以避免延遲。

## 開發整合 {#develop-integration}

Adobe建議您使用 [Adobe Developer執行階段](https://developer.adobe.com/runtime/) 用於整合層。 它包含在第三方的CIF附加元件中。 由於它搭配類似微服務的方法運作，因此非常適合輕鬆整合多個解決方案。

此 [參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference) 是建置整合至您的商務解決方案的絕佳起點。 雖然支援GraphQL，但也可以與其他型別的API （例如REST）整合。

如果有協力廠商層可用（例如Mulesoft），或整合是以協力廠商解決方案為基礎而建立，則不需要此整合層。

## 預先建立的聯結器 {#connectors}

聯結器是專案的良好起點。 附隨商業解決方案特定的連線和預設API對應。 這些聯結器是由第三方建置，而不是Adobe維護。 如需相關資訊，請洽詢相關合作夥伴。

* [SAP商務](https://github.com/diconium/commerce-cif-graphql-integration-hybris)，由Diconium建置
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)，由Diconium建置

>[!TIP]
>
>雖然聯結器可協助專案加速商務整合，但並非隨插即用。 Enterprise Commerce解決方案大量自訂，需要自訂整合。 需要具備Commerce平台、Adobe Commerce GraphQL結構描述和Adobe I/O Runtime的良好知識。
