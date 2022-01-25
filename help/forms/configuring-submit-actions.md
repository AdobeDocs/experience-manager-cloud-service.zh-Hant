---
title: 如何為自適應表單配置提交操作
description: 自適應表單提供多個提交操作。 提交操作定義在提交後如何處理自適應表單。 您可以使用內置的「提交操作」或建立自己的操作。
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 895290aa0080e159549cd2de70f0e710c4a0ee34
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 3%

---

# 自適應表單提交操作 {#configuring-the-submit-action}

當用戶按一下「提交操作」時， **[!UICONTROL 提交]** 按鈕。 Adaptive Forms提供了一些現成的「提交操作」。 現成的「提交操作」包括：

* [提交到REST終結點](#submit-to-rest-endpoint)
* [傳送電子郵件](#send-email)
* [使用表單資料模型提交](#submit-using-form-data-model)
* [調用工AEM作流](#invoke-an-aem-workflow)

您也可以 [擴展預設提交操作](custom-submit-action-form.md) 建立您自己的提交操作。

您可以在 **[!UICONTROL 提交]** 工具欄中。

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




## 提交到REST終結點 {#submit-to-rest-endpoint}

使用 **[!UICONTROL 提交到REST終結點]** 將提交的資料發佈到剩餘URL的操作。 該URL可以是內部（其上呈現表單的伺服器）或外部伺服器。

要將資料發佈到內部伺服器，請提供資源路徑。 資料將發佈到資源的路徑。 例如，/content/restEndPoint。 對於這種帖子請求，使用提交請求的驗證資訊。

要將資料發佈到外部伺服器，請提供URL。 URL的格式為 `https://host:port/path_to_rest_end_point`。 確保配置路徑以匿名處理POST請求。

![作為「感謝」頁參數傳遞的欄位值的映射](assets/post-enabled-actionconfig.png)

在上例中，用戶在 `textbox` 使用參數捕獲 `param1`。 用於發佈使用 `param1` 為：

`String data=request.getParameter("param1");`

同樣，用於過帳XML資料和附件的參數是 `dataXml` 和 `attachments`。

例如，在指令碼中使用這兩個參數將資料解析到余下端點。 可以使用以下語法來儲存和分析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在本例中， `data` 儲存XML資料， `att` 儲存附件資料。

的 **[!UICONTROL 提交到REST終結點]** 「提交操作」將表單中填寫的資料作為HTTPGET請求的一部分提交到配置的確認頁。 您可以添加要請求的欄位的名稱。 請求的格式為：

`{fieldName}={request parameter name}`

如下圖所示， `param1` 和 `param2` 作為參數傳遞，其值從 **文本框** 和 **數字框** 的子菜單。

![配置REST終結點提交操作](assets/action-config.png)

您也可以 **[!UICONTROL 啟用POST請求]** 並提供一個URL來發佈請求。 要將資料提交AEM到承載表單的伺服器，請使用與伺服器根路徑相應的相AEM對路徑。 比如說， `/content/forms/af/SampleForm.html`。 要將資料提交到任何其他伺服器，請使用絕對路徑。

>[!NOTE]
>
>要將欄位作為REST URL中的參數傳遞，所有欄位必須具有不同的元素名稱，即使這些欄位放置在不同的面板上也是如此。

## 傳送電子郵件 {#send-email}

您可以使用 **[!UICONTROL 發送電子郵件]** 提交操作：在成功提交表單時向一個或多個收件人發送電子郵件。 生成的電子郵件可以包含預定義格式的表單資料。 例如，在以下模板中，從已提交的表單資料中檢索客戶名稱、發運地址、狀態名稱和郵遞區號。

    「」
    
    您好${customer_Name},
    
    以下設定為預設發運地址：
    ${customer_name},
    ${customer_shipping_Address},
    ${customer_state},
    ${customer_ZIPCode}
    
    致謝，
    WKND
    
    「」

>[!NOTE]
>
> * 所有表單域必須具有不同的元素名稱，即使這些欄位放置在「自適應表單」的不同面板上也是如此。
> * AEMas a Cloud Service要求加密出站郵件。 預設情況下，禁用出站電子郵件。 要激活它，請提交支援票證至 [請求訪問](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email)。


您還可以將附件和記錄文檔(DoR)包含到電子郵件中。 啟用 **[!UICONTROL 附加記錄文檔]** 選項，配置自適應表單以生成記錄文檔(DoR)。 您可以啟用該選項以從「自適應表單」屬性生成「記錄文檔」。



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## 使用表單資料模型提交 {#submit-using-form-data-model}

的 **[!UICONTROL 使用表單資料模型提交]** 「提交操作」將表單資料模型中指定資料模型對象的已提交自適應表單資料寫入其資料源。 配置提交操作時，您可以選擇要將其提交的資料寫回其資料源的資料模型對象。

此外，您可以使用表單資料模型和記錄文檔(DoR)向資料源提交表單附件。 有關表單資料模型的資訊，請參見 [[!DNL AEM Forms] 資料整合](data-integration.md)。

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## 調用工AEM作流 {#invoke-an-aem-workflow}

的 **[!UICONTROL 調用工AEM作流]** 提交操作將自適應表單與 [工AEM作流](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem)。 提交表單後，關聯的工作流將自動在「作者」實例上啟動。 您可以將資料檔案、附件和「記錄文檔」保存到工作流的負載位置或變數。 如果將工作流標籤為外部資料儲存並配置為外部資料儲存，則只有變數選項可用。 可以從工作流模型可用的變數清單中選擇。 如果工作流在以後階段而不是在建立工作流時被標籤為外部資料儲存，則請確保所需的變數配置已就位。

「提交操作」(Submit Action)將下列內容放在工作流的負載位置，或在工作流標籤為外部資料儲存時將變數放在位置：

* **資料檔案**:它包含提交到自適應表單的資料。 您可以使用 **[!UICONTROL 資料檔案路徑]** 選項，指定檔案的名稱和檔案相對於負載的路徑。 例如， `/addresschange/data.xml` 路徑建立名為 `addresschange` 並把它放在有效載荷上。 也只能指定 `data.xml` 只發送已提交的資料而不建立資料夾層次結構。 如果將工作流標籤為外部資料儲存，請使用變數選項並從可用於工作流模型的變數清單中選擇變數。

* **附件**:您可以使用 **[!UICONTROL 附件路徑]** 的子菜單。 資料夾是相對於負載建立的。 如果將工作流標籤為外部資料儲存，請使用變數選項並從可用於工作流模型的變數清單中選擇變數。

* **記錄文檔**:它包含為自適應表單生成的記錄文檔。 您可以使用 **[!UICONTROL 記錄路徑的文檔]** 選項，指定「記錄文檔」檔案的名稱和檔案相對於負載的路徑。 例如， `/addresschange/DoR.pdf` 路徑建立名為 `addresschange` 與負載相關，並將 `DoR.pdf` 相對負載。 也只能指定 `DoR.pdf` 只保存「記錄文檔」而不建立資料夾層次結構。 如果將工作流標籤為外部資料儲存，請使用變數選項並從可用於工作流模型的變數清單中選擇變數。

使用 **[!UICONTROL 調用工AEM作流]** 提交操作為 **[!UICONTROL AEM DS設定服務]** 配置：

* **[!UICONTROL 正在處理伺服器URL]**:處理伺服器是觸發Forms或工作AEM流的伺服器。 這可以與作者實例或另AEM一伺服器的URL相同。

* **[!UICONTROL 正在處理伺服器用戶名]**:工作流用戶的用戶名

* **[!UICONTROL 正在處理伺服器密碼]**:工作流用戶的密碼

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。

## 使用同步或非同步提交 {#use-synchronous-or-asynchronous-submission}

提交操作可以使用同步或非同步提交。

**同步提交**:傳統上，Web表單配置為同步提交。 在同步提交中，當用戶提交表單時，會將其重定向到確認頁、感謝頁，或者如果提交失敗，則返回錯誤頁。 可以選擇 **[!UICONTROL 使用非同步提交]** 選項將用戶重定向到網頁或顯示提交消息。

![配置提交操作](assets/thank-you-setting.png)

**非同步提交**:現代Web體驗，如單頁應用程式，越來越受到歡迎。在後台，網頁保持靜態，而客戶端與伺服器交互發生。 您現在可以通過Adaptive Forms提供此體驗 [配置非同步提交](asynchronous-submissions-adaptive-forms.md)。

## Adaptive Form中的伺服器端重新驗證 {#server-side-revalidation-in-adaptive-form}

通常，在任何線上資料捕獲系統中，開發人員都會在客戶端上進行一些JavaScript驗證，以強制執行一些業務規則。 但在現代瀏覽器中，最終用戶可以繞過這些驗證，使用各種技術（如Web瀏覽器DevTools控制台）手動執行提交。 這種技術也適用於自適應Forms。 表單開發人員可以建立各種驗證邏輯，但從技術上講，最終用戶可以繞過這些驗證邏輯，將無效資料提交到伺服器。 無效資料會破壞表單作者強制執行的業務規則。

伺服器端重新驗證功能還提供了運行Adaptive Forms作者在伺服器上設計Adaptive Form時提供的驗證的功能。 它防止以表單驗證形式表示的資料提交和業務規則違規的任何可能危害。

### 在伺服器上驗證什麼？ {#what-to-validate-on-server-br}

在伺服器上重新運行的Adaptive Form的現成(OOTB)欄位驗證包括：

* 必要
* 驗證圖片子句
* 驗證表達式

### 啟用伺服器端驗證 {#enabling-server-side-validation-br}

使用 **[!UICONTROL 在伺服器上重新驗證]** 的子菜單。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果最終用戶繞過這些驗證並提交表單，伺服器將再次執行驗證。 如果驗證在伺服器端失敗，則提交事務將停止。 最終用戶再次呈現原始形式。 捕獲的資料和提交的資料作為錯誤呈現給用戶。

>[!NOTE]
>
>伺服器端驗證會驗證表單模型。 建議您建立單獨的客戶端庫以進行驗證，但不要將其與HTML樣式和DOM操作等其他內容混合到同一客戶端庫中。

### 在驗證表達式中支援自定義函式 {#supporting-custom-functions-in-validation-expressions-br}

有時，如果 **複雜驗證規則**，確切的驗證指令碼位於自定義函式中，作者從欄位驗證表達式中調用這些自定義函式。 要使此自定義函式館在執行伺服器端驗證時已知且可用，表單作者可以在以下位置配置AEM客戶端庫的名稱： **[!UICONTROL 基本]** 頁籤，如下所示。

![在驗證表達式中支援自定義函式](assets/clientlib-cat.png)

在驗證表達式中支援自定義函式

作者可以按自適應表單配置customJavaScript庫。 在庫中，只保留可重用函式，這些函式依賴於jquery和underloge.js第三方庫。

## 提交操作時出錯 {#error-handling-on-submit-action}

作為安全和強AEM化指南的一部分，配置自定義錯誤頁，如400.jsp、404.jsp和500.jsp。 在提交表單400、404或500錯誤時，將調用這些處理程式。 在「發佈」節點上觸發這些錯誤代碼時，也會調用處理程式。 也可以為其他HTTP錯誤代碼建立JSP頁。

當您預填表單資料模型或基於架構的自適應表單（帶有XML或JSON資料抱怨）時，向不包含資料的架構 `<afData>`。 `<afBoundData>`, `</afUnboundData>` 標籤，則自適應表單中無界欄位的資料丟失。 架構可以是XML架構、JSON架構或表單資料模型。 無界欄位是沒有 `bindref` 屬性。

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
