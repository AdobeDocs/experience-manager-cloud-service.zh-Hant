---
title: 如何設定最適化表單的提交動作
description: 最適化表單提供多個提交動作。 提交動作會定義在提交後如何處理最適化表單。 您可以使用內建的提交動作或建立自己的提交動作。
hide: true
hidefromtoc: true
source-git-commit: 8ac35abd1335b4e31a6dc0d8812cc9df333e69a4
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 2%

---

# 最適化表單提交動作 {#configuring-the-submit-action}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service  | 本文 |

**套用至**：✔️用最適化表單核心元件❌ [最適化表單基礎元件](/help/forms/configuring-submit-actions.md). Adobe建議使用核心元件 [將最適化Forms新增至AEM Sites頁面](create-or-add-an-adaptive-form-to-aem-sites-page.md) 或 [建立獨立的最適化Forms](creating-adaptive-form-core-components.md).

提交動作可讓您選擇透過最適化表單擷取的資料目的地。 當使用者按一下 **[!UICONTROL 提交]** 最適化表單上的按鈕。

Formsas a Cloud Service適用於建置在核心元件上的最適化Forms，提供一系列預先建置的提交動作。 這些現成的提交動作可讓您：

* 透過電子郵件輕鬆傳送表單資料。
* 在傳輸資料時啟動Microsoft Power Automate流程或AEM Workflow。
* 直接將表單資料傳輸至Microsoft SharePoint Server、Microsoft Azure Blob Storage或Microsoft OneDrive。
* 使用表單資料模型，順暢地將資料傳送至已設定的資料來源。
* 方便您將資料提交至REST端點。

您也可以 [擴充預設提交動作](custom-submit-action-form.md) 建立自己的提交動作。

## 選取並設定最適化表單的提交動作 {#select-and-configure-submit-action}

若要選取並設定表單的提交動作：

1. 開啟「內容」瀏覽器，然後選取 **[!UICONTROL 參考線容器]** 最適化表單的元件。
1. 按一下指南容器屬性 ![指南屬性](/help/forms/assets/configure-icon.svg) 圖示。 「最適化表單容器」對話方塊開啟。

1. 按一下  **[!UICONTROL 提交]** 標籤。

   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定提交動作](/help/forms/assets/adaptive-forms-submit-message.png)

