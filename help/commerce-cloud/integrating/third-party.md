---
title: 基於AEMCommerce Integration Framework的第三方商務整合
description: 企業可能需要額外的第三方商業解決方案來為其店面供電。 商務整合框架(CIF)可用於此類整合方案中，以使用I/O運行時將第三方商務解決方案連接到Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c,42dd8922-540d-4a93-9e45-b5e83dc11e16
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 2%

---

# 基於AEMCommerce Integration Framework的第三方商務整合 {#aem-third-party}

非Adobe Commerce解決辦法的一體化是CIF的常見情況。 具有不同API和架構的第三方解決方案通過整合層連接。

## 架構 {#architecture}

總體體系結構如下：

![非AEMMagento/第三方體系結構概述](../assets//AEM_nonMagento_Architecture.png)

此整合層的目的是將第三方API和架構與Experience Manager外支援的Adobe CommerceGraphQLAPI和架構進行映射。 通過這種封裝，整合邏輯和系統可以在不更改Experience Manager內代碼的情況下得到更新。

## 整合的解決方案要求

當Experience Manager按需檢索資料時，需要產品目錄的即時API。

>[!TIP]
>
>如果沒有可用的即時API，則應使用帶API的外部產品快取進行整合。 示例 [Magento開源](https://magento.com/products/magento-open-source)。

不需要實現完整的GraphQL模式，只需該模式的對象即可啟用所需的使用案例。

## 後端使用案例

CIF通過即時產品目錄訪問和產品體驗管理工具擴展了Experience Manager. 這種無縫整合使作者能夠在需要時使用嵌入的UI訪問商業資料，而不會離開內容上下文。

需要整合產品目錄API才能解鎖這些使用情形。

## 正面使用案例

[AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components) 通過CIF支援的Adobe CommerceAPI檢索和交換資料。 要重新使用元件，需要實現各個API。

效能關鍵的客戶端元件建議直接與第三方解決方案通信以避免延遲。

## 開發整合 {#develop-integration}

我們建議使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) 的上界。 列在CIF第三方的附加項中。 在與類似微服務的方法協作時，它非常適合於輕鬆整合多個解決方案。

的 [參考實現](https://github.com/adobe/commerce-cif-graphql-integration-reference) 是構建與您的商業解決方案整合的絕佳起點。 儘管它支援GraphQL，但也可以與任何其它類型的API（如REST）整合。

如果第三方層可用（例如Mulesoft）或整合在第三方解決方案之上，則不需要此整合層。

## 預構建的連接器 {#connectors}

連接器為項目提供了良好的開始。 它們附帶了特定於商業解決方案的連接和預設API映射。 這些連接器由第三方構建，不由Adobe維護。 請聯繫各合作夥伴以獲取資訊。

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris)由迪庫銨建造
* [商業工具](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)由迪庫銨建造

>[!TIP]
>
>雖然連接器有助於項目加速商業整合，但它們不是即插即用的。 企業商務解決方案通常高度定製化，需要定制整合。 需要對商業平台、Adobe CommerceGraphQL模式和Adobe I/O Runtime有充分的瞭解。
