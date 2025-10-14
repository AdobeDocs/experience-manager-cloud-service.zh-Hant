---
title: 管理 [!DNL Assets]中的 [!DNL Adobe Stock] 資產。
description: 從 [!DNL Adobe Experience Manager]內搜尋、擷取、授權及管理 [!DNL Adobe Stock] 資產。 將授權資產作為任何其他數位資產使用。
contentOwner: Vishabh Gupta
feature: Adobe Stock
role: Admin, User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 4%

---

# 在[!DNL Adobe Experience Manager Assets]中使用[!DNL Adobe Stock]個資產 {#use-adobe-stock-assets-in-aem-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Stock]服務可讓設計師和企業存取數百萬張高品質、精選且免版稅的像片、向量、插圖、影片、範本和3D資產，以供其所有創意專案使用。

根據預設，企業方案的[!DNL Adobe Stock]包含整個組織的共用許可權。 當資產獲得組織使用者的授權後，組織的其他使用者可以識別、下載和使用此資產，而無需再次授權。 一旦您的組織授權資產，其使用權利即永久有效。

組織可以整合其企業[!DNL Adobe Stock]計畫與[!DNL Experience Manager Assets]，以確保授權資產可廣泛用於其創意和行銷專案，並具備[!DNL Experience Manager]的強大資產管理功能。 [!DNL Experience Manager]使用者無需離開[!DNL Experience Manager]介面，即可快速尋找、預覽及授權[!DNL Experience Manager]中儲存的Adobe Stock資產。

## 整合[!DNL Experience Manager]和[!DNL Adobe Stock]的必要條件 {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets]讓使用者能夠直接從[!DNL Experience Manager]搜尋、預覽、儲存及授權[!DNL Adobe Stock]資產。

符合下列要求才能啟用此整合：

* 以[!DNL Cloud Service]執行個體形式啟動並執行[!DNL Experience Manager Assets]。
* 企業[!DNL Adobe Stock]計畫。
* 在[!DNL Admin Console]中擁有預設Stock產品設定檔許可權的使用者。
* 擁有在[!DNL Adobe Developer Console]中建立整合之[!DNL Developer Access profile]許可權的使用者。

企業[!DNL Adobe Stock]計畫，

* 提供[!DNL Adobe Stock]的產品權益(與Experience Manager連結的庫存)。
* 針對您的股票權益購買到[!DNL Adobe Admin Console]的積分。
* 啟用從[!DNL Adobe Admin Console]內全域管理信用額度與授權。

在權益中，[!DNL Adobe Stock]的預設產品設定檔存在於[!DNL Admin Console]中。 可建立多個設定檔，這些設定檔決定誰可以授權Stock資產。 直接存取產品設定檔的使用者可以存取[https://stock.adobe.com/](https://stock.adobe.com/)並授權Stock資產。 而有其他方法可使用開發人員存取權建立整合(API)。 此整合會驗證[!DNL Experience Manager Assets]與[!DNL Adobe Stock]之間的通訊。

<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).
-->

<!-- 
TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

## 整合[!DNL Experience Manager]和[!DNL Adobe Stock] {#integrate-adobe-stock-with-aem-assets}

以開發人員身分，執行以下步驟以整合[!DNL Adobe Experience Manager]和[!DNL Adobe Stock]。

