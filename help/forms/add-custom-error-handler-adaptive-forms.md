---
title: 在AEM Adaptive Forms中新增自訂錯誤處理常式
description: AEM Forms使用設定為叫用外部服務的REST端點，為表單提供現成的成功和錯誤處理常式。 您可以在AEM最適化表單中新增預設錯誤處理常式以及自訂錯誤處理常式。
seo-description: Error handler function and Rule Editor in Adaptive Forms helps you to effectively manage and customize error handling. You can add a default error handler as well as custom error handler in an AEM Adaptive Form.
keywords: 新增自訂錯誤處理程式、新增預設錯誤處理程式、在表單中新增錯誤處理程式、使用規則編輯器的叫用服務來新增自訂錯誤處理程式、設定規則編輯器來新增自訂錯誤處理程式、使用規則編輯器新增自訂錯誤處理程式
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
source-git-commit: a635a727e431a73086a860249e4f42d297882298
workflow-type: tm+mt
source-wordcount: '2428'
ht-degree: 4%

---

# 在AEM Adaptive Forms中新增自訂錯誤處理常式 {#error-handlers-in-adaptive-form}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/creating-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html) |
| AEM as a Cloud Service  | 本文章 |

AEM Forms為表單提交提供現成可用的成功和錯誤處理常式。 此外，還提供自訂錯誤處理常式函式的功能。 例如，您可以針對特定錯誤程式碼在後端叫用自訂的工作流程，或通知客戶服務已關閉。處理常式是根據伺服器回應執行的使用者端功能。 使用API叫用外部服務時，資料會傳輸到伺服器進行驗證，伺服器會傳回回應給使用者端，其中包含提交成功或錯誤事件的相關資訊。 此資訊會以引數形式傳遞至相關處理常式，以執行函式。 錯誤處理常式有助於管理和顯示所遇到的錯誤或驗證問題。

![錯誤處理常式工作流程，以瞭解如何在表單中新增自訂錯誤處理常式](/help/forms/assets/error-handler-workflow.png)

調適型表單會根據預先設定的驗證條件，驗證您在欄位中提供的輸入，並檢查由設定為叫用外部服務的REST端點傳回的各種錯誤。 您可以根據搭配最適化表單使用的資料來源來設定驗證條件。 例如，如果您使用RESTful Web服務做為資料來源，您可以在Swagger定義檔案中定義驗證條件。

如果輸入值符合驗證准則，則會將值提交至資料來源，否則「最適化表單」會使用錯誤處理常式顯示錯誤訊息。 與此方法類似，最適化Forms整合自訂錯誤處理常式，以執行資料驗證。 如果輸入值不符合驗證准則，則錯誤訊息會在最適化表單中的欄位層級顯示。 當伺服器傳回的驗證錯誤訊息為標準訊息格式時，就會發生這種情況。


## 使用錯誤處理常式 {#uses-of-error-handler}

錯誤處理常式有多種用途。 以下列出錯誤處理常式函式的一些用法：
* **執行驗證**：錯誤處理從根據預先定義的規則或條件驗證使用者輸入開始。 使用者填寫最適化表單時，錯誤處理常式會驗證輸入內容，確保符合所需格式、長度或任何其他限制。

* **提供即時意見反應**：偵測到任何錯誤時，錯誤處理常式會立即向使用者顯示回饋，例如對應表單欄位下的內嵌錯誤訊息。 此意見回饋可幫助使用者識別和更正錯誤，而無需提交表單並等待回應。


* **顯示錯誤訊息**：當最適化表單提交遇到任何驗證錯誤時，錯誤處理常式會顯示適當的錯誤訊息。 錯誤訊息應清晰簡潔，並醒目提示需要注意的特定欄位。

* **反白顯示錯誤的欄位**：為了吸引使用者注意特定的不正確欄位，錯誤處理常式會醒目顯示或視覺化地區分對應欄位。 透過變更背景顏色、新增圖示或框線，或任何其他可協助使用者快速找到並解決錯誤的視覺提示來執行此操作。


## 失敗/錯誤回應格式 {#failure-response-format}

如果伺服器驗證錯誤訊息為以下標準格式，最適化表單會在欄位層級顯示錯誤。
以下程式碼說明現有的失敗回應結構：

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


其中：