1. 選取並設定 **[!UICONTROL 提交動作]**，根據您的需求。 如需所選「提交動作」的詳細資訊，請參閱：

   * [傳送電子郵件](#send-email)
   * [提交至 SharePoint](#submit-to-sharedrive)
   * [使用表單資料模型提交](#submit-using-form-data-model)
   * [提交到 Azure Blob 儲存體](#azure-blob-storage)
   * [提交至REST端點](#submit-to-rest-endpoint)
   * [提交至 OneDrive](#submit-to-onedrive)
   * [叫用AEM工作流程](#invoke-an-aem-workflow)

## 傳送電子郵件 {#send-email}

若要在成功提交表單後傳送電子郵件給一或多位收件者，您可以使用 **[!UICONTROL 傳送電子郵件]** 提交動作。 此動作可讓您建立包含預先定義格式之表單資料的電子郵件。 例如，考慮下列範本，其中客戶名稱、送貨地址、州名和郵遞區號是從提交的表單資料中擷取：

    ```
    
    $，您好{customer_Name}，
    
    下列專案設定為您的預設送貨地址：
    ${customer_Name}，
    ${customer_Shipping_Address}，
    ${customer_State}，
    ${customer_ZIPCode}
    
    祝順心，
    WKND
    
    ```

>[!NOTE]
>
> * 所有表單欄位都必須有唯一元素名稱，即使這些欄位位於調適型表單的不同面板上亦然。
> * 使用AEMas a Cloud Service時，傳出電子郵件需要加密。 預設會停用傳出電子郵件功能。 若要啟用支援服務單，請將支援服務單提交至 [要求存取權](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

此外， **[!UICONTROL 傳送電子郵件]** 「提交動作」提供將附件和記錄檔案(DoR)納入電子郵件的選項。

若要啟用 [!UICONTROL 附加記錄檔案] 選項，請參閱以下檔案： [設定最適化表單以產生記錄檔案(DoR)](generate-document-of-record-core-components.md). 您可以從最適化表單屬性中啟用此選項。

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

## 提交至 SharePoint {#submit-to-sharedrive}

此 **[!UICONTROL 提交至SharePoint]** 提交動作會連線最適化表單與Microsoft® SharePoint儲存體。 您可以將表單資料檔案、附件或記錄檔案提交至連線的Microsoft® Sharepoint儲存體。 若要使用 **[!UICONTROL 提交至SharePoint]** 以最適化表單提交動作：

1. [建立SharePoint設定](#create-a-sharepoint-configuration-create-sharepoint-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint儲存體。
2. [在最適化表單中使用提交至SharePoint提交動作](#use-sharepoint-configuartion-in-af)：它將您的最適化表單連線到已設定的Microsoft® SharePoint。

### 建立SharePoint設定 {#create-sharepoint-configuration}

若要將AEM Forms連線至您的Microsoft® Sharepoint儲存體：

1. 前往您的 **AEM Forms** 執行個體> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. 選取 **設定容器**. 請勿按一下設定容器的核取方塊。 按一下設定容器的名稱以選取它。 設定會儲存在選取的設定容器中。
1. 按一下&#x200B;**[!UICONTROL 建立]**。SharePoint設定精靈隨即出現。
   ![Sharepoint設定](/help/forms/assets/sharepoint_configuration.png)
1. 指定 **[!UICONTROL 標題]**， **[!UICONTROL 使用者端ID]**， **[!UICONTROL 使用者端密碼]** 和 **[!UICONTROL OAuth URL]**. 如需如何為OAuth URL擷取使用者端ID、使用者端密碼、租使用者ID的相關資訊，請參閱 [Microsoft®檔案](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * 您可以擷取 `Client ID` 和 `Client Secret` 從Microsoft® Azure入口網站存取您的應用程式。
   * 在Microsoft® Azure入口網站中，將重新導向URI新增為 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Replace `[author-instance]` 以及您的AEM Forms Author例項的URL。
   * 新增API許可權 `offline_access` 和 `Sites.Manage.All` 以提供讀取/寫入許可權。
   * 使用OAuth URL： `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` 使用 `tenant-id` 從Microsoft® Azure入口網站存取您的應用程式。

   >[!NOTE]
   >
   > 此 **使用者端密碼** 視您的Azure Active Directory應用程式組態而定，欄位是必要或選用的。 如果您的應用程式設定為使用使用者端密碼，則必須提供使用者端密碼。

1. 按一下 **[!UICONTROL Connect]**. 成功連線時， `Connection Successful` 訊息便會出現。

1. 若要選取要儲存資料的資料夾，請選取 **SharePoint網站** > **檔案庫** > **SharePoint資料夾**， 。

   >[!NOTE]
   >
   >* 根據預設， `forms-ootb-storage-adaptive-forms-submission` 資料夾可在選取的SharePoint網站中使用。 如果資料夾無法使用，請使用 **建立資料夾** 選項來建立它。

現在，您可以使用此SharePoint Sites設定 **提交至SharePoint** 在最適化表單中提交動作。

### 在最適化表單中使用提交至SharePoint提交動作 {#use-sharepoint-configuartion-in-af}

您可以使用上一節建立的SharePoint設定，將資料或記錄檔案儲存至SharePoint資料夾。 執行以下步驟，在最適化表單中使用提交至SharePoint提交動作：

1. 建立 [最適化表單](/help/forms/creating-adaptive-form.md). 建立最適化表單時，選取 [!UICONTROL 設定容器] 用於 [建立SharePoint設定](#create-sharepoint-configuration).

   >[!NOTE]
   >
   > 當否 [!UICONTROL 設定容器] 已選取，則全域 [!UICONTROL 儲存設定] 資料夾會出現在「提交動作」屬性視窗中。

1. 選取 **提交動作** 作為 **[!UICONTROL 提交至SharePoint]**.
1. 選取已設定的 **[!UICONTROL 儲存設定]**. 它會指定SharePoint中儲存表單資料和記錄檔案的資料夾。
1. 按一下 **[!UICONTROL 儲存]** 以儲存「提交」設定。

提交表單時，資料會儲存在指定的Microsoft® Sharepoint儲存位置（資料夾）中。
已儲存資料的資料夾結構為 `/folder_name/form_name/year/month/date/submission_id/data`.

## 使用表單資料模型提交 {#submit-using-form-data-model}

此 **[!UICONTROL 使用表單資料模型提交]** 提交動作會將表單資料模型中指定資料模型物件的已提交調適型表單資料寫入其資料來源。 在設定「提交」動作時，您可以選擇資料模型物件，將其提交的資料寫回其資料來源。

此外，您可以使用表單資料模型和記錄檔案(DoR)將表單附件提交至資料來源。 如需表單資料模型的相關資訊，請參閱 [[!DNL AEM Forms] 資料整合](data-integration.md).

## 提交至REST端點 {#submit-to-rest-endpoint}

使用 **[!UICONTROL 提交至REST端點]** 將已提交的資料發佈至rest URL的動作。 URL可以是內部（呈現表單的伺服器）或外部伺服器。

若要將資料發佈到內部伺服器，請提供資源的路徑。 資料會張貼在資源的路徑中。 例如，/content/restEndPoint。 對於此類貼文請求，會使用提交請求的驗證資訊。

若要將資料發佈至外部伺服器，請提供URL。 URL的格式為 `https://host:port/path_to_rest_end_point`. 請確定您設定匿名處理POST請求的路徑。

![以「感謝您」頁面引數傳遞的欄位值對應](assets/post-enabled-actionconfig.png)

在上述範例中，使用者輸入資訊於 `textbox` 是使用引數擷取 `param1`. 張貼使用擷取之資料的語法 `param1` 為：

`String data=request.getParameter("param1");`

同樣地，您用於公佈XML資料和附件的引數為 `dataXml` 和 `attachments`.

例如，您可以在指令碼中使用這兩個引數，將資料剖析至其餘端點。 您使用下列語法來儲存及剖析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此範例中， `data` 儲存XML資料，以及 `att` 儲存附件資料。

此 **[!UICONTROL 提交至REST端點]** 提交動作會將表單中填入的資料提交至已設定的確認頁面，作為HTTPGET請求的一部分。 您可以新增要請求的欄位名稱。 請求的格式為：

`{fieldName}={request parameter name}`

如下圖所示， `param1` 和 `param2` 會以引數形式傳遞，其值複製自 **文字方塊** 和 **numericbox** 下一個動作的欄位。

![設定Rest端點提交動作](assets/action-config.png)

您也可以 **[!UICONTROL 啟用POST請求]** 並提供一個URL以張貼請求。 若要將資料提交至託管表單的AEM伺服器，請使用與AEM伺服器根路徑對應的相對路徑。 例如，`/content/forms/af/SampleForm.html`。若要將資料提交至任何其他伺服器，請使用絕對路徑。

>[!NOTE]
>
>若要在REST URL中將欄位作為引數傳遞，所有欄位都必須有不同的元素名稱，即使欄位位於不同的面板上也是如此。

<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->



<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## 叫用AEM工作流程 {#invoke-an-aem-workflow}

此 **[!UICONTROL 叫用AEM工作流程]** 提交動作會將最適化表單與以下專案建立關聯： [AEM工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). 提交表單時，相關工作流程會在作者執行個體上自動啟動。 您可以將資料檔案、附件和記錄檔案儲存至工作流程的裝載位置或變數。 如果工作流程標示為外部資料儲存並設定為外部資料儲存，則只有變數選項可用。 您可以從工作流程模型可用的變數清單中選取。 如果工作流程在稍後階段而非建立工作流程時標籤為外部資料儲存，則請確保必要的變數設定已準備就緒。

提交動作會將下列專案放在工作流程的裝載位置，如果工作流程標示為外部資料儲存，則放入變數：

* **資料檔案**：此變數包含提交至最適化表單的資料。 您可以使用 **[!UICONTROL 資料檔案路徑]** 選項來指定檔案的名稱及相對於承載的檔案路徑。 例如， `/addresschange/data.xml` path會建立名為的資料夾 `addresschange` 並將其相對於承載放置。 您也可僅指定 `data.xml` 只傳送已提交的資料，而不建立資料夾階層。 如果工作流程已標籤為外部資料儲存，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

* **附件**：您可以使用 **[!UICONTROL 附件路徑]** 用於指定資料夾名稱以儲存已上傳至最適化表單的附件。 資料夾會相對於承載建立。 如果工作流程已標籤為外部資料儲存，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

* **記錄檔案**：它包含為最適化表單產生的記錄檔案。 您可以使用 **[!UICONTROL 記錄檔案路徑]** 選項以指定記錄檔案檔案的名稱以及相對於承載的檔案路徑。 例如， `/addresschange/DoR.pdf` path會建立名為的資料夾 `addresschange` 相對於裝載，並放置 `DoR.pdf` 相對於裝載。 您也可僅指定 `DoR.pdf` 只儲存記錄檔案，而不建立資料夾階層。 如果工作流程已標籤為外部資料儲存，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

使用之前 **[!UICONTROL 叫用AEM工作流程]** 提交動作為設定以下內容 **[!UICONTROL AEM DS設定服務]** 設定：

* **[!UICONTROL 處理伺服器URL]**：處理伺服器是觸發Forms或AEM工作流程的伺服器。 這可以與AEM編寫執行個體或其他伺服器的URL相同。

* **[!UICONTROL 處理伺服器使用者名稱]**：工作流程使用者的使用者名稱

* **[!UICONTROL 處理伺服器密碼]**：工作流程使用者密碼



## 提交至 OneDrive {#submit-to-onedrive}

此 **[!UICONTROL 提交至OneDrive]** 提交動作會將最適化表單與Microsoft® OneDrive連線。 您可以將表單資料、檔案、附件或記錄檔案提交至已連線的Microsoft® OneDrive儲存體。 若要使用 [!UICONTROL 提交至OneDrive] 以最適化表單提交動作：

1. [建立OneDrive設定](#create-a-onedrive-configuration-create-onedrive-configuration)：它會將AEM Forms連線至您的Microsoft® OneDrive儲存空間。
2. [在最適化表單中使用提交至OneDrive提交動作](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af)：它將您的最適化表單連線到設定的Microsoft® OneDrive。

### 建立OneDrive設定 {#create-onedrice-configuration}

若要將AEM Forms連線至您的Microsoft® OneDrive儲存體：

1. 前往您的 **AEM Forms Author** 執行個體> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® OneDrive]**.
1. 一旦您選取 **[!UICONTROL Microsoft® OneDrive]**，您便會被重新導向至 **[!UICONTROL OneDrive瀏覽器]**.
1. 選取 **設定容器**. 設定會儲存在選取的設定容器中。
1. 按一下&#x200B;**[!UICONTROL 建立]**。出現OneDrive設定精靈。

   ![OneDrive設定畫面](/help/forms/assets/onedrive-configuration.png)

1. 指定 **[!UICONTROL 標題]**， **[!UICONTROL 使用者端ID]**， **[!UICONTROL 使用者端密碼]** 和 **[!UICONTROL OAuth URL]**. 如需如何為OAuth URL擷取使用者端ID、使用者端密碼、租使用者ID的相關資訊，請參閱 [Microsoft®檔案](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * 您可以擷取 `Client ID` 和 `Client Secret` 從Microsoft® Azure入口網站存取您的應用程式。
   * 在Microsoft® Azure入口網站中，將重新導向URI新增為 `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Replace `[author-instance]` ，並使用您的Author例項的URL。
   * 新增API許可權 `offline_access` 和 `Files.ReadWrite.All` 以提供讀取/寫入許可權。
   * 使用OAuth URL： `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` 使用 `tenant-id` 從Microsoft® Azure入口網站存取您的應用程式。

   >[!NOTE]
   >
   > 此 **使用者端密碼** 欄位是必要欄位或選用欄位，視您的Azure Active Directory應用程式設定而定。 如果您的應用程式設定為使用使用者端密碼，則必須提供使用者端密碼。

1. 按一下 **[!UICONTROL Connect]**. 成功連線時， `Connection Successful` 訊息便會出現。

1. 現在，選取 **[!UICONTROL OneDrive容器]** > **[OneDrive資料夾]**  以儲存資料。

   >[!NOTE]
   >
   >* 依預設， `forms-ootb-storage-adaptive-forms-submission` 存在於OneDrive容器中。
   > * 建立資料夾為 `forms-ootb-storage-adaptive-forms-submission`，如果尚未出現，請按一下 **建立資料夾**.

現在，您可以使用此OneDrive儲存體設定在最適化表單中執行提交動作。

### 在最適化表單中使用OneDrive設定 {#use-onedrive-configuartion-in-af}

您可以使用在最適化表單中建立的OneDrive儲存體設定，將資料或產生的記錄檔案儲存到OneDrive資料夾中。 執行以下步驟，在最適化表單中使用OneDrive儲存體設定：
1. 建立 [最適化表單](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * 選取相同的 [!UICONTROL 設定容器] 最適化表單，您已在該表單中建立OneDrive儲存空間。
   > * 若否 [!UICONTROL 設定容器] 選取「 」，然後全域 [!UICONTROL 儲存設定] 資料夾會出現在「提交動作」屬性視窗中。

1. 選取 **提交動作** 作為 **[!UICONTROL 提交至OneDrive]**.
   ![OneDriveGIF](/help/forms/assets/onedrive-video.gif)
1. 選取 **[!UICONTROL 儲存設定]**，您想要儲存資料的位置。
1. 按一下 **[!UICONTROL 儲存]** 以儲存「提交」設定。

提交表單時，資料會儲存在指定的Microsoft® OneDrive儲存體中。
要儲存資料的資料夾結構為 `/folder_name/form_name/year/month/date/submission_id/data`.

## 提交到 Azure Blob 儲存體 {#submit-to-azure-blob-storage}

此 **[!UICONTROL 提交至Azure Blob儲存體]**  提交動作會將最適化表單與Microsoft® Azure入口網站連線。 您可以將表單資料、檔案、附件或記錄檔案提交至已連線的Azure儲存體容器。 若要對Azure Blob儲存體使用提交動作：

1. [建立Azure Blob儲存體容器](#create-a-azure-blob-storage-container-create-azure-configuration)：它會將AEM Forms連線至Azure儲存體容器。
2. [在最適化表單中使用Azure儲存體設定](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af)：它將您的最適化表單連線到已設定的Azure儲存體容器。

### 建立Azure Blob儲存體容器 {#create-azure-configuration}

若要將AEM Forms連線至您的Azure儲存體容器：
1. 前往您的 **AEM Forms Author** 執行個體> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Azure儲存體]**.
1. 一旦您選取 **[!UICONTROL Azure儲存體]**，您便會被重新導向至 **[!UICONTROL Azure儲存體瀏覽器]**.
1. 選取 **設定容器**. 設定會儲存在選取的設定容器中。
1. 按一下&#x200B;**[!UICONTROL 建立]**。便會顯示「建立Azure儲存體設定」精靈。

   ![Azure儲存體設定](/help/forms/assets/azure-storage-configuration.png)

1. 指定 **[!UICONTROL 標題]**， **[!UICONTROL Azure儲存體帳戶]** 和 **[!UICONTROL Azure存取金鑰]**.

   * 您可以擷取 `Azure Storage Account` 名稱和 `Azure Access key` 從Microsoft® Azure入口網站中的儲存體帳戶。

1. 按一下「**[!UICONTROL 儲存]**」。

現在，您可以在最適化表單中將此Azure儲存體容器設定用於提交動作。

### 在最適化表單中使用Azure儲存體設定 {#use-azure-storage-configuartion-in-af}

您可以在調適型表單中使用已建立的Azure儲存體容器設定，在Azure儲存體容器中儲存資料或產生的記錄檔案。 執行以下步驟，在最適化表單中使用Azure儲存體容器設定，如下所示：
1. 建立 [最適化表單](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * 選取相同的 [!UICONTROL 設定容器] 最適化表單，您已在該表單中建立OneDrive儲存空間。
   > * 若否 [!UICONTROL 設定容器] 選取「 」，然後全域 [!UICONTROL 儲存設定] 資料夾會出現在「提交動作」屬性視窗中。

1. 選取 **提交動作** 作為 **[!UICONTROL 提交至Azure Blob儲存體]**.
   ![Azure Blob儲存GIF](/help/forms/assets/azure-submit-video.gif)

1. 選取 **[!UICONTROL 儲存設定]**，您想要儲存資料的位置。
1. 按一下 **[!UICONTROL 儲存]** 以儲存「提交」設定。

當您提交表單時，資料會儲存在指定的Azure儲存體容器設定中。
要儲存資料的資料夾結構為 `/configuration_container/form_name/year/month/date/submission_id/data`.

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。

## 使用同步或非同步提交 {#use-synchronous-or-asynchronous-submission}

提交動作可以使用同步或非同步提交。

**同步提交**：傳統上，網路表單會設定為同步提交。 在同步提交中，當使用者提交表單時，系統會將他們重新導向至認可頁面、感謝頁面，或如果提交失敗，則導向至錯誤頁面。 您可以選取 **[!UICONTROL 使用非同步提交]** 將使用者重新導向至網頁或在提交時顯示訊息的選項。

![設定提交動作](assets/thank-you-setting.png)

**非同步提交**：單頁應用程式等現代網頁體驗越來越熱門，這是因為網頁保持靜態，而使用者端 — 伺服器互動發生在背景。 您現在可以透過以下方式提供此最適化Forms體驗 [設定非同步提交](asynchronous-submissions-adaptive-forms.md).

## Adaptive Form中的伺服器端重新驗證 {#server-side-revalidation-in-adaptive-form}

在任何線上資料擷取系統中，開發人員通常會在使用者端放置一些JavaScript驗證，以強制執行一些商業規則。 但在現代瀏覽器中，一般使用者可以略過這些驗證，並使用各種技術手動提交內容，例如網頁瀏覽器DevTools主控台。 這些技術對於Adaptive Forms也是有效的。 表單開發人員可以建立各種驗證邏輯，但技術上來說，一般使用者可以略過這些驗證邏輯，並將無效資料提交至伺服器。 無效資料會破壞表單作者已強制執行的商業規則。

伺服器端重新驗證功能也讓您能夠執行Adaptive Forms作者在伺服器上設計Adaptive Form時所提供的驗證。 它可防止表單驗證中顯示的資料提交和業務規則違規的任何可能危害。

### 要在伺服器上驗證什麼？ {#what-to-validate-on-server-br}

在伺服器上重新執行的最適化表單的所有開箱即用(OOTB)欄位驗證包括：

* 必要
* 驗證圖片子句
* 驗證運算式

### 啟用伺服器端驗證 {#enabling-server-side-validation-br}

使用 **[!UICONTROL 在伺服器上重新驗證]** 在側欄的「調適型表單容器」下，啟用或停用目前表單的伺服器端驗證。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果一般使用者略過這些驗證並提交表單，伺服器會再次執行驗證。 如果驗證在伺服器端失敗，則送出交易會停止。 使用者會再次看到原始表單。 擷取的資料和提交的資料會向使用者呈現為錯誤。

>[!NOTE]
>
>伺服器端驗證會驗證表單模型。 建議您建立個別的使用者端程式庫進行驗證，不要將其與相同使用者端程式庫中的HTML樣式和DOM操作等其他專案混合。

### 在驗證運算式中支援自訂函式 {#supporting-custom-functions-in-validation-expressions-br}

有時，如果存在 **複雜驗證規則**，確切的驗證指令碼位於自訂函式中，且作者會從欄位驗證運算式呼叫這些自訂函式。 AEM若要在執行伺服器端驗證時讓此自訂函式館為已知且可用，表單作者可在 **[!UICONTROL 基本]** 最適化表單容器屬性的索引標籤，如下所示。

![在驗證運算式中支援自訂函式](assets/clientlib-cat.png)

在驗證運算式中支援自訂函式

作者可以根據每個最適化表單設定customJavaScript程式庫。 在程式庫中，僅保留可重複使用的函式，這些函式依賴於jquery和underscore.js第三方程式庫。

## 提交動作的錯誤處理 {#error-handling-on-submit-action}

在AEM安全性和強化准則中，請設定自訂錯誤頁面，例如400.jsp、404.jsp和500.jsp。 提交表單時出現400、404或500錯誤時，會呼叫這些處理常式。 在Publish節點上觸發這些錯誤碼時，也會呼叫處理常式。 您也可以為其他HTTP錯誤碼建立JSP頁面。

當您將表單資料模型或具有XML或JSON資料投訴的結構描述預填到資料未包含的結構描述時 `<afData>`， `<afBoundData>`、和 `</afUnboundData>` 標籤填入，則最適化表單中無限制欄位的資料會遺失。 結構描述可以是XML結構描述、JSON結構描述或表單資料模型。 未限制欄位為最適化表單欄位，不含 `bindref` 屬性。

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
