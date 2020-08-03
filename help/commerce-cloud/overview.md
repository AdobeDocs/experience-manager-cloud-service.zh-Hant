---
title: AEM Commerce as a Cloud Service簡介
description: AEM Commerce的新增功能：雲端服務。
translation-type: tm+mt
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 0%

---


# AEM Commerce As a Cloud服務簡介 {#commerce-intro}

Experience Manager Commerce as a Cloud Services由Commerce Integration Framework(CIF)組成，這是Adobe建議的模式，可將Magento和其他協力廠商商務解決方案的商務服務與Experience Cloud整合併延伸。 這可讓Adobe客戶根據最新技術，提供非凡的個人化全通道購物體驗。

Commerce Integration Framework是Experience Manager的Cloud服務附加模組，提供一組製作工具、元件和參考店面，以加速Experience Manager雲端服務與商務解決方案之間整合的開發。

## CIF優點 {#cif-benefits}

主要好處是：

* 整合是一個抽象層，用於標準化和封裝與多個系統的整合。

* CIF支援無頭／全通道體驗：

   * 單頁應用程式和多頁應用程式
   * GraphQL端點

* CIF為定制和擴展商務服務提供了無伺服器、基於微服務的流程和業務邏輯層。

* CIF提供與Adobe解決方案（例如AEM和Magento）的現成整合

## CIF元素 {#cif-elements}

![CIF元素](/help/commerce-cloud/assets/cif-overview1.jpg)


### CIF製作工具附加元件 {#add-on-authoring-tools}

CIF附加元件可存取商務製作工具，例如產品主控台、產品與類別挑選器或產品搜尋，讓作者能夠建立包含行銷與商務內容的豐富體驗。 該附加模組還通過GraphQL管理到Magento（或替代商務系統）的後端連接。 在布建附加元件後，它會自動部署在AEM上，做為雲端服務環境。

### AEM CIF核心元件 {#aem-cif-core}

AEM CIF核心元件是伺服器端和用戶端轉譯的元件，並支援Magento GraphQL。 它們可用來建立以AEM技術為基礎的靜態、可快取且適合SEO的商務商店。

提供基本元件，在商務實作（例如產品詳細資訊、產品清單、導覽、搜尋等）中通用。 它們可以按原樣使用或擴展。

