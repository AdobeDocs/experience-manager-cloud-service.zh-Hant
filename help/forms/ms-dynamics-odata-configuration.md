---
title: 如何配置 [!DNL Microsoft Dynamics] OData?
description: 瞭解如何基於中定義的實體、屬性和服務建立表單資料模型 [!DNL Microsoft Dynamics] 服務。 表單資料模型可用於建立與交互的自適應Forms [!DNL Microsoft Dynamics] 伺服器以啟用業務工作流。
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 1%

---

# [!DNL Microsoft Dynamics] OData配置 {#microsoft-dynamics-odata-configuration}

![資料整合](assets/data-integeration.png)

[!DNL Microsoft Dynamics] 是一種客戶關係管理(CRM)和企業資源規劃(ERP)軟體，它為建立和管理客戶帳戶、聯繫人、銷售線索、業務機會和案例提供企業解決方案。 [[!DNL Experience Manager Forms] 資料整合](data-integration.md) 提供OData雲服務配置，將Forms與線上和本地整合 [!DNL Microsoft Dynamics] 伺服器。 它使您能夠根據在中定義的實體、屬性和服務建立表單資料模型 [!DNL Microsoft Dynamics] 服務。 表單資料模型可用於建立與交互的自適應Forms [!DNL Microsoft Dynamics] 伺服器以啟用業務工作流。 例如：

