---
title: 移轉至AEM Commerce integration framework (CIF)附加元件
description: 如何從舊版移轉至AEM Commerce integration framework (CIF)附加元件
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 20%

---

# Experience Manager Cloud Service移轉指南 {#cif-migration}

本指南幫助識別 Experience Manager Cloud Service 移轉時須更新的區域。

## CIF附加元件

對於Experience Manager as a Cloud Service，CIF附加元件是Adobe Commerce和協力廠商商務解決方案唯一支援的商務整合解決方案。 Experience Manager as a Cloud Service 上會自動部署 CIF 附加元件，客戶不需手動部署。請參閱 [AEM Commerce as a Cloud Service 快速入門](getting-started.md)。

若要支援部署CIF Adobe的專案，請提供[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)。

[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)也提供了適用於 AEM 6.5 的 CIF 附加元件。它是相容的，提供和適用於 Experience Manager as a Cloud Service 的 CIF 附加元件相同的功能，不需調整。

Classic CIF 及其相依性已不再可用。依賴此CIF版本（使用`com.adobe.cq.commerce.api` Java API）的程式碼必須調整為CIF附加元件及其原則。

先前可用的CIF聯結器無法再安裝。 依賴此聯結器的程式碼需要調整為CIF附加元件及其原則。

## 專案結構

瞭解[AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=zh-Hant)和AEM as a Cloud Service的特性。 將您的專案設定調整為AEM as a Cloud Service版面。
與AEM 6.5部署相比，以下有兩個主要差異：

* GraphQL使用者端OSGI套件&#x200B;**不得再包含在AEM專案中**，它是透過CIF附加元件部署的
* GraphQL使用者端和Graphql資料服務&#x200B;**的OSGI設定不得**&#x200B;再包含到AEM專案中

>[!TIP]
>
>檢視GitHub上的[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)專案。 此專案提供AEM as a Cloud Service和內部部署的Maven設定檔，這些設定檔會考慮不同的框架條件。

## 產品目錄

不再支援匯入產品目錄資料。 透過對外部商務解決方案的即時呼叫，您可隨選使用CIF附加元件主參與者產品和目錄請求。 前往整合一章以進一步瞭解整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則應使用具有API的外部產品快取進行整合。 範例[Magento開放原始碼](https://business.adobe.com/products/magento/open-source.html)。

## 具有AEM轉譯的產品目錄體驗

如果您使用包含Classic CIF的目錄Blueprint，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料和購物互動

對不可快取資料和互動的使用者端請求（例如加入購物車、搜尋）應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