AEM [CIF核心元件與](https://github.com/adobe/aem-core-cif-components) AEM Sites核心元件類似 [](https://github.com/adobe/aem-core-wcm-components) ，但專用於商務特定使用案例。

這些元件的主要優點是：

* 這些工具在您的專案中很容易使用。
* 它們可依現狀使用，或只做極小的修改。
* 它們提供了通過GraphQL API或REST API與Magento連接的最佳實踐

提供「產品摘要」和「產品轉盤」等元件，讓AEM作者能夠在AEM中建立「體驗」頁面，並結合行銷和商務內容。 這些元件可輕鬆拖放至在AEM中建立的內容頁面，並使用CIF製作工具（例如Cloud Service中的產品或類別選擇器）連結至特定產品或類別。

所有元件都是在 [GitHub上開源的](https://github.com/adobe/aem-core-cif-components)。 如此可顯示未來變更的完整透明度，讓您輕鬆取得最新版本。 您也可以提供可整合的改善與錯誤修正的提取請求。

### AEM Venia Storefront {#aem-venia-storefront}

AEM Venia Storefront [](https://github.com/adobe/aem-cif-guides-venia) （AEM Venia Storefront店面）是現代化、可立即生產使用的參考店面，展示基本的B2C商務旅程。 它可用來啟動商務專案，並使用AEM、CIF和Magento加速專案。 它示範整合AEM和Magento的最佳範例，並說明如何使用 [AEM CIF核心元件和](https://github.com/adobe/aem-core-cif-components) AEM Sites核心元件 [](https://github.com/adobe/aem-core-wcm-components) ，並支援Adobe Commerce GraphQL端點。 此外，它還為售前人員提供參考網站，以示範AEM與Magento之間的整合。

AEM Venia Storefront是混合頁面應用程式，AEM擁有玻璃，而Magento以無頭的方式為商務後端提供支援。 店面會使用伺服器端轉換和用戶端轉換。 伺服器端演算可用來傳送靜態內容，用戶端演算則可用來傳送動態內容。

產品和型錄頁面相對靜態，並會使用AEM CIF核心元件（例如AEM中建立的一般範本上的產品詳細資訊和產品清單）在伺服器端轉譯。 這些元件通過GraphQL API從Magento獲取資料。
這些頁面會動態建立、在伺服器上轉譯、快取到AEM分派器，然後傳送至瀏覽器。
對於庫存或價格等更動態屬性，則使用用戶端元件。 客戶端元件或Web元件通過GraphQL API直接從Magento獲取資料，然後內容在瀏覽器上呈現。

#### 結帳 {#checkout}

此參考店面使用用戶端購物車元件來轉換購物車和結帳表單，以展示完整的體驗整合模式，讓您透過Magento以完全無頭的方式執行，而AEM擁有玻璃，來提供商務體驗。 建議使用所提供的抽象化付款方法。 這可讓瀏覽器用戶端直接與付款閘道提供者通訊，讓Adobe和Magento雲端都不會儲存或傳遞PCI敏感資料。

#### 帳戶管理 {#account-management}

帳戶管理由Magento負責，而參考店面則利用用戶端的React-based元件，讓AEM可針對下列功能提供體驗： 建立帳戶、登入和忘記密碼。

AEM Venia Storefront專案是開放原始碼，如需詳細資訊，請參閱 [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia)。

### AEM Project Archetype {#aem-project-archtype}

AEM Project Archetype [(](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html) AEM專案原型)可用來建立以最簡化、最佳實務為基礎的Adobe Experience Manager專案，做為您自己AEM專案的起點。 (可 [選)AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) ，可加入新產生的專案中。

### CIF延伸層 {#cif-extension}

CIF擴展層是代管複雜業務邏輯的中間層。 它可在Adobe的無伺服器平台Adobe I/O Runtime上執行。 它可讓您在微型服務層級注入商業和流程邏輯，以擴充端對端服務呼叫。 例如，商業邏輯會使用位置和通道來決定庫存策略。 例如，流程邏輯可以檢索個性化資訊。

### CIF整合層 {#cif-integration-layer}

CIF整合層用於標準化與其他商務解決方案的整合。 它可在Adobe的無伺服器平台Adobe I/O Runtime上執行，並透過將協力廠商API對應至Adobe商務API，在微型服務層級進行整合。 為協助您開始建立與AEM的協力廠商整合，我們建立了參考實作 [](https://github.com/adobe/commerce-cif-graphql-integration-reference) ，以示範如何透過Adobe Commerce API(Magento GraphQL API)整合非Magento商務後端。

## AEM Commerce整合模式 {#aem-commerce-integration}

下方顯示一些常用的AEM Commerce整合模式。

![AEM CIF整合模式](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### 整合模式1 {#integration-pattern-one}

這是我們建議的整合模式，AEM擁有整個玻璃，並透過Adobe Commerce GraphQL API整合商務服務。 此模式為AEM在各種裝置上量身打造豐富型媒體網站設計提供了完整的彈性。 這種整合模式受到CIF的支援，是現成的解決方案。


### 整合模式2 {#integration-pattern-two}

此模式描述了完全無頭的內容與商務傳送方式。 傳送完全由用戶端進行。 在此模式中，內容會透過API傳送，而HTML和商務資料則會透過GraphQL傳送。 目前CIF出廠預裝不支援這種模式。


### 整合模式3 {#integration-pattern-three}

在此模式中，Magento擁有玻璃，並內嵌AEM編寫的內容。 AEM製作的內容可透過「體驗片段」或「內容片段」傳送。 這種整合模式將需要專案工作，而且無法與CIF一起立即實施。


### 整合模式4 {#integration-pattern-four}

這是常見的整合模式，其中玻璃或表現層會在AEM和商務解決方案之間分割。 通常，Commerce解決方案會提供非行銷頁面，例如結帳和我的帳戶，而AEM則會提供行銷頁面和店面目錄體驗。 在此模式中，您需要確保在兩個系統之間正確處理購物車和使用者工作階段，以避免使用者體驗脫節。 例如，Magento會將購物車與使用者作業儲存在Cookie中，可在AEM與Magento之間共用。 這種模式需要具體項目工作，而且無法與CIF一起立即實施。