<!--
1. [Obtain public certificate](#public-certificate)
   
   In [!DNL Experience Manager], create an IMS account and generate a public certificate (public key).

1. [Create service account (JWT) connection](#createnewintegration) 
   
   In [!DNL Adobe Developer Console], create a project for your [!DNL Adobe Stock] organization. Under the project, configure an API using the public key to create a service account (JWT) connection. Get the service account credentials and JWT payload information.

1. [Configure IMS account](#create-ims-account-configuration)

   In [!DNL Experience Manager], configure the IMS account using the service account credentials and JWT payload.

1. [Configure cloud service](#configure-the-cloud-service)

   In [!DNL Experience Manager], configure an [!DNL Adobe Stock] cloud service using the IMS account.


### Create an IMS configuration {#create-an-ims-configuration}

The IMS configuration authenticates your [!DNL Experience Manager Assets] author instance with the [!DNL Adobe Stock] entitlement. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your product profile in Adobe Developer Console.

1. Log in to your [!DNL Experience Manager Assets] cloud instance.

1. From the **[!UICONTROL Tools]** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** page opens. 

1. In the **[!UICONTROL Certificate]** tab, select **[!UICONTROL Adobe Stock]** from the **[!UICONTROL Cloud Solution]** drop-down list.  

1. You can create a certificate or reuse an existing certificate for the configuration. 

   To create a certificate, select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   Click **[!UICONTROL Next]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. In the **Account** tab, Adobe IMS account is created which requires the service account credentials.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration). 

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at organization level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. In this example, the service account credentials are generated by uploading the public key.

To generate the service account credentials and JWT payload:

1. Log in to Adobe Developer Console with system administrator privileges. The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Ensure that you have selected the correct IMS organization (Stock entitlement) from the drop-down (organization) list.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]**. Update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and then click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL Adobe Stock]**. Click **[!UICONTROL Next]**. 

1. In the **[!UICONTROL Configure API]** window, select **[!UICONTROL Service Account (JWT)]** authentication. Click **[!UICONTROL Next]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Click **[!UICONTROL Upload your public key]**. Click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. Click **[!UICONTROL Next]**.

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select the default **[!UICONTROL Adobe Stock]** product profile and click **[!UICONTROL Save configured API]**. 

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option. Here, you can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configure IMS account {#create-ims-account-configuration}

You must have the [certificate](#public-certificate) and [service account (JWT) credentials](#createnewintegration) to configure the IMS account.

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, enter the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Enter the client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

1. Click **[!UICONTROL Create]**. An IMS account configuration is created. 

   ![configure-ims-acount](assets/aem-stock-ims-config.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![health-check](assets/aem-stock-healthcheck.png)
-->

1. [在 [!DNL Developer Console]中設定程式](#set-up-a-program-in-developer-console)
1. [在 [!DNL AEM] 作者執行個體中新增設定](#add-configuration-in-the-aem-author-instance)

### 在[!DNL Developer Console]中設定程式 {#set-up-a-program-in-developer-console}

執行以下步驟，在[!DNL Developer Console]中設定程式：
1. 導覽至[[!DNL Adobe Developer Console]](https://developer.adobe.com/console/14431/user/servicesandapis)並登入您的組織。
1. 選取&#x200B;**[!UICONTROL 專案]**&#x200B;儀表板上的&#x200B;**[!UICONTROL 建立新專案]**。
   ![將aem資產與adobe stock整合](/help/assets/assets/create-new-project-in-adobe-dev-console.png)
1. 按一下&#x200B;**[!UICONTROL 新增至專案]**&#x200B;並選取&#x200B;**[!UICONTROL API]**。
1. 選取&#x200B;**[!UICONTROL Adobe Stock]**&#x200B;並按一下&#x200B;**[!UICONTROL 下一步]**。
1. 指定&#x200B;**[!UICONTROL 認證名稱]**&#x200B;並確認已選取&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**，然後按一下[下一步]&#x200B;**&#x200B;**。
1. 選取&#x200B;**[!UICONTROL AEM Assets]** **[!UICONTROL 產品設定檔]**，然後按一下&#x200B;**[!UICONTROL 儲存設定的API]**。 系統會顯示成功訊息，確認您已在[!DNL Developer Console]中建立專案。 您的專案儀表板隨即開啟，在頂端顯示專案名稱，**[!UICONTROL API]**&#x200B;底下的&#x200B;**[!UICONTROL Adobe Stock]**&#x200B;和&#x200B;**[!UICONTROL 產品設定檔]**&#x200B;底下的&#x200B;**[!UICONTROL AEM Assets]**，以及&#x200B;**[!UICONTROL 連線的認證]**&#x200B;底下的&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**&#x200B;認證卡。
   ![整合aem assets和adobe stock](/help/assets/assets/adc-project-name.png)
1. 選取&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**&#x200B;認證卡，並顯示&#x200B;**[!UICONTROL 認證詳細資料]**。 使用您專案的[!DNL OAuth Server-to-Server]認證詳細資料，例如&#x200B;**[!UICONTROL 使用者端ID]**、**[!UICONTROL 使用者端密碼]**、**[!UICONTROL 範圍]**、**[!UICONTROL 認證名稱]**、**[!UICONTROL 技術帳戶ID]**、**[!UICONTROL 組織ID]**，將設定新增至AEM編寫執行個體[&#128279;](#add-configuration-in-the-aem-author-instance)。
   ![aem assets和adobe stock](/help/assets/assets/oauth-server-server-credentials-details-page.png)

### 在[!DNL AEM]作者執行個體中新增設定 {#add-configuration-in-the-aem-author-instance}

執行以下步驟，在您的[!DNL AEM]作者執行個體中新增設定：

1. [在您的 [!DNL AEM] 作者執行個體中設定新的 [!DNL Adobe Stock IMS configuration] &#x200B;](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)
1. [新增雲端設定以連線至 [!DNL Adobe Stock]](#add-cloud-configuration-to-connect-adobe-stock)

#### 在您的[!DNL AEM author]執行個體中設定新的[!DNL Adobe Stock IMS configuration] {#set-up-adobe-stock-ims-configuration-in-aem-author-instance}

執行以下步驟，在您的[!DNL AEM]作者執行個體中設定新的[!DNL Adobe Stock IMS configuration]：
1. 導覽至您的[!DNL AEM]作者執行個體。
1. 按一下![aem assets和adobe stock](/help/assets/assets/Hammer.svg)，選取&#x200B;**[!UICONTROL 安全性]**，然後選取&#x200B;**[!UICONTROL Adobe IMS設定]**。
1. 按一下「**[!UICONTROL 建立]**」以建立新的IMS設定。 **[!UICONTROL Adobe IMS技術帳戶設定]**&#x200B;頁面會顯示多個欄位，例如&#x200B;**[!UICONTROL 雲端解決方案]**、**[!UICONTROL 標題]**、**[!UICONTROL 授權伺服器]**、**[!UICONTROL 使用者端ID]**、**[!UICONTROL 使用者端密碼]**、**[!UICONTROL 領域]**&#x200B;和&#x200B;**[!UICONTROL 組織ID]**。 請依照下列指示，在這些欄位中指定詳細資料：
   * **[!UICONTROL 雲端解決方案]**：選取&#x200B;**[!UICONTROL Adobe Stock]**。
   * **[!UICONTROL 標題]**：指定此整合的名稱。
   * **[!UICONTROL 授權伺服器]**：新增[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)做為授權伺服器。
   * **[!UICONTROL 使用者端ID]**：瀏覽至您的專案儀表板，按一下左窗格中可用的&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**&#x200B;選項，選取&#x200B;**[!UICONTROL 認證詳細資料]**，複製&#x200B;**[!UICONTROL 使用者端ID]**&#x200B;並貼至此處（請參閱[步驟7](#set-up-a-program-in-developer-console)）。

   * **[!UICONTROL 使用者端密碼]**：瀏覽至您的專案儀表板，按一下左窗格中可用的&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**&#x200B;選項，選取&#x200B;**[!UICONTROL 認證詳細資料]**，按一下&#x200B;**[!UICONTROL 擷取使用者端密碼]**，複製&#x200B;**[!UICONTROL 使用者端密碼]**&#x200B;並貼至此處（請參閱[步驟7](#set-up-a-program-in-developer-console)）。

   * **[!UICONTROL 領域]**：瀏覽至您的專案儀表板，按一下左窗格中可用的&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**&#x200B;選項，選取&#x200B;**[!UICONTROL 認證詳細資料]**，複製&#x200B;**[!UICONTROL 領域]**&#x200B;並貼至此處（請參閱[步驟7](#set-up-a-program-in-developer-console)）。

   * **[!UICONTROL 組織ID]**：瀏覽至您的專案儀表板，按一下左窗格中可用的&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**&#x200B;選項，選取&#x200B;**[!UICONTROL 認證詳細資料]**，複製&#x200B;**[!UICONTROL 組織ID]**&#x200B;並貼至此處（請參閱[步驟7](#set-up-a-program-in-developer-console)）。

     ![aem assets和adobe stock](/help/assets/assets/adobe-ims-technical-account-configuration.png)
1. 按一下「**[!UICONTROL 建立]**」，**[!UICONTROL Adobe IMS設定]**&#x200B;頁面會開啟並顯示您建立的[!DNL Adobe Stock]整合。

#### 新增雲端設定以連線至[!DNL Adobe Stock] {#add-cloud-configuration-to-connect-adobe-stock}

執行以下步驟，新增雲端設定以連線至[!DNL Adobe Stock]：

1. 導覽至您的[!DNL AEM author]執行個體。
1. 按一下![aem assets和adobe stock](/help/assets/assets/Hammer.svg)，選取&#x200B;**[!UICONTROL 雲端服務]**，瀏覽並選取&#x200B;**[!UICONTROL Adobe Stock]**。
   ![搭配aem](/help/assets/assets/adding-cloud-config-to-adobe-stock.png)使用adobe stock
1. 按一下「**[!UICONTROL 建立]**」，**[!UICONTROL Adobe Stock組態]**&#x200B;頁面會顯示多個欄位。 請依照下列指示，在這些欄位中指定詳細資料：
   * **[!UICONTROL 標題]**：導覽至&#x200B;**[!UICONTROL Adobe IMS技術帳戶設定]**&#x200B;頁面（請參閱[步驟3](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)），複製標題並貼到這裡。
   * **[!UICONTROL 關聯的Adobe IMS設定]**：選取您建立的[!DNL Adobe Stock]整合。
   * **[!UICONTROL 地區設定]**：選取&#x200B;**[!UICONTROL 英文（美國）]**。
1. 按一下「**[!UICONTROL 儲存並關閉]**」。
   ![搭配aem](/help/assets/assets/adobe-stock-config-page.png)使用adobe stock

<!--
### Configure cloud service {#configure-the-cloud-service}

To configure the [!DNL Adobe Stock] cloud service:

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. In the [!DNL Adobe Stock Configurations] page, click **[!UICONTROL Create]**.

1. Specify a **[!UICONTROL Title]** for the cloud configuration. 

   Select the IMS configuration that you have created while [configuring the IMS account](#create-ims-account-configuration).

   Select your locale from the drop-down list.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Click **[!UICONTROL Save & Close]**. 
-->
您的[!DNL Experience Manager Assets]作者執行個體現在已與[!DNL Adobe Stock]整合。 您可以建立多個[!DNL Adobe Stock]組態（例如地區設定組態）。 您現在可以從[!DNL Experience Manager]使用者介面存取、搜尋及授權[!DNL Adobe Stock]資產。

![search-stock-assets](assets/aem-stock-searchstocks.png)

>[!NOTE]
>
>在此整合階段，只有管理員可以存取[!DNL Adobe Stock]資產、搜尋Stock資產（使用Omnisearch），以及授權[!DNL Adobe Stock]資產。
>
>管理員可以進一步將使用者或群組新增至[!DNL Adobe Stock]雲端服務，並在[!DNL Experience Manager]中授予這些非管理員使用者存取Stock設定的許可權。

1. 若要新增使用者或群組，請選取[!DNL Adobe Stock]雲端設定，然後按一下&#x200B;**[!UICONTROL 屬性]**。

1. 搜尋以新增您已指派許可權來存取Adobe Stock設定的使用者或群組。 請參閱[將許可權指派給使用者群組](#assign-permissions-to-group)。


## 指派許可權給使用者群組 {#assign-permissions-to-group}

管理員可以建立使用者群組，並將許可權授予特定使用者或群組以存取[!DNL Adobe Stock]雲端服務。

以下是使用者搜尋和授權Adobe Stock資產所需的許可權：

* 設定路徑： `/conf/global/settings/stock`
* 許可權： `jcr:read`
* 許可權型別： `Allow`

您可以建立使用者群組或指派許可權給現有的使用者群組。 可從[!DNL Experience Manager Assets]介面或[!DNL User Admin]主控台指派許可權。

**若要從[!DNL Experience Manager]提供使用者群組的存取權：**

1. 在[!DNL Experience Manager]使用者介面中，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 群組]**。 建立[!DNL Adobe Stock]的使用者群組。

1. 瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 許可權]**。

1. 在左側面板中搜尋使用者群組，並為Adobe Stock新增新的&#x200B;**[!UICONTROL 存取控制專案(ACE)]**。

   * 設定路徑： `/conf/global/settings/stock`
   * 許可權： `jcr:read`
   * 許可權型別： `Allow`

   按一下&#x200B;**[!UICONTROL 新增]**。

   ![使用者許可權](assets/aem-stock-user-permissions.png)

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Adobe Stock]**。 選取[!DNL Adobe Stock]雲端設定，然後按一下&#x200B;**[!UICONTROL 屬性]**。

1. 將已建立的使用者群組新增至[!DNL Adobe Stock]設定。 按一下「**[!UICONTROL 儲存並關閉]**」。

   ![指派使用者](assets/aem-stock-adduser.png)

**若要提供存取權給來自[!DNL User Admin Console]的使用者：**

1. 開啟[!DNL Experience Manager]使用者Admin Console。 預設URL為`http://localhost:4502/userdamin`。

1. 在左側面板中，輸入`user_id`或`name`來搜尋使用者。 按兩下以開啟使用者屬性。

1. 瀏覽至&#x200B;**[!UICONTROL 許可權]**&#x200B;索引標籤，並允許[!DNL Adobe Stock]雲端設定的`read`許可權： `/conf/global/settings/stock`。

   >[!CAUTION]
   >
   >如果不允許雲端設定，則使用者只能在[!DNL Experience Manager]介面中存取&#x200B;**[!UICONTROL Assets]**。
   >
   >若要允許存取[!UICONTROL Assets]和[!DNL Adobe Stock]資產，請確定使用者允許雲端設定。

1. 按一下[儲存]以更新許可權。**&#x200B;**

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. 將使用者或群組新增至[!DNL Adobe Stock]雲端設定。


## 存取Adobe Stock資產 {#access-stock-assets}

擁有[!DNL Adobe Stock]雲端設定許可權的非管理員使用者可以從[!DNL Experience Manager]介面搜尋及授權[!DNL Adobe Stock]資產。

使用者在存取[!DNL Adobe Stock]個資產之前，必須執行啟用[!DNL Adobe Stock]雲端設定的額外步驟。 這是單次活動。 如果使用者在多個[!DNL Adobe Stock]雲端設定上被指派許可權，則使用者可以從&#x200B;**[!UICONTROL 使用者偏好設定]**&#x200B;中選取所需的設定。

若要啟用[!DNL Adobe Stock]雲端設定：

1. 登入[!DNL Experience Manager]。

1. 從右上角按一下使用者圖示，然後按一下&#x200B;**[!UICONTROL 我的偏好設定]**。 **[!UICONTROL 使用者偏好設定]**&#x200B;視窗隨即開啟。

1. 從下拉式清單中選取所需的&#x200B;**[!UICONTROL Stock組態]**，然後按一下&#x200B;**[!UICONTROL 接受]**&#x200B;以啟動組態。

   ![使用者偏好設定](assets/aem-stock-preferences.png)

1. 導覽至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**。 您現在可以檢視、搜尋及授權[!DNL Adobe Stock]資產。

下表說明存取[!DNL Adobe Stock]資產時使用者許可權的運作方式：

| 使用者 | 群組 | 權限 | 接受使用者偏好設定中的Stock設定 | 存取Assets | 存取Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| 管理員 | 不適用 | 全部 | 不適用 | 是 | 是 |
| test-doc1 | DAM 使用者 | /conf/global/settings/stock/cloud-config | 是 | 是 | 是 |
| test-doc1 | DAM 使用者 | /conf/global/settings/stock/cloud-config | 否 | 錯誤：無法載入資料 | 否 |
| test-doc1 | DAM 使用者 | **允許**： /conf/global/settings/stock **deny**： /cloud-config | Stock設定不可見 | 是 | 否 |

## 使用和管理[!DNL Experience Manager]中的[!DNL Adobe Stock]資產 {#usemanage}

使用此功能，組織可以允許其使用者使用[!DNL Experience Manager Assets]中的[!DNL Adobe Stock]個資產進行工作。 在[!DNL Experience Manager]使用者介面中，使用者可以搜尋[!DNL Adobe Stock]資產並授權必要的資產。

在[!DNL Experience Manager]中授權[!DNL Adobe Stock]資產後，就可以像一般資產一樣使用和管理它。 在[!DNL Experience Manager]中，使用者可以搜尋及預覽資產；複製及發佈資產；在[!DNL Brand Portal]上共用資產；透過[!DNL Experience Manager]案頭應用程式存取及使用資產；以此類推。

![搜尋[!DNL Adobe Stock]資產，並從[!DNL Adobe Experience Manager]工作區篩選結果](assets/adobe-stock-search-results-workspace.png)

**A.**&#x200B;搜尋與已提供[!DNL Adobe Stock] ID之資產的類似資產。 **B.** 搜尋與您選取的型態或方向相符的資產。**C.**&#x200B;搜尋一或多個支援的資產型別&#x200B;**D.**&#x200B;開啟或收合篩選器窗格&#x200B;**E.**&#x200B;授權並將選取的資產儲存在[!DNL Experience Manager] **F.**&#x200B;將資產儲存在[!DNL Experience Manager]中(含浮水印&#x200B;**G.**&#x200B;在[!DNL Adobe Stock]網站上探索與選取的資產類似的資產&#x200B;**H.**&#x200B;在[!DNL Adobe Stock]網站上檢視選取的資產&#x200B;**I.**&#x200B;搜尋結果中選取的資產數目&#x200B;**H j.**&#x200B;在卡片檢視和清單檢視之間切換

### 尋找資產 {#find-assets}

您的[!DNL Experience Manager]使用者可以在[!DNL Experience Manager]和[!DNL Adobe Stock]中搜尋資產。 當搜尋位置不限於[!DNL Adobe Stock]時，會顯示來自[!DNL Experience Manager]和[!DNL Adobe Stock]的搜尋結果。

* 若要搜尋[!DNL Adobe Stock]資產，請按一下&#x200B;**[!UICONTROL 導覽]** > **[!UICONTROL Assets]** > **[!UICONTROL 搜尋Adobe Stock]**。

* 若要搜尋[!DNL Adobe Stock]與[!DNL Experience Manager Assets]之間的資產，請按一下搜尋![搜尋](assets/do-not-localize/search_icon.png)。

或者，開始在搜尋列中輸入`Location: Adobe Stock`以選取[!DNL Adobe Stock]資產。 [!DNL Experience Manager]針對搜尋的資產提供進階篩選功能，讓使用者能夠使用篩選器快速鎖定所需的資產，例如支援的資產型別、影像方向和授權狀態。

>[!NOTE]
>
>從[!DNL Adobe Stock]搜尋的Assets會顯示在[!DNL Experience Manager]中。 [!DNL Adobe Stock]資產只有在使用者[儲存資產](/help/assets/aem-assets-adobe-stock.md#saveassets)或[授權並儲存資產](/help/assets/aem-assets-adobe-stock.md#licenseassets)之後，才會擷取並儲存在[!DNL Experience Manager]存放庫中。 已儲存在[!DNL Experience Manager]中的Assets會顯示並反白顯示，以方便參考和存取。 此外，[!DNL Stock]資產會與一些額外的中繼資料一起儲存，以將來源指示為[!DNL Stock]。

![在[!DNL Experience Manager]中搜尋篩選器，並在搜尋結果中反白顯示[!DNL Adobe Stock]個資產](assets/aem-search-filters2.jpg)

### 儲存並檢視必要的資產 {#saveassets}

選取您要儲存於[!DNL Experience Manager]的資產。 按一下頂端工具列中的[!UICONTROL 儲存]，並提供資產的名稱和位置。 未授權資產會使用浮水印儲存在本機。

下次當您搜尋資產時，儲存的資產會以徽章強調顯示，以表示這些資產可在[!DNL Experience Manager Assets]中使用。

>[!NOTE]
>
>最近新增的資產會顯示新徽章，而非授權徽章。

### 授權資產 {#licenseassets}

使用者可以使用其[!DNL Adobe Stock]企業計畫的配額來授權[!DNL Adobe Stock]資產。 當您授權資產時，儲存時不會加上浮水印，且可在[!DNL Experience Manager Assets]中搜尋和使用。

![在[!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)中授權及儲存[!DNL Adobe Stock]個資產的對話方塊


### 存取中繼資料和資產屬性 {#access-metadata-and-asset-properties}

使用者可以存取及預覽中繼資料，包括儲存在[!DNL Experience Manager]中之資產的[!DNL Adobe Stock]中繼資料屬性，以及新增資產的&#x200B;**[!UICONTROL 授權參考]**。 但是，[!DNL Experience Manager]與[!DNL Adobe Stock]網站之間未同步授權參考的更新。

使用者可以看到已授權和未授權資產的屬性。

![檢視及存取已儲存資產的中繼資料和授權參考](assets/metadata_properties.jpg)


## 已知限制 {#known-limitations}

* **限制使用者授權的功能無法正常運作**：所有具有Stock設定`read`許可權的使用者都可以搜尋及授權[!DNL Adobe Stock]資產。

* **非管理員使用者必須手動啟用[!DNL Adobe Stock]雲端設定**：在&#x200B;**[!UICONTROL 使用者偏好設定]**&#x200B;視窗中，**[!UICONTROL Stock設定]**&#x200B;會將[!DNL Adobe Stock]雲端設定顯示為已啟用，但無法用於非管理員使用者。 使用者必須按一下&#x200B;**[!UICONTROL 接受]**&#x200B;按鈕才能啟用Stock設定。 如果沒有此步驟，系統會在存取&#x200B;**[!UICONTROL Assets]**&#x200B;時反映錯誤訊息。

* **未顯示編輯影像警告**：授權影像時，使用者無法檢查影像是否僅限編輯使用。 為避免可能誤用，管理員可以從Admin Console關閉編輯資產的存取權。

* **顯示的授權型別錯誤**：資產的[!DNL Experience Manager]可能顯示不正確的授權型別。 使用者可以登入[!DNL Adobe Stock]網站以檢視授權型別。

* **參考欄位和中繼資料未同步**：當使用者更新授權參考欄位時，授權參考資訊會在[!DNL Experience Manager]中更新，但不會在[!DNL Adobe Stock]網站上更新。 同樣地，如果使用者更新[!DNL Adobe Stock]網站上的參考欄位，則更新不會在[!DNL Experience Manager]中同步。

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
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

>[!MORELIKETHIS]
>
>* [搭配Experience Manager Assets使用Adobe Stock資產的教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html?lang=zh-Hant)
>* [Adobe Stock企業計畫說明](https://helpx.adobe.com/tw/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock常見問題集](https://helpx.adobe.com/tw/stock/faq.html)
