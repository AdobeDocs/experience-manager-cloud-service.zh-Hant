---
title: '''[!DNL Experience Manager Assets]與 [!DNL Adobe Workfront]整合'
description: ' [!DNL Assets] 與 [!DNL Workfront]之間的整合簡介'
role: Admin, Leader, Architect
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager]作為[!DNL Cloud Service] [!DNL Assets]與[!DNL Adobe Workfront]整合 {#assets-integration-overview}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開發人員檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Workfront]是工作管理應用程式，可協助您在一個地方管理整個工作生命週期。 [!DNL Workfront]與[!DNL Adobe Experience Manager Assets]之間的整合可讓組織在本質上連線工作和數位資產管理，藉以改善內容速度和上市時間。 在Workfront中管理其工作的情況下，使用者可以存取所需的檔案和影像。

將選件Adobe至[原生整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets]  (支援Assets Essentials和Assetsas a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html)。

透過原生Experience Manager整合，您可以：

* 在Workfront中快速設定整合。

* 自動建立在Workfront和Experience Manager之間連結的資料夾。

* 輕鬆同步現有連結資產的中繼資料。

* 在Workfront中變更專案中繼資料時自動更新。

* 將多個Experience Manager Assets存放庫順利連線到一個Workfront環境，或多個Workfront環境連線到跨組織ID的一個Experience Manager Assets存放庫。


## Experience Manager增強型聯結器的Adobe Workfront {#enhanced-connector-information}


2022年6月，Adobe發行新的原生整合，用於將Workfront與Adobe Experience Manager Assetsas a Cloud Service連線。 此整合已成為連線這兩個解決方案的必要方法。 未來任何新實施的增強型聯結器（1.9.8及更新版本）都會遭到封鎖，以便將Workfront與AEM Assetsas a Cloud Service連線。 如需如何設定此整合的詳細資訊，請參閱[設定Experience Manager Assetsas a Cloud Service整合](workfront-connector-configure.md)。

>[!NOTE]
>
>Adobe不支援同時使用Workfront進行Experience Manager增強型聯結器和Experience Manager整合。

對於2022年6月之前的安裝，[!DNL Adobe Workfront for Experience Manager enhanced connector]的部署和設定需要注意以下幾點：

* Adobe僅需要透過認證合作夥伴或[!DNL Adobe Professional Services]來部署和設定[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未使用認證合作夥伴或[!DNL Adobe Professional Services]進行部署與設定，則Adobe不支援此功能。
* Adobe可能會發行[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]的更新，使此聯結器成為多餘的；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請參閱[增強型聯結器安裝指示](workfront-connector-install.md)的步驟5(a)。
* 請參閱Experience Manager Assets增強型聯結器的[Workfront合作夥伴認證測驗](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 如需有關考試的資訊，請參閱[考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。