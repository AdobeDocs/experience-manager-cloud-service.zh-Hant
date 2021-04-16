---
title: 移轉至AEMCommerce Integration Framework(CIF)附加元件
description: 如何從舊版移AEM轉至Commerce Integration Framework(CIF)附加元件
translation-type: tm+mt
source-git-commit: cda25048e171f6aacd5349706ad4192965e703db
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 1%

---

# {#cif-migration}Experience Manager Cloud Service遷移指南

本指南可協助您識別Experience Manager Cloud Service移轉需要更新的區域。

## CIF附加元件

對於Experience Manager來說，CIF附加元件是Adobe商務和第三方商務解決方案唯一支援的商務整合解決方案。 CIF附加元件會自動部署給Experience Manager的客戶，做為Cloud Service，不需要手動部署。 請參閱[以Cloud ServiceAEM形式開始使用商務](getting-started.md)。

要支援部署CIFAdobe的項目，請提供[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)。

CIF附加元件也AEM可透過[軟體散發入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)取得6.5版。 它相容，提供與Experience ManagerCIF附加元件相同的功能，不需要調整。

傳統CIF及其依賴性已不再可用。 使用`com.adobe.cq.commerce.api` Java API的依賴此CIF版本的代碼必須調整為CIF附加元件及其原則。

以前可用的CIF連接器無法再安裝。 依賴此連接器的程式碼需要調整為CIF附加元件及其原則。

## 專案結構

瞭解[AEM Project Structure](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)以及作為Cloud Service的AEM特性。 將您的專案設定調整AEM為Cloud Service版面。
與6.AEM5部署相比，這裡有兩個主要差異：

* GraphQL客戶端OSGI包&#x200B;**不能再包含在項目中AEM，它通過CIF附加模組進行部署**
* GraphQL客戶端和Graphql資料服務&#x200B;**的OSGI配置不能再包含在項AEM目中**

>[!TIP]
>
>查看GitHub上的AEM[Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)專案。 本專案提供Maven設定檔，AEM做為Cloud Service部署和內部部署，可考慮不同的架構條件。

## 產品目錄

不再支援匯入產品目錄資料。 使用CIF附加承擔者產品和型錄要求是透過對外部商務解決方案的即時呼叫進行隨選。 請至「整合」一章，進一步瞭解整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則應使用含API的外部產品快取進行整合。 示例[Magentoopen-source](https://magento.com/products/magento-open-source)。

## 產品型錄體驗與轉AEM譯

如果您搭配使用Classic CIF的型錄藍圖，就需要更新產品型錄工作流程。 CIF附加元件現在使用型錄範本即時轉換產品型AEM錄體驗。 您不再需要複製產品資料或產品頁面。

## 無法快取的資料與購物互動

用戶端要求不可快取的資料和互動（例如，新增至購物車、搜尋）應透過CDN/Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除只是代理AEM的任何呼叫。
