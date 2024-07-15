---
title: 如何為AEM Forms設定 [!DNL Microsoft Dynamics] OData？
description: 瞭解如何根據 [!DNL Microsoft Dynamics] 服務中定義的實體、屬性和服務來建立表單資料模型(FDM)。
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# [!DNL Microsoft Dynamics] OData設定 {#microsoft-dynamics-odata-configuration}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/ms-dynamics-odata-configuration.html) |
| AEM as a Cloud Service  | 本文章 |

![資料整合](assets/data-integeration.png)

[!DNL Microsoft Dynamics]是客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案來建立和管理客戶帳戶、連絡人、潛在客戶、商機和案例。 [[!DNL Experience Manager Forms] 資料整合](data-integration.md)提供OData雲端服務設定，將Forms與線上和內部部署[!DNL Microsoft Dynamics]伺服器整合。 它可讓您根據[!DNL Microsoft Dynamics]服務中定義的實體、屬性和服務來建立表單資料模型(FDM)。 表單資料模型(FDM)可用來建立與[!DNL Microsoft Dynamics]伺服器互動的Adaptive Forms，以啟用業務工作流程。 例如：

* 查詢[!DNL Microsoft Dynamics]伺服器以取得資料並預先填入Adaptive Forms
* 在提交最適化表單時將資料寫入[!DNL Microsoft Dynamics]
* 透過表單資料模型(FDM)中定義的自訂實體寫入[!DNL Microsoft Dynamics]中的資料，反之亦然

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  MS Dynamics ODataCloud Service（OData服務）適用於所有執行模式。 如需設定[!DNL Experience Manager]執行個體的執行模式的詳細資訊，請參閱[執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#runmodes)。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/configure-submit-actions-core-components.md)文章中進一步瞭解這些選項。


## 先決條件 {#prerequisites}

在您開始設定和設定[!DNL Microsoft Dynamics]之前，請確定您擁有：

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* 已線上上設定[!DNL Microsoft Dynamics] 365，或已安裝下列[!DNL Microsoft Dynamics]版本之一的執行個體：

   * [!DNL Microsoft Dynamics] 365內部部署
   * [!DNL Microsoft Dynamics] 2016內部部署

* [已在 [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)註冊 [!DNL Microsoft Dynamics] 線上服務的應用程式。 記下註冊服務的使用者端ID （也稱為應用程式ID）和使用者端密碼的值。 在[為您的 [!DNL Microsoft Dynamics] 服務](#configure-cloud-service-for-your-microsoft-dynamics-service)設定雲端服務時，會使用這些值。

## 設定已登入[!DNL Microsoft Dynamics]應用程式的回覆URL {#set-reply-url-for-registered-microsoft-dynamics-application}

執行下列動作，為已登入的[!DNL Microsoft Dynamics]應用程式設定回覆URL：

>[!NOTE]
>
>只有在將[!DNL Experience Manager Forms]與線上[!DNL Microsoft Dynamics]伺服器整合時，才使用此程式。

1. 移至[!DNL Microsoft Azure] Active Directory帳戶，並為您註冊的應用程式在&#x200B;**[!UICONTROL 回覆URL]**&#x200B;設定中新增下列雲端服務設定URL：

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 儲存設定。

## 為IFD設定[!DNL Microsoft Dynamics] {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics]使用宣告式驗證來提供[!DNL Microsoft Dynamics] CRM伺服器上資料的存取權給外部使用者。 若要啟用此功能，請執行下列動作，為網際網路對向部署(IFD)設定[!DNL Microsoft Dynamics]並設定宣告設定。

>[!NOTE]
>
> 只有在將[!DNL Experience Manager Forms]與內部部署[!DNL Microsoft Dynamics]伺服器整合時，才使用此程式。

1. 設定[!DNL Microsoft Dynamics]內部部署執行個體以進行IFD，如[設定IFD for [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx)中所述。
1. 使用Windows PowerShell執行以下命令，以設定啟用IFD的[!DNL Microsoft Dynamics]上的宣告設定：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   如需詳細資訊，請參閱[CRM內部部署(IFD)的應用程式註冊](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd)。

## 在AD FS電腦上設定OAuth使用者端 {#configure-oauth-client-on-ad-fs-machine}

執行下列動作，在Active Directory Federation Services (AD FS)電腦上註冊OAuth使用者端並授與AD FS電腦上的存取權：

>[!NOTE]
>
>只有在將[!DNL Experience Manager Forms]與內部部署[!DNL Microsoft Dynamics]伺服器整合時，才使用此程式。

1. 執行以下命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID`是您可以使用任何GUID產生器產生的使用者端ID。
   * `redirect-uri`是[!DNL Experience Manager Forms]上[!DNL Microsoft Dynamics] OData雲端服務的URL。 與[!DNL Experience Manager Forms]一起安裝的預設雲端服務部署在以下URL：
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 執行以下命令來授予AD FS電腦上的存取權：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource`是[!DNL Microsoft Dynamics]組織URL。

1. [!DNL Microsoft Dynamics]使用HTTPS通訊協定。 若要從[!DNL Forms]伺服器叫用AD FS端點，請在執行[!DNL Experience Manager Forms]的電腦上使用`keytool`命令將[!DNL Microsoft Dynamics]站台憑證安裝到Java憑證存放區。

## 設定您[!DNL Microsoft Dynamics]服務的雲端服務 {#configure-cloud-service-for-your-microsoft-dynamics-service}

OData服務由其服務根URL識別。 若要以[!DNL Experience Manager]as a Cloud Service設定OData服務，請確定您有服務的服務根URL，並執行下列動作：

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>如需設定[!DNL Microsoft Dynamics 365] （線上或內部部署）的逐步指南，請參閱[[!DNL Microsoft Dynamics] OData設定](ms-dynamics-odata-configuration.md)。

1. 移至&#x200B;**[!UICONTROL 工具>Cloud Service>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。 指定組態的名稱與標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL OData服務]**，選擇性地瀏覽並選取組態的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。
在**[!UICONTROL 驗證設定]**&#x200B;索引標籤中：

   1. 輸入&#x200B;**[!UICONTROL 服務根]**&#x200B;欄位的值。 移至Dynamics執行個體並導覽至&#x200B;**[!UICONTROL 開發人員資源]**，以檢視[服務根目錄]欄位的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 選取&#x200B;**[!UICONTROL OAuth 2.0]**&#x200B;做為驗證型別。

   1. 將&#x200B;**[!UICONTROL 使用者端識別碼]** （也稱為&#x200B;**應用程式識別碼**）、**[!UICONTROL 使用者端密碼]**、**[!UICONTROL OAuth URL]**、**[!UICONTROL 重新整理權杖URL]**、**[!UICONTROL 存取權杖URL]**&#x200B;和&#x200B;**[!UICONTROL 資源]**&#x200B;欄位中的預設值，取代為您從[!DNL Microsoft Dynamics]服務設定中取得的值。 必須在&#x200B;**[!UICONTROL 資源]**&#x200B;欄位中指定動態執行個體URL，才能使用表單資料模型(FDM)設定[!DNL Microsoft Dynamics]。 使用服務根URL衍生動態執行個體URL。 例如，[https://org.crm.dynamics.com](https://org.crm.dynamics.com/)。

   1. 在&#x200B;**[!UICONTROL 授權範圍]**&#x200B;欄位中指定&#x200B;**[!UICONTROL openid]**，以便在[!DNL Microsoft Dynamics]上進行授權程式。

      ![驗證設定](assets/dynamics_authentication_settings_new.png)
表單資料模型(FDM)
1. 按一下&#x200B;**[!UICONTROL 連線至OAuth]**。 您被重新導向到[!DNL Microsoft Dynamics]登入頁面。
1. 使用您的[!DNL Microsoft Dynamics]認證登入，並接受允許雲端服務設定連線到[!DNL Microsoft Dynamics]服務。 建立表單資料模型(FDM) 、雲端服務和服務是一次性工作。

   您是雲端服務設定頁面的表單資料模型，此頁面會顯示OData設定已成功儲存的訊息。

MS Dynamics ODataCloud Service（OData服務）雲端服務已設定，並已與您的Dynamics服務連線。 表單資料模型(FDM)

## 建立表單資料模型(FDM) {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

設定MS Dynamics OData雲端服務後，您可以在建立表單資料模型(FDM)時使用此服務。 如需詳細資訊，請參閱[建立表單資料模型(FDM)](create-form-data-models.md)。

接下來，您可以建立最適化表單式表單資料模型(FDM)，並用於各種最適化表單使用案例，例如：

* 透過查詢[!DNL Microsoft Dynamics]實體和服務中的資訊預填調適型表單
* 使用最適化表單規則叫用表單資料模型(FDM)中定義的[!DNL Microsoft Dynamics]伺服器作業
* 將提交的表單資料寫入[!DNL Microsoft Dynamics]個實體

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

您可以[為最適化表單](/help/forms/using-form-data-model.md)設定表單資料模型提交動作，以將資料傳送至Microsoft Dynamics OData。

如需在業務工作流程中建立和使用表單資料模型(FDM)的詳細資訊，請參閱[資料整合](data-integration.md)。

## 相關文章

{{af-submit-action}}
