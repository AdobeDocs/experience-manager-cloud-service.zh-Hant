---
title: 如何使用OAuth 2.0使用者端認證流程整合Salesforce與AEM Forms？
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
description: 使用OAuth 2.0使用者端認證流程整合Salesforce與AEM Forms的步驟
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration
source-git-commit: 2c0a816b61cfc17a83b24b28be1f317e9681c6c5
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 5%

---


# 使用OAuth 2.0使用者端認證流程整合Salesforce應用程式 {#configure-salesforce-with-ouath-2.0-client-credential}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service  | 本文章 |

您可以使用OAuth 2.0使用者端認證，將AEM Forms與Salesforce應用程式整合。 OAuth 2.0使用者端憑證是直接通訊的標準和安全方法，使用者無需參與。

![設定AEM Forms與Salesforce應用程式之間的通訊時的工作流程](/help/forms/assets/salesforce-workflow.png)
AEM Forms會交換在Salesforce連線應用程式中定義的使用者端憑證（消費者金鑰和使用者密碼）以取得存取權杖。

使用OAuth 2.0使用者端憑證來驗證授權碼流程驗證有多種好處：

* OAuth 2.0使用者端憑證驗證允許每個使用者有超過五個連線。
* AEM資料來源設定會繼續處理AEM使用者的停用、存取變更和密碼更新工作。

## 必備條件 {#prerequisites}

設定Salesforce應用程式與AEM環境之間的通訊之前：

* 建立 [使用OAuth 2.0使用者端認證流程的Salesforce已連線應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) 以及貴組織僅限API的使用者，並取得應用程式的消費者金鑰和消費者機密。

* 確保您的Swagger檔案已正確設定，以符合貴組織的API。 或者，您可以選擇使用 [建立Swagger檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) 從頭開始，針對您的AEM環境使用量身打造。


## 使用OAuth 2.0使用者端認證流程設定Salesforce應用程式 {#steps-to-create-aem-datasource-configuration}

若要使用OAuth 2.0使用者端認證驗證設定整合Salesforce應用程式與最適化表單，請執行下列步驟：

1. 登入您的  作者執行個體；
1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 資料來源]**.
1. 選取設定資料夾。
1. 按一下 **[!UICONTROL 建立]** 和 **[!UICONTROL 建立資料來源組態]** 隨即顯示。
1. 指定 **[!UICONTROL 標題]** 並選取 **[!UICONTROL 服務型別]** 作為 **[!UICONTROL RESTful服務]**.
1. 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 選取 **[!UICONTROL Swagger來源]** 作為 **[!UICONTROL 檔案].**

   >[!NOTE]
   >
   > 選取swagger檔案時，會自動填入「配置」、「主機」名稱和「基底」路徑。

1. 按一下「 」，從本機電腦上傳已建立的swagger檔案 **[!UICONTROL 瀏覽]**.
1. 選取 **[!UICONTROL 驗證型別]** 作為 **[!UICONTROL OAuth 2.0]** 和 **[!UICONTROL 驗證設定]** 面板隨即顯示。
1. 選取 **[!UICONTROL 授權型別]** 作為 **[!UICONTROL 使用者端認證]**.
1. 指定 **[!UICONTROL 使用者端ID]** 和 **[!UICONTROL 使用者端密碼]** 取得自Salesforce連線應用程式。
1. 指定 **[!UICONTROL 存取記號URL]** 格式
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 每個組織都有其專屬的網域名稱。

1. 按一下 **[!UICONTROL 測試連線]**.
1. 如果連線成功，請按一下 **[!UICONTROL 建立]** 按鈕。

現在，您可以 [建立表單資料模型](/help/forms/create-form-data-models.md) 將已設定的資料來源與您的調適型表單整合。
