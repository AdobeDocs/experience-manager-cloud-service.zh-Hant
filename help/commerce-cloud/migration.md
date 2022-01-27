---
title: 遷移到AEMCommerce Integration Framework(CIF)附加項
description: 如何從舊版AEM本遷移到Commerce Integration Framework(CIF)附加模組
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 遷移指南Experience Manager Cloud Service {#cif-migration}

本指南幫助確定需要更新的Experience Manager Cloud Service遷移區域。

## CIF附加

對於Experience Manageras a Cloud Service,CIF附加模組是Adobe Commerce和第三方商務解決方案唯一支援的商務整合解決方案。 CIF附加模組是自動為Experience Manageras a Cloud Service上的客戶部署的，不需要手動部署。 請參閱 [Commerce AEMas a Cloud Service入門](getting-started.md)。

支援部署CIFAdobe的項目 [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components)。

CIF附加模組也可AEM通過 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。 它相容，提供與Experience Manageras a Cloud Service的CIF附加功能相同的功能 — 無需調整。

傳統CIF及其依賴項已不可用。 依賴此CIF版本的代碼使用 `com.adobe.cq.commerce.api` Java API必須調整為CIF附加模組及其原則。

無法再安裝以前可用的CIF連接器。 依賴此連接器的代碼需要調整為CIF附加元件及其原則。

## 項目結構

瞭解 [項AEM目結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 以及AEMas a Cloud Service。 將項目設定調整為AEMas a Cloud Service佈局。
與6.AEM5部署相比，這裡有兩個主要區別：

* GraphQL客戶端OSGI捆綁包 **不能** 已包括到AEM項目中，通過CIF附加程式部署
* GraphQL客戶端和Graphql資料服務的OSGI配置 **不能** 已經被納入項AEM目了

>[!TIP]
>
>查看 [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia) 在GitHub上執行項目。 此項目為as a Cloud Service部署和AEM內部部署提供了Maven配置檔案，這些配置檔案考慮了不同的框架條件。

## 產品目錄

不再支援導入產品目錄資料。 使用CIF附加承擔者產品和目錄請求是通過即時呼叫外部商業解決方案而按需進行的。 請轉至「整合」一章，瞭解有關整合商務解決方案的詳細資訊。

>[!TIP]
>
>如果沒有可用的即時API，則應使用帶API的外部產品快取進行整合。 示例 [Magento開源](https://business.adobe.com/products/magento/open-source.html)。

## 產品目錄體驗與呈AEM現

如果將目錄藍圖與經典CIF一起使用，則需要更新產品目錄工作流。 CIF附加模組現在使用目錄模板即時提供產品目AEM錄體驗。 不再需要複製產品資料或產品頁。

## 不可快取資料與購物互動

客戶端請求不可快取的資料和交互（例如，添加到購物車、搜索）應通過CDN/Dispatcher直接轉到商業端點（商業解決方案或整合層）。 刪除僅是代AEM理的任何呼叫。
