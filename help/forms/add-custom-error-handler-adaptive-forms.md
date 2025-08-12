---
title: 在適用於AEM的最適化Forms的最適化Forms中新增自訂錯誤處理常式
description: AEM Forms 會使用為調用外部服務所設定的 REST 端點，為表單提供現成可用的成功和錯誤處理常式。您可以在 AEM Adaptive Form 中新增預設錯誤處理常式和自訂錯誤處理常式。
keywords: 新增自訂錯誤處理常式、新增預設錯誤處理常式、在表單中新增錯誤處理常式、使用規則編輯器的調用服務來新增自訂的錯誤處理常式、設定規則編輯器以新增自訂錯誤處理常式、使用規則編輯器以新增自訂錯誤處理常式
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Foundation Components
exl-id: 198a26a9-d6bb-457d-aab8-0a5d15177c48
role: User, Developer
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 83%

---

# 在AEM Adaptive Forms中新增自訂錯誤處理常式 {#error-handlers-in-adaptive-form}

>[!NOTE]
>
> Adobe建議針對[建立新的Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)或[將Adaptive Forms新增至AEM Sites頁面](/help/forms/creating-adaptive-form-core-components.md)，使用現代且可擴充的資料擷取[核心元件](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文說明使用基礎元件製作最適化Forms的舊方法。

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

AEM Forms 為表單提交提供現成可用的成功和錯誤處理常式。這還可提供自訂錯誤處理常式函數的功能。例如，您可以針對特定錯誤程式碼在後端叫用自訂的工作流程，或通知客戶服務已關閉。處理常式是根據伺服器回應執行的用戶端函數。當使用 API 調用外部服務時，資料會傳輸至伺服器進行驗證，伺服器會向用戶端傳回回應，其中包含有關提交成功或錯誤事件的資訊。這項資訊可以參數傳遞至相關處理常式以執行該函數。錯誤處理常式有助於管理和顯示遇到的錯誤或驗證問題。

![錯誤處理常式工作流程，可了解如何在表單中新增自訂錯誤處理程序](/help/forms/assets/error-handler-workflow.png)

最適化表單會根據預設的驗證標準來驗證您在欄位中輸入的數值，並查看為調用外部服務所設定 REST 端點傳回的各種錯誤。您可以根據與最適化表單一起使用的資料來源設定驗證標準。例如，如果您以資料來源來使用 RESTful Web 服務，則可以在 Swagger 定義檔案中定義驗證標準。

如果輸入值符合驗證標準，則將輸入值提交到資料來源，否則最適化表單會使用錯誤處理常式來顯示錯誤訊息。與此方法類似，最適化表單會與自定義錯誤處理常式整合以執行資料驗證。如果輸入值不符合驗證標準，則錯誤訊息會在最適化表單的欄位層級來顯示。當伺服器傳回的驗證錯誤訊息採用標準訊息格式時，就會發生這種情況。


## 錯誤處理常式的用途 {#uses-of-error-handler}

錯誤處理常式有多種用途。下面列出了錯誤處理常式函數的一些用途：

* **執行驗證**：錯誤處理首先會根據預定義的規則或標準來驗證使用者的輸入值。當用戶填寫最適化表單時，錯誤處理常式會驗證輸入值，以確保符合規定的格式、長度或任何其他限制。

* **提供即時意見回饋**：當檢測到任何錯誤時，錯誤處理常式會立即向使用者顯示意見回饋，例如對應表單欄位下方的內聯錯誤訊息。此意見回饋可幫助使用者識別並糾正錯誤，而無需提交表單並等待回應。


* **顯示錯誤訊息**：當最適化表單提交遇到任何驗證錯誤時，錯誤處理常式會顯示正確的錯誤訊息。錯誤訊息應該清晰、簡潔，並醒目顯示需要注意的特定欄位。

* **醒目顯示錯誤欄位**：為了吸引用戶注意特定的不正確欄位，錯誤處理常式會醒目顯示或以視覺效果區分相應的欄位。執法方法是改變背景顏色、新增圖示或邊框或，或新增任何有助使用者快速找出和解決錯誤的其他視覺提示。


## 失敗/錯誤回應格式 {#failure-response-format}

如果伺服器驗證錯誤訊息採用以下標準格式，則最適化表單會在欄位層級顯示錯誤。
以下代碼旨在解說現有失敗回應的結構：

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
* `errors`提及未通過驗證准則的欄位的SOM運算式以及驗證錯誤訊息。
* `originCode` 由 AEM 新增的欄位，並包含外部服務傳回的 http 狀態代碼。
* `originMessage`由 AEM 新增的欄位，並包含外部服務傳回的原始錯誤資料。

隨著 AEM Forms 版本的功能改善和後續更新，現有的失敗回應結構會改變為以 RFC7807 為主的新格式，可回溯相容於現有的失敗回應結構：

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
> * 確保錯誤回應結構包括 **fieldName** 或 **dataRef**。
> * 確保 **ContentType** 標頭是 **應用程式/問題+json**。

其中：

* `type (required)` 是指定失敗類型。這可以是以下其中一個值：
   * `SERVER_SIDE_VALIDATION` 是指由於伺服器端驗證的失敗。
   * `FORM_SUBMISSION` 是指表單提交期間的失敗
   * `SERVICE_INVOCATION` 是指第三方服務調用期間的失敗。
   * `FAILURE` 是指一般失敗。
   * `VALIDATION_ERROR` 是指由於驗證錯誤的失敗。

* `title (optional)` 會提供失敗的標題或簡要說明。
* `detail (optional)` 會提供有關失敗的其他詳細資訊 (若需要)。
* `instance (optional)` 會表示與失敗相關的執行個體或識別碼，有助於追蹤或識別失敗的具體情況。
* `validationErrors (required)` 包含有關驗證錯誤的資訊。其中包含下列欄位：
   * `fieldname`提及未通過驗證准則的欄位的SOM運算式。
   * `dataRef` 表示驗證失敗欄位的 JSON 路徑或 XPath。
   * `details` 包含帶有錯誤欄位的驗證錯誤訊息。
* `originCode (optional)` 由 AEM 新增的欄位，並包含外部服務傳回的 http 狀態代碼
* `originMessage (optional)`由 AEM 新增的欄位，並包含外部服務傳回的原始錯誤資料。

### 錯誤回應格式範例 {#sample-error-response-format}

顯示錯誤回應的一些選項是：

+++  以調適型單為主的 fieldName 屬性


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

  您可以點選任何欄位並選取&#x200B;**[!UICONTROL 檢視SOM運算式]**，以檢視最適化表單中任何欄位的SOM運算式。

  ![適用性表單欄位的Som運算式，以在自訂錯誤處理常式中顯示錯誤回應](/help/forms/assets/custom-error-handler-somexpression.png)

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

  ![最適化表單欄位的資料參考，以在自訂錯誤處理常式中顯示錯誤回應](/help/forms/assets/custom-errorhandler-dataref.png)

您可以在表單元件的「**[!UICONTROL 屬性]**」視窗內查看 dataRef 值。

+++


## 使用規則編輯器新增錯誤處理常式 {#add-error-handler-using-rule-editor}

透過使用[規則編輯器調用服務](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=zh-Hant#invoke)的動作，您可以根據與最適化表單一起使用的資料來源來定義驗證標準。如果您以資料來源來使用 RESTful Web 服務，則可以在 Swagger 定義檔案中定義驗證標準。透過使用最適化表單中的錯誤處理常式函數和規則編輯器，您可以有效地管理和自訂錯誤處理。您可以使用規則編輯器來定義條件，並設定觸發規則時要執行的必要動作。調適型單會根據預設的驗證標準來驗證您在欄位中輸入的資料。如果輸入值不符合驗證標準，最適化表單的欄位層級會顯示錯誤訊息。

>[!NOTE]
>
> * 若要使用錯誤處理常式搭配規則編輯器的「叫用」服務動作，請使用表單資料模型(FDM)來設定Adaptive Forms 。
> * 如果錯誤回應是在標準結構描述中，則系統會提供預設的錯誤處理常式以顯示欄位的錯誤訊息。您還可以從自訂錯誤處理常式函數來呼叫預設的錯誤處理常式。

使用規則編輯器可以：

* [新增預設錯誤處理常式函數](#add-default-errror-handler)
* [新增自訂錯誤處理常式函數](#add-custom-error-handler-function)


### 新增預設錯誤處理常式函數 {#add-default-errror-handler}

如果錯誤回應是在標準結構描述中或是伺服器端驗證失敗，則系統會支援預設錯誤處理常式以顯示欄位的錯誤訊息。
若要了解如何使用採用[規則編輯器調用服務](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=zh-Hant#invoke)動作的預設錯誤處理常式，請以含有兩個欄位的簡單最適化表單為例 (**寵物 ID** 和&#x200B;**寵物名稱**)，並在「**寵物 ID**」欄位使用預設的錯誤處理常式，查看為調用外部服務所設定 REST 端點傳回的各種錯誤，例如 `200 - OK`、`404 - Not Found`、`400 - Bad Request`。要使用規則編輯器的調用服務操作添加默認錯誤處理程序，請執行以下步驟：

1. 以編寫模式開啟最適化表單，選取表單元件，然後選取&#x200B;**[!UICONTROL 規則編輯器]**&#x200B;以開啟規則編輯器。
1. 選取「**[!UICONTROL 建立]**」。
1. 在「**何時**」規則部分中建立條件。例如，[寵物 ID 欄位名稱&#x200B;]&#x200B;**&#x200B;**&#x200B;何時變更。「選取」從「**選取狀態**」下拉式清單變更「選取」。
1. 在「**然後**」部分，從「**選取動作**」下拉式清單中選取「**[!UICONTROL 調用服務]**」。
1. 選取「**郵遞服務**」，及其自「**輸入**」部分的對應資料綁定。例如，若要驗證&#x200B;**Pet ID**，請選取&#x200B;**貼文服務**&#x200B;作為&#x200B;**GET /pet/{petId}**，並在&#x200B;**輸入**&#x200B;區段中選取&#x200B;**Pet ID**。
1. 從「**輸出**」部分，選取資料綁定。選取「**寵物名稱**」(在「**輸出**」部分)。
1. 選取「**[!UICONTROL 預設錯誤處理常式]**」(來自「**錯誤處理常式**」部分)。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

![新增預設錯誤處理常式，以便在表單中進行欄位驗證檢查](/help/forms/assets/default-error-handler.png)

根據此規則，您輸入的「**寵物 ID**」值會使用 REST 端點調用的外部服務檢查&#x200B;**寵物名稱**&#x200B;的驗證。如果根據資料來源的驗證標準失敗，欄位層級將顯示錯誤訊息。

![當您在表單中新增預設錯誤處理常式來處理錯誤回應時會顯示預設錯誤訊息](/help/forms/assets/default-error-message.png)

### 新增自訂錯誤處理常式函數

您可以新增自訂錯誤處理常式函數來執行一些動作，例如：

* 處理使用非標準或標準錯誤回應的錯誤回應。要特別注意，這些非標準錯誤回應不符合[錯誤回應的標準結構描述](#failure-response-format)。
* 將分析事件發送到任何分析平台。(例如，Adobe Analytics。)
* 顯示有錯誤訊息的模式對話框。

除了上述動作之外，自訂錯誤處理常式還可用於執行符合特定使用者要求的自訂函數。

自訂錯誤處理常式是一個函數 (用戶端資料庫)，旨在回應外部服務傳回的錯誤並向一般使用者提供自訂回應。任何有附註 `@errorHandler` 的用戶端資料庫會被視為是自訂錯誤處理常式函數。該附註有助於識別 `.js` 檔案中指定的錯誤處理常式函數。
若要了解如何建立和使用採用[規則編輯器調用服務](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=zh-Hant#invoke)動作的自訂錯誤處理常式，讓我們以含有兩個欄位的簡單最適化表單為例 (**寵物 ID** 和&#x200B;**寵物名稱**)，並在「**寵物 ID**」欄位使用自訂的錯誤處理程式，查看為調用外部服務所設定 REST 端點傳回的各種錯誤，例如 `200 - OK`、`404 - Not Found`、`400 - Bad Request`。

若要在最適化表單中新增和使用自訂錯誤處理常式，請執行以下步驟：

1. [新增錯誤處理常式的自訂函式](#1-add-the-custom-function-for-the-error-handler)
2. [使用規則編輯器設定自訂錯誤處理常式](#use-custom-error-handler)

#### 1.新增錯誤處理常式的自訂函式

若要瞭解如何新增自訂函式，請按一下[根據核心元件在適用性表單中建立自訂函式](/help/forms/custom-function-core-component-create-function.md#create-a-custom-function)。

<!-- To create a custom error function, perform the following steps:

1. [Clone your AEM Forms as a Cloud Service Repository](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#accessing-git). 
2. Create a folder under the `[AEM Forms as a Cloud Service repository folder]/apps/` folder. For example, create a folder named as `experience-league`
3. Navigate to `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` and create a `ClientLibraryFolder` as `clientlibs`.
4. Create a folder named `js`.
5. Navigate to the `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` folder. -->

1. 在JavaScript檔案中新增以下自訂錯誤處理常式的程式碼，例如`function.js`。 該檔案包含自訂錯誤處理常式的代碼。
讓我們將以下代碼新增至 JavaScript 檔案中，以便在瀏覽器主控台中顯示從 REST 服務端點接收到的回應和標頭。

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

   >[!NOTE]
   >
   > * 若要從自訂錯誤處理常式呼叫預設錯誤處理常式，會使用下列程式碼範例行： `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `
   > * 在`.content.xml`檔案中，新增`allowProxy`和`categories`屬性，以在最適化表單中使用自訂錯誤處理常式使用者端程式庫。
   >
   >   * `allowProxy = [Boolean]true`
   >   * `categories= customfunctionsdemo`
   >       例如，在這種情況下，提供 [自訂-錯誤處理常式-名稱] 為 `customfunctionsdemo`。


1. 新增、認可及推送存放庫中的變更。

<!--
1. Save the `function.js` file.
1. Navigate to the `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` folder.
2. Add a text file as `js.txt`. The file contains:

    ```javascript
        #base=js
        functions.js
    ```

3. Save the `js.txt` file.    
The created folder structure looks like:

    ![Created Client Library Folder Structure](/help/forms/assets/customclientlibrary_folderstructure.png) 
    using the below commands:
         
    ```javascript

        git add .
        git commit -a -m "Adding error handling files"
        git push
    ```
-->

1. [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)。

成功執行管道後，自訂錯誤處理常式將可在最適化表單規則編輯器中使用。現在，讓我們了解如何使用 AEM Forms 規則編輯器的調用服務來設定和使用自訂錯誤處理常式。

#### &#x200B;2. 使用規則編輯器設定自訂錯誤處理常式 {#use-custom-error-handler}

在最適化表單中實施自訂錯誤處理常式之前，請確保&#x200B;**[!UICONTROL 用戶端資料庫類別]**&#x200B;中的用戶端資料庫名稱符合 `.content.xml` 檔案類別選項所指定的名稱。

![在最適化表單容器設定中新增用戶端資料庫的名稱](/help/forms/assets/client-library-category-name.png)

在此情況下，使用者端資料庫名稱會在`customfunctionsdemo`檔案中以`.content.xml`的形式提供。

若要使用自訂錯誤處理常式，請使用&#x200B;**[!UICONTROL 規則編輯器調用服務]**&#x200B;行動：

1. 以編寫模式開啟最適化表單，選取表單元件，然後選取&#x200B;**[!UICONTROL 規則編輯器]**&#x200B;以開啟規則編輯器。
1. 選取「**[!UICONTROL 建立]**」。
1. 在「**何時**」規則部分中建立條件。例如，當&#x200B;**[寵物 ID 欄位名稱]**&#x200B;已變更，請從「**選擇狀態**」下拉式清單選取「**已變更**」。
1. 在「**然後**」部分，從「**選取動作**」下拉式清單中選取「**[!UICONTROL 調用服務]**」。
1. 選取「**郵遞服務**」，及其自「**輸入**」部分的對應資料綁定。例如，若要驗證&#x200B;**Pet ID**，請選取&#x200B;**貼文服務**&#x200B;作為&#x200B;**GET /pet/{petId}**，並在&#x200B;**輸入**&#x200B;區段中選取&#x200B;**Pet ID**。
1. 從「**輸出**」部分，選取資料綁定。例如，選取「**寵物名稱**」(在「**輸出**」部分)。
1. 選取「**[!UICONTROL 自訂錯誤處理程式]**」(來自「**[!UICONTROL 錯誤處理程式]**」部分)。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

![在表單中新增自訂錯誤處理常式，以處理錯誤回應](/help/forms/assets/custom-error-handler.png)

根據此規則，您輸入的「**寵物 ID**」值會使用 REST 端點調用的外部服務檢查&#x200B;**寵物名稱**&#x200B;的驗證。如果根據資料來源的驗證標準失敗，欄位層級將顯示錯誤訊息。

![在表單中新增自訂錯誤處理常式以處理錯誤回應](/help/forms/assets/custom-error-handler-message.png)s

開啟瀏覽器主控台，並查看從 REST 服務端點接收的回應和標頭是否有驗證錯誤訊息。


自訂錯誤處理常式函數負責根據錯誤回應執行其他動作，例如顯示模式對話框或發送分析事件。自訂錯誤處理常式函數可提供靈活性，會根據特定使用者需求來訂制錯誤處理行動。

