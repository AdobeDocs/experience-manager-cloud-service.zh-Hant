---
title: 在最適化表單中使用自訂函式
description: AEM Forms支援自訂函式，可讓使用者在規則編輯器中建立並使用自己的函式。
keywords: 新增自訂函式、使用自訂函式、建立自訂函式，以及在規則編輯器中使用自訂函式。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 5b5b44f8dffc01a75eda464cd7759cf03028c2c6
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 2%

---


# 以核心元件為主之自適應表單的自訂函數簡介

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions-core-components) |
| AEM as a Cloud Service  | 本文章 |

AEM Forms支援自訂函式，可讓使用者定義JavaScript函式以實作複雜的商業規則。 這些自訂功能可協助您根據指定需求操控和處理輸入的資料，進而擴充表單的功能。 它們可根據預先定義的條件來啟用表單行為的動態變更。 自訂函式也可讓開發人員強制實施複雜的驗證邏輯、執行動態計算，以及根據使用者互動或預先定義的條件控制表單元素的顯示或行為。

>[!NOTE]
>
> 請確定[核心元件](https://github.com/adobe/aem-core-forms-components)設定為最新版本，以使用最新功能。

## 使用自訂函式 {#uses-of-custom-function}

在最適化Forms中使用自訂函式的優點包括：
* **資料處理**：自訂函式可協助處理輸入到表單欄位中的資料。
* **資料驗證**：自訂函式可讓您對表單輸入執行自訂檢查，並提供指定的錯誤訊息。
* **動態行為**：自訂函式可讓您根據特定條件控制表單的動態行為。 例如，您可以顯示/隱藏欄位、修改欄位值或動態調整表單邏輯。
* **整合**：您可以使用自訂函式與外部API或服務整合。 它有助於從外部來源擷取資料、傳送資料至外部Rest端點，或根據外部事件執行自訂動作。

自訂函式基本上是新增至JavaScript檔案中的使用者端程式庫。 建立自訂函式後，規則編輯器中即可供使用者在最適化表單中選擇。 自訂函式由規則編輯器中的JavaScript註解識別。

## 支援自訂功能的JavaScript註解 {#js-annotations}

JavaScript註解是用來提供JavaScript程式碼的中繼資料。 其中包含以特定符號(例如/**和@)開頭的註解。 註解提供關於程式碼中函式、變數和其他元素的重要資訊。 最適化表單支援下列自訂函式的JavaScript註解：

### 名稱

此名稱用於識別最適化表單的規則編輯器中的自訂函式。 下列語法可用來命名自訂函式：

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`。
  `functionName`是函式的名稱。 不允許空格。
  `<Function Name>`是適用性表單的規則編輯器中函式的顯示名稱。
如果函式名稱與函式本身的名稱相同，您可以在語法中省略`[functionName]`。

### 參數

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
   * 範圍：代表全域物件，其中包含唯讀變數，例如表單例項、目標欄位例項，以及在自訂函式內執行表單修改的方法。 這會宣告為JavaScript註解中的最後一個引數，且不會顯示在最適化表單的規則編輯器中。 scope引數可存取表單或元件的物件，以觸發表單處理所需的規則或事件。 如需有關Globals物件及其使用方式的進一步資訊，[請按一下這裡](/help/forms/custom-function-core-component-scope-function.md)。

引數型別不區分大小寫，而且引數名稱中不允許使用空格。

`<Parameter Description>`包含有關引數用途的詳細資料。 它可以有多個字詞。

#### 選用參數

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

### 傳回型別

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

### 私人

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

## 已知問題

* 自訂函式不支援JavaScript規則運算式常值。 在自訂函式中使用規則運算式常值會導致執行期間發生錯誤。 例如：
  `const pattern = /^abc$/;`

  若要確保相容性，請在自訂函式中使用RegExp建構函式。

  `const pattern = new RegExp("^abc$");`
重構規則運算式以使用RegExp建構函式，以確保一致且可靠的執行。

## 下一步

若要在最適化表單中建立和使用自訂函式，請參閱[根據核心元件建立最適化表單的自訂函式](/help/forms/custom-function-core-component-create-function.md)一文。

## 另請參閱

{{see-also-rule-editor}}