---
title: AEM Commerce as a Cloud Service的顯著變更
description: 與Adobe Experience Manager 6.5相比，AEM Commerce的雲端服務顯著變更。
translation-type: tm+mt
source-git-commit: 2934d0d8d3977bb7884bae9654ac26e9fa57b34f
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 5%

---


# AEM Commerce as a Cloud Service {#notable-changes}的顯著變更

Adobe Experience Manager即雲端服務，為您的AEM專案帶來許多新功能與可能。 本檔案著重說明Commerce Integration Framework(CIF)在內部部署、Adobe Managed Service和Experience Manager（即雲端服務）之間商務功能的重要差異。 如需其他變更，請參閱Experience Manager的一般[變更，即雲端服務](/help/release-notes/aem-cloud-changes.md)。

與Experience Manager 6.5相比，主要差異在於：
* [支援CIF Classic](#cif-classic)
* [部署CIF製作工具](#cif-tools)
* [從內部部署和Adobe Managed Service](#moving-cif-cs)

## 在Experience Manager上支援CIF Classic/Quickstart作為雲服務{#cif-classic}

Experience Manager中不再提供Classic Commerce Integration Framework（包含Product Importer以匯入和儲存Experience Manager中的產品目錄），即為雲端服務。 Experience Manager不支援將Classic CIF用作雲端服務，而使用Classic CIF的專案必須取代Classic CIF實作，如Experience Manager的[CIF中描述為雲端服務](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/architecture/magento.html#overview)所支援的版本

## CIF {#deployment}的部署

以下為不同AEM方案的Commerce Integration Framework不同部署模型：

|  | AEM On-premise | AEM Managed Services | AEM Cloud服務 |
|-------------     |-----------|-----------|-----------|
| 如何為Magento後端部署CIF製作工具 | [請參閱AEM 6.5](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) 上支援的CIF連接器 | [請參閱AEM 6.5](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) 上支援的CIF連接器 | AEM作為雲端服務，必須布建CIF附加元件。 如需詳細資訊，請洽詢您的銷售代表 |
| 如何部署[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) | AEM套件安裝 | 透過[Cloud Manager](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)完成部署 | 專案移入[Cloud Manager Git Repository](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)，並透過[Cloud Manager](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/deploying/overview.html)完成部署 |

>[!NOTE]
>
>如需如何搭配AEM Managed Service或AEM On-premise使用CIF的其他檔案，請參閱[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)

>[!NOTE]
>
>CIF Classic/Quickstart版的Commerce Integration Framework可用於AEM內部部署方案，但使用案例有限。 不過，這不是建議的解決方案。

## 從內部部署和受管理服務{#moving-cif-cs}移轉至AEM Commerce作為雲端服務

從AEM內部部署或「受管理服務」安裝移轉至AEM做為雲端服務的客戶，需要對AEM專案進行一些小幅調整。

如上所述，CIF連接器需要進行第一次調整。 CIF連接器由Adobe部署的CIF附加元件取代。 因此，請勿在AEM上將CIF Connector安裝為雲端服務。 此外，不支援與本機AEM Cloud SDK搭配使用，Adobe也針對[本機開發](develop.md)提供CIF附加元件。

其次，瞭解[AEM專案結構](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)以及AEM雲端服務的特性。 將您的專案設定調整為AEM的雲端服務版面。
這裡的主要區別是：

* GraphQL客戶端OSGI包&#x200B;**不能再包含在AEM項目中，它通過CIF附加模組部署**
* GraphQL客戶端和Graphql資料服務&#x200B;**的OSGI配置不能再包含在AEM項目中**

>[!TIP]
>
>查看GitHub上的[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)專案。 此專案提供AEM的Maven設定檔，做為雲端服務和內部部署，可考慮不同的架構條件。
