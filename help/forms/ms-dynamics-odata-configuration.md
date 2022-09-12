---
title: 如何配置 [!DNL Microsoft Dynamics] OData?
description: 了解如何根據 [!DNL Microsoft Dynamics] 服務。 表單資料模型可用來建立與互動的適用性Forms [!DNL Microsoft Dynamics] 伺服器啟用業務工作流程。
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

[!DNL Microsoft Dynamics] 是客戶關係管理(CRM)和企業資源規劃(ERP)軟體，它提供企業解決方案，用於建立和管理客戶帳戶、聯繫人、銷售機會、銷售機會和案例。 [[!DNL Experience Manager Forms] 資料整合](data-integration.md) 提供OData雲服務配置，以將Forms與線上和本地整合 [!DNL Microsoft Dynamics] 伺服器。 它可讓您根據中定義的實體、屬性和服務來建立表單資料模型 [!DNL Microsoft Dynamics] 服務。 表單資料模型可用來建立與互動的適用性Forms [!DNL Microsoft Dynamics] 伺服器啟用業務工作流程。 例如：

* 查詢 [!DNL Microsoft Dynamics] 資料伺服器並預先填入Adaptive Forms
* 將資料寫入 [!DNL Microsoft Dynamics] 適用性表單提交
* 將資料寫入 [!DNL Microsoft Dynamics] 透過表單資料模型中定義的自訂實體，反之亦然

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  MS Dynamics OData Cloud Service (OData Service) is available with all run modes. For more information on configuring run modes for an [!DNL Experience Manager] instance, see [Run Modes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#runmodes).

## 必備條件 {#prerequisites}

開始設定和配置之前 [!DNL Microsoft Dynamics]，請確定您有：

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* 已配置 [!DNL Microsoft Dynamics] 365聯機或安裝了以下實例之一 [!DNL Microsoft Dynamics] 版本：

   * [!DNL Microsoft Dynamics] 365個內部部署
   * [!DNL Microsoft Dynamics] 2016年內部部署

* [註冊申請 [!DNL Microsoft Dynamics] 線上服務 [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). 記下註冊服務的用戶端ID（也稱為應用程式ID）和用戶端密碼的值。 這些值會在 [配置雲服務 [!DNL Microsoft Dynamics] 服務](#configure-cloud-service-for-your-microsoft-dynamics-service).

## 設定已註冊的回復URL [!DNL Microsoft Dynamics] 應用程式 {#set-reply-url-for-registered-microsoft-dynamics-application}

請執行以下操作來設定已註冊的回復URL [!DNL Microsoft Dynamics] 應用程式：

>[!NOTE]
>
>只有在整合時才使用此程式 [!DNL Experience Manager Forms] 線上 [!DNL Microsoft Dynamics] 伺服器。

1. 前往 [!DNL Microsoft Azure] Active Directory帳戶，並在 **[!UICONTROL 回覆URL]** 註冊應用程式的設定：

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 儲存設定。

## 設定 [!DNL Microsoft Dynamics] IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] 使用基於聲明的身份驗證提供對資料的訪問 [!DNL Microsoft Dynamics] CRM伺服器傳送給外部使用者。 若要啟用此功能，請執行下列動作以設定 [!DNL Microsoft Dynamics] 用於面向網際網路的部署(IFD)並配置聲明設定。

>[!NOTE]
>
>只有在整合時才使用此程式 [!DNL Experience Manager Forms] 內部 [!DNL Microsoft Dynamics] 伺服器。

1. 設定 [!DNL Microsoft Dynamics] IFD的本地實例，如 [為配置IFD [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. 使用Windows PowerShell運行以下命令，在啟用IFD時配置聲明設定 [!DNL Microsoft Dynamics]:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   請參閱 [CRM內部部署(IFD)的應用程式註冊](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 以取得詳細資訊。

## 在AD FS電腦上配置OAuth客戶端 {#configure-oauth-client-on-ad-fs-machine}

執行以下操作以在Active Directory聯合身份驗證服務(AD FS)電腦上註冊OAuth客戶端，並在AD FS電腦上授予訪問權：

>[!NOTE]
>
>只有在整合時才使用此程式 [!DNL Experience Manager Forms] 內部 [!DNL Microsoft Dynamics] 伺服器。

1. 執行下列命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是可使用任何GUID產生器產生的用戶端ID。
   * `redirect-uri` 是 [!DNL Microsoft Dynamics] OData雲服務開啟 [!DNL Experience Manager Forms]. 隨 [!DNL Experience Manager Forms] 部署於下列URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 運行以下命令以授予AD FS電腦上的訪問權：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是 [!DNL Microsoft Dynamics] 組織URL。

1. [!DNL Microsoft Dynamics] 使用HTTPS通訊協定。 從調用AD FS端點 [!DNL Forms] 伺服器，安裝 [!DNL Microsoft Dynamics] 網站憑證存放區(使用 `keytool` 命令 [!DNL Experience Manager Forms].

## 為您的 [!DNL Microsoft Dynamics] 服務 {#configure-cloud-service-for-your-microsoft-dynamics-service}

OData服務由其服務根URL識別。 若要在 [!DNL Experience Manager] as a Cloud Service，請確定您有服務的服務根URL，並執行下列操作：

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>設定的逐步指南 [!DNL Microsoft Dynamics 365]、線上或內部部署，請參閱 [[!DNL Microsoft Dynamics] OData配置](ms-dynamics-odata-configuration.md).

1. 前往 **[!UICONTROL 工具>Cloud Services>資料來源]**. 點選以選取您要建立雲端設定的資料夾。

   請參閱 [配置雲端服務配置的資料夾](#cloud-folder) 如需建立和設定雲端服務設定資料夾的相關資訊。

1. 點選 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**. 指定配置的名稱和（可選）標題，選擇 **[!UICONTROL OData服務]** 從 **[!UICONTROL 服務類型]** 下拉式清單，（可選）瀏覽並選取設定的縮圖影像，然後點選 **[!UICONTROL 下一個]**.
在 **[!UICONTROL 驗證設定]** 標籤：

   1. 輸入 **[!UICONTROL 服務根]** 欄位。 前往Dynamics例項，並導覽至 **[!UICONTROL 開發人員資源]** 查看「服務根」欄位的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 選擇 **[!UICONTROL OAuth 2.0]** 作為驗證類型。

   1. 取代 **[!UICONTROL 用戶端ID]** (又稱為 **應用程式ID**), **[!UICONTROL 用戶端密碼]**, **[!UICONTROL OAuth URL]**, **[!UICONTROL 重新整理Token URL]**, **[!UICONTROL 存取權杖URL]**，和 **[!UICONTROL 資源]** 的 [!DNL Microsoft Dynamics] 服務設定。 必須在 **[!UICONTROL 資源]** 配置欄位 [!DNL Microsoft Dynamics] 表單資料模型。 使用服務根URL來衍生Dynamics實例URL。 例如， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. 指定 **[!UICONTROL openid]** 在 **[!UICONTROL 授權範圍]** 授權處理的欄位 [!DNL Microsoft Dynamics].

      ![驗證設定](assets/dynamics_authentication_settings_new.png)
表單資料模型
1. 按一下 **[!UICONTROL 連線至OAuth]**. 系統會將您重新導向至 [!DNL Microsoft Dynamics] 登入頁面。
1. 使用 [!DNL Microsoft Dynamics] 憑證並接受，以允許雲端服務設定連線至 [!DNL Microsoft Dynamics] 服務。 在雲服務和雲服務之間建立表單資料模型是一項一次性的任務。

   您是雲服務配置頁面的「表單資料模型」，該頁面顯示已成功保存OData配置的消息。

MS Dynamics ODataCloud Service（OData服務）雲服務已配置並與Dynamics服務連接。 表單資料模型表單資料模型

## 建立表單資料模型 {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

配置MS Dynamics OData Cloud用戶表單資料模型(ce)雲服務後，您可以在建立表單資料模型時使用該服務。 如需詳細資訊，請參閱 [建立表單資料模型](create-form-data-models.md).

接下來，您可以根據表單資料模型建立最適化表單，並在各種最適化表單使用案例中使用，例如：

* 查詢資訊以預填適用性表單 [!DNL Microsoft Dynamics] 實體和服務
* 叫用 [!DNL Microsoft Dynamics] 使用適用性表單規則在表單資料模型中定義的伺服器操作
* 將提交的表單資料寫入 [!DNL Microsoft Dynamics] 實體

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

如需在業務工作流程中建立和使用表單資料模型的詳細資訊，請參閱 [資料整合](data-integration.md).
