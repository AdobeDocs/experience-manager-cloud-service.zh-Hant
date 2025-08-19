---
title: 引入 AEM 商務整合框架 (CIF)
description: 瞭解如何透過CIF使用及管理Experience Manager內容和Commerce as a Cloud Service。
thumbnail: introducing-aem-commerce.jpg
feature: Commerce Integration Framework
role: Admin
exl-id: 3f18f976-ff8a-4726-b4c5-db4e19ae7cee
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 61%

---


# 引入 AEM 商務整合框架 (CIF) {#cif-intro}

商務解決方案範圍廣泛，從 Adobe Commerce Cloud 等商務解決方案到一組自訂商務服務皆是。整合在很大程度上取決於使用案例和生態系統。 它通常會影響各種系統，而且有許多不同的種類：

* 整合複雜且動態的生態系統（例如產品目錄）
* 企業必須透過自己的生命週期，以有效率且全通路的方式管理產品內容
* 為各種不同的個人建立複雜和個人化的購物歷程
* 能夠在後端和前端快速適應和創新
* 執行可擴充且穩定的E2E基礎架構，專為尖峰效能（快閃銷售、黑色星期五……）所打造，包括整合式搜尋和快取管理

這種複雜性可能為導致故障點出現、TCO 增加、延遲和價值實現降低。這些原因促使開發商務整合框架 (CIF)，它是 Experience Manager 的附加元件。CIF 擴充 Experience Manager 使其具有商務功能，並標準化與商務引擎的整合。如此一來，您便能以較低的總體擁有成本(TCO)，獲得經得起未來考驗的穩定且可擴充的解決方案。 它提供靈活的工具和無縫整合的功能，開啟技術和商業創新，以建立極具吸引力的商務體驗。

![CIF 元素](./assets/CIF/CIF_Overview.png)

## CIF 的優點 {#cif-benefits}

CIF 提供開箱即用的商務核心元件，可減少對自訂程式碼的需求，從而加快品牌的上市時間。所有核心元件都與 Adobe 的用戶端資料相整合且立即可用，以序列化客戶設定檔，例如統一的設定檔。此設定檔會詳細捕捉訪客行為，可用於即時預測和個人化客戶歷程。

CIF 附加元件將產品情境帶入 Experience Manager 並提供編寫工具 (例如產品主控台) 和產品/類別選擇器，使行銷人員不用依賴開發人員，即可在 Experience Manager 中建立和傳遞可購物的體驗。優點包括：

* [引人入勝的體驗](#experiences)
* [加速實現價值](#ttv)
* [強大的整合](#integrations)

### 體驗 {#experiences}

強大的 AEM CIF 工具可讓內容建立者以可擴展且與傳遞無關的方式，快速建立豐富及個人化的商務體驗，以利用商機。

![CIF 元素](./assets/CIF/CIF_Product_Experience_Management.png)

### 實現價值時間 (TTV) {#ttv}

CIF使用[AEM核心元件](https://www.aemcomponents.dev/)、[AEM Venia參考店面](https://github.com/adobe/aem-cif-guides-venia)、[AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)和PWA （Headless內容與商務）的整合模式來加速專案開發。

CIF是專為持續創新而打造，採用始終最新的附加元件，讓您存取最新改進的功能。

### 整合 {#integrations}

使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)、微服務式無伺服器的 PaaS 和 [CIF 的參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference)，將您的生態系統 (例如，商務解決方案) 與 Experience Cloud 相連接。

## 經驗證的模式和最佳做法 {#proven}

CIF會根據最佳實務提供標準化的整合模式來支援您。 這有助於您今日獲得成功，並具備彈性可隨您的成長並因應未來的需求：

* 排除產品目錄整合可能發生的典型挑戰，例如：
   * 目錄量或複雜性變高的效能問題
   * 無法存取中繼資料
   * 需要即時產品資料和體驗
* 數位成熟度的日益成長，導致需要體驗管理
* &#x200B;
   * CIF 提供產品體驗管理功能，無需額外的 IT 工作即可逐步整合。
* 準備好使用全通道
   * CIF支援各種接觸點技術（伺服器端、混合式、使用者端），並具備模式、加速器和核心元件。

## 歷程 {#journey}

如果您正在依循 Commerce 歷程，請移至下一步：

* [AEM 內容作者歷程](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/getting-started.md)
