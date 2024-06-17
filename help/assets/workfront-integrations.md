---
title: 『[!DNL Experience Manager Assets] 與整合 [!DNL Adobe Workfront]『
description: 以下專案之間的整合簡介： [!DNL Assets] 和 [!DNL Workfront]
role: Admin, Leader, Architect
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 與整合 [!DNL Adobe Workfront] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Workfront] 是工作管理應用程式，協助您在一個地方管理整個工作生命週期。 以下兩者的整合： [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 可讓組織在本質上連線工作和數位資產管理，藉以改善內容速度和上市時間。 在Workfront中管理其工作的情況下，使用者可以存取所需的檔案和影像。

Adobe優惠至 [整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 原生(as a Cloud Service支援Assets Essentials和資產)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html).

透過原生Experience Manager整合，您可以：

* 在Workfront中快速設定整合。

* 自動建立在Workfront和Experience Manager之間連結的資料夾。

* 輕鬆同步現有連結資產的中繼資料。

* 在Workfront中變更專案中繼資料時自動更新。

* 將多個Experience Manager Assets存放庫順利連線到一個Workfront環境，或多個Workfront環境連線到跨組織ID的一個Experience Manager Assets存放庫。


## Experience Manager增強型聯結器的Adobe Workfront {#enhanced-connector-information}


自2022年6月起，Adobe已發行新的原生整合，用於將Workfront與Adobe Experience Manager Assetsas a Cloud Service連線。 此整合已成為連線這兩個解決方案的必要方法。 日後任何新實施的增強型聯結器（1.9.8及更新版本）都會遭到封鎖，以便將Workfront與AEM Assetsas a Cloud Service連線。 如需如何設定此整合的詳細資訊，請參閱 [設定Experience Manager Assetsas a Cloud Service整合](workfront-connector-configure.md).

>[!NOTE]
>
>Adobe不支援同時使用Workfront進行Experience Manager增強型聯結器和Experience Manager整合。

對於2022年6月之前的安裝，以下是部署和設定的幾點注意事項 [!DNL Adobe Workfront for Experience Manager enhanced connector]：

* Adobe需要部署和設定 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署與設定沒有認證合作夥伴或 [!DNL Adobe Professional Services]，Adobe不支援。
* Adobe可能會將更新發行至 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 讓此聯結器成為多餘的；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請參閱的步驟5(a) [增強型聯結器安裝指示](workfront-connector-install.md).
* 另請參閱 [適用於Experience Manager Assets增強型聯結器的Workfront合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有關考試的資訊，請參閱 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).