---
title: '[!DNL Experience Manager Assets]與 [!DNL Adobe Workfront]整合'
description: ' [!DNL Assets] 與 [!DNL Workfront]之間的整合簡介'
role: Admin, Leader, Developer
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 13%

---

# [!DNL Adobe Experience Manager]作為[!DNL Cloud Service] [!DNL Assets]與[!DNL Adobe Workfront]整合 {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Workfront]是工作管理應用程式，可協助您在一個地方管理整個工作生命週期。 [!DNL Workfront] 與 [!DNL Adobe Experience Manager Assets] 整合之後，組織便可以透過工作和數位資產管理的內在連結，改善內容速度與上市時間。就在 Workfront 中管理其工作而言，使用者可以存取必要的文件和影像。

Adobe提供給[原生整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets]  (支援Assets Essentials和Assets as a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html?lang=zh-Hant)。

透過原生Experience Manager整合，您可以：

* 在Workfront中快速設定整合。

* 自動建立在Workfront和Experience Manager之間連結的資料夾。

* 輕鬆同步現有連結資產的中繼資料。

* 在Workfront中變更專案中繼資料時自動更新。

* 將多個Experience Manager Assets存放庫順利連線到一個Workfront環境，或多個Workfront環境連線到跨組織ID的一個Experience Manager Assets存放庫。


## 適用於Experience Manager的Adobe Workfront增強型聯結器 {#enhanced-connector-information}


自2022年6月起，Adobe已發行新的原生整合，用於將Workfront與Adobe Experience Manager Assets as a Cloud Service連線。 此整合已成為連線這兩個解決方案的必要方法。 日後任何新實施的增強型聯結器（1.9.8及更新版本）都會遭到封鎖，以便將Workfront與AEM Assets as a Cloud Service連線。 如需如何設定此整合的詳細資訊，請參閱[設定Experience Manager Assets as a Cloud Service整合](workfront-connector-configure.md)。

>[!NOTE]
>
>Adobe不支援並行使用Workfront for Experience Manager增強型聯結器和Experience Manager整合。

對於2022年6月之前的安裝，[!DNL Adobe Workfront for Experience Manager enhanced connector]的部署和設定需要注意以下幾點：

* Adobe僅需要透過認證合作夥伴或[!DNL Adobe Workfront for Experience Manager enhanced connector]來部署及設定[!DNL Adobe Professional Services]。 如果未透過認證合作夥伴或[!DNL Adobe Professional Services]進行部署與設定，則Adobe不支援此功能。
* Adobe可能會發行[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]的更新，使此聯結器成為多餘的；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請參閱[增強型聯結器安裝指示](workfront-connector-install.md)的步驟5(a)。
* 請參閱Experience Manager Assets增強型聯結器的[Workfront合作夥伴認證測驗](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 如需有關考試的資訊，請參閱[考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。