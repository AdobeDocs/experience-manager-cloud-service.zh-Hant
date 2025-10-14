---
title: 如何使用OAuth 2.0使用者端憑證流程整合Salesforce與AEM Forms？
description: 瞭解如何使用OAuth 2.0使用者端認證流程整合Salesforce與AEM Forms。 其中會顯示AEM Forms Salesforce整合的步驟。
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration, AEM Forms Salesforce integration
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2c2029ab-6fb4-41a6-846c-175c3a79d921
source-git-commit: 9eb15dda5f56938d686d0b863cb1ffa841f8228b
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 56%

---

# 整合最適化表單與Salesforce {#configure-salesforce-with-ouath-2.0-client-credential}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

Adobe Experience Manager (AEM) Forms與Salesforce的整合可讓組織透過將其表單建立和管理功能與Salesforce平台連線來簡化流程。 將最適化表單與Salesforce連線可讓兩個平台之間無縫交換資料。 使用者提交表單時，資料會自動與Salesforce同步。 這可確保所有客戶資訊都是最新狀態，並集中在系統內。

您可以使用 OAuth 2.0 用戶端認證將 AEM Forms 與 Salesforce 應用程式進行整合。OAuth 2.0 用戶端認證是一種標準且安全的直接通訊方式，無需使用者參與。

![設定AEM Forms與Salesforce應用程式之間的通訊時的工作流程](/help/forms/assets/salesforce-workflow.png)

AEM Forms會交換在Salesforce連線應用程式中定義的使用者端憑證（消費者金鑰和使用者密碼）以取得存取權杖。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)文章中進一步瞭解這些選項。

比起授權代碼流程驗證，使用 OAuth 2.0 用戶端認證進行驗證有多種好處：

* OAuth 2.0 用戶端認證驗證允許每個使用者有五個以上的連線。
* AEM 資料來源設定可繼續進行 AEM 使用者的停用、存取變更、密碼更新。

## 先決條件 {#prerequisites}

設定 Salesforce 應用程式和 AEM 環境之間的通訊以前：

* 為貴組織建立一個[使用 OAuth 2.0 用戶端認證流程的 Salesforce 連線應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5)以及一個僅限 API 的使用者，並獲取應用程式的客戶金鑰和客戶密碼。

* 確保您的 Swagger 檔案已適當設定，和貴組織的 API 相符。或者，您可以選擇從頭開始[建立 Swagger 檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=zh-Hant)，專為在您的 AEM 環境中使用而量身打造。


## 使用 OAuth 2.0 用戶端認證流程設定 Salesforce 應用程式 {#steps-to-create-aem-datasource-configuration}

若要使用OAuth 2.0使用者端認證驗證設定將Adaptive Form連線至Salesforce應用程式，請執行下列步驟：

1. 登入您的作者執行個體。
1. 前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL 資料來源]**。
1. 選取設定檔案夾。
1. 按一下「**[!UICONTROL 建立]**」，「**[!UICONTROL 建立資料來源設定]**」會隨即顯示。
1. 指定&#x200B;**[!UICONTROL 標題]**&#x200B;並選取&#x200B;**[!UICONTROL 服務類型]**&#x200B;作為 **[!UICONTROL RESTful 服務]**。
1. 按一下「**[!UICONTROL 下一步]**」。
1. 選取 **[!UICONTROL Swagger 來源]**&#x200B;作為&#x200B;**[!UICONTROL 檔案]。**

   >[!NOTE]
   >
   > 選取 swagger 檔案後，綱要、主機名稱和基本路徑都會自動填入。

1. 按一下「**[!UICONTROL 瀏覽]**」，即可從您的本機電腦上傳已建立的 swagger 檔案。
1. 選取&#x200B;**[!UICONTROL 驗證類型]**&#x200B;作為&#x200B;**[!UICONTROL OAuth 2.0]**，**[!UICONTROL 驗證設定]**&#x200B;面板會隨即顯示。
1. 選取&#x200B;**[!UICONTROL 授予類型]**&#x200B;作為&#x200B;**[!UICONTROL 用戶端認證]**。
1. 指定&#x200B;**[!UICONTROL 用戶端 ID]**&#x200B;以及從 Salesforce 連線的應用程式獲取的&#x200B;**[!UICONTROL 用戶端密碼]**。
1. 指定&#x200B;**[!UICONTROL 存取權杖 URL]** 格式
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 每個組織都有自己特定的網域名稱。

1. 按一下「**[!UICONTROL 測試連線]**」。
1. 如果連線成功，按一下「**[!UICONTROL 建立]**」按鈕。


設定Salesforce應用程式後，您可以在建立表單資料模型(FDM)時使用設定。 如需詳細資訊，請參閱[建立表單資料模型(FDM)](create-form-data-models.md)。 [設定最適化表單的表單資料模型提交動作](/help/forms/using-form-data-model.md)，以將資料傳送至Salesforce應用程式。

如需在業務工作流程中建立和使用表單資料模型(FDM)的詳細資訊，請參閱[資料整合](data-integration.md)。

## 相關文章

{{af-submit-action}}


