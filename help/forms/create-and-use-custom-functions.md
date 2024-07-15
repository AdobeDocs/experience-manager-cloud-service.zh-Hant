---
title: 在最適化表單中建立及新增自訂函式
description: AEM Forms支援自訂函式，可讓使用者在規則編輯器中建立並使用自己的函式。
keywords: 新增自訂函式、使用自訂函式、建立自訂函式，以及在規則編輯器中使用自訂函式。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '4333'
ht-degree: 1%

---


# 最適化Forms中的自訂函式（核心元件）

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service  | 本文章 |

## 簡介

AEM Forms支援自訂函式，可讓使用者定義JavaScript函式以實作複雜的商業規則。 這些自訂功能可協助您根據指定需求操控和處理輸入的資料，進而擴充表單的功能。 它們還可以根據預先定義的條件來啟用表單行為的動態變更。

>[!NOTE]
>
> 請確定[核心元件](https://github.com/adobe/aem-core-forms-components)設定為最新版本，以使用最新功能。

### 使用自訂函式 {#uses-of-custom-function}

在最適化Forms中使用自訂函式的優點包括：
* **資料處理**：自訂函式可協助處理輸入到表單欄位中的資料。
* **資料驗證**：自訂函式可讓您對表單輸入執行自訂檢查，並提供指定的錯誤訊息。
* **動態行為**：自訂函式可讓您根據特定條件控制表單的動態行為。 例如，您可以顯示/隱藏欄位、修改欄位值或動態調整表單邏輯。
* **整合**：您可以使用自訂函式與外部API或服務整合。 它有助於從外部來源擷取資料、傳送資料至外部Rest端點，或根據外部事件執行自訂動作。

自訂函式基本上是新增至JavaScript檔案中的使用者端程式庫。 建立自訂函式後，規則編輯器中即可供使用者在最適化表單中選擇。 自訂函式由規則編輯器中的JavaScript註解識別。

### 支援自訂功能的JavaScript註解 {#js-annotations}

JavaScript註解是用來提供JavaScript程式碼的中繼資料。 其中包含以特定符號(例如/**和@)開頭的註解。 註解提供關於程式碼中函式、變數和其他元素的重要資訊。 最適化表單支援下列自訂函式的JavaScript註解：

#### 名稱

此名稱用於識別最適化表單的規則編輯器中的自訂函式。 下列語法可用來命名自訂函式：

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`。
  `functionName`是函式的名稱。 不允許空格。
  `<Function Name>`是適用性表單的規則編輯器中函式的顯示名稱。
如果函式名稱與函式本身的名稱相同，您可以在語法中省略`[functionName]`。

#### 參數

引數是自訂函式使用的引數清單。 函式可支援多個引數。 下列語法可用來定義自訂函式中的引數：

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`。
  `{type}`代表引數型別。  允許的引數型別包括：

   * string：代表單一字串值。
   * 數字：代表單一數值。
   * 布林值：代表單一布林值（true或false）。
   * string[]：代表字串值的陣列。
   * number[]：代表數值陣列。
   * 布林值[]：代表布林值的陣列。
   * date：代表單一日期值。
   * date[]：代表日期值的陣列。
   * array：代表包含各種型別值的泛型陣列。
   * object：代表傳遞至自訂函式的表單物件，而非直接傳遞其值。
   * 範圍：代表全域物件，其中包含唯讀變數，例如表單例項、目標欄位例項，以及在自訂函式內執行表單修改的方法。 這會宣告為JavaScript註解中的最後一個引數，且不會顯示在最適化表單的規則編輯器中。 scope引數可存取表單或元件的物件，以觸發表單處理所需的規則或事件。 如需有關Globals物件及其使用方式的進一步資訊，[請按一下這裡](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects)。

引數型別不區分大小寫，而且引數名稱中不允許使用空格。

`<Parameter Description>`包含有關引數用途的詳細資料。 它可以有多個字詞。

**選用引數**
依預設，所有引數都是必要引數。 您可以在引數型別後新增`=`或在`[]`中封入引數名稱，將引數定義為選用引數。 在JavaScript註解中定義為選用性的引數，會在規則編輯器中顯示為選用專案。
若要將變數定義為選用引數，您可以使用下列任一語法：

* `@param {type=} Input1`

在上一行程式碼中，`Input1`是選用引數，沒有任何預設值。 以預設值宣告選用引數：
`@param {string=<value>} input1`

`input1`為選擇性引數，預設值設為`value`。

* `@param {type} [Input1]`

在上一行程式碼中，`Input1`是選用引數，沒有任何預設值。 以預設值宣告選用引數：
`@param {array} [input1=<value>]`
`input1`是陣列型別的選用引數，預設值設定為`value`。
請確定將引數型別括在大括弧{}中，並將引數名稱括在方括弧中。

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

下圖顯示規則編輯器中使用的`OptionalParameterFunction`自訂函式：

![選用或必要的引數](/help/forms/assets/optional-default-params.png)

您可以儲存規則而不指定所需引數的值，但規則不會執行，且會顯示警告訊息如下：

![不完整的規則警告](/help/forms/assets/incomplete-rule.png)

當使用者將選用引數留空時，則會將「未定義」值傳遞給選用引數的自訂函式。

若要進一步瞭解如何在JSDocs中定義選用引數，[請按一下這裡](https://jsdoc.app/tags-param)。

#### 傳回型別

傳回型別會指定自訂函式在執行後傳回的值型別。 下列語法可用來定義自訂函式中的傳回型別：

* `@return {type}`
* `@returns {type}`
  `{type}`代表函式的傳回型別。 允許的傳回型別為：
   * string：代表單一字串值。
   * 數字：代表單一數值。
   * 布林值：代表單一布林值（true或false）。
   * string[]：代表字串值的陣列。
   * number[]：代表數值陣列。
   * 布林值[]：代表布林值的陣列。
   * date：代表單一日期值。
   * date[]：代表日期值的陣列。
   * array：代表包含各種型別值的泛型陣列。
   * object：代表表單物件，而非直接代表其值。

  傳回型別不區分大小寫。

#### 私人

宣告為私用的自訂函式不會出現在最適化表單的規則編輯器中的自訂函式清單中。 自訂函式預設為公用。 宣告自訂函式為私用的語法為`@private`。


## 建立自訂函式時的准則

若要在規則編輯器中列出自訂函式，您可以使用下列任一格式：

### 包含或不包含jsdoc註解的函式陳述式

您可以建立包含或不包含jsdoc註解的自訂函式。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
如果使用者未將任何JavaScript註解新增至自訂函式，則會依函式名稱在規則編輯器中列出。 不過，建議您加入JavaScript註解，以提升自訂函式的可讀性。

### 箭頭功能與強制JavaScript註解或註解

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

如果使用者沒有將任何JavaScript註解新增到自訂函式，則自訂函式不會列在最適化表單的規則編輯器中。

### 含有強制JavaScript註解或註解的函式運算式

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

如果使用者沒有將任何JavaScript註解新增到自訂函式，則自訂函式不會列在最適化表單的規則編輯器中。

## 建立自訂函數 {#create-custom-function}

建立使用者端程式庫以呼叫規則編輯器中的自訂函式。 如需詳細資訊，請參閱[使用使用者端資料庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing)。

建立自訂函式的步驟如下：
1. [建立使用者端資源庫](#create-client-library)
1. [將使用者端程式庫新增至最適化表單](#use-custom-function)


### 建立自訂函式的先決條件

開始將自訂函式新增至最適化Forms之前，請確定您具備下列條件：

**軟體：**

* **純文字編輯器(IDE)**：雖然任何純文字編輯器都可以運作，但Microsoft Visual Studio Code之類的整合式開發環境(IDE)可提供進階功能，讓編輯更輕鬆。

* **Git：**&#x200B;管理程式碼變更需要此版本控制系統。 如果您尚未安裝，請從https://git-scm.com下載。

### 建立使用者端資源庫 {#create-client-library}

您可以透過新增使用者端資料庫來新增自訂函式。 若要建立使用者端程式庫，請執行下列步驟：

**複製存放庫**

複製您的[AEM Formsas a Cloud Service存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#accessing-git)：

1. 開啟命令列或終端機視窗。

1. 導覽至您電腦上要儲存存放庫的位置。

1. 執行以下命令以複製存放庫：

   `git clone [Git Repository URL]`

這個命令會下載存放庫並在您的電腦上建立複製存放庫的本機資料夾。 在本指南中，我們將此資料夾稱為[AEMaaCS專案目錄]。

**新增使用者端資料庫資料夾**

若要將新的使用者端程式庫資料夾新增至[AEMaaCS專案目錄]，請遵循下列步驟：

1. 在編輯器中開啟[AEMaaCS專案目錄]。

   ![自訂函式資料夾結構](/help/forms/assets/custom-library-folder-structure.png)

1. 找到`ui.apps`。
1. 新增資料夾。 例如，新增名為`experience-league`的資料夾。
1. 導覽至`/experience-league/`資料夾並新增`ClientLibraryFolder`。 例如，建立名為`customclientlibs`的使用者端資料庫資料夾。

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**新增檔案和資料夾至使用者端資料庫資料夾**

將下列專案新增至新增的使用者端程式庫資料夾：

* .content.xml檔案
* js.txt檔案
* js資料夾

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. 在`.content.xml`中新增下列幾行程式碼：

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > 您可以為`client library folder`和`categories`屬性選擇任何名稱。

1. 在`js.txt`中新增下列幾行程式碼：

   ```javascript
         #base=js
       function.js
   ```
1. 在`js`資料夾中，將JavaScript檔案新增為`function.js`，其中包含自訂函式：

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
1. 儲存檔案。

![自訂函式資料夾結構](/help/forms/assets/custom-function-added-files.png)

**在filter.xml中包含新資料夾**：

1. 導覽至[AEMaaCS專案目錄]中的`/ui.apps/src/main/content/META-INF/vault/filter.xml`檔案。

1. 開啟檔案，並在結尾新增下列行：

   `<filter root="/apps/experience-league" />`
1. 儲存檔案。

![自訂函式篩選器xml](/help/forms/assets/custom-function-filterxml.png)

**將新建立的使用者端資料庫資料夾部署至您的AEM環境**

將AEM as a Cloud Service [AEMaaCS專案目錄]部署至您的Cloud Service環境。 若要部署至您的Cloud Service環境：

1. 提交變更

   1. 使用以下命令在存放庫中新增、提交和推播變更：

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. 部署更新的程式碼：

   1. 透過現有的完整棧疊管道觸發計畫碼部署。 這會自動建置及部署更新的程式碼。

如果您尚未設定管道，請參閱[上的指南如何設定AEM Formsas a Cloud Service的管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)。

管道執行成功後，新增到使用者端資料庫中的自訂函式便可在[最適化表單規則編輯器](/help/forms/rule-editor-core-components.md)中使用。

### 將使用者端程式庫新增至最適化表單{#use-custom-function}

將使用者端程式庫部署到Forms CS環境後，請在最適化表單中使用其功能。 若要在最適化表單中新增使用者端程式庫

1. 在編輯模式中開啟您的表單。 若要以編輯模式開啟表單，請選取表單並選取&#x200B;**[!UICONTROL 編輯]**。
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 開啟&#x200B;**[!UICONTROL 基本]**&#x200B;標籤，並從下拉式清單中選取&#x200B;**[!UICONTROL 使用者端程式庫類別]**&#x200B;的名稱（在此案例中選取`customfunctionscategory`）。

   ![正在新增自訂函式使用者端程式庫](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > 在&#x200B;**[!UICONTROL 使用者端資料庫類別]**&#x200B;欄位中指定逗號分隔的清單，可新增多個類別。

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

您可以使用[JavaScript註解](##js-annotations)，在最適化表單](/help/forms/rule-editor-core-components.md)的[規則編輯器中使用自訂函式。

## 在最適化表單中使用自訂函式

在最適化表單中，您可以在規則編輯器](/help/forms/rule-editor-core-components.md)中使用[自訂函式。 讓我們將下列程式碼新增至JavaScript檔案（`Function.js`檔案），以根據出生日期計算年齡(YYYY-MM-DD)。 建立自訂函式為`calculateAge()`，它以出生日期作為輸入並傳回年齡：

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

在上述範例中，當使用者以(YYYY-MM-DD)格式輸入出生日期時，會叫用自訂函式`calculateAge`並傳回年齡。

![規則編輯器中的Calcualte Agae自訂函式](/help/forms/assets/custom-function-calculate-age.png)

讓我們預覽表單，以觀察如何透過規則編輯器實作自訂函式：

![在規則編輯器表單預覽中計算Agae自訂函式](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 您可以參考下列[自訂函式](/help/forms/assets//customfunctions.zip)資料夾。 使用[封裝管理員](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager)下載此資料夾，並將其安裝在您的AEM執行個體中。


### 使用自訂函式設定下拉式清單選項

核心元件中的規則編輯器不支援&#x200B;**屬性的**&#x200B;設定選項以在執行階段設定下拉式清單選項。 不過，您可以使用自訂函式來設定下拉式清單選項。

檢視以下程式碼，瞭解如何使用自訂函式來設定下拉式清單選項：

```javascript
    /**
    * @name setEnums
    * @returns {string[]}
    **/
    function setEnums() {
    return ["0","1","2","3","4","5","6"];   
    }

    /**
    * @name setEnumNames
    * @returns {string[]}
    **/
    function setEnumNames() {
    return ["Sunday","Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
    }
```

在上述程式碼中，`setEnums`是用來設定`enum`屬性，`setEnumNames`是用來設定下拉式清單的`enumNames`屬性。

讓我們為`Next`按鈕建立規則，當使用者按一下`Next`按鈕時，此規則會設定下拉式清單選項的值：

![下拉式清單選項](/help/forms/assets/drop-down-list-options.png)

請參考下圖，示範按一下「顯示」按鈕時，下拉式清單的選項設定位置：

![規則編輯器中的下拉式清單選項](/help/forms/assets/drop-down-option-rule-editor.png)



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

在上述範例中，asyncFunction函式是`asynchronous function`。 它透過向`https://petstore.swagger.io/v2/store/inventory`發出`GET`請求來執行非同步操作。 它會使用`await`等待回應、使用`response.json()`將回應本文剖析為JSON，然後傳回資料。 `callAsyncFunction`函式是同步自訂函式，會叫用`asyncFunction`函式並在主控台中顯示回應資料。 雖然`callAsyncFunction`函式是同步的，但它會呼叫非同步asyncFunction函式，並以`then`和`catch`陳述式處理其結果。

若要檢視其運作情況，讓我們新增按鈕，並為按鈕建立規則，此規則會在按鈕按一下時叫用非同步函式。

![為非同步函式建立規則](/help/forms/assets/rule-for-async-funct.png)

請參考下方主控台視窗的圖例，以示範當使用者按一下`Fetch`按鈕時，會叫用自訂函式`callAsyncFunction`，進而呼叫非同步函式`asyncFunction`。 Inspect主控台視窗中，檢視對按鈕點按的回應：

![主控台視窗](/help/forms/assets/async-custom-funct-console.png)

讓我們來探討自訂函式的功能。

## 自訂功能的各種功能

您可以使用自訂函式，將個人化功能新增至表單。 這些函式支援各種功能，例如使用特定欄位、使用全域欄位或快取。 此彈性可讓您根據組織的需求自訂表格。

### 自訂函式中的欄位和全域範圍物件 {#support-field-and-global-objects}

欄位物件是指表單中的個別元件或元素，例如文字欄位、核取方塊。 全域物件包含唯讀變數，例如表單例項、目標欄位例項，以及在自訂函式內進行表單修改的方法。

>[!NOTE]
>
> `param {scope} globals`必須是最後一個引數，且不會顯示在調適型表單的規則編輯器中。

<!-- Let us look at the following code snippet:

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
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

讓我們瞭解自訂函式如何透過使用不同使用案例的`Contact Us`表單來使用欄位和全域物件。

![連絡我們表單](/help/forms/assets/contact-us-form.png)

+++ **使用案例**：使用`SetProperty`規則顯示面板

在自訂函式中新增下列程式碼（如[create-custom-function](#create-custom-function)區段中所述），以將表單欄位設為`Required`。

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
> * 您可以使用位於`[form-path]/jcr:content/guideContainer.model.json`中的可用屬性來設定欄位屬性。
> * 使用Globals物件的`setProperty`方法修改表單時，其本質是非同步的，不會在執行自訂函式時反映出來。

在此範例中，在按一下按鈕時就會進行`personaldetails`面板的驗證。 如果在面板中未偵測到任何錯誤，則按一下按鈕時，另一個面板（`feedback`面板）會變成可見。

讓我們為`Next`按鈕建立規則，以驗證`personaldetails`面板，並讓使用者按一下`Next`按鈕時顯示`feedback`面板。

![設定屬性](/help/forms/assets/custom-function-set-property.png)

請參閱下圖以示範，按一下`Next`按鈕後，`personaldetails`面板在哪裡驗證。 如果`personaldetails`中的所有欄位都已驗證，`feedback`面板就會顯示出來。

![設定屬性表單預覽](/help/forms/assets/set-property-form-preview.png)

如果「`personaldetails`」面板的欄位中存在錯誤，則按一下「`Next`」按鈕後，這些錯誤將顯示在欄位層級，而「`feedback`」面板將保持隱藏狀態。

![設定屬性表單預覽](/help/forms/assets/set-property-panel.png)

+++

+++ **使用案例**：驗證欄位。

依照[create-custom-function](#create-custom-function)區段中的說明，在自訂函式中新增下列程式碼，以驗證欄位。

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
> 如果未在`validate()`函式中傳遞引數，則會驗證表單。

在此範例中，自訂驗證模式套用至`contact`欄位。 使用者必須輸入以`10`開頭後接`8`位數的電話號碼。 如果使用者輸入的電話號碼不是以`10`開頭或包含多於`8`位數，則按一下按鈕時會出現驗證錯誤訊息：

![電子郵件地址驗證模式](/help/forms/assets/custom-function-validation-pattern.png)

現在，下一步是為`Next`按鈕建立規則，以驗證按鈕點選上的`contact`欄位。

![驗證模式](/help/forms/assets/custom-function-validate.png)

請參考下圖以示範，如果使用者輸入的電話號碼不是以`10`開頭，則欄位層級會顯示錯誤訊息：

![電子郵件地址驗證模式](/help/forms/assets/custom-function-validate-error-message.png)

如果使用者輸入有效的電話號碼且`personaldetails`面板中的所有欄位都經過驗證，`feedback`面板就會顯示在畫面上：

![電子郵件地址驗證模式](/help/forms/assets/validate-form-preview-form.png)

+++

+++ **使用案例**：重設面板

依照[create-custom-function](#create-custom-function)區段中的說明，在自訂函式中新增下列程式碼，以重設面板。

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
> 如果未在`reset()`函式中傳遞引數，則會驗證表單。

在此範例中，按一下`Clear`按鈕時，`personaldetails`面板會重設。 下一步是為`Clear`按鈕建立規則，以在按鈕點選時重設面板。

![清除按鈕](/help/forms/assets/custom-function-reset-field.png)

請參閱下圖以顯示，如果使用者按一下`clear`按鈕，`personaldetails`面板會重設：

![重設表單](/help/forms/assets/custom-function-reset-form.png)

+++

+++ **使用案例**：在欄位層級顯示自訂訊息，並將欄位標籤為無效

您可以使用`markFieldAsInvalid()`函式將欄位定義為無效，並在欄位層級設定自訂錯誤訊息。 `fieldIdentifier`值可以是`fieldId`、`field qualifiedName`或`field dataRef`。 名稱為`option`的物件值可以是`{useId: true}`、`{useQualifiedName: true}`或`{useDataRef: true}`。
用於將欄位標示為無效並設定自訂訊息的語法如下：

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

在自訂函式中新增下列程式碼（如[create-custom-function](#create-custom-function)區段中所述），以在欄位層級啟用自訂訊息。

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

下一步是為`comments`欄位建立規則：

![將欄位標示為無效](/help/forms/assets/custom-function-invalid-field.png)

請參閱下列示範，說明在`comments`欄位中輸入負面意見會觸發在欄位層級顯示自訂訊息：

![將欄位標示為無效的預覽表單](/help/forms/assets/custom-function-invalidfield-form.png)

如果使用者在評論文字方塊中輸入超過15個字元，該欄位將會驗證並提交表單：

![將欄位標示為有效的預覽表單](/help/forms/assets/custom-function-validfield-form.png)

+++

+++ **使用案例**：將變更的資料提交至伺服器

下列程式碼行：
`globals.functions.submitForm(globals.functions.exportData(), false);`用於在操作後提交表單資料。
* 第一個引數是要提交的資料。
* 第二個引數代表是否要在提交前驗證表單。 它是`optional`，預設為`true`。
* 第三個引數是提交的`contentType`，也是選擇性的，預設值為`multipart/form-data`。 其他值可以是`application/json`和`application/x-www-form-urlencoded`。

在自訂函式中新增下列程式碼（如[create-custom-function](#create-custom-function)區段中所述），以在伺服器上提交操作過的資料：

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

在此範例中，如果使用者將`comments`文字方塊留空，則在提交表單時會將`NA`提交至伺服器。

現在，為提交資料的`Submit`按鈕建立規則：

![提交資料](/help/forms/assets/custom-function-submit-data.png)

請參考下圖`console window`以示範，如果使用者將`comments`文字方塊留空，則會在伺服器上提交值為`NA`：

![在主控台視窗提交資料](/help/forms/assets/custom-function-submit-data-form.png)

您也可以檢查主控台視窗，以檢視提交給伺服器的資料：

在主控台視窗![Inspect資料](/help/forms/assets/custom-function-submit-data-console-data.png)

+++

+++ **使用案例**：覆寫表單提交成功和錯誤處理常式

新增下列程式碼行（如[create-custom-function](#create-custom-function)區段中所述），以自訂表單提交的提交或失敗訊息，並在強制回應方塊中顯示表單提交訊息：

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

在此範例中，當使用者使用`customSubmitSuccessHandler`和`customSubmitErrorHandler`自訂函式時，成功和失敗訊息會顯示在強制回應視窗中。 JavaScript函式`showModal(type, message)`可用來在熒幕上動態建立及顯示模型對話方塊。

現在，為成功的表單提交建立規則：

![表單提交成功](/help/forms/assets/form-submission-success.png)

請參考下圖以示範，成功提交表單時，成功訊息會顯示於強制回應視窗中：

![表單提交成功訊息](/help/forms/assets/form-submission-success-message.png)

同樣地，讓我們為失敗的表單提交建立規則：

![表單提交失敗](/help/forms/assets/form-submission-fail.png)

請參考下圖以示範，當表單提交失敗時，強制回應視窗中會顯示錯誤訊息：

![表單提交失敗訊息](/help/forms/assets/form-submission-fail-message.png)

若要以預設方式顯示表單提交成功與失敗，`Default submit Form Success Handler`與`Default submit Form Error Handler`函式為現成可用。

如果自訂提交處理常式無法在現有AEM專案或表單中如預期般執行，請參閱[疑難排解](#troubleshooting)區段。

+++

+++ **使用案例**：在可重複面板的特定執行個體中執行動作

使用可重複面板上的視覺化規則編輯器建立的規則會套用至可重複面板的最後一個例項。 若要為可重複面板的特定執行個體編寫規則，我們可以使用自訂函式。

讓我們建立另一個表格，以收集前往目的地的旅行者相關資訊。 將旅行者面板新增為可重複的面板，使用者可在其中使用`Add Traveler`按鈕新增5個旅行者的詳細資料。

![旅行者資訊](/help/forms/assets/traveler-info-form.png)

新增下列程式碼行（如[create-custom-function](#create-custom-function)區段中所述），以於可重複面板的特定執行個體中執行動作，而非最後一個執行個體：

```javascript
/**
* @name hidePanelInRepeatablePanel
* @param {scope} globals
*/
function hidePanelInRepeatablePanel(globals)
{    
    var repeatablePanel = globals.form.travelerinfo;
    // hides a panel inside second instance of repeatable panel
    globals.functions.setProperty(repeatablePanel[1].traveler, {visible : false});
}  
```

在此範例中，`hidePanelInRepeatablePanel`自訂函式會在可重複面板的特定執行個體中執行動作。 在上述程式碼中，`travelerinfo`代表可重複的面板。 `repeatablePanel[1].traveler, {visible: false}`程式碼會在可重複面板的第二個執行個體中隱藏面板。

讓我們新增標示為`Hide`的按鈕，並新增規則以隱藏可重複面板的第二個執行個體。

![隱藏面板規則](/help/forms/assets/custom-function-hidepanel-rule.png)

請參考以下影片，示範按一下`Hide`時，第二個可重複執行個體中的面板會隱藏：

>[!VIDEO](https://video.tv.adobe.com/v/3429554?quality=12&learn=on)

+++

+++ **使用案例**：當表單載入時，以值預先填入欄位

新增下列程式碼行（如[create-custom-function](#create-custom-function)區段中所述），以在表單初始化時載入欄位中的預先填入值：

```javascript
/**
 * Tests import data
 * @name testImportData
 * @param {scope} globals
 */
function testImportData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount','10000']]));
} 
```

在上述程式碼中，當表單載入時，`testImportData`函式會預填`Booking Amount`文字方塊欄位。 我們假設預訂表單要求最低預訂金額為`10,000`。

讓我們在表單初始化時建立規則，當表單載入時，`Booking Amount`文字方塊欄位中的值會預先填入指定的值：

![匯入資料規則](/help/forms/assets/custom-function-import-data.png)

請參考下列熒幕擷圖，以示範當表單載入時，`Booking Amount`文字方塊中的值會預先填入指定的值：

![匯入資料規則表單](/help/forms/assets/custom-function-prefill-form.png)

+++

+++ **Usecase**：將焦點設定在特定欄位

新增下列程式碼行（如[create-custom-function](#create-custom-function)區段中所述），以便在按一下`Submit`按鈕時將焦點設定在指定的欄位上：

```javascript
/**
 * @name testSetFocus
 * @param {object} emailField
 * @param {scope} globals
 */
    function testSetFocus(field, globals)
    {
        globals.functions.setFocus(field);
    }
```

讓我們在`Submit`按鈕中新增規則，以便在按一下`Email ID`文字方塊欄位時設定焦點：

![設定焦點規則](/help/forms/assets/custom-function-set-focus.png)

請參閱下列熒幕擷圖，示範按一下`Submit`按鈕時，焦點設定在`Email ID`欄位上：

![設定焦點規則](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> 如果您想要專注在相對於`email`欄位的下一個或上一個欄位，可以使用選用的`$focusOption`引數。

+++

+++ **Usecase**：使用`dispatchEvent`屬性新增或刪除可重複的面板

新增下列程式碼行（如[create-custom-function](#create-custom-function)區段中所述），以在使用`dispatchEvent`屬性按一下`Add Traveler`按鈕時新增面板：

```javascript
/**
 * Tests add instance with dispatchEvent
 * @name testAddInstance
 * @param {scope} globals
 */
function testAddInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel,'addInstance');
}
```

讓我們在`Add Traveler`按鈕中新增規則，以便在點選時新增可重複面板：

![新增面板規則](/help/forms/assets/custom-function-add-panel.png)

請參考下方的gif，示範按一下`Add Traveler`按鈕時，使用`dispatchEvent`屬性新增面板：

![新增面板](/help/forms/assets/custom-function-add-panel.gif)

同樣地，新增下列程式碼行（如[create-custom-function](#create-custom-function)區段中所述），以便在使用`dispatchEvent`屬性按一下`Delete Traveler`按鈕時刪除面板：

```javascript
/**
 
 * @name testRemoveInstance
 * @param {scope} globals
 */
function testRemoveInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 
```

讓我們在`Delete Traveler`按鈕中新增規則，以便在點選重複面板時將其刪除：

![刪除面板規則](/help/forms/assets/custom-function-delete-panel.png)

請參考下方的gif，示範按一下`Delete Traveler`按鈕時，會使用`dispatchEvent`屬性刪除旅行者面板：

![刪除面板](/help/forms/assets/custom-function-delete-panel.gif)

+++

## 自訂函式的快取支援

Adaptive Forms會在規則編輯器中擷取自訂函式清單時，實作自訂函式的快取，以增強回應時間。 在`error.log`檔案中會顯示訊息為`Fetched following custom functions list from cache`。

具有快取支援的![自訂函式](/help/forms/assets/custom-function-cache-error.png)

如果修改自訂函式，快取會失效，並加以剖析。

## 疑難排解 {#troubleshooting}

* 如果自訂提交處理常式無法在現有AEM專案或表單中如預期般執行，請執行下列步驟：
   * 請確定[核心元件版本已更新至3.0.18和更新版本](https://github.com/adobe/aem-core-forms-components)。 不過，對於現有的AEM專案和表單，還有其他要遵循的步驟：

   * 對於AEM專案，使用者應使用`submitForm()`取代`submitForm('custom:submitSuccess', 'custom:submitError')`的所有執行個體，並透過Cloud Manager管道部署專案。

   * 針對現有表單，如果自訂提交處理常式無法正常運作，使用者需要使用規則編輯器在&#x200B;**提交**&#x200B;按鈕上開啟並儲存`submitForm`規則。 此動作將表單中`submitForm('custom:submitSuccess', 'custom:submitError')`的現有規則取代為`submitForm()`。


* 如果包含自訂函式程式碼的JavaScript檔案發生錯誤，則自訂函式不會列在最適化表單的規則編輯器中。 若要檢查自訂函式清單，您可以導覽至`error.log`檔案以找出錯誤。 發生錯誤時，自訂函式清單會顯示為空白：

  ![錯誤記錄檔](/help/forms/assets/custom-function-list-error-file.png)

  如果沒有錯誤，則會擷取自訂函式並出現在`error.log`檔案中。 在`error.log`檔案中顯示為`Fetched following custom functions list`的訊息：

  使用適當的自訂函式![錯誤記錄檔](/help/forms/assets/custom-function-list-fetched-in-error.png)

## 考量事項

* `parameter type`和`return type`不支援`None`。

* 自訂函式清單中不支援的函式包括：
   * 產生器函式
   * 非同步/等待函式
   * 方法定義
   * 類別方法
   * 預設引數
   * Rest引數

## 另請參閱 {#see-also}

{{see-also}}


