---
title: 移轉至AEM Commerce integration framework (CIF)附加元件
description: 如何從舊版移轉至AEM Commerce integration framework (CIF)附加元件
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 0664e5dc4a7619a52cd28c171a44ba02c592ea3d
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 10%

---


# Experience Manager Cloud Service移轉指南 {#cif-migration}

本指南幫助識別 Experience Manager Cloud Service 移轉時須更新的區域。

## CIF附加元件 {#cif-add-on}

對於Experience Manager as a Cloud Service，CIF附加元件是Adobe Commerce和協力廠商商務解決方案唯一支援的商務整合解決方案。 Experience Manager as a Cloud Service 上會自動部署 CIF 附加元件，客戶不需手動部署。請參閱[AEM Commerce as a Cloud Service快速入門。](/help/commerce-cloud/cif-storefront/getting-started.md)

若要支援部署CIF Adobe的專案，請提供[AEM CIF核心元件。](https://github.com/adobe/aem-core-cif-components)

AEM 6.5也透過[軟體發佈入口網站提供CIF附加元件。](/help/implementing/developing/tools/package-manager.md)它是相容的，提供和Experience Manager as a Cloud Service的CIF附加元件相同的功能，不需調整。

Classic CIF 及其相依性已不再可用。依賴此CIF版本（使用`com.adobe.cq.commerce.api` Java API）的程式碼必須調整為CIF附加元件及其原則。

先前可用的CIF聯結器無法再安裝。 依賴此聯結器的程式碼需要調整為CIF附加元件及其原則。

## 專案結構 {#project-structure}

瞭解[AEM專案結構](/help/implementing/developing/introduction/aem-project-content-package-structure.md)和AEM as a Cloud Service的特性。 將您的專案設定調整為AEM as a Cloud Service版面。

與AEM 6.5部署相比，有兩個主要差異：

* GraphQL使用者端OSGi套件組合&#x200B;**不得再包含在AEM專案中**，已透過CIF附加元件部署
* GraphQL使用者端和Graphql資料服務&#x200B;**的OSGi設定不得**&#x200B;再包含到AEM專案中。

>[!TIP]
>
>檢視GitHub上的[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)專案。 此專案提供AEM as a Cloud Service和內部部署的Maven設定檔，這些設定檔會考慮不同的框架條件。

## 產品目錄 {#product-catalog}

不再支援匯入產品目錄資料。 透過對外部商務解決方案的即時呼叫，您可隨選使用CIF附加元件主參與者產品和目錄請求。 前往整合一章以進一步瞭解整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則應使用具有API的外部產品快取進行整合。 範例[Magento開放原始碼。](https://business.adobe.com/products/magento/open-source.html)

## 具有AEM轉譯的產品目錄體驗 {#aem-rendering}

如果您使用包含Classic CIF的目錄Blueprint，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料和購物互動 {#non-cacheable}

對不可快取資料和互動的使用者端請求（例如加入購物車、搜尋）應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
