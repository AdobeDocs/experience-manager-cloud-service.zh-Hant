---
title: 移轉至AEM Commerce Integration Framework(CIF)附加元件
description: 如何從舊版移轉至AEM Commerce Integration Framework(CIF)附加元件
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# {#cif-migration}Experience Manager Cloud Service的遷移指南

本指南可協助您識別Experience Manager Cloud Service移轉所需更新的領域。

## CIF附加元件

針對Experience Manager作為Cloud Service,CIF附加元件是Adobe商務和第三方商務解決方案唯一支援的商務整合解決方案。 CIF附加元件會自動部署給Experience ManagerCloud Service的客戶，不需手動部署。 請參閱[AEM Commerce as aCloud Service快速入門](getting-started.md)。

若要支援部署CIFAdobe的專案，請提供[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)。

AEM 6.5也可透過[Software Distribution入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)使用CIF附加元件。 它與CIF附加元件相容，提供與Experience ManagerCloud Service相同的功能 — 不需要進行調整。

傳統CIF及其相依性已無法使用。 依賴此CIF版本（使用`com.adobe.cq.commerce.api` Java API）的程式碼必須調整為CIF附加元件及其原則。

舊有的CIF連接器無法再安裝。 依賴此連接器的程式碼需調整為CIF附加元件及其原則。

## 專案結構

了解[AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)以及AEM作為Cloud Service的特性。 將專案設定調整為AEMCloud Service配置。
與AEM 6.5部署相比，這裡有兩個主要差異：

* GraphQL用戶端OSGI套件組合&#x200B;**不得再**&#x200B;包含在AEM專案中，而是透過CIF附加元件部署
* GraphQL用戶端和Graphql資料服務&#x200B;**的OSGI設定不得再**&#x200B;包含在AEM專案中

>[!TIP]
>
>查看GitHub上的[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)專案。 此專案提供AEM的Maven設定檔，作為Cloud Service和內部部署，且會考慮不同的架構條件。

## 產品目錄

不再支援匯入產品目錄資料。 使用CIF附加主體產品與目錄請求是透過對外部商務解決方案的即時呼叫而隨選。 請前往章節整合，深入了解如何整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則整合應使用具有API的外部產品快取。 範例[Magento開放原始碼](https://magento.com/products/magento-open-source)。

## 透過AEM轉譯提供產品目錄體驗

如果您搭配Classic CIF使用目錄藍圖，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料和購物互動

用戶端對無法快取的資料和互動（例如購物車附加元件、搜尋）的請求，應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