* `errorCausedBy` 說明失敗的原因。
* `errors` 提及未通過驗證准則的欄位的SOM運算式以及驗證錯誤訊息。
* `originCode` 欄位由AEM新增，並包含外部服務傳回的http狀態代碼。
* `originMessage` 欄位由AEM新增，並包含外部服務傳回的原始錯誤資料。

隨著AEM Forms版本的功能改良和後續更新，現有的失敗回應結構已變更為以RFC7807為基礎的新格式，並可回溯相容於現有的失敗回應結構：

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<SOM expression of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * 請確定錯誤回應結構包含 **fieldName** 或 **dataRef**.
> * 確保 **內容型別** 標題為 **application/problem+json**.

其中：
* `type (required)` 指定失敗型別。 可以是下列其中一個值：
   * `SERVER_SIDE_VALIDATION` 表示因為伺服器端驗證而失敗。
   * `FORM_SUBMISSION` 表示表單提交期間失敗
   * `SERVICE_INVOCATION` 表示在第三方服務呼叫期間發生失敗。
   * `FAILURE` 表示一般失敗。
   * `VALIDATION_ERROR` 表示因驗證錯誤而失敗。

* `title (optional)` 提供失敗的標題或簡短說明。
* `detail (optional)` 如有必要，會提供失敗的其他詳細資訊。
* `instance (optional)` 代表與失敗關聯的例項或識別碼，可協助追蹤或識別失敗的特定發生次數。
* `validationErrors (required)` 包含有關驗證錯誤的資訊。 其包含下列欄位：
   * `fieldname` 提及未通過驗證准則的欄位的SOM運算式。
   * `dataRef` 代表驗證失敗之欄位的JSON路徑或XPath。
   * `details` 包含驗證錯誤訊息和錯誤欄位。
* `originCode (optional)` 欄位由AEM新增，並包含外部服務傳回的http狀態代碼
* `originMessage (optional)` 欄位由AEM新增，並包含外部服務傳回的原始錯誤資料。

### 範例錯誤回應格式 {#sample-error-response-format}

顯示錯誤回應的部分選項包括：

