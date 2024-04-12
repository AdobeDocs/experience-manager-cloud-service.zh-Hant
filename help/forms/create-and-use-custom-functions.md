---
title: 在最適化表單中建立及新增自訂函式
description: AEM Forms支援自訂函式，可讓使用者在規則編輯器中建立並使用自己的函式。
keywords: 新增自訂函式、使用自訂函式、建立自訂函式，以及在規則編輯器中使用自訂函式。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
source-git-commit: a22ecddf7c97c5894cb03eb44296e0562ac46ddb
workflow-type: tm+mt
source-wordcount: '3039'
ht-degree: 2%

---


<span class="preview"> 本文包含部分搶鮮版功能的內容。 這些搶鮮版功能只能透過我們的 [發行前通道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). 搶鮮版計畫下的功能包括：
* 自訂函式中的選用引數支援
* 自訂函式的快取功能
* 自訂函式的全域範圍物件和欄位物件支援
* 支援現代JavaScript功能，例如let和arrow函式（ES10支援）。
確保 [核心元件已設定為3.0.8版](https://github.com/adobe/aem-core-forms-components) 在自訂功能中使用發行前功能。 </span>

# 最適化Forms中的自訂函式（核心元件）

## 簡介

AEM Forms支援自訂函式，可讓使用者定義JavaScript函式以實作複雜的商業規則。 這些自訂功能可協助您根據指定需求操控和處理輸入的資料，進而擴充表單的功能。 它們還可以根據預先定義的條件來啟用表單行為的動態變更。

### 使用自訂函式 {#uses-of-custom-function}

在最適化Forms中使用自訂函式的優點包括：

* **資料處理**：自訂函式可協助處理輸入至表單欄位中的資料。
* **資料驗證**：自訂函式可讓您對表單輸入執行自訂檢查，並提供指定的錯誤訊息。
* **動態行為**：自訂函式可讓您根據特定條件控制表單的動態行為。 例如，您可以顯示/隱藏欄位、修改欄位值或動態調整表單邏輯。
* **整合**：您可以使用自訂函式與外部API或服務整合。 它有助於從外部來源擷取資料、傳送資料至外部Rest端點，或根據外部事件執行自訂動作。

自訂函式基本上是新增到JavaScript檔案中的使用者端程式庫。 建立自訂函式後，規則編輯器中即可供使用者在最適化表單中選擇。 自訂函式由規則編輯器中的JavaScript註解來識別。

### 自訂函式支援的JavaScript註解 {#js-annotations}

JavaScript註解是用來提供JavaScript程式碼的中繼資料。 其中包含以特定符號(例如/**和@)開頭的註解。 註解提供關於程式碼中函式、變數和其他元素的重要資訊。 最適化表單支援自訂函式的下列JavaScript註解：

* **名稱**
此名稱用於識別最適化表單的規則編輯器中的自訂函式。 下列語法可用來命名自訂函式：
   * `@name [functionName] <Function Name>`
   * `@function [functionName] <Function Name>`
   * `@func [functionName] <Function Name>`。
     `functionName` 是函式的名稱。 不允許空格。
     `<Function Name>` 是函式在最適化表單的規則編輯器中的顯示名稱。
如果函式名稱與函式本身的名稱相同，則可以省略 `[functionName]` 語法中的。 <!-- For example,  in the `calculateAge` custom function, the name is defined as:
`* @name calculateAge` -->

* **引數**
引數是自訂函式使用的引數清單。 函式可支援多個引數。 下列語法可用來定義自訂函式中的引數：
   * `@param {type} name <Parameter Description>`
   * `@argument` `{type} name <Parameter Description>`
   * `@arg` `{type}` `name <Parameter Description>`.
     `{type}` 代表引數型別。  允許的引數型別包括：
      * string：代表單一字串值。
      * 數字：代表單一數值。
      * 布林值：代表單一布林值（true或false）。
      * 字串[]：代表字串值的陣列。
      * 數字[]：代表數值陣列。
      * 布林值[]：代表布林值的陣列。
      * date：代表單一日期值。
      * 日期[]：代表日期值的陣列。
      * array：代表包含各種型別值的泛型陣列。
      * object：代表傳遞至自訂函式的表單物件，而非直接傳遞其值。
      * scope：代表自訂函式在執行階段所使用的全域物件。 這會宣告為JavaScript註解中的最後一個引數，且不會顯示在調適型表單的規則編輯器中。 scope引數可存取表單或元件的物件，以觸發表單處理所需的規則或事件。

  引數型別不區分大小寫，而且引數名稱中不允許使用空格。

  `<Parameter Description>` 包含有關引數用途的詳細資訊。 它可以有多個字詞。

  依預設，所有引數都是必要引數。 您可以透過新增引數將引數定義為選用的 `=` 在引數型別之後或將引數名稱括在  `[]`. 在JavaScript註解中定義為選用引數的規則編輯器會顯示為選用引數。
若要將變數定義為選用引數，您可以使用下列任一語法：

   * `@param {type=} Input1`
在上一行程式碼中， `Input1` 是不含任何預設值的選用引數。 以預設值宣告選用引數：
     `@param {string=<value>} input1`

     `input1` 作為選用引數，預設值設為 `value`.

   * `@param {type} [Input1]`
在上一行程式碼中， `Input1` 是不含任何預設值的選用引數。 以預設值宣告選用引數：
     `@param {array} [input1=<value>]`
     `input1` 是陣列型別的選用引數，其預設值設定為 `value`.
請確定引數型別括在大括弧中 {} 且引數名稱會括在方括弧中 [].

     請考慮下列程式碼片段，其中input2定義為選用引數：

     ```javascript
          /**
          * optional parameter function
          * @name OptionalParameterFunction
          * @param {string} input1 
          * @param {string=} input2 
          * @return {string}
         */
         function OptionalParameterFunction(input1, input2) {
         let result = "Result: ";
         result += input1;
         if (input2 !== null) {
             result += " " + input2;
         }
         return result;
         }
     ```

     下圖使用 `OptionalParameterFunction` 規則編輯器中的自訂函式：

     ![選用或必要的引數](/help/forms/assets/optional-default-params.png)

     您可以儲存規則而不指定所需引數的值，但規則不會執行，且會顯示警告訊息如下：

     ![不完整的規則警告訊息](/help/forms/assets/incomplete-rule.png)

     當使用者將選用引數留空時，則會將「未定義」值傳遞給選用引數的自訂函式。

* **傳回型別**
傳回型別會指定自訂函式在執行後傳回的值型別。 下列語法可用來定義自訂函式中的傳回型別：
   * `@return {type}`
   * `@returns {type}`
     `{type}` 代表函式的傳回型別。 允許的傳回型別為：
      * string：代表單一字串值。
      * 數字：代表單一數值。
      * 布林值：代表單一布林值（true或false）。
      * 字串[]：代表字串值的陣列。
      * 數字[]：代表數值陣列。
      * 布林值[]：代表布林值的陣列。
      * date：代表單一日期值。
      * 日期[]：代表日期值的陣列。
      * array：代表包含各種型別值的泛型陣列。
      * object：代表表單物件，而非直接代表其值。

     傳回型別不區分大小寫。

* **私人**
宣告為私用的自訂函式不會出現在最適化表單的規則編輯器中的自訂函式清單中。 自訂函式預設為公用。 宣告自訂函式為private的語法為 `@private`.

若要進一步瞭解如何在JSDocs中定義選用引數， [按一下這裡](https://jsdoc.app/tags-param).

## 建立自訂函式時的准則 {#considerations}

若要在規則編輯器中列出自訂函式，您可以使用下列任一格式：

* **包含或不包含jsdoc註解的函式陳述式**

您可以建立包含或不包含jsdoc註解的自訂函式。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
如果使用者未將任何JavaScript註解新增至自訂函式，則會依函式名稱在規則編輯器中列出。 不過，建議您加入JavaScript註解，以提升自訂函式的可讀性。

* **具有強制JavaScript註解或註解的Arrow函式**

您可以使用箭頭函式語法來建立自訂函式：

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

* **含有必要JavaScript註解或註解的函式運算式**

若要列出最適化表單的規則編輯器中的自訂函式，請以下列格式建立自訂函式：

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

## 建立自訂函式 {#create-custom-function}

建立使用者端程式庫以呼叫規則編輯器中的自訂函式。 如需詳細資訊，請參閱 [使用使用者端資料庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

建立自訂函式的步驟如下：
1. [建立使用者端資源庫](#create-client-library)
1. [將使用者端程式庫新增至最適化表單](#use-custom-function)

### 建立使用者端資源庫 {#create-client-library}

您可以透過新增使用者端資料庫來新增自訂函式。 若要建立使用者端程式庫，請執行下列步驟：

1. [複製AEM Formsas a Cloud Service存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#accessing-git).
1. 在 `[AEM Forms as a Cloud Service repository folder]/apps/` 檔案夾中建立一個檔案夾。例如，建立名為的資料夾 `experience-league`.
1. 瀏覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` 並建立 `ClientLibraryFolder`. 例如，建立使用者端資源庫資料夾為 `customclientlibs`.
1. 新增屬性 `categories` 字串型別值的組合。 例如，指派值 `customfunctionscategory` 至 `categories` 的屬性 `customclientlibs` 資料夾。

   >[!NOTE]
   >
   > 您可以選擇任何名稱 `client library folder` 和 `categories` 屬性。

1. 建立一個名為 `js` 的檔案夾。
1. 導覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` 檔案夾。
1. 新增JavaScript檔案，例如 `function.js`. 此檔案包含自訂函式的程式碼。
1. 儲存 `function.js` 檔案。
1. 導覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` 檔案夾。
1. 新增文字檔案為`js.txt`。該檔案包含：

   ```javascript
       #base=js
       functions.js
   ```

1. 儲存 `js.txt` 檔案。
1. 使用以下命令在存放庫中新增、提交和推播變更：

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline) 以部署自訂函式。

管道執行成功後，使用者端資料庫中新增的自訂函式即可在中使用 [最適化表單規則編輯器](/help/forms/rule-editor-core-components.md).

### 將使用者端程式庫新增至最適化表單{#use-custom-function}

將使用者端程式庫部署到Forms CS環境後，請在最適化表單中使用其功能。 若要在最適化表單中新增使用者端程式庫

1. 在編輯模式中開啟您的表單。 若要以編輯模式開啟表單，請選取表單並選取 **[!UICONTROL 編輯]**.
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 開啟 **[!UICONTROL 基本]** 標籤並選取 **[!UICONTROL 使用者端資料庫類別]** 從下拉式清單（在此例中為「選取」） `customfunctionscategory`)。

   ![新增自訂函式使用者端程式庫](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > 透過在「 」中指定逗號分隔清單，可新增多個類別 **[!UICONTROL 使用者端資料庫類別]** 欄位。

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

您可在以下位置使用自訂函式： [最適化表單的規則編輯器](/help/forms/rule-editor-core-components.md) 使用 [Javascript註解](##js-annotations).

## 在最適化表單中使用自訂函式

在最適化表單中，您可以使用 [規則編輯器中的自訂函式](/help/forms/rule-editor-core-components.md). 讓我們將下列程式碼新增至JavaScript檔案(`Function.js` 檔案)，以根據出生日期計算年齡(YYYY-MM-DD)。 建立自訂函式為 `calculateAge()` 以出生日期作為輸入並傳回年齡：

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

在上述範例中，當使用者以格式(YYYY-MM-DD)輸入出生日期時，自訂函式 `calculateAge` 叫用並傳回年齡。

![在規則編輯器中重新計算自訂函式](/help/forms/assets/custom-function-calculate-age.png)

讓我們預覽表單，以觀察如何透過規則編輯器實作自訂函式：

![在規則編輯器表單預覽中再次計算自訂函式](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 您可參考以下內容 [自訂函式](/help/forms/assets//customfunctions.zip) 資料夾。 使用下載此資料夾並將其安裝在您的AEM執行個體中 [封裝管理員](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

### 支援自訂函式中的非同步函式 {#support-of-async-functions}

非同步自訂函式未出現在規則編輯器清單中。 不過，您也可以在使用同步函式運算式建立的自訂函式中叫用非同步函式。

![同步和非同步自訂函式](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> 在自訂函式中呼叫非同步函式的優點在於，非同步函式允許同時執行多個任務，而自訂函式中使用的每個函式的結果都是如此。

檢視以下程式碼，瞭解如何使用自訂函式叫用非同步函式：

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

在上述範例中，asyncFunction函式為 `asynchronous function`. 它會透過建立 `GET` 要求給 `https://petstore.swagger.io/v2/store/inventory`. 它會使用來等待回應 `await`，使用將回應內文剖析為JSON `response.json()`，然後傳回資料。 此 `callAsyncFunction` 函式是同步的自訂函式，會叫用 `asyncFunction` 函式中，並在主控台中顯示回應資料。 雖然 `callAsyncFunction` 函式是同步的，它會呼叫非同步asyncFunction函式，並使用處理其結果 `then` 和 `catch` 陳述式。

若要檢視其運作情況，讓我們新增按鈕，並為按鈕建立規則，此規則會在按鈕按一下時叫用非同步函式。

![建立非同步函式的規則](/help/forms/assets/rule-for-async-funct.png)

請參考下方主控台視窗的圖例，以示範當使用者按一下 `Fetch` 按鈕，自訂函式 `callAsyncFunction` 會叫用，進而呼叫非同步函式 `asyncFunction`. Inspect主控台視窗中，檢視按下按鈕時的回應：

![主控台視窗](/help/forms/assets/async-custom-funct-console.png)

讓我們來探討自訂函式的功能。

## 自訂功能的各種功能

您可以使用自訂函式，將個人化功能新增至表單。 這些函式支援各種功能，例如使用特定欄位、使用全域欄位或快取。 此彈性可讓您根據組織的需求自訂表格。

### 自訂函式中的欄位和全域範圍物件 {#support-field-and-global-objects}

欄位物件是指表單中的個別元件或元素，例如文字欄位、核取方塊。 全域範圍物件是指在整個表單中可存取的全域變數或設定。 讓我們檢視下列程式碼片段：

```JavaScript
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals 
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time
    field.value = formattedDateTime;
    }
```

>[!NOTE]
>
> 此 `param {scope} globals` 必須是最後一個引數，且不會顯示在最適化表單的規則編輯器中。

在上述程式碼片段中，名為的自訂函式 `updateDateTime` 會採用欄位物件和全域物件等引數。 使用全域範圍存取物件的日期和時間。 欄位代表在表單中顯示格式化日期與時間值的文字方塊物件。

讓我們瞭解自訂函式如何透過使用欄位和全域物件 `Contact Us` 使用不同使用案例的表單。

![聯絡我們表單](/help/forms/assets/contact-us-form.png)

#### **使用案例**：使用顯示面板 `SetProperty` 規則

在自訂函式中新增下列程式碼，如 [create-custom-function](#create-custom-function) 區段，將表單欄位設為 `Required`.

```javascript
    
	/**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> 您可以使用中的可用屬性來設定欄位屬性 `[form-path]/jcr:content/guideContainer.model.json`.

在此範例中，驗證 `personaldetails` 面板會在按一下按鈕時發生。 如果在面板、另一個面板、 `feedback` 面板，在按一下按鈕時就會顯示。

讓我們為「 」建立一個規則 `Next` 按鈕，驗證 `personaldetails` 面板並做出 `feedback`  當使用者按一下 `Next` 按鈕。

![設定屬性](/help/forms/assets/custom-function-set-property.png)

請參閱下圖，以示範 `personaldetails` 按一下 `Next` 按鈕。 萬一中 `personaldetails` 已驗證， `feedback` 面板會變成可見。

![設定屬性表單預覽](/help/forms/assets/set-property-form-preview.png)

如果的欄位中出現錯誤 `personaldetails` 面板，按一下「 」即可將其顯示在欄位層級 `Next` 按鈕，以及 `feedback` 面板會保持不可見。

![設定屬性表單預覽](/help/forms/assets/set-property-panel.png)

#### **使用案例**：驗證欄位。

在自訂函式中新增下列程式碼，如 [create-custom-function](#create-custom-function) 區段，以驗證欄位。

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> 若未在中傳遞引數 `validate()` 功能，驗證表單。

在此範例中，自訂驗證模式套用至 `contact` 欄位。 使用者必須輸入開頭為的電話號碼 `10` 後面接著 `8` 數字。 如果使用者輸入的電話號碼開頭不是 `10` 或包含大於或小於 `8` 數字，按一下按鈕時會出現驗證錯誤訊息：

![電子郵件地址驗證模式](/help/forms/assets/custom-function-validation-pattern.png)

現在，下一步是建立 `Next` 驗證按鈕 `contact` 欄位在按鈕上按一下。

![驗證模式](/help/forms/assets/custom-function-validate.png)

請參閱下圖以示範，如果使用者輸入的電話號碼開頭不是 `10`，欄位層級會顯示錯誤訊息：

![電子郵件地址驗證模式](/help/forms/assets/custom-function-validate-error-message.png)

如果使用者輸入有效的電話號碼和 `personaldetails` 面板已經過驗證， `feedback` 面板會顯示在畫面上：

![電子郵件地址驗證模式](/help/forms/assets/validate-form-preview-form.png)

#### **使用案例**：重設面板

在自訂函式中新增下列程式碼，如 [create-custom-function](#create-custom-function) 區段，以重設面板。

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> 若未在中傳遞引數 `reset()` 功能，驗證表單。

在此範例中， `personaldetails` 面板會在按一下 `Clear` 按鈕。 下一步是建立 `Clear` 按一下按鈕以重設面板的按鈕。

![清除按鈕](/help/forms/assets/custom-function-reset-field.png)

請參閱下圖以顯示，如果使用者按一下 `clear` 按鈕， `personaldetails` 面板重設：

![重設表單](/help/forms/assets/custom-function-reset-form.png)

#### **使用案例**：在欄位層級顯示自訂訊息並將欄位標籤為無效的方式

您可以使用 `markFieldAsInvalid()` 函式將欄位定義為無效，並在欄位層級設定自訂錯誤訊息。 此 `fieldIdentifier` 值可以是 `fieldId`，或 `field qualifiedName`，或 `field dataRef`. 物件的值，命名為 `option` 可以是 `{useId: true}`， `{useQualifiedName: true}`，或 `{useDataRef: true}`.
用於將欄位標示為無效並設定自訂訊息的語法如下：

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

在自訂函式中新增下列程式碼，如 [create-custom-function](#create-custom-function) 區段，以在欄位層級啟用自訂訊息。

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

在此範例中，如果使用者在註解文字方塊中輸入少於15個字元，則欄位層級會顯示自訂訊息。

下一步是建立 `comments` 欄位：

![將欄位標籤為無效](/help/forms/assets/custom-function-invalid-field.png)

請參閱下列示範，說明在 `comments` 欄位會觸發在欄位層級顯示自訂訊息：

![將欄位標示為無效的預覽表單](/help/forms/assets/custom-function-invalidfield-form.png)

如果使用者在評論文字方塊中輸入超過15個字元，則欄位會通過驗證並提交表單：

![將欄位標示為有效的預覽表單](/help/forms/assets/custom-function-validfield-form.png)


#### **使用案例**：將變更後的資料提交至伺服器

下列程式碼行：
`globals.functions.submitForm(globals.functions.exportData(), false);` 用於在操作後提交表單資料。
* 第一個引數是要提交的資料。
* 第二個引數代表是否要在提交前驗證表單。 它是 `optional` 並設為 `true` 依預設。
* 第三個引數為 `contentType` 提交的，也就是 `optional` 預設值為 `multipart/form-data`.

在自訂函式中新增下列程式碼，如 [create-custom-function](#create-custom-function) 區段，若要在伺服器上提交操作過的資料：

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */

    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

在此範例中，如果使用者離開 `comments` 文字方塊空白， `NA` 在提交表單時提交至伺服器。

現在為以下專案建立規則 `Submit` 提交資料的按鈕：

![提交資料](/help/forms/assets/custom-function-submit-data.png)

請參考的圖例 `console window` 以下示範，如果使用者離開 `comments` Textbox空白，則值為 `NA` 已提交至伺服器：

![在主控台視窗提交資料](/help/forms/assets/custom-function-submit-data-form.png)

您也可以檢查主控台視窗，以檢視提交給伺服器的資料：

![控制檯視窗中的Inspect資料](/help/forms/assets/custom-function-submit-data-console-data.png)

## 自訂函式的快取支援

Adaptive Forms會在規則編輯器中擷取自訂函式清單時，實作自訂函式的快取，以增強回應時間。 訊息為 `Fetched following custom functions list from cache` 顯示在 `error.log` 檔案。

![支援快取的自訂函式](/help/forms/assets/custom-function-cache-error.png)

如果修改自訂函式，快取會失效，並加以剖析。

## 疑難排解

如果包含自訂函式程式碼的JavaScript檔案發生錯誤，則自訂函式不會列在調適型表單的規則編輯器中。 若要檢查自訂函式清單，您可以導覽至 `error.log` 錯誤檔案。 發生錯誤時，自訂函式清單會顯示為空白：

![錯誤記錄檔](/help/forms/assets/custom-function-list-error-file.png)

如果沒有錯誤，則會擷取自訂函式並出現在 `error.log` 檔案。 訊息為 `Fetched following custom functions list` 顯示在 `error.log` 檔案：

![具有適當自訂函式的錯誤記錄檔](/help/forms/assets/custom-function-list-fetched-in-error.png)

## 考量事項

* 此 `parameter type` 和 `return type` 不支援 `None`.

* 自訂函式清單中不支援的函式包括：
   * 產生器函式
   * 非同步/等待函式
   * 方法定義
   * 類別方法
   * 預設引數
   * Rest引數

## 另請參閱 {#see-also}

{{see-also}}


