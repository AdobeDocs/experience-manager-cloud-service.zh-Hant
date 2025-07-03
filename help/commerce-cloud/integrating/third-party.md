---
title: AEM與使用Commerce integration framework的第三方Commerce整合
description: 企業可能需要額外的協力廠商商業解決方案來強化店面。 Commerce integration framework (CIF)可用於這類整合案例，以使用I/O Runtime將協力廠商商務解決方案連線至Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# 使用 Commerce Integration Framework 的 AEM 和第三方商務整合 {#aem-third-party}

CIF的常見案例是整合非Adobe Commerce解決方案。 具有不同API和結構描述的協力廠商解決方案可透過整合層進行連線。

## 架構 {#architecture}

整體架構如下：

![AEM非Magento/協力廠商架構概述](../assets//AEM_nonMagento_Architecture.png)

此整合層的用途是將第三方API和結構描述對應至Experience Manager外部支援的Adobe Commerce GraphQL API和結構描述。 有了此封裝，整合邏輯和系統可以更新，而不需要變更Experience Manager中的程式碼。

## 整合的解決方案需求

Experience Manager會隨選擷取資料，因此需要產品目錄的即時API。

>[!TIP]
>
>如果沒有可用的即時API，則應使用具有API的外部產品快取進行整合。 範例[Adobe Commerce開啟Source](https://business.adobe.com/products/magento/open-source.html)。

不需要實作完整的GraphQL結構描述，只需要結構描述的物件即可啟用所需的使用案例。

## 後端使用案例

CIF利用即時產品目錄存取和產品體驗管理工具來擴充Experience Manager。 這項緊密整合可讓作者在需要時使用內嵌式UI存取商務資料，而不需離開內容內容。

解鎖這些使用案例需要整合產品目錄API。

## 前端使用案例

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)透過CIF支援的Adobe Commerce API擷取及交換資料。 若要重複使用元件，必須實作個別API。

對於效能關鍵使用者端元件，建議直接與協力廠商解決方案通訊，以避免延遲。

## 開發整合 {#develop-integration}

Adobe建議您將[Adobe Developer Runtime](https://developer.adobe.com/runtime/)用於整合層。 它包含在適用於第三方的CIF附加元件中。 由於採用類似微服務的方式，因此非常適合輕鬆整合多個解決方案。

[參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference)是建置與您的商務解決方案整合的絕佳起點。 雖然其支援GraphQL，但也可以與任何其他型別的API （例如REST）整合。

如果有協力廠商層可用（例如Mulesoft），或整合是在協力廠商解決方案之上建置，則不需要此整合層。

## 預先建立的聯結器 {#connectors}

聯結器是專案的良好起點。 附隨商業解決方案特定的連線和預設API對應。 這些聯結器是由第三方建置，而非由Adobe維護。 如需相關資訊，請洽詢個別合作夥伴。

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris)，由Diconium建置
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)，由Diconium建置

>[!TIP]
>
>雖然聯結器可協助專案加速商務整合，但並非隨插即用。 企業商務解決方案高度自訂，需要自訂整合。 需要精通Commerce平台、Adobe Commerce GraphQL結構描述和Adobe I/O Runtime。