+++  根據最適化表單fieldName屬性


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```

  您可以點選任何欄位並選取「 」，以檢視最適化表單中任何欄位的SOM運算式 **[!UICONTROL 檢視SOM運算式]**.

  ![在自訂錯誤處理常式中顯示錯誤回應的最適化表單欄位的SOM運算式](/help/forms/assets/custom-error-handler-somexpression.png)

+++


+++ 根據最適化表單dataRef屬性

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "/Pet/id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

  ![在自訂錯誤處理常式中顯示錯誤回應的最適化表單欄位的資料參考](/help/forms/assets/custom-errorhandler-dataref.png)

您可以檢視dataRef的值，位於 **[!UICONTROL 屬性]** 表單元件的視窗。

+++


## 使用規則編輯器新增錯誤處理常式 {#add-error-handler-using-rule-editor}

使用 [規則編輯器的叫用服務](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 動作，您會根據您用於最適化表單的資料來源來定義驗證條件。 如果您使用RESTful Web服務做為資料來源，則可以在Swagger定義檔案中定義驗證條件。 使用調適型Forms中的錯誤處理常式函式和規則編輯器，您便可有效地管理和自訂錯誤處理。 您可以使用規則編輯器定義條件，並設定要在規則觸發時執行的所需動作。 「最適化表單」會根據預先設定的驗證條件，驗證您在欄位中輸入的輸入。 如果輸入值不符合驗證標準，錯誤訊息會在最適化表單的欄位層級顯示。

>[!NOTE]
>
> * 若要使用錯誤處理常式搭配規則編輯器的「叫用」服務動作，請使用表單資料模型設定Adaptive Forms 。
> * 如果錯誤回應位於標準結構描述中，則會提供預設錯誤處理常式，以在欄位上顯示錯誤訊息。 您也可以從自訂錯誤處理常式函式呼叫預設錯誤處理常式。

使用規則編輯器，您可以：
* [新增預設錯誤處理常式函式](#add-default-errror-handler)
* [新增自訂錯誤處理常式函式](#add-custom-errror-handler)


### 新增預設錯誤處理常式函式 {#add-default-errror-handler}

如果錯誤回應位於標準結構描述或伺服器端驗證失敗，則支援預設錯誤處理常式，以在欄位上顯示錯誤訊息。
若要瞭解如何使用預設錯誤處理常式，請 [規則編輯器的叫用服務](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 動作，以具有兩個欄位的簡單調適型表單為例， **寵物ID** 和 **寵物名稱** 並在以下位置使用預設錯誤處理常式： **寵物ID** 用於檢查由配置為呼叫外部服務的REST端點傳回的各種錯誤的欄位，例如 `200 - OK`，`404 - Not Found`， `400 - Bad Request`. 若要使用規則編輯器的叫用服務動作新增預設錯誤處理常式，請執行下列步驟：

1. 在撰寫模式中開啟最適化表單，選取表單元件並點選 **[!UICONTROL 規則編輯器]** 以開啟規則編輯器。
1. 點選「**[!UICONTROL 建立]**」。
1. 在中建立條件 **時間** 區段。 例如， **時間[Pet ID欄位名稱]** 已變更。 選取已變更，從 **選取狀態** 下拉式清單。
1. 在 **則** 區段，選取 **[!UICONTROL 啟動服務]** 從 **選取動作** 下拉式清單。
1. 選取 **貼文服務** 以及與其對應的資料繫結 **輸入** 區段。 例如，驗證 **寵物ID**，選取 **貼文服務** 作為 **GET/pet/{petId}** 並選取 **寵物ID** 在 **輸入** 區段。
1. 選取資料繫結 **輸出** 區段。 選取 **寵物名稱** 在 **輸出** 區段。
1. 選取 **[!UICONTROL 預設錯誤處理常式]** 從 **錯誤處理常式** 區段。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

![在表單中新增欄位驗證檢查的預設錯誤處理常式](/help/forms/assets/default-error-handler.png)

根據此規則，您為下列專案輸入的值 **寵物ID** 檢查驗證 **寵物名稱** 使用REST端點叫用的外部服務。 如果以資料來源為基礎的驗證條件失敗，則錯誤訊息會顯示在欄位層級。

![在表單中新增預設錯誤處理常式以處理錯誤回應時，顯示預設錯誤訊息](/help/forms/assets/default-error-message.png)

### 新增自訂錯誤處理常式函式 {#add-custom-errror-handler}

您可以新增自訂錯誤處理常式函式，以執行某些動作，例如：

* 處理使用非標準或標準錯誤回應的錯誤回應。 請務必注意，這些非標準錯誤回應不符合 [錯誤回應的標準結構描述](#failure-response-format).
* 將analytics事件傳送至任何analytics平台。 例如，Adobe Analytics。
* 顯示包含錯誤訊息的模型對話方塊。

除了上述動作之外，自訂錯誤處理常式也可用來執行符合特定使用者需求的自訂函式。

自訂錯誤處理常式是函式（使用者端程式庫），設計用於回應外部服務傳回的錯誤，並為一般使用者提供自訂回應。 任何具有註解的使用者端資料庫 `@errorHandler` 視為自訂錯誤處理常式函式。 此註解有助於識別 `.js` 檔案。
若要瞭解如何使用建立和使用自訂錯誤處理常式， [規則編輯器的Invoke服務](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 動作，以含有兩個欄位的最適化表單為例， **寵物ID** 和 **寵物名稱** 並在以下位置使用自訂錯誤處理常式： **寵物ID** 用於檢查由配置為呼叫外部服務的REST端點傳回的各種錯誤的欄位，例如 `200 - OK`，`404 - Not Found`， `400 - Bad Request`.

若要在最適化表單中新增和使用自訂錯誤處理常式，請執行以下步驟：
1. [建立自訂錯誤處理常式](#create-custom-error-message)
1. [使用規則編輯器來設定自訂錯誤處理常式](#use-custom-error-handler)

#### 1.建立自訂錯誤處理常式 {#create-custom-error-message}

若要建立自訂錯誤函式，請執行下列步驟：

1. [原地複製您的 AEM Forms as a Cloud Service 存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. 在下建立資料夾 `[AEM Forms as a Cloud Service repository folder]/apps/` 資料夾。 例如，建立名為的資料夾 `experience-league`
1. 瀏覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` 並建立 `ClientLibraryFolder` 作為 `clientlibs`.
1. 建立名為的資料夾 `js`.
1. 導覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` 資料夾。
1. 新增JavaScript檔案，例如 `function.js`. 此檔案包含自訂錯誤處理常式的程式碼。
讓我們將下列程式碼新增至JavaScript檔案，以在瀏覽器主控台中顯示從REST服務端點收到的回應和標題。

   ```javascript
       /**
       * Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers);
           console.log("Custom Error Handler processing end...");
       }
   ```

   若要從自訂錯誤處理常式呼叫預設錯誤處理常式，會使用下列程式碼範例行：
   `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `

   >[!NOTE]
   >
   > 在 `.content.xml` 檔案，新增 `allowProxy` 和 `categories` 屬性。
   >
   > * `allowProxy = [Boolean]true`
   > * `categories= customfunctionsdemo`
   >例如，在此案例中， [custom-errorhandler-name] 提供為 `customfunctionsdemo`.

1. 儲存 `function.js` 檔案。
1. 導覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` 資料夾。
1. 新增文字檔為 `js.txt`. 檔案包含：

   ```javascript
       #base=js
       functions.js
   ```

1. 儲存 `js.txt` 檔案。\
   建立的資料夾結構如下所示：

   ![已建立的使用者端資料庫資料夾結構](/help/forms/assets/customclientlibrary_folderstructure.png)

   >[!NOTE]
   >
   > 若要深入瞭解如何建立自訂函式，請按一下 [規則編輯器中的自訂函式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#write-rules).

1. 使用下列命令新增、認可及推送存放庫中的變更：

   ```javascript
       git add .
       git commit -a -m "Adding error handling files"
       git push
   ```

1. [執行管道.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)

管道執行成功後，自訂錯誤處理常式便可在最適化表單規則編輯器中使用。 現在，讓我們瞭解如何在AEM Forms中使用規則編輯器的叫用服務來設定和使用自訂錯誤處理常式。

#### 2.使用規則編輯器來設定自訂錯誤處理常式 {#use-custom-error-handler}

在實作最適化表單中的自訂錯誤處理常式之前，請確定使用者端程式庫名稱位於 **[!UICONTROL 使用者端資料庫類別]** 會與的類別選項中指定的名稱對齊 `.content.xml` 檔案。

![在調適型表單容器設定中新增使用者端資料庫的名稱](/help/forms/assets/client-library-category-name.png)

在此情況下，使用者端程式庫名稱提供為 `customfunctionsdemo` 在 `.content.xml` 檔案。

若要使用自訂錯誤處理常式，請使用 **[!UICONTROL 規則編輯器的叫用服務]** 動作：

1. 在撰寫模式中開啟最適化表單，選取表單元件並點選 **[!UICONTROL 規則編輯器]** 以開啟規則編輯器。
1. 點選「**[!UICONTROL 建立]**」。
1. 在中建立條件 **時間** 區段。 例如，當 **[Pet ID欄位名稱]** 已變更，請選取 **已變更** 從 **選取狀態** 下拉式清單。
1. 在 **則** 區段，選取 **[!UICONTROL 啟動服務]** 從 **選取動作** 下拉式清單。
1. 選取 **貼文服務** 以及與其對應的資料繫結 **輸入** 區段。 例如，驗證 **寵物ID**，選取 **貼文服務** 作為 **GET/pet/{petId}** 並選取 **寵物ID** 在 **輸入** 區段。
1. 選取資料繫結 **輸出** 區段。 例如，選取 **寵物名稱** 在 **輸出** 區段。
1. 選取 **[!UICONTROL 自訂錯誤處理常式]** 從 **[!UICONTROL 錯誤處理常式]** 區段。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

![在表單中新增自訂錯誤處理常式，以處理錯誤回應](/help/forms/assets/custom-error-handler.png)

根據此規則，您為下列專案輸入的值 **寵物ID** 檢查驗證 **寵物名稱** 使用REST端點叫用的外部服務。 如果以資料來源為基礎的驗證條件失敗，則錯誤訊息會顯示在欄位層級。

![在表單中新增自訂錯誤處理常式，以處理錯誤回應](/help/forms/assets/custom-error-handler-message.png)

開啟瀏覽器主控台，並檢查從REST服務端點收到的回應和標頭，以取得驗證錯誤訊息。


自訂錯誤處理常式函式會根據錯誤回應，負責執行其他動作，例如顯示模組對話方塊或傳送分析事件。 自訂錯誤處理常式函式可靈活地根據特定使用者需求量身打造錯誤處理方式。

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Tap ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and tap  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and tap **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and tap **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->
