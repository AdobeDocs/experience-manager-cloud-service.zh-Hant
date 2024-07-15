---
title: 使用Brand Portal設定AEM Assets as a [!DNL Cloud Service]
description: 瞭解如何使用Brand Portal設定AEM Assets。 此設定可讓您從AEM例項將核准的品牌資產發佈到Brand Portal，並將它們發佈給Brand Portal使用者。
contentOwner: AK
feature: Brand Portal, Asset Distribution, Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 7%

---

# 使用Brand Portal設定Experience Manager Assets {#configure-aem-assets-with-brand-portal}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

設定Adobe Experience Manager Assets Brand Portal可讓您從Adobe Experience Manager Assets將核准的品牌資產以[!DNL Cloud Service]執行個體形式發佈到Brand Portal，並將它們發佈給Brand Portal使用者。

## 使用Cloud Manager啟動Brand Portal {#activate-brand-portal}

Cloud Manager使用者為Experience Manager Assets as a [!DNL Cloud Service]執行個體啟用Brand Portal。 啟動工作流程會在後端建立所需的設定(授權權杖、IMS設定和Brand Portal雲端服務)，並反映Cloud Manager中Brand Portal租使用者的狀態。 啟用Brand Portal可讓Experience Manager Assets使用者將資產發佈至Brand Portal，並分發給Brand Portal使用者。

**必備條件**

您需要下列專案，才能在Experience Manager Assets上以[!DNL Cloud Service]執行個體形式啟用Brand Portal：

* 以[!DNL Cloud Service]執行個體形式啟動並執行Experience Manager Assets。
* 有權存取Cloud Manager的使用者，已指派給Cloud Manager產品的設定檔。 如需詳細資訊，請參閱[存取Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager)。

>[!NOTE]
>
>Experience Manager Assets as a [!DNL Cloud Service]執行個體需要已設定的生產環境才能與Brand Portal租使用者連線。

**啟動Brand Portal的步驟**

您可以在以[!DNL Cloud Service]執行個體形式建立Experience Manager Assets的生產環境時啟用Brand Portal，或單獨啟用。 假設環境已建立，您現在必須啟用Brand Portal。

1. 登入AdobeCloud Manager並導覽至&#x200B;**[!UICONTROL 環境]**。

   **[!UICONTROL 環境]**&#x200B;頁面會顯示所有現有環境的清單。

1. 從清單中選取環境（一個接一個）以檢視環境詳細資訊。

   Brand Portal有權使用其中一個可用的環境，並會反映在&#x200B;**[!UICONTROL 環境資訊]**&#x200B;下。

   找到與Brand Portal關聯的環境後，按一下&#x200B;**[!UICONTROL 啟動Brand Portal]**&#x200B;按鈕以開始啟動工作流程。

   ![啟動Brand Portal](assets/create-environment4.png)

