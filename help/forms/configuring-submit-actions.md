---
title: 如何設定最適化表單的提交動作
description: 適用性表單提供多個提交動作。 「提交動作」可定義提交後最適化表單的處理方式。 您可以使用內建的提交動作，或建立自己的動作。
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 6a124b476b4dd18ea38d35438866a07958918461
workflow-type: tm+mt
source-wordcount: '3131'
ht-degree: 2%

---

# 適用性表單提交動作 {#configuring-the-submit-action}

使用者按一下 **[!UICONTROL 提交]** 按鈕。 適用性Forms提供一些立即可用的提交動作。 可用的「提交動作」為：

* [提交到REST端點](#submit-to-rest-endpoint)
* [傳送電子郵件](#send-email)
* [使用表單資料模型提交](#submit-using-form-data-model)
* [叫用AEM工作流程](#invoke-an-aem-workflow)
* [提交至 SharePoint](#submit-to-sharedrive)
* [提交至 OneDrive](#submit-to-onedrive)
* [提交到 Azure Blob 儲存體](#azure-blob-storage)

您也可以 [擴展預設的提交操作](custom-submit-action-form.md) 來建立自己的提交動作。

您可以在 **[!UICONTROL 提交]** 區段（位於側邊欄中）。

![配置提交操作](assets/submission.png)


<!-- [!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it. -->

<!--

>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.


-->

## 提交到REST端點 {#submit-to-rest-endpoint}

使用 **[!UICONTROL 提交到REST端點]** 動作，將提交的資料張貼至其餘URL。 URL可以是內部（轉譯表單的伺服器）或外部伺服器。

若要將資料發佈至內部伺服器，請提供資源的路徑。 資料會發佈在資源的路徑上。 例如/content/restEndPoint。 對於這些帖子請求，使用提交請求的驗證資訊。

若要將資料發佈至外部伺服器，請提供URL。 URL的格式為 `https://host:port/path_to_rest_end_point`. 請確定您已設定以匿名方式處理POST要求的路徑。

![以感謝頁面參數傳遞之欄位值的對應](assets/post-enabled-actionconfig.png)

在上述範例中，使用者在 `textbox` 使用參數擷取 `param1`. 用於發佈使用 `param1` 為：

`String data=request.getParameter("param1");`

同樣地，用於發佈XML資料和附件的參數也是 `dataXml` 和 `attachments`.

例如，在指令碼中使用這兩個參數可將資料剖析至余下的端點。 您使用下列語法來儲存和剖析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此範例中， `data` 儲存XML資料，並 `att` 儲存附件資料。

此 **[!UICONTROL 提交到REST端點]** 提交動作會將表單中填入的資料提交至已設定的確認頁面，作為HTTPGET請求的一部分。 您可以新增要請求的欄位名稱。 請求的格式為：

`{fieldName}={request parameter name}`

如下圖所示， `param1` 和 `param2` 會以參數的形式傳遞，且值會從 **textbox** 和 **數字框** 欄位供下一個動作使用。

![配置Rest端點提交操作](assets/action-config.png)

您也可以 **[!UICONTROL 啟用POST請求]** 和提供要求張貼的URL。 若要將資料提交至托管表單的AEM伺服器，請使用與AEM伺服器的根路徑相對應的相對路徑。 例如， `/content/forms/af/SampleForm.html`. 要向任何其他伺服器提交資料，請使用絕對路徑。

>[!NOTE]
>
>若要在REST URL中以參數形式傳遞欄位，所有欄位都必須有不同的元素名稱，即使欄位放在不同面板上亦然。

## 傳送電子郵件 {#send-email}

您可以使用 **[!UICONTROL 傳送電子郵件]** 提交動作，以便在成功提交表單時傳送電子郵件給一或多個收件者。 產生的電子郵件可包含預先定義格式的表單資料。 例如，在下列範本中，會從提交的表單資料中擷取客戶名稱、運送地址、狀態名稱和郵遞區號。

    &quot;
    
    您是${customer_Name},
    
    以下是預設發運地址：
    ${customer_name},
    ${customer_Shipping_Address},
    ${customer_state},
    ${customer_ZIPCode}
    
    請注意，
    WKND
    
    &quot;

>[!NOTE]
>
> * 所有表單欄位必須具有不同的元素名稱，即使欄位放置在適用性表單的不同面板上亦然。
> * AEMas a Cloud Service需要加密傳出郵件。 依預設，會停用傳出電子郵件。 若要啟用支援，請提交支援票證至 [請求存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


您也可以將附件和記錄檔案(DoR)包含在電子郵件中。 啟用 **[!UICONTROL 附加記錄檔案]** 選項，配置適用性表單以生成記錄文檔(DoR)。 您可以啟用從適用性表單屬性產生記錄檔案的選項。



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## 使用表單資料模型提交 {#submit-using-form-data-model}

此 **[!UICONTROL 使用表單資料模型提交]** 「提交動作」會將表單資料模型中指定資料模型物件的已提交適用性表單資料寫入其資料來源。 在配置「提交操作」時，您可以選擇資料模型對象，其提交的資料要寫回其資料源。

此外，您可以使用「表單資料模型」和「記錄檔案(DoR)」將表單附件提交到資料源。 如需表單資料模型的相關資訊，請參閱 [[!DNL AEM Forms] 資料整合](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## 叫用AEM工作流程 {#invoke-an-aem-workflow}

此 **[!UICONTROL 叫用AEM工作流程]** 「提交動作」會將適用性表單與 [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). 提交表單時，相關的工作流程會自動在製作執行個體上啟動。 您可以將資料檔案、附件和記錄檔案儲存至工作流程的裝載位置或變數。 如果將工作流程標示為外部資料儲存，並設定為外部資料儲存，則只有變數選項可用。 您可以從工作流模型可用的變數清單中選取。 如果工作流程在稍後階段標示為外部資料儲存，而不是在建立工作流程時，請確定已備妥必要的變數設定。

「提交動作」會將下列項目放置在工作流程的裝載位置，或如果工作流程已標示為外部資料儲存，則會放置變數：

* **資料檔案**:其中包含提交至最適化表單的資料。 您可以使用 **[!UICONTROL 資料檔案路徑]** 選項，指定檔案的名稱和相對於裝載的檔案路徑。 例如， `/addresschange/data.xml` 路徑會建立名為 `addresschange` 並將其與有效負載相對。 您也可以僅指定 `data.xml` 僅傳送已提交的資料而不建立資料夾階層。 如果工作流程已標籤為外部資料儲存，請使用變數選項，然後從可用於工作流模型的變數清單中選取變數。

* **附件**:您可以使用 **[!UICONTROL 附件路徑]** 選項，指定要儲存上傳至適用性表單的附件的資料夾名稱。 資料夾會依據裝載建立。 如果工作流程已標籤為外部資料儲存，請使用變數選項，然後從可用於工作流模型的變數清單中選取變數。

* **記錄檔案**:它包含為最適化表單產生的記錄檔案。 您可以使用 **[!UICONTROL 記錄路徑文檔]** 選項，指定記錄檔案的檔案名稱和與裝載相關的檔案路徑。 例如， `/addresschange/DoR.pdf` 路徑會建立名為 `addresschange` 相對於裝載，並將 `DoR.pdf` 相對於裝載。 您也可以僅指定 `DoR.pdf` 僅保存記錄文檔而不建立資料夾層次結構。 如果工作流程已標籤為外部資料儲存，請使用變數選項，然後從可用於工作流模型的變數清單中選取變數。

使用 **[!UICONTROL 叫用AEM工作流程]** 提交動作會為 **[!UICONTROL AEM DS設定服務]** 配置：

* **[!UICONTROL 處理伺服器URL]**:處理伺服器是觸發Forms或AEM工作流程的伺服器。 這可以與AEM製作執行個體或其他伺服器的URL相同。

* **[!UICONTROL 處理伺服器用戶名]**:工作流程使用者的使用者名稱

* **[!UICONTROL 處理伺服器密碼]**:工作流用戶密碼

## 提交至 SharePoint {#submit-to-sharedrive}

此 **[!UICONTROL 提交至SharePoint]** 「提交動作」會將適用性表單與Microsoft SharePoint儲存空間連結。 您可以將表單資料檔案、附件或記錄檔案提交到連接的Microsoft Sharepoint儲存。 若要使用 **[!UICONTROL 提交至SharePoint]** 以最適化表單提交動作：

1. [建立SharePoint設定](#create-a-sharepoint-configuration-create-sharepoint-configuration):它將AEM Forms連接到您的Microsoft Sharepoint儲存。
2. [在適用性表單中使用提交至SharePoint提交動作](#use-sharepoint-configuartion-in-af):它會將您的適用性表單連結至設定的Microsoft SharePoint。

### 建立SharePoint設定 {#create-sharepoint-configuration}

將AEM Forms連接到您的Microsoft Sharepoint儲存：

1. 前往 **AEM Forms作者** 例項> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL MicrosoftSharePoint]**.
1. 選取 **[!UICONTROL MicrosoftSharePoint]**，您會被重新導向至 **[!UICONTROL SharePoint瀏覽器]**.
1. 選取 **組態容器**. 配置儲存在選定的配置容器中。
1. 按一下&#x200B;**[!UICONTROL 建立]**。SharePoint設定精靈隨即出現。
   ![Sharepoint配置](/help/forms/assets/sharepoint_configuration.png)
1. 指定 **[!UICONTROL 標題]**, **[!UICONTROL 用戶端ID]**, **[!UICONTROL 用戶端密碼]** 和 **[!UICONTROL OAuth URL]**. 如需如何擷取用戶端ID、用戶端密碼、OAuth URL的租用戶ID的相關資訊，請參閱 [Microsoft檔案](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * 您可以擷取 `Client ID` 和 `Client Secret` 從Microsoft Azure入口網站取得。
   * 在Microsoft Azure入口網站中，將重新導向URI新增為 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. 取代 `[author-instance]` 搭配您Author例項的URL。
   * 新增API權限 `offline_access` 和 `Sites.Manage.All` 提供讀/寫權限。
   * 使用OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. 取代 `<tenant-id>` 和 `tenant-id` 從Microsoft Azure入口網站取得。

   >[!NOTE]
   >
   > 此 **用戶密碼** 欄位為必填或選填，取決於您的Azure Active Directory應用程式配置。 如果您的應用程式設定為使用用戶端密碼，則必須提供用戶端密碼。

1. 按一下 **[!UICONTROL Connect]**. 在成功連線上， `Connection Successful` 訊息。

1. 現在，請選取 **SharePoint網站** > **檔案庫** > **SharePoint資料夾**，以儲存資料。

   >[!NOTE]
   >
   >* 依預設， `forms-ootb-storage-adaptive-forms-submission` 存在於選取的SharePoint網站。
   >* 將資料夾建立為 `forms-ootb-storage-adaptive-forms-submission`，如果尚未出現在 `Documents` 儲存庫，方法是按一下 **建立資料夾**.


現在，您可以在適用性表單中使用此SharePoint Sites設定進行提交動作。

### 在最適化表單中使用SharePoint設定 {#use-sharepoint-configuartion-in-af}

您可以在適用性表單中使用建立的SharePoint設定，將資料或產生的記錄檔案儲存至SharePoint資料夾。 執行下列步驟，在適用性表單中將SharePoint儲存設定使用為：
1. 建立 [適用性表單](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * 選取相同 [!UICONTROL 組態容器] 適用於您已建立SharePoint儲存空間的適用性表單。
   > * 若否 [!UICONTROL 組態容器] ，則全域 [!UICONTROL 儲存配置] 資料夾會顯示在「提交操作」屬性窗口中。


1. 選擇 **提交動作** as **[!UICONTROL 提交至SharePoint]**.
   ![SharepointGIF](/help/forms/assets/sharedrive-video.gif)
1. 選取 **[!UICONTROL 儲存配置]**，即可儲存資料。
1. 按一下 **[!UICONTROL 儲存]** 以儲存「提交」設定。

提交表單時，資料將保存在指定的Microsoft Sharepoint儲存中。
要儲存資料的資料夾結構為 `/folder_name/form_name/year/month/date/submission_id/data`.

## 提交至 OneDrive {#submit-to-onedrive}

此 **[!UICONTROL 提交到OneDrive]** 「提交動作」會將適用性表單與Microsoft OneDrive連線。 您可以將表單資料、檔案、附件或記錄檔案提交到連接的Microsoft OneDrive儲存。 若要使用 [!UICONTROL 提交到OneDrive] 以最適化表單提交動作：

1. [建立OneDrive配置](#create-a-onedrive-configuration-create-onedrive-configuration):它會將AEM Forms連接到您的Microsoft OneDrive儲存。
2. [在適用性表單中使用「提交至OneDrive」提交操作](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af):它會將您的適用性表單連結至設定的Microsoft OneDrive。

### 建立OneDrive配置 {#create-onedrice-configuration}

將AEM Forms連接到您的Microsoft OneDrive儲存：

1. 前往 **AEM Forms作者** 例項> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft OneDrive]**.
1. 選取 **[!UICONTROL Microsoft OneDrive]**，您會被重新導向至 **[!UICONTROL OneDrive瀏覽器]**.
1. 選取 **組態容器**. 配置儲存在選定的配置容器中。
1. 按一下&#x200B;**[!UICONTROL 建立]**。出現OneDrive配置嚮導。

   ![OneDrive配置螢幕](/help/forms/assets/onedrive-configuration.png)

1. 指定 **[!UICONTROL 標題]**, **[!UICONTROL 用戶端ID]**, **[!UICONTROL 用戶端密碼]** 和 **[!UICONTROL OAuth URL]**. 如需如何擷取用戶端ID、用戶端密碼、OAuth URL的租用戶ID的相關資訊，請參閱 [Microsoft檔案](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * 您可以擷取 `Client ID` 和 `Client Secret` 從Microsoft Azure入口網站取得。
   * 在Microsoft Azure入口網站中，將重新導向URI新增為 `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. 取代 `[author-instance]` 搭配您Author例項的URL。
   * 新增API權限 `offline_access` 和 `Files.ReadWrite.All` 提供讀/寫權限。
   * 使用OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. 取代 `<tenant-id>` 和 `tenant-id` 從Microsoft Azure入口網站取得。

   >[!NOTE]
   >
   > 此 **用戶密碼** 欄位為必填或選填，取決於您的Azure Active Directory應用程式配置。 如果您的應用程式設定為使用用戶端密碼，則必須提供用戶端密碼。

1. 按一下 **[!UICONTROL Connect]**. 在成功連線上， `Connection Successful` 訊息。

1. 現在，請選取 **[!UICONTROL OneDrive容器]** > **[OneDrive資料夾]**  來儲存資料。

   >[!NOTE]
   >
   >* 依預設， `forms-ootb-storage-adaptive-forms-submission` 存在於OneDrive容器中。
   > * 將資料夾建立為 `forms-ootb-storage-adaptive-forms-submission`，如果尚未存在，請按一下 **建立資料夾**.


現在，您可以在適用性表單中將此OneDrive儲存配置用於提交操作。

### 在最適化表單中使用OneDrive配置 {#use-onedrive-configuartion-in-af}

您可以在適用性表單中使用建立的OneDrive儲存配置，將資料或生成的記錄文檔保存到OneDrive資料夾中。 執行以下步驟以在適用性表單中使用OneDrive儲存配置：
1. 建立 [適用性表單](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * 選取相同 [!UICONTROL 組態容器] 適用於已建立OneDrive儲存的適用性表單。
   > * 若否 [!UICONTROL 組態容器] ，則全域 [!UICONTROL 儲存配置] 資料夾會顯示在「提交操作」屬性窗口中。


1. 選擇 **提交動作** as **[!UICONTROL 提交到OneDrive]**.
   ![OneDriveGIF](/help/forms/assets/onedrive-video.gif)
1. 選取 **[!UICONTROL 儲存配置]**，即可儲存資料。
1. 按一下 **[!UICONTROL 儲存]** 以儲存「提交」設定。

提交表單時，資料將保存在指定的Microsoft OneDrive儲存中。
要儲存資料的資料夾結構為 `/folder_name/form_name/year/month/date/submission_id/data`.

## 提交到 Azure Blob 儲存體 {#submit-to-azure-blob-storage}

此 **[!UICONTROL 提交至Azure Blob儲存]**  「提交動作」會將適用性表單與Microsoft Azure入口網站連線。 您可以將表單資料、檔案、附件或記錄檔案提交到連接的Azure儲存容器。 要使用Azure Blob儲存的提交操作：

1. [建立Azure Blob儲存容器](#create-a-azure-blob-storage-container-create-azure-configuration):它會將AEM Forms連接至Azure儲存容器。
2. [在最適化表單中使用Azure儲存配置 ](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af):它會將您的適用性表單連接至設定的Azure儲存容器。

### 建立Azure Blob儲存容器 {#create-azure-configuration}

將AEM Forms連接到Azure儲存容器：
1. 前往 **AEM Forms作者** 例項> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Azure儲存]**.
1. 選取 **[!UICONTROL Azure儲存]**，您會被重新導向至 **[!UICONTROL Azure儲存瀏覽器]**.
1. 選取 **組態容器**. 配置儲存在選定的配置容器中。
1. 按一下&#x200B;**[!UICONTROL 建立]**。出現「Create Azure Storage Configuration（建立Azure儲存配置）」嚮導。

   ![Azure儲存配置](/help/forms/assets/azure-storage-configuration.png)

1. 指定 **[!UICONTROL 標題]**, **[!UICONTROL Azure儲存帳戶]** 和 **[!UICONTROL Azure訪問密鑰]**.

   * 您可以擷取 `Azure Storage Account` 名稱和 `Azure Access key` 從Microsoft Azure入口網站的儲存帳戶。

1. 按一下「**[!UICONTROL 儲存]**」。

現在，您可以在適用性表單中將此Azure儲存容器設定用於提交動作。

### 在最適化表單中使用Azure儲存配置 {#use-azure-storage-configuartion-in-af}

您可以在適用性表單中使用已建立的Azure儲存容器配置，在Azure儲存容器中保存資料或生成的記錄文檔。 執行下列步驟以在適用性表單中使用Azure儲存容器配置：
1. 建立 [適用性表單](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * 選取相同 [!UICONTROL 組態容器] 適用於已建立OneDrive儲存的適用性表單。
   > * 若否 [!UICONTROL 組態容器] ，則全域 [!UICONTROL 儲存配置] 資料夾會顯示在「提交操作」屬性窗口中。


1. 選擇 **提交動作** as **[!UICONTROL 提交至Azure Blob儲存]**.
   ![Azure Blob儲存GIF](/help/forms/assets/azure-submit-video.gif)

1. 選取 **[!UICONTROL 儲存配置]**，即可儲存資料。
1. 按一下 **[!UICONTROL 儲存]** 以儲存「提交」設定。

提交表單時，資料將保存在指定的Azure儲存容器配置中。
要儲存資料的資料夾結構為 `/configuration_container/form_name/year/month/date/submission_id/data`.

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。

## 使用同步或非同步提交 {#use-synchronous-or-asynchronous-submission}

提交動作可使用同步或非同步提交。

**同步提交**:傳統上，網路表單的設定是同步提交。 在同步提交中，當使用者提交表單時，系統會將他們重新導向至確認頁面、感謝頁面，或如果提交失敗，則會導致錯誤頁面。 您可以選取 **[!UICONTROL 使用非同步提交]** 選項，將使用者重新導向至網頁或在提交時顯示訊息。

![配置提交操作](assets/thank-you-setting.png)

**非同步提交**:單頁應用程式等現代化網頁體驗正日益普及，當用戶端與伺服器互動於背景時，網頁會維持靜態。 您現在可以透過適用性Forms提供此體驗，方法為 [配置非同步提交](asynchronous-submissions-adaptive-forms.md).

## 適用性表單中的伺服器端重新驗證 {#server-side-revalidation-in-adaptive-form}

通常，在任何線上資料擷取系統中，開發人員會在用戶端放置一些JavaScript驗證，以強制執行一些業務規則。 但在現代瀏覽器中，一般使用者可以略過這些驗證，並使用各種技術（例如網頁瀏覽器DevTools主控台）手動執行提交作業。 此類技術對適用性Forms也有效。 表單開發人員可以建立各種驗證邏輯，但技術上，一般使用者可以略過這些驗證邏輯，並將無效資料提交至伺服器。 無效資料會破壞表單作者已強制執行的業務規則。

伺服器端重新驗證功能也可執行Adaptive Forms作者在伺服器上設計Adaptive Form時提供的驗證。 它可防止表單驗證中呈現的資料提交和業務規則違反行為受到任何可能的影響。

### 要在伺服器上驗證什麼？ {#what-to-validate-on-server-br}

伺服器上重新執行的適用性表單的現成可用(OOTB)欄位驗證包括：

* 必要
* 驗證子句
* 驗證運算式

### 啟用伺服器端驗證 {#enabling-server-side-validation-br}

使用 **[!UICONTROL 在伺服器上重新驗證]** 在側邊欄的適用性表單容器下，啟用或停用目前表單的伺服器端驗證。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果最終用戶繞過這些驗證並提交表單，伺服器將再次執行驗證。 如果驗證在伺服器端失敗，則提交交易會停止。 最終用戶將再次顯示原始表單。 擷取的資料和提交的資料會以錯誤形式呈現給使用者。

>[!NOTE]
>
>伺服器端驗證會驗證表單模型。 建議您建立個別的用戶端程式庫以進行驗證，但不要在相同的用戶端程式庫中混合使用HTML樣式和DOM操作等其他項目。

### 支援驗證運算式中的自訂函式 {#supporting-custom-functions-in-validation-expressions-br}

有時，如果 **複雜驗證規則**，完全驗證指令碼位於自訂函式中，而作者會從欄位驗證運算式呼叫這些自訂函式。 若要讓此自訂函式程式庫在執行伺服器端驗證時已知且可供使用，表單作者可在 **[!UICONTROL 基本]** 標籤，如下所示。

![支援驗證運算式中的自訂函式](assets/clientlib-cat.png)

支援驗證運算式中的自訂函式

作者可以根據最適化表單設定customJavaScript程式庫。 在程式庫中，僅保留可重複使用的函式，這些函式依存於jquery和underscore.js協力廠商程式庫。

## 提交操作的錯誤處理 {#error-handling-on-submit-action}

作為AEM安全性和強化准則的一部分，請配置自定義錯誤頁，如400.jsp、404.jsp和500.jsp。 提交表單400、404或500錯誤時，會呼叫這些處理常式。 在發佈節點上觸發這些錯誤代碼時，也會呼叫處理常式。 您也可以為其他HTTP錯誤代碼建立JSP頁。

當您預先填入表單資料模型，或使用XML或JSON資料抱怨的結構式適用性表單，針對的資料不包含的結構式 `<afData>`, `<afBoundData>`，和 `</afUnboundData>` 標籤，則適用性表單的無界欄位資料會遺失。 結構可以是XML結構、JSON結構或表單資料模型。 無界欄位是適用性表單欄位，沒有 `bindref` 屬性。

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
