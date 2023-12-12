---
title: 如何設定最適化表單的提交動作？
description: 最適化表單提供多個提交動作。提交動作會定義提交之後處理最適化表單的方式。您可以使用內建的提交動作或建立您自己的提交動作
keywords: 如何選取最適化表單的提交動作、將最適化表單連線至sharepoint清單、將最適化表單連線至sharepoint檔案庫、將最適化表單連線至表單資料模型
feature: Adaptive Forms, Core Components
exl-id: 495948e8-30a7-4e7c-952f-c71de15520f0
source-git-commit: eaab351460363b83c7d3667e048235506cc71c41
workflow-type: tm+mt
source-wordcount: '4114'
ht-degree: 82%

---

# 最適化表單提交動作 {#configuring-the-submit-action}

<span class="preview">Adobe 建議使用核心元件[將最適化表單新增到 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)或[建立獨立的最適化表單](/help/forms/creating-adaptive-form-core-components.md)。</span>


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service  | 本文章 |
| 套用至 | ✅ 最適化表單核心元件，❎[最適化表單基礎元件](/help/forms/configuring-submit-actions.md) |


提交動作讓您可選擇透過最適化表單擷取的資料目標。使用者按一下最適化表單上的「**[!UICONTROL 提交]**」按鈕時，就會加以觸發。針對以核心元件為基礎的最適化表單，Forms as a Cloud Service 提供了一系列預先建立的提交動作。這些現成可用的提交動作可讓您：

* 透過電子郵件輕鬆傳送表單資料。
* 在傳輸資料時啟動 Microsoft Power Automate 流程或 AEM 工作流程。
* 直接將表單資料傳輸到 Microsoft SharePoint 伺服器、Microsoft Azure Blob 儲存體或 Microsoft OneDrive。
* 使用表單資料模型將資料順暢地傳送到已設定的資料來源。
* 方便地將資料提交到 REST 端點。

您也可以[擴展預設的提交動作](custom-submit-action-form.md)以建立自己的提交動作。

## 選取並設定最適化表單的提交動作 {#select-and-configure-submit-action}

若要為您的表單選取並設定提交動作：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。

1. 按一下「**[!UICONTROL 提交]**」標籤。

   ![按一下扳手圖示可開啟「最適化表單容器」對話框，以設定提交動作](/help/forms/assets/adaptive-forms-submit-message.png)

