---
title: 簡介和概觀
description: 了解不同的店面選項
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: 80f1c9548b8b87dc6280e0e95988d84a8376f7ab
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---


# Content and Commerce {#content-commerce}

隨著客戶對意圖型與高效能商務體驗的期望增加，品牌面臨著在不犧牲品質的情況下更快速地提供更多內容的壓力。 有了Adobe Experience Manager，品牌可以更快地進行擴展和創新，打造沈浸式商務體驗，並捕捉更多流量和不斷增長的線上支出。

Adobe Experience Manager提供強大的工具，可建立和管理內容豐富、個人化的客戶體驗。 透過將AEM與商務解決方案(例如Adobe Commerce、Salesforce Commerce、SAP Commerce Cloud或任何其他解決方案)整合，品牌可整合內容與商務，以跨管道提供順暢的購物歷程。

## 店面方法概覽 {#overview}

AEM可以根據您的情況和偏好設定為您提供支援。 請遵循下列指引，為您挑選正確的方法：

* [使用Edge Delivery Services （建議）](#edge)
* [使用您自己的店面(headless AEM整合)](#own-storefront)
* [使用AEM CIF店面](#cif)

### 使用Edge Delivery Services （建議） {#edge}

如果您的企業想要網路上速度最快且最適合AI的店面，而您的開發人員想要一流的開發人員體驗，請使用[Edge Delivery Services。](../edge/overview.md) Edge Delivery Services符合目前與未來的所有需求。 根據我們的後端和解決方案，您有不同的選項：

#### 1.與Adobe Commerce as a Cloud Service整合 {#acaacs}

Adobe建議使用Edge Delivery和[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hant)作為您的起點。 店面附有預先與Adobe Commerce服務、API整合的展示板，並提供各種Commerce下拉式元件以快速建立店面。

適用性極佳：Adobe Commerce as a Cloud Service的一般店面體驗

#### 2.與Adobe Commerce Optimizer整合（適用於任何第三方解決方案） {#aco}

如果您想要整合現有的商務解決方案並提升目錄效能，Adobe的建議是使用[Adobe Commerce Optimizer](https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview)作為現代化的整合層。 Commerce Optimizer透過用於目錄和商品銷售的高效能SaaS服務來增強您的商務解決方案。 和Adobe Commerce as a Cloud Service一樣，[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hant)可立即與其搭配使用。

可與商業商務解決方案(例如Salesforce Commerce)整合。 請洽詢您的Adobe代表。

適用性極佳：使用現有商務解決方案提供典型的店面體驗

#### 3.自訂整合 {#custom}

如果您想要建立自訂整合，Adobe也建議使用Edge Delivery Services。 您可以從頭開始，或在Edge Delivery店面中重複使用現有JS-framework商務元件（例如交易零件）。 如此一來，您的客戶將獲得超快的購物體驗，並具備代理程式功能，同時您可以重複利用現有的投資來增加TTV。 您的起始點是預設的[Edge Delivery樣板](https://www.aem.live/developer/tutorial)。

配合良好：Edge Deliery店面的低價值

### 使用您自己的店面(Headless AEM整合) {#own-storefront}

您已有現成的店面（例如使用React JS建置），且想要使用Adobe Experience Manager進行內容管理和傳送（內容片段）、資產，以及內容內編輯（通用編輯器）。 您整合的起點是[Adobe Experience Manager as a Headless CMS簡介](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/headless/introduction)和[CIF附加元件](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/authoring/enrich-product-associated-content)。 CIF附加元件可讓您將產品資料順暢整合至AEM (在AEM UI中搜尋、瀏覽和尋找產品)，以便用於建立商務專屬體驗。

### AEM CIF店面 {#cif}

Adobe的建議與參考架構為使用Edge Delivery Services。 CIF店面及其AEM CIF核心元件現在處於維護模式，不應在新專案中使用。 如需參考，請參閱[CIF檔案。](/help/commerce-cloud/cif-storefront/introduction.md)

>[!NOTE]
>
>現有客戶若想使用新的AEM / Commerce功能，應將其網站移至Edge Delivery。 常見的模式是僅將一部分頁面移動到Edge Delivery，並以並排方式執行Edge Deliery和CIF頁面。 您也可以使用新的[AEM CIF增益集元件](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=zh-Hant)來取代Commerce元件，以運用新的Commerce功能。