* 查詢 [!DNL Microsoft Dynamics] 用於資料和預填充的伺服器，AdaptiveForms
* 將資料寫入 [!DNL Microsoft Dynamics] 關於自適應表單提交
* 將資料寫入 [!DNL Microsoft Dynamics] 通過在表單資料模型中定義的自定義圖元，反之亦然

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  MS Dynamics OData Cloud Service (OData Service) is available with all run modes. For more information on configuring run modes for an [!DNL Experience Manager] instance, see [Run Modes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#runmodes).

## 必備條件 {#prerequisites}

開始設定和配置之前 [!DNL Microsoft Dynamics]，確保您有：

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* 已配置 [!DNL Microsoft Dynamics] 365聯機或安裝了以下實例之一 [!DNL Microsoft Dynamics] 版本：

   * [!DNL Microsoft Dynamics] 365個內部部署
   * [!DNL Microsoft Dynamics] 2016年內地

* [已註冊申請 [!DNL Microsoft Dynamics] 線上服務 [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)。 記下註冊服務的客戶端ID（也稱為應用程式ID）和客戶端機密的值。 在 [配置雲服務 [!DNL Microsoft Dynamics] 服務](#configure-cloud-service-for-your-microsoft-dynamics-service)。

## 設定已註冊的回復URL [!DNL Microsoft Dynamics] 應用 {#set-reply-url-for-registered-microsoft-dynamics-application}

執行以下操作以設定已註冊的回復URL [!DNL Microsoft Dynamics] 應用程式：

>[!NOTE]
>
>僅在整合時使用此過程 [!DNL Experience Manager Forms] 線上 [!DNL Microsoft Dynamics] 伺服器。

1. 轉到 [!DNL Microsoft Azure] Active Directory帳戶，並在中添加以下雲服務配置URL **[!UICONTROL 答復URL]** 註冊應用程式的設定：

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 儲存設定。

## 配置 [!DNL Microsoft Dynamics] IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] 使用基於聲明的身份驗證提供對資料的訪問 [!DNL Microsoft Dynamics] CRM伺服器到外部用戶。 要啟用此功能，請執行以下操作來配置 [!DNL Microsoft Dynamics] 用於面向Internet的部署(IFD)並配置聲明設定。

>[!NOTE]
>
>僅在整合時使用此過程 [!DNL Experience Manager Forms] 內部 [!DNL Microsoft Dynamics] 伺服器。

1. 配置 [!DNL Microsoft Dynamics] IFD的本地實例，如中所述 [為配置IFD [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx)。
1. 使用Windows PowerShell運行以下命令以在啟用IFD時配置聲明設定 [!DNL Microsoft Dynamics]:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   請參閱 [CRM本地(IFD)的應用程式註冊](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 的雙曲餘切值。

## 在AD FS電腦上配置OAuth客戶端 {#configure-oauth-client-on-ad-fs-machine}

執行以下操作以在Active Directory聯合身份驗證服務(AD FS)電腦上註冊OAuth客戶端並授予對AD FS電腦的訪問權限：

>[!NOTE]
>
>僅在整合時使用此過程 [!DNL Experience Manager Forms] 內部 [!DNL Microsoft Dynamics] 伺服器。

1. 運行以下命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   位置：

   * `Client-ID` 是可以使用任何GUID生成器生成的客戶端ID。
   * `redirect-uri` 是 [!DNL Microsoft Dynamics] OData雲服務 [!DNL Experience Manager Forms]。 隨安裝的預設雲服務 [!DNL Experience Manager Forms] 部署在以下URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 運行以下命令以授予對AD FS電腦的訪問權限：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   位置：

   * `resource` 是 [!DNL Microsoft Dynamics] 組織URL。

1. [!DNL Microsoft Dynamics] 使用HTTPS協定。 從調用AD FS終結點 [!DNL Forms] 伺服器，安裝 [!DNL Microsoft Dynamics] 站點證書到Java證書儲存 `keytool` 命令 [!DNL Experience Manager Forms]。

## 為您配置雲服務 [!DNL Microsoft Dynamics] 服務 {#configure-cloud-service-for-your-microsoft-dynamics-service}

OData服務由其服務根URL標識。 在中配置OData服務 [!DNL Experience Manager] as a Cloud Service，確保您有服務的根URL，並執行以下操作：

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>有關配置的逐步指南 [!DNL Microsoft Dynamics 365]，聯機或本地，請參閱 [[!DNL Microsoft Dynamics] OData配置](ms-dynamics-odata-configuration.md)。

1. 轉到 **[!UICONTROL 工具>Cloud Services>資料源]**。 點擊以選擇要在其中建立雲配置的資料夾。

   請參閱 [為雲服務配置配置資料夾](#cloud-folder) 有關為雲服務配置建立和配置資料夾的資訊。

1. 點擊 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**。 指定配置的名稱和標題（可選），選擇 **[!UICONTROL OData服務]** 從 **[!UICONTROL 服務類型]** 下拉，（可選）瀏覽並選擇配置的縮略圖，然後點擊 **[!UICONTROL 下一個]**。
在 **[!UICONTROL 驗證設定]** 頁籤：

   1. 輸入 **[!UICONTROL 服務根]** 的子菜單。 轉至Dynamics實例並導航至 **[!UICONTROL 開發人員資源]** 查看「服務根」欄位的值。 例如，https://&lt;tenant-name>/api/data/v9.1

   1. 選擇 **[!UICONTROL OAuth 2.0]** 類型。

   1. 替換 **[!UICONTROL 客戶端ID]** (亦稱： **應用程式ID**) **[!UICONTROL 客戶端密碼]**。 **[!UICONTROL OAuth URL]**。 **[!UICONTROL 刷新標籤URL]**。 **[!UICONTROL 訪問令牌URL]**, **[!UICONTROL 資源]** 從 [!DNL Microsoft Dynamics] 服務配置。 必須在 **[!UICONTROL 資源]** 欄位 [!DNL Microsoft Dynamics] 表格資料模型。 使用服務根URL可導出動態實例URL。 比如說， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/)。

   1. 指定 **[!UICONTROL openid]** 的 **[!UICONTROL 授權範圍]** 在上的授權進程欄位 [!DNL Microsoft Dynamics]。

      ![驗證設定](assets/dynamics_authentication_settings_new.png)
窗體資料模型
1. 按一下 **[!UICONTROL 連接到OAuth]**。 您被重定向到 [!DNL Microsoft Dynamics] 登錄頁。
1. 使用 [!DNL Microsoft Dynamics] 憑據，並接受允許雲服務配置連接到 [!DNL Microsoft Dynamics] 服務。 在雲服務和服務之間建立表單資料模型是一項一次性的任務。

   您是雲服務配置頁的「表單資料模型」，其中顯示OData配置已成功保存的消息。

MS Dynamics ODataCloud Service（OData服務）雲服務已配置並與您的Dynamics服務連接。 表單資料模型表單資料模型

## 建立表單資料模型 {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

配置MS Dynamics OData雲伺服器表單資料模型ce)雲服務後，可以在建立表單資料模型時使用該服務。 有關詳細資訊，請參見 [建立表單資料模型](create-form-data-models.md)。

接下來，您可以建立基於表單資料模型的自適應表單，並在各種自適應表單使用情形中使用它，例如：

* 通過從中查詢資訊來預填自適應表單 [!DNL Microsoft Dynamics] 實體及服務
* 調用 [!DNL Microsoft Dynamics] 在使用Adaptive Form規則的表單資料模型中定義的伺服器操作
* 將提交的表單資料寫入 [!DNL Microsoft Dynamics] 實體

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

有關在業務工作流中建立和使用表單資料模型的詳細資訊，請參閱 [資料整合](data-integration.md)。