1. 根據您的要求選取和設定「**[!UICONTROL 提交動作]**」。如需有關所選取提交動作的詳細資訊，請參閱：

   * [寄送電子郵件](#send-email)
   * [提交到 SharePoint](#submit-to-sharedrive)
   * [使用表單資料模型提交](#submit-using-form-data-model)
   * [提交到 Azure Blob 儲存體](#azure-blob-storage)
   * [提交到 REST 端點](#submit-to-rest-endpoint)
   * [提交到 OneDrive](#submit-to-onedrive)
   * [叫用 AEM 工作流程](#invoke-an-aem-workflow)
   * [提交至 Power Automate](#microsoft-power-automate)
   * [提交至Workfront Fusion](#workfront-fusion)

## 寄送電子郵件 {#send-email}

若要在成功提交表單後寄送電子郵件給一或多個收件者，您可以利用「**[!UICONTROL 寄送電子郵件]**」提交動作。此動作可讓您建立包含預先定義格式之表單資料的電子郵件。例如，考慮以下範本，其中從已提交的表單資料中擷取客戶名稱、送貨地址、州名稱和郵遞區號：

    ```
    
    ${customer_Name} 您好：
    
    以下設定為您的預設送貨地址：
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    謹此，
    WKND
    
    ```

>[!NOTE]
>
> * 即使是放置在最適化表單的不同面板上，對於所有表單欄位而言，擁有唯一的元素名稱至關重要。
> * 使用 AEM as a Cloud Service 時，傳出的電子郵件必須加密。傳出的電子郵件功能預設會停用。若要啟用，請提交支援服務單至[要求存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=zh-Hant#sending-email)。

此外，「**[!UICONTROL 寄送電子郵件]**」提交動作會提供在電子郵件中包含附件和記錄文件 (DoR) 的選項。

若要啟用「[!UICONTROL 附加記錄文件]」選項，請參閱有關[設定最適化表單以產生記錄文件 (DoR)](generate-document-of-record-core-components.md) 的文件。您可以從最適化表單屬性中啟用此選項。

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

## 提交到 SharePoint {#submit-to-sharedrive}

「**[!UICONTROL 提交到 SharePoint]**」提交動作會將最適化表單與 Microsoft® SharePoint 儲存空間建立連結。您可以將表單資料檔案、附件或記錄檔案提交至連線的Microsoft® Sharepoint儲存體。

使用提交至SharePoint，您可以：
* [將最適化表單連線至SharePoint檔案庫](#connect-af-sharepoint-doc-library)
* [將最適化表單連線至SharePoint清單](#connect-af-sharepoint-list)

### 將最適化表單連線至SharePoint檔案庫 {#connect-af-sharepoint-doc-library}

若要使用 **[!UICONTROL 提交至SharePoint檔案庫]** 以最適化表單提交動作：

1. [建立SharePoint檔案庫組態](#create-a-sharepoint-configuration-create-sharepoint-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint儲存空間。
2. [使用最適化表單中的「提交到 SharePoint」提交動作](#use-sharepoint-configuartion-in-af)：會將您的最適化表單連結到已設定的 Microsoft® SharePoint。

#### 建立SharePoint檔案庫組態 {#create-sharepoint-configuration}

若要將AEM Forms連線至您的Microsoft® Sharepoint檔案庫儲存空間：

1. 前往您的 **AEM Forms Author** 執行個體> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. 一旦您選取 **[!UICONTROL Microsoft® SharePoint]**，您就會被重新導向至 **[!UICONTROL SharePoint瀏覽器]**.
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下 **[!UICONTROL 建立]** > **[!UICONTROL SharePoint檔案庫]** 下拉式清單中的。 此時會顯示 SharePoint 設定精靈。

![SharePoint 設定](/help/forms/assets/sharepoint_configuration.png)
1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 新增 API 權限 `offline_access` 和 `Sites.Manage.All` 以提供讀取/寫入權限。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

   >[!NOTE]
   >
   > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。

1. 現在，選取 **SharePoint網站** > **檔案庫** > **SharePoint資料夾**，以儲存資料。

   >[!NOTE]
   >
   >* 根據預設， `forms-ootb-storage-adaptive-forms-submission` 出現在選取的SharePoint網站。
   >* 建立資料夾為 `forms-ootb-storage-adaptive-forms-submission`，如果尚未出現在 `Documents` 所選SharePoint網站的程式庫，方法是按一下 **建立資料夾**.

現在，您可以使用此SharePoint Sites設定，在最適化表單中執行提交動作。

#### 在最適化表單中使用SharePoint檔案庫設定 {#use-sharepoint-configuartion-in-af}

您可以使用在最適化表單中建立的SharePoint檔案庫組態，將資料或產生的記錄檔案儲存在SharePoint資料夾中。 執行以下步驟，在最適化表單中使用SharePoint檔案庫儲存設定，如下所示：

1. 建立[最適化表單](/help/forms/creating-adaptive-form-core-components.md)。

   >[!NOTE]
   >
   > * 選取相同的 [!UICONTROL 設定容器] 最適化表單(您已在其中建立SharePoint檔案庫儲存空間)。
   > * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

1. 選取「**提交動作**」做為「**[!UICONTROL 提交到 SharePoint]**」。
   ![SharepointGIF](/help/forms/assets/sharedrive-video.gif)
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

當您提交表單時，資料會儲存在指定的Microsoft® Sharepoint檔案庫儲存空間中。
儲存資料的資料夾結構是 `/folder_name/form_name/year/month/date/submission_id/data`。

### 將最適化表單連線至Microsoft® SharePoint清單 {#connect-af-sharepoint-list}

<span class="preview">這是一項預先發佈功能，可透過我們的[預先發佈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)存取。</span>

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

若要使用 [!UICONTROL 提交至SharePoint清單] 以最適化表單提交動作：

1. [建立SharePoint清單設定](#create-sharepoint-list-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint清單儲存空間。
1. [在最適化表單中使用表單資料模型提交](#use-submit-using-fdm)：此動作會將您的最適化表單連線至設定的Microsoft® SharePoint。

#### 建立SharePoint清單設定 {#create-sharepoint-list-configuration}

若要將AEM Forms連線至您的Microsoft®Sharepoint清單：

1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下 **[!UICONTROL 建立]** > **[!UICONTROL SharePoint清單]** 下拉式清單中的。 此時會顯示 SharePoint 設定精靈。
1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 新增API許可權 `offline_access` 和 `Sites.Manage.All` 在 **Microsoft® Graph** 索引標籤以提供讀取/寫入許可權。 新增 `AllSites.Manage` 中的許可權 **Sharepoint** 索引標籤以與SharePoint資料進行遠端互動。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

     >[!NOTE]
     >
     > **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。
1. 選取 **[!UICONTROL SharePoint網站]** 和 **[!UICONTROL SharePoint清單]** 下拉式清單中的。
1. 選取 **[!UICONTROL 建立]** 以建立Microsoft® SharePointList的雲端設定。


#### 在最適化表單中使用表單資料模型提交 {#use-submit-using-fdm}

您可以在調適型表單中使用已建立的SharePoint清單設定，以在SharePoint清單中儲存資料或產生的記錄檔案。 執行以下步驟，在最適化表單中使用SharePoint清單：

1. [使用Microsoft建立表單資料模型](/help/forms/create-form-data-models.md)
1. [設定表單資料模型以擷取及傳送資料](/help/forms/work-with-form-data-model.md#configure-services)
1. [建立最適化表單](/help/forms/creating-adaptive-form-core-components.md)
1. [使用表單資料模型設定提交動作](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)

提交表單時，資料會儲存在指定的Microsoft® Sharepoint清單儲存空間中。

>[!NOTE]
>
> Microsoft® SharePoint清單不支援下列欄型別：
* 影像欄
* 中繼資料欄
* 人員欄
* 外部資料欄

## 使用表單資料模型提交 {#submit-using-form-data-model}

「**[!UICONTROL 使用表單資料模型提交]**」提交動作，會將表單資料模型中指定資料模型物件的已提交最適化表單資料寫入其資料來源。設定提交動作時，您可以選擇要將其提交資料寫回其資料來源的資料模型物件。

您可以使用表單資料模型提交動作，將最適化表單連結至Microsoft SharePoint清單。

此外，您可以使用表單資料模型和記錄文件 (DoR) 將表單附件提交到資料來源。如需有關表單資料模型的資訊，請參閱 [[!DNL AEM Forms] 資料整合](data-integration.md)。

## 提交到 REST 端點 {#submit-to-rest-endpoint}

使用「**[!UICONTROL 提交到 REST 端點]**」動作會將提交的資料發佈到 REST URL。該 URL 可以是內部伺服器 (呈現表單的伺服器) 或外部伺服器。

若要將資料發佈到內部伺服器，請提供資源的路徑。資料會發佈到資源的路徑。例如 /content/restEndPoint。對於此類發佈要求，會使用提交要求的驗證資訊。

若要將資料發佈到外部伺服器，請提供 URL。URL 的格式是：`https://host:port/path_to_rest_end_point`。請確保設定以匿名方式處理 POST 要求的路徑。

![做為「感謝頁面」參數傳遞之欄位值的對應](assets/post-enabled-actionconfig.png)

在上面的範例中，在 `textbox` 輸入的資訊是使用 `param1` 參數來擷取。使用 `param1` 發佈所擷取之資料的語法是：

`String data=request.getParameter("param1");`

同樣地，用於發佈 XML 資料和附件的參數是 `dataXml` 和 `attachments`。

例如，您會在指令碼中使用這兩個參數將資料剖析到 REST 端點。您會使用以下語法來儲存和剖析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在這個範例中，`data` 會儲存 XML 資料，而 `att` 會儲存附件資料。

「**[!UICONTROL 提交到 REST 端點]**」提交動作會將表單中填寫的資料做為 HTTP GET 要求的一部分，提交到已設定的確認頁面。您可以新增要求的欄位名稱。要求的格式為：

`{fieldName}={request parameter name}`

如下圖所示，`param1` 和 `param2` 是做為參數傳遞，其值是從 **textbox** 和 **numericbox** 欄位複製做為下一個動作。

![設定 REST 端點提交動作](assets/action-config.png)

您也可以「**[!UICONTROL 啟用 POST 要求]**」並提供用於發佈要求的 URL。若要將資料提交到託管表單的 AEM 伺服器，請使用對應至 AEM 伺服器根路徑的相對路徑。例如 `/content/forms/af/SampleForm.html`。若要將資料提交到任何其他伺服器，請使用絕對路徑。

>[!NOTE]
>
若要將欄位做為 REST URL 的參數傳遞，所有欄位都必須具有不同的元素名稱，即使這些欄位位於不同面板上也是如此。

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

## 叫用 AEM 工作流程 {#invoke-an-aem-workflow}

「**[!UICONTROL 叫用 AEM 工作流程]**」提交動作會將最適化表單與 [AEM 工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hant#extending-aem)建立關聯。提交表單後，相關聯的工作流程就會在作者執行個體上自動開始。您可以將資料檔案、附件和記錄文件儲存到工作流程的承載位置，或儲存到變數。如果工作流程標記為外部資料儲存空間，且設定為外部資料儲存空間，則只有變數選項可使用。您可以從可用於工作流程模型的變數清單中選取。如果工作流程是在後續階段標記為外部資料儲存空間，而不是在建立工作流程時標記，則請確保已經具備所需的變數設定。

提交動作會將以下內容放置於工作流程的承載位置，或放置到變數 (如果工作流程標記為外部資料儲存空間)：

* **資料檔案**：包含提交給最適化表單的資料。您可以使用「**[!UICONTROL 資料檔案路徑]**」選項來指定相對於承載的檔案名稱和檔案路徑。例如，`/addresschange/data.xml` 路徑會建立一個名為 `addresschange` 的資料夾，並將其置於相對於承載的位置。您也可以僅指定 `data.xml`，僅發送提交的資料而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項並從工作流程模型可用的變數清單中選取變數。

* **附件**：您可以使用「**[!UICONTROL 附件路徑]**」選項，指定用來儲存上傳到最適化表單之附件的資料夾名稱。該資料夾會建立在相對於承載的位置。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

* **記錄文件**：包含為最適化表單產生的記錄文件。您可以使用「**[!UICONTROL 記錄文件路徑]**」選項指定記錄文件檔案的名稱，以及相對於承載的檔案路徑。例如，`/addresschange/DoR.pdf` 路徑會在相對於承載的位置建立一個名為 `addresschange` 的資料夾，並將 `DoR.pdf` 放置在相對於承載的位置。您也可以指定 `DoR.pdf` 僅儲存記錄文件而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

使用「**[!UICONTROL 叫用 AEM 工作流程]**」提交動作為 **[!UICONTROL AEM DS 設定服務]**&#x200B;設定以下內容之前：

* **[!UICONTROL 處理伺服器 URL]**：處理伺服器是觸發表單或 AEM 工作流程所在的伺服器。這可以與 AEM 作者執行個體或另一個伺服器的 URL 相同。

* **[!UICONTROL 處理伺服器使用者名稱]**：工作流程使用者的使用者名稱

* **[!UICONTROL 處理伺服器密碼]**：工作流程使用者的密碼



## 提交到 OneDrive {#submit-to-onedrive}

「**[!UICONTROL 提交到 OneDrive]**」提交動作會將最適化表單連結到 Microsoft® OneDrive。您可以將表單資料、檔案、附件或記錄檔案提交至已連線的Microsoft® OneDrive儲存體。

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

若要在最適化表單中使用「[!UICONTROL 提交到 OneDrive]」提交動作：

1. [建立 OneDrive 設定](#create-a-onedrive-configuration-create-onedrive-configuration)：將 AEM Forms 連接到您的 Microsoft® OneDrive 儲存空間。
2. [在最適化表單中使用「提交到 OneDrive」提交動作](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af)：將您的最適化表單連結到
已設定的 Microsoft® OneDrive。

### 建立 OneDrive 設定 {#create-onedrice-configuration}

若要將 AEM Forms 連結到您的 Microsoft® OneDrive 儲存空間：

1. 前往您的 **AEM Forms 作者**&#x200B;執行個體 >「**[!UICONTROL 工具]**」>「**[!UICONTROL 雲端服務]**」>「**[!UICONTROL Microsoft® OneDrive]**」。
1. 一旦您選取了「**[!UICONTROL Microsoft® OneDrive]**」，系統就會將您重新導向到「**[!UICONTROL OneDrive 瀏覽器]**」。
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下「**[!UICONTROL 建立]**」。此時會顯示 OneDrive 設定精靈。

   ![OneDrive 設定畫面](/help/forms/assets/onedrive-configuration.png)

1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 新增 API 權限 `offline_access` 和 `Files.ReadWrite.All` 以提供讀取/寫入權限。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

   >[!NOTE]
   >
   **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。

1. 現在，請選取「**[!UICONTROL OneDrive 容器]**」>「**[OneDrive 資料夾]**」以儲存資料。

   >[!NOTE]
   >
   * 根據預設，`forms-ootb-storage-adaptive-forms-submission` 會顯示在 OneDrive 容器中。
   * 建立一個資料夾做為 `forms-ootb-storage-adaptive-forms-submission`；如果尚未出現，請按一下「**建立資料夾**」。

現在，您可以使用此 OneDrive 儲存空間設定，在最適化表單中使用該提交動作。

### 在最適化表單中使用 OneDrive 設定 {#use-onedrive-configuartion-in-af}

您可以在最適化表單中使用建立的 OneDrive 儲存空間設定，將資料或產生的記錄文件儲存在 OneDrive 資料夾中。執行以下步驟，即可在最適化表單中使用 OneDrive 儲存空間設定：
1. 建立[最適化表單](/help/forms/creating-adaptive-form.md)。

   >[!NOTE]
   >
   * 對於已在其中建立 OneDrive 儲存空間的最適化表單，請選取相同的「[!UICONTROL 設定容器]」。
   * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

1. 選取「**提交動作**」做為「**[!UICONTROL 提交到 OneDrive]**」。
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

您提交表單時，資料將儲存在指定的 Microsoft® OneDrive 儲存空間。
儲存資料的資料夾結構是 `/folder_name/form_name/year/month/date/submission_id/data`。

## 提交到 Azure Blob 儲存體 {#submit-to-azure-blob-storage}

「**[!UICONTROL 提交到 Azure Blob 儲存體]**」提交動作會將最適化表單連結到 Microsoft® Azure 入口網站。您可以將表單資料、檔案、附件或記錄文件提交到連結的 Azure 儲存體容器。若要使用對 Azure Blob 儲存體的提交動作：

1. [建立 Azure Blob 儲存體容器](#create-a-azure-blob-storage-container-create-azure-configuration)：將 AEM Forms 連結到 Azure 儲存體容器。
2. [在最適化表單中使用 Azure 儲存體設定](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af)：將您的最適化表單連結到已設定的 Azure 儲存體容器。

### 建立 Azure Blob 儲存體容器 {#create-azure-configuration}

若要將 AEM Forms 連結到 Azure 儲存體容器：
1. 前往 **AEM Forms 作者**&#x200B;執行個體 >「**[!UICONTROL 工具]**」>「**[!UICONTROL 雲端服務]**」>「**[!UICONTROL Azure 儲存體]**」。
1. 一旦選取了「**[!UICONTROL Azure 儲存體]**」，系統就會將您重新導向至「**[!UICONTROL Azure 儲存體瀏覽器]**」。
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下「**[!UICONTROL 建立]**」。此時會顯示「建立 Azure 儲存體設定」精靈。

   ![Azure 儲存體設定](/help/forms/assets/azure-storage-configuration.png)

1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL Azure 儲存體帳戶]**」和「**[!UICONTROL Azure 存取金鑰]**」。

   * 您可以從 Microsoft® Azure 入口網站的儲存體帳戶擷取 `Azure Storage Account` 名稱和 `Azure Access key`。

1. 按一下「**[!UICONTROL 儲存]**」。

現在，您可以使用此 Azure 儲存體容器設定，在最適化表單中使用該提交動作。

### 在最適化表單中使用 Azure 儲存體設定 {#use-azure-storage-configuartion-in-af}

您可以在最適化表單中使用建立的 Azure 儲存體器設定，將資料或產生的記錄文件儲存在 Azure 儲存體容器中。執行以下步驟，即可在最適化表單中使用 Azure 儲存體容器設定：
1. 建立[最適化表單](/help/forms/creating-adaptive-form-core-components.md)。

   >[!NOTE]
   >
   * 對於已在其中建立 OneDrive 儲存空間的最適化表單，請選取相同的「[!UICONTROL 設定容器]」。
   * 如果沒有選取「[!UICONTROL 設定容器]」，「提交動作」屬性視窗中會顯示全域「[!UICONTROL 儲存空間設定]」資料夾。

1. 將「**提交動作**」選取作為「**[!UICONTROL 提交到 Azure Blob 儲存體]**」。
   ![Azure Blob 儲存體 GIF](/help/forms/assets/azure-submit-video.gif)

1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

提交表單時，資料會儲存在指定的 Azure 儲存體容器設定中。
儲存資料的資料夾結構是 `/configuration_container/form_name/year/month/date/submission_id/data`。

若要設定值，請[使用 AEM SDK 產生 OSGi 設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hant#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並[將設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant#deployment-process)您的 Cloud Service 執行個體。




## 提交至 Power Automate {#microsoft-power-automate}

您可以設定最適化表單，在提交時執行 Microsoft® Power Automate Cloud Flow。設定的最適化表單會將擷取的資料、附件和記錄文件傳送到 Power Automate Cloud Flow 進行處理。那有助於建置自訂資料擷取體驗，同時利用 Microsoft® Power Automate 的強大功能，根據擷取的資料建置商業邏輯，並將客戶工作流程自動化。以下是整合最適化表單與 Microsoft® Power Automate 後，可以執行的部分操作範例：

* 在 Power Automate 業務流程中使用最適化表單資料
* 使用 Power Automate 將擷取的資料傳送到 500 多個資料來源或任何公開可用的 API
* 對擷取的資料執行複雜的計算
* 按預定義的排程將最適化表單資料儲存到儲存系統

最適化表單編輯器提供&#x200B;**叫用 Microsoft® Power Automate 流程**&#x200B;提交動作，將最適化表單資料、附件和記錄文件發送到 Power Automate Cloud Flow。若要使用提交動作將擷取的資料傳送到 Microsoft® Power Automate，[請使用 Microsoft® Power Automate 連線您的 Forms as a Cloud Service 執行個體](forms-microsoft-power-automate-integration.md)

在設定成功之後，使用[叫用 Microsoft® Power Automate 流程](forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action)提交動作，將資料傳送到 Power Automate Flow。

## 提交至Workfront Fusion {#workfront-fusion}

您可以設定最適化表單，在提交時提交資料給Workfront Fusion。 Workfront Fusion允許流程自動化，以便使用者可以專注於新任務，而不是一遍又一遍地重複相同的任務。 它可自動化簡單和複雜的工作，節省時間並確保一致的流程執行。

最適化Forms編輯器提供 **叫用Workfront Fusion案例** 提交動作以將最適化Forms資料或附件傳送至Workfront Fusion案例。 若要使用提交動作將擷取的資料傳送至Workfront Fusion案例，請參閱 [提交最適化表單至Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md).


## 使用同步或異步提交 {#use-synchronous-or-asynchronous-submission}

提交動作可以使用同步或異步提交。

**同步提交**：傳統上，Web 表單設定為同步提交。在同步提交中，使用者提交表單時，系統會將其被重新導向至確認頁面、感謝頁面；如果提交失敗，則會重新導向至錯誤頁面。您可以選擇「**[!UICONTROL 使用異步提交]**」選項，將使用者重新導向至網頁，或在提交時顯示訊息。

![設定提交動作](assets/thank-you-setting.png)

**異步提交**：單一頁面應用程式等現代 Web 體驗越來越受歡迎，其中網頁會保持靜態，而用戶端-伺服器的互動則是在背景中執行。透過[設定異步提交](asynchronous-submissions-adaptive-forms.md)，您現在就可以對最適化表單提供此體驗了。

## 最適化表單中的伺服器端重新驗證 {#server-side-revalidation-in-adaptive-form}

一般而言，在任何線上資料擷取系統中，開發人員都會在用戶端放置一些 JavaScript 驗證，以強制執行一些業務規則。但在現代的瀏覽器中，一般使用者可以略過那些驗證，並使用各種技巧 (例如 Web Browser DevTools Console) 手動進行提交。此類技術對於最適化表單也有效。表單開發人員可以建立各種驗證邏輯，但技術上而言，一般使用者可以略過那些驗證邏輯並提交無效的資料給伺服器。無效的資料會破壞表單作者強制執行的業務規則。

伺服器端重新驗證功能也能夠執行最適化表單作者在伺服器上設計最適化表單時提供的驗證能力。這樣可以避免對提交的資料造成任何可能的危害，以及在表單驗證方面違反業務規則。

### 伺服器上會進行哪些驗證？ {#what-to-validate-on-server-br}

會在伺服器上對最適化表單重新執行的所有立即可用 (OOTB) 欄位驗證包括：

* 必填
* 驗證圖片子句
* 驗證運算式

### 啟用伺服器端驗證 {#enabling-server-side-validation-br}

使用在側邊欄「最適化表單容器」下方的「**[!UICONTROL 在伺服器上重新驗證]**」，即可對目前表單啟用或停用伺服器端驗證。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果一般使用者略過那些驗證並提交表單，伺服器將再次執行驗證。如果伺服器端驗證失敗，就會停止提交交易。使用者會再次看到原始表單。 擷取的資料和提交的資料會做為錯誤呈現給使用者。

>[!NOTE]
>
伺服器端驗證會驗證表單模型。建議您建立獨立的用戶端程式庫已進行驗證，並避免與相同用戶端程式庫中其他內容混淆，例如 HTML 樣式和 DOM 操作等。

### 支援驗證運算式中的自訂函數 {#supporting-custom-functions-in-validation-expressions-br}

有時候，如果有&#x200B;**複雜的驗證規則**，則確切的驗證指令碼會駐留在自訂函數中，且作者會從欄位驗證運算式中呼叫這些自訂函數。若要在執行伺服器端驗證時公開和提供此自訂函數程式庫，表單作者可以在「最適化表單容器」屬性的「**[!UICONTROL 基礎]**」標籤下方，設定 AEM 用戶端程式庫的名稱，如以下所示。

![支援驗證運算式中的自訂函數](assets/clientlib-cat.png)

支援驗證運算式中的自訂函數

作者可以根據最適化表單來設定自訂 JavaScript 程式庫。程式庫中只會保留可重複使用的函數，這些函數與 jquery 和 underscore.js 第三方程式庫有相依性。

## 提交動作的錯誤處理 {#error-handling-on-submit-action}

為了 AEM 安全性和強化準則，請設定自訂錯誤頁面，例如 400.jsp、404.jsp 和 500.jsp。提交表單時，如果出現 400、404 或 500 錯誤，就會呼叫這些處理常式。在發佈節點上觸發這些錯誤代碼時，也會呼叫處理常式。您也可以為其他 HTTP 錯誤代碼建立 JSP 頁面。

您使用符合結構描述 (其資料不含 `<afData>`、`<afBoundData>` 和 `</afUnboundData>` 標記) 的 XML 或 JSON 資料，預先填入表單資料模型或以結構描述為主的最適化表單的綱要時，最適化表單的未繫結欄位資料會遺失。該結構描述可以是 XML 結構描述、JSON 結構描述或表單資料模型。未繫結欄位是最適化表單欄位，但沒有 `bindref` 屬性。

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->


<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)
* [Create a custom Submit Action for Adaptive Forms](/help/forms/custom-submit-action-form.md)

-->

## 另請參閱 {#see-also}

{{see-also}}

