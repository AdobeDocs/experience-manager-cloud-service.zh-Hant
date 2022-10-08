---
title: AEM與使用Commerce Integration Framework的第三方商務整合
description: 企業可能需要額外的第三方商務解決方案來支援其店面。 商務整合架構(CIF)可用於這類整合案例，以使用I/O Runtime將第三方商務解決方案連結至Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c,42dd8922-540d-4a93-9e45-b5e83dc11e16
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# AEM與使用Commerce Integration Framework的第三方商務整合 {#aem-third-party}

非Adobe Commerce解決方案的整合是CIF的常見案例。 透過整合層連線具有不同API和結構的第三方解決方案。

## 架構 {#architecture}

整體架構如下：

![AEM非Magento/第三方架構概述](../assets//AEM_nonMagento_Architecture.png)

此整合層的用途是根據Experience Manager外支援的Adobe Commerce GraphQL API和結構，對應第三方API和結構。 有了這種封裝，整合邏輯和系統可以更新，而無需更改Experience Manager內的代碼。

## 整合的解決方案需求

當Experience Manager隨選擷取資料時，就需要產品目錄的即時API。

>[!TIP]
>
>如果沒有可用的即時API，則整合應使用具有API的外部產品快取。 範例 [Magento開放原始碼](https://magento.com/products/magento-open-source).

不需要實作完整的GraphQL架構，只需架構的物件即可啟用所需的使用案例。

## 後端使用案例

CIF透過即時產品目錄存取和產品體驗管理工具，延伸Experience Manager。 這項緊密整合可讓作者在需要時使用內嵌的UI來存取商務資料，而不需離開內容內容。

必須整合產品目錄API才能解鎖這些使用案例。

## 前端使用案例

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 透過CIF支援的Adobe Commerce API擷取和交換資料。 若要重複使用元件，必須實作個別API。

效能關鍵用戶端元件的建議是直接與第三方解決方案通訊，以避免延遲。

## 開發整合 {#develop-integration}

建議您使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) （整合層）。 CIF附加元件中包含了該ID。 由於它與類似微服務的方法配合使用，因此非常適合於輕鬆整合多個解決方案。

此 [參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference) 是建置與商務解決方案整合的絕佳起點。 雖然支援GraphQL，但也可與任何其他類型的API（例如REST）整合。

如果第三方層可用（例如Mulesoft），或整合是在第三方解決方案之上建置，則不需要此整合層。

## 預先建立的連接器 {#connectors}

連接器為專案提供良好的開始。 隨附商務解決方案專用的連線和預設API對應。 這些連接器由第三方建置，而非由Adobe維護。 請連絡各合作夥伴以取得資訊。

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris)，由迪庫明建造
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)，由迪庫明建造

>[!TIP]
>
>連接器雖然有助於專案加速商務整合，但不是外掛程式。 企業商務解決方案通常需大量自訂，且需要自訂整合。 您必須熟悉商務平台、Adobe Commerce GraphQL結構和Adobe I/O Runtime。
