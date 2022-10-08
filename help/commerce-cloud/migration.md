---
title: 移轉至AEM Commerce Integration Framework(CIF)附加元件
description: 如何從舊版移轉至AEM Commerce Integration Framework(CIF)附加元件
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 27%

---

# Experience Manager Cloud Service移轉指南 {#cif-migration}

本指南幫助識別 Experience Manager Cloud Service 移轉時須更新的區域。

## CIF附加元件

CIF 附加元件是 Experience Manager as a Cloud Service 唯一支援用於 Adobe Commerce 和第三方商務解決方案的商務整合解決方案。Experience Manager as a Cloud Service 上會自動部署 CIF 附加元件，客戶不需手動部署。請參閱 [AEM Commerce as a Cloud Service 快速入門](getting-started.md)。

若要支援部署CIFAdobe的專案，請提供 [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components).

[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)也提供了適用於 AEM 6.5 的 CIF 附加元件。它是相容的，提供和適用於 Experience Manager as a Cloud Service 的 CIF 附加元件相同的功能，不需調整。

Classic CIF 及其相依性已不再可用。依賴此CIF版本的程式碼使用 `com.adobe.cq.commerce.api` Java API必鬚根據CIF附加元件及其原則進行調整。

舊有的CIF連接器無法再安裝。 依賴此連接器的程式碼需調整為CIF附加元件及其原則。

## 專案結構

了解 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 以及AEMas a Cloud Service的特點。 調整專案設定，使其與AEMas a Cloud Service版面配置一致。
與AEM 6.5部署相比，這裡有兩個主要差異：

* GraphQL用戶端OSGI套件組合 **不能** 再也包含在AEM專案中，而是透過CIF附加元件部署
* GraphQL用戶端和Graphql資料服務的OSGI設定 **不能** 已包含在AEM專案中

>[!TIP]
>
>查看 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) 專案。 此專案提供AEMas a Cloud Service和內部部署的Maven設定檔，可考慮不同的架構條件。

## 產品目錄

不再支援匯入產品目錄資料。 使用CIF附加主體產品與目錄請求是透過對外部商務解決方案的即時呼叫而隨選。 請前往章節整合，深入了解如何整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則整合應使用具有API的外部產品快取。 範例 [Magento開放原始碼](https://business.adobe.com/products/magento/open-source.html).

## 透過AEM轉譯提供產品目錄體驗

如果您搭配Classic CIF使用目錄藍圖，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料和購物互動

用戶端對無法快取的資料和互動（例如，加到購物車、搜尋）的請求，應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
