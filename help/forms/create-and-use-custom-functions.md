---
title: 在最適化表單中建立及新增自訂函式
description: AEM Forms支援自訂函式，可讓使用者在規則編輯器中建立並使用自己的函式。
keywords: 新增自訂函式、使用自訂函式、建立自訂函式，以及在規則編輯器中使用自訂函式。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 1fb7fece71eec28219ce36c72d628867a222b618
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 10%

---


# 最適化Forms中的自訂函式（核心元件）

## 簡介

AEM Forms支援自訂函式，可讓使用者定義JavaScript函式以實作複雜的商業規則。 這些自訂功能可協助您根據指定需求操控和處理輸入的資料，進而擴充表單的功能。 它們還可以根據預先定義的條件來啟用表單行為的動態變更。
在調適型Forms中，您可以在中使用自訂函式 [最適化表單的規則編輯器](/help/forms/rule-editor.md#custom-functions) 以建立表單欄位的特定驗證規則。

讓我們瞭解自訂功能的使用方式，使用者可在其中輸入電子郵件地址，而您想要確保輸入的電子郵件地址遵循特定格式（其中包含「@」符號和網域名稱）。 將自訂函式建立為「ValidateEmail」，此函式會以電子郵件地址作為輸入，並在有效時傳回true，否則傳回false。

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

在上述範例中，當使用者嘗試提交表單時，會叫用自訂函式「ValidateEmail」以檢查輸入的電子郵件地址是否有效。

### 使用自訂函式 {#uses-of-custom-function}

在最適化Forms中使用自訂函式的優點包括：

* **資料操控**：自訂函式會操控及處理輸入至表單欄位中的資料。
* **資料驗證**：自訂函式可讓您對表單輸入執行自訂檢查，並提供指定的錯誤訊息。
* **動態行為**：自訂函式可讓您根據特定條件控制表單的動態行為。 例如，您可以顯示/隱藏欄位、修改欄位值或動態調整表單邏輯。
* **整合**：您可以使用自訂函式與外部API或服務整合。 它有助於從外部來源擷取資料、傳送資料至外部Rest端點，或根據外部事件執行自訂動作。

## 建立自訂函式時的注意事項 {#considerations}

若要在規則編輯器中列出自訂函式，您可以使用下列任一格式來宣告它們：

* **包含或不包含jsdoc註解的函式陳述式**

您可以建立包含或不包含jsdoc註解的自訂函式。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
<!--

* **Arrow function with mandatory jsdoc comment**

Some of the examples to create Arrow functions are:
```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} a some parameter description
    * @param {string} b another parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
```

    * @param {string=} b another parameter description
      /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;-->

* **含有必要jsdoc註解的函式運算式**

若要列出最適化表單的規則編輯器中的自訂函式，請以下列格式建立自訂函式：

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} input1 parameter description
    * @param {string} input2 another parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

<!--
* @param {string=} input2 another parameter description
The functions that are not supported in the custom function list are:
* Generator functions
* Async/Await functions 
* Method definitions
* Class methods
* Default parameters
* Rest parameters -->

>[!NOTE]
>
> 您可以檢查 `error.log` 任何錯誤的檔案，例如未列在規則編輯器中的自訂函式。

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## 建立自訂函式 {#create-custom-function}

建立使用者端程式庫以呼叫規則編輯器中的自訂函式。 如需詳細資訊，請參閱 [使用使用者端資料庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

建立自訂函式的步驟如下：
1. [建立使用者端資源庫](#create-client-library)
1. [在最適化表單中新增使用者端程式庫](#use-custom-function)

### 建立使用者端資源庫 {#create-client-library}

您可以透過新增使用者端資料庫來新增自訂函式。 若要建立使用者端程式庫，請執行下列步驟：

1. [複製AEM Formsas a Cloud Service存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#accessing-git).
1. 在 `[AEM Forms as a Cloud Service repository folder]/apps/` 檔案夾中建立一個檔案夾。例如，建立名為的資料夾 `experience-league`.
1. 瀏覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` 並建立 `ClientLibraryFolder`. 例如，建立使用者端資源庫資料夾為 `es6clientlibs`.
1. 新增屬性 `categories` 字串型別值的組合。 例如，指派值 `es6customfunctions` 至 `categories` 的屬性 `es6clientlibs` 資料夾。

   >[!NOTE]
   >
   > 您可以選擇任何名稱 `client library folder` 和 `categories` 屬性。

1. 建立一個名為 `js` 的檔案夾。
1. 導覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js` 檔案夾。
1. 新增JavaScript檔案，例如 `function.js`. 此檔案包含自訂函式的程式碼。

   >[!NOTE]
   >
   > 如果包含自訂函式程式碼的JavaScript檔案發生錯誤，則自訂函式不會列在調適型表單的規則編輯器中。 您也可以檢查 `error.log` 錯誤檔案。

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

1. 儲存 `function.js` 檔案。
1. 導覽至 `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js` 檔案夾。
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

1. [執行管道.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)

管道執行成功後，使用者端資料庫中新增的自訂函式即可在中使用 [最適化表單規則編輯器](/help/forms/rule-editor.md).

### 在最適化表單中新增使用者端程式庫{#use-custom-function}

將使用者端程式庫部署到Forms CS環境後，請在最適化表單中使用其功能。 若要在最適化表單中新增使用者端程式庫

1. 在編輯模式中開啟您的表單。 若要以編輯模式開啟表單，請選取表單並選取 **[!UICONTROL 編輯]**.
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 開啟 **[!UICONTROL 基本]** 標籤並選取 **[!UICONTROL 使用者端資料庫類別]** 從下拉式清單（在此例中為「選取」） `es6customfunctions`)。

   ![新增自訂函式使用者端程式庫](/help/forms/assets/clientlib-custom-function.png)

1. 按一下 **[!UICONTROL 完成]** .

現在，您可以建立規則，以在規則編輯器中使用自訂函式。

<!--

Create a rule to use custom function in the rule editor. 

### Support for the optional parameters in custom functions{#support-for-optional-parameter}

AEM supports including optional parameters in JSDocs. These parameters are displayed as optional in the rule editor. There are two ways to add optional parameters in JSDocs:
*  `@param {string=abc} b -- some description for b which is optional`

    In the above line of code, `b` is an optional parameter with the default value set to `abc`. 
    Alternatively, you can define `b` as an optional parameter without assigning any default value as `@param {string=} b -- some description for b which is optional`

* `@param {array} [z=[def,xyz]] - - some description for z which is optional`

    In the above line of code, `z` is an optional parameter of array type with the default value set to `[def , xyz]`. 
    Alternatively, you can define `z` as an optional parameter without assigning any default value as `@param {array} [z=] - - some description for z which is optional`

>[!NOTE]
>
> Ensure that the parameter name is enclosed in square brackets [] and the parameter type is enclosed in curly brackets {}. 

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

In the rule editor of an Adaptive Form, the parameters are displayed as `required`. By default the parameters are `required`, if not defined as optional in JSDocs.

  ![Optional or required parameters](/help/forms/assets/optional-default-params.png) 

  You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

  ![incomplete rule warning message](/help/forms/assets/incomplete-rule.png) 
  
  The rule is executed even if you do not specify a value for optional parameters. Undefined values are passed for optional parameters on executing the rule.

  ### Support for field and globals objects in custom functions {#support-field-and-global-objects}

  needs to be discussed

  -->

## 另請參閱 {#see-also}

{{see-also}}