1. 啟動Brand Portal租使用者需要幾分鐘的時間，因為啟動工作流程會在後端建立所需的設定。 Brand Portal租使用者啟動後，狀態會變更為「已啟用」。

   ![檢視狀態](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal必須在與Experience Manager Assets相同的IMS組織上啟用作為[!DNL Cloud Service]執行個體。
>
>如果您的IMS組織(org1-existing)已有現有的Brand Portal雲端設定([使用Adobe Developer Console](#manual-configuration)手動設定)，且您的Experience Manager Assets as a [!DNL Cloud Service]執行個體已設定為另一個IMS組織(org2-new)，則從Cloud Manager啟用Brand Portal會將Brand Portal IMS組織重設為`org2-new`。 雖然在`org1-existing`上手動設定的雲端設定可在Experience Manager Assets編寫執行個體中看到，但在從Cloud Manager啟動Brand Portal後將不再使用。
>
>如果現有的Brand Portal雲端設定和Experience Manager Assets as a [!DNL Cloud Service]執行個體使用相同的IMS組織(org1)，您只需從Cloud Manager啟用Brand Portal即可。
>
>請勿修改任何自動產生的設定。

**另請參閱**：

* [在Experience Manager Assets中新增使用者和角色as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [在Cloud Manager中管理環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**登入您的Brand Portal租使用者**：

在Cloud Manager中啟用Brand Portal租使用者後，您可以從Admin Console登入Brand Portal，或直接使用租使用者URL。

您的Brand Portal租使用者的預設URL為： `https://<tenant-id>.brand-portal.adobe.com/`。

其中，租使用者ID是IMS組織。


如果您不確定Brand Portal URL，請執行以下步驟：

1. 登入[Admin Console](https://adminconsole.adobe.com/)並導覽至&#x200B;**[!UICONTROL 產品]**。
1. 從左側面板中選取&#x200B;**[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**。
1. 按一下&#x200B;**[!UICONTROL 前往Brand Portal]**，直接在瀏覽器中開啟Brand Portal。

   或是從&#x200B;**[!UICONTROL 移至Brand Portal]**&#x200B;連結複製Brand Portal租使用者URL，並將其貼到您的瀏覽器中以開啟Brand Portal介面。

   ![存取Brand Portal](assets/access-bp-on-cloud.png)


**測試連線**

執行以下步驟來驗證Experience Manager Assets as a [!DNL Cloud Service]執行個體與Brand Portal租使用者之間的連線：

1. 登入Experience Manager Assets。

1. 從&#x200B;**工具**&#x200B;面板，瀏覽至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 發佈]**。

   ![瀏覽至發佈選項](assets/test-bpconfig1.png)

   已在&#x200B;**[!UICONTROL Publish下建立至Brand Portal]**&#x200B;的Brand Portal發佈代理程式(**[!UICONTROL bpdistributionagent0]**)。

   ![建立發佈代理程式](assets/test-bpconfig2.png)

1. 按一下&#x200B;**[!UICONTROL Publish到Brand Portal]**&#x200B;以開啟發佈代理程式。

   您可以在&#x200B;**[!UICONTROL 狀態]**&#x200B;標籤下看到發佈佇列。

   發佈代理程式包含兩個佇列：
   * **processing-queue**：用於將資產發佈至Brand Portal。

   * **error-queue**：針對發佈失敗的資產。

   >[!NOTE]
   >
   >建議定期檢閱失敗並清除&#x200B;**錯誤佇列**。

   ![正在處理資產分配的佇列](assets/test-bpconfig3.png)

1. 若要驗證Experience Manager Assets as a [!DNL Cloud Service]與Brand Portal之間的連線，請按一下&#x200B;**[!UICONTROL 測試連線]**&#x200B;圖示。

   ![驗證AEM與Brand Portal之間的連線](assets/test-bpconfig4.png)

   出現訊息，指出您的&#x200B;*測試封裝已成功傳遞*。

   >[!NOTE]
   >
   >請避免停用發佈代理程式，因為可能導致在佇列中執行的資產發佈失敗。

若要驗證您的Experience Manager Assets as a [!DNL Cloud Service]執行個體與Brand Portal租使用者之間的連線，請從Experience Manager Assets發佈資產到Brand Portal。 如果連線成功，已發佈的資產會顯示在Brand Portal介面中。


您現在可以：

* [從Experience Manager Assets到Brand Portal的Publish資產](publish-to-brand-portal.md)
* [從Experience Manager Assets到Brand Portal的Publish資料夾](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [從Experience Manager Assets到Brand Portal的Publish集合](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* 從Brand Portal到Experience Manager Assets的[Publish資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-Hant) - Brand Portal中的資產來源
* [將預設集、結構和 Facet 發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

如需詳細資訊，請參閱[Brand Portal檔案](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)。

**散發記錄檔**

您可以監視資產發佈工作流程的分發代理程式記錄。

現在，讓我們從Experience Manager Assets發佈資產到Brand Portal並檢視記錄。

1. 請依照&#x200B;**測試連線**&#x200B;區段中所示步驟（從1到4）操作，並導覽至發佈代理程式頁面。
1. 按一下&#x200B;**[!UICONTROL 記錄檔]**&#x200B;以檢視處理和錯誤記錄檔。

   ![處理及錯誤記錄](assets/test-bpconfig5.png)

發佈代理程式已產生下列記錄：

* INFO：這是系統產生的記錄，會在成功設定發佈代理程式時觸發。
* DSTRQ1 （請求1）：測試連線上的觸發程式。

發佈資產時，會產生下列請求和回應記錄檔：

**發佈代理程式請求**：

* DSTRQ2 (請求 2)：觸發資產發佈請求。
* DSTRQ3 （請求3）：系統會觸發另一個請求，以發佈Experience Manager Assets資料夾（資產位於其中）並複製Brand Portal中的資料夾。

**發佈代理程式回應**：

* queue-bpdistributionagent0 (DSTRQ2)：資產已發佈至 Brand Portal。
* queue-bpdistributionagent0 (DSTRQ3)：系統會複製Brand Portal中的Experience Manager Assets資料夾（包含資產）。

在上述範例中，系統會觸發其他請求和回應。 由於資產是首次發佈，系統在Brand Portal中找不到父資料夾（新增路徑），因此觸發了額外的請求，要在Brand Portal中建立發佈資產的同名父資料夾。

>[!NOTE]
>
>如果父資料夾不存在於Brand Portal中或在Experience Manager Assets中經過修改，則會產生其他請求。

除了在Experience Manager Assets as a [!DNL Cloud Service]上啟動Brand Portal的自動化工作流程外，還有另一種使用Adobe Developer Console手動設定Experience Manager Assets as a [!DNL Cloud Service]與Brand Portal的方法，我們不再建議使用。

>[!NOTE]
>
>如果您在啟用Brand Portal租使用者時遇到任何問題，請聯絡客戶支援。

## 使用Adobe Developer Console手動設定 {#manual-configuration}

>[!NOTE]
>
> 從2024年6月起，您無法建立新的JWT憑證。 此後，只會建立OAuth認證。
> 檢視更多[建立OAuth設定](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration:~:text=For%20example%3A-,Creating%20an%20OAuth%20configuration,-To%20create%20a)。

以下章節說明如何使用Adobe Developer Console手動設定Experience Manager Assets as a [!DNL Cloud Service]與Brand Portal。

之前，Experience Manager Assets as a [!DNL Cloud Service]是透過Adobe Developer Console以Brand Portal手動設定，這種方式會取得Adobe的Identity Management Services (IMS)帳戶Token以授權Brand Portal租使用者。 它需要在Experience Manager Assets和Adobe Developer Console中進行設定。

<!--1. In Experience Manager Assets, create an IMS account and generate a public key (certificate).-->
<!--1. Under the project, configure an API using the public key to create a service account connection.
1. Get the service account credentials and JSON Web Token (JWT) payload information.
1. In Experience Manager Assets, configure the IMS account using the service account credentials and JWT payload.-->
1. 在Adobe Developer Console中，為您的Brand Portal租使用者（組織）建立專案。
1. 在Experience Manager Assets中，使用IMS帳戶和Brand Portal端點（組織URL）設定Brand Portal雲端服務。
1. 從Experience Manager Assets發佈資產到Brand Portal以測試設定。

>[!NOTE]
>
>Experience Manager Assets as a [!DNL Cloud Service]執行個體只能設定為一個Brand Portal租使用者。

**必備條件**

您需要下列專案才能使用Brand Portal設定Experience Manager Assets：

* 以[!DNL Cloud Service]執行個體身份啟動並執行Experience Manager Assets
* Brand Portal租使用者URL
* 在Brand Portal租使用者的IMS組織具有系統管理員許可權的使用者

## 建立設定 {#create-new-configuration}

以指定順序執行下列步驟，使用Brand Portal設定Experience Manager Assets。

1. [在Adobe Developer Console中設定OAuth認證](#config-oauth)
1. [使用OAuth建立新的Adobe IMS整合](#create-ims-account-configuration)
1. [設定雲端服務](#configure-cloud-service)
   <!--1. [Obtain public certificate](#public-certificate)-->
<!--1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure IMS account](#create-ims-account-configuration)-->

<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your Experience Manager Assets as a [!DNL Cloud Service] instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)
-->
<!--

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Login to Experience Manager Assets.
1. From the **Tools** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. It will redirect to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.
1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** drop-down list.  
1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 
1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (CRT) file on your machine.

   The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.  

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**.

    In the **Account** tab, Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

    Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) to get the credentials and JWT payload for configuring the IMS account. 
-->
<!--

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. To configure Experience Manager Assets with Brand Portal, you must generate a public key (certificate) in Experience Manager Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in Experience Manager Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in Experience Manager Assets.

Perform the following steps to generate the service account credentials and JWT payload:

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list located at the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** to update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the Experience Manager Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 

   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE] 
   >
   >* You can view the credentials and perform actions such as generate JWT tokens, copy credential details, retrieve client secret, and so on.
   >* Currently, only the Adobe's Developer Console Service Account (JWT) credential type is supported. Do not use the `OAuth Server-to-Server` credential type until it is supported in mid-April. Read more at [JWT Credentials Deprecation in Adobe Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html).

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in Experience Manager Assets.
-->
<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create an integration page. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### 在Adobe Developer Console中設定OAuth認證 {#config-oauth}

[在Adobe Developer Console中設定OAuth認證](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#credentials-in-the-developer-console)，並選取Brand Portal API。

### 使用OAuth建立新的Adobe IMS整合 {#create-ims-account-configuration}

[使用OAuth建立新的Adobe IMS整合](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration)，並在「雲端解決方案」下方的下拉式清單中選取Brand Portal。

<!--
Ensure that you have performed the following steps:

* [Obtain public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)
-->

<!--1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. Keep the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)  
-->
<!--
1. Complete the configuration based on details from the [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Click **[!UICONTROL Create]**.
-->
<!--Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)

 <!--  
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Adobe IMS Configurations Check Health.](assets/create-new-integration5.png)
-->
<!--
>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. You must delete it and create another valid configuration.
-->

### 設定雲端服務 {#configure-cloud-service}

執行以下步驟來設定Brand Portal雲端服務：

1. 登入Experience Manager Assets。

1. 從&#x200B;**工具**&#x200B;面板，瀏覽至&#x200B;**[!UICONTROL Cloud Service]** > **[!UICONTROL AEM Brand Portal]**。

1. 在Brand Portal設定頁面中，按一下&#x200B;**[!UICONTROL 建立]**。

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選取您在[設定IMS帳戶](#create-ims-account-configuration)時所建立的IMS設定。

   在&#x200B;**[!UICONTROL 服務URL]**&#x200B;欄位中，指定您的Brand Portal租使用者（組織） URL。

   ![Brand Portal設定對話方塊。](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。 雲端設定已建立。

   您的Experience Manager Assets as a [!DNL Cloud Service]執行個體現在已設定為Brand Portal租使用者。

您現在可以檢查發佈代理程式，並將資產發佈到Brand Portal以測試設定。

如果啟用安全預覽，則在SPS中允許清單輸出IP ****
如果使用Dynamic Media-Scene7並為公司啟用[安全預覽](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en)，則建議Scene7公司管理員[允許列出使用SPS (Scene7 Publishing System) Flash UI之個別地區的公開輸出IP](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en#testing-the-secure-testing-service)。
輸出IP如下：

| **地區** | **輸出IP** |
|--- |--- |
| 不適用 | 130.248.160.68， 20.94.203.130 |
| EMEA | 51.132.146.75， 130.248.244.202， 130.248.244.203， 130.248.244.204， 130.248.244.210， 130.248.244.211， 130.248.244 12 |
| APAC | 63.140.44.54 |

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![test-bpconfig1](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![test-bpconfig2](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![test-bpconfig3](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![test-bpconfig4](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![ctest-bpconfig4](assets/ctest-bpconfig4.png)

The distribution agent has generated the following logs:

* INFO: This is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the AEM Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the AEM Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response is triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in AEM Assets. 
-->

<!--

## Additional information {#additional-information}

Go to `/system/console/slingmetrics` for statistics related to the distributed content:

1. **Counter metrics**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Time metrics**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`

-->

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
-->

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
