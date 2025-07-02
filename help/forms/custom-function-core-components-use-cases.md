---
title: 本文概述根據核心元件在最適化表單中自訂功能的各種使用案例。
description: 本文概述根據核心元件在最適化表單中自訂功能的各種使用案例。 規則編輯器中會使用自訂函式，為表單建立自訂規則。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: df92b91e-f3b0-4a08-bd40-e99edc9a50a5
source-git-commit: 5b5b44f8dffc01a75eda464cd7759cf03028c2c6
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 0%

---

# 自訂函數的開發和使用範例

本文提供根據核心元件的最適化表單的詳細自訂函式範例，對於在各種情況下有效實施提供寶貴的見解。 自訂函式用於AEM Forms的規則編輯器，可讓開發人員定義及控制控制表單行為的邏輯。
本文探討自訂函式的不同實作，說明如何使用這些函式來量身打造表單以符合特定需求並增強整體功能。

## 使用自訂函式填入下拉式清單選項

核心元件中的規則編輯器不支援&#x200B;**Set Options**&#x200B;屬性，無法在執行階段動態填入下拉式清單選項。 不過，您可以使用自訂函式填入下拉式清單選項，這可讓您根據特定邏輯擷取選項。 自訂函式可讓您更靈活地控制下拉式清單選項的填入方式和時間，進而增強使用者體驗。

若要使用自訂函式填入下拉式清單選項，請新增下列程式碼，如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中所述：


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

## 使用`SetProperty`規則顯示面板

讓我們瞭解自訂函式如何透過`Contact Us`表單使用欄位和全域物件。

![連絡我們表單](/help/forms/assets/contact-us-form.png)

在自訂函式中新增下列程式碼（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中所述），以將表單欄位設為`Required`。

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

## 驗證欄位

讓我們瞭解自訂函式如何透過`Contact Us`表單使用欄位和全域物件來驗證欄位。

依照[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中的說明，在自訂函式中新增下列程式碼，以驗證欄位。

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

## 重設面板

讓我們瞭解自訂函式如何在`Contact Us`表單的協助下，使用欄位和全域物件來重設欄位。

依照[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中的說明，在自訂函式中新增下列程式碼，以重設面板。

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

## 在欄位層級顯示自訂訊息並將欄位標籤為無效的方式

讓我們瞭解自訂函式如何使用欄位和全域物件在欄位層級顯示自訂訊息，並透過`Contact Us`表單將欄位標籤為無效。

您可以使用`markFieldAsInvalid()`函式將欄位定義為無效，並在欄位層級設定自訂錯誤訊息。 `fieldIdentifier`值可以是`fieldId`、`field qualifiedName`或`field dataRef`。 名稱為`option`的物件值可以是`{useId: true}`、`{useQualifiedName: true}`或`{useDataRef: true}`。
用於將欄位標示為無效並設定自訂訊息的語法如下：

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

在自訂函式中新增下列程式碼（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中所述），以在欄位層級啟用自訂訊息。

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

## 將變更的資料提交至伺服器

讓我們瞭解自訂函式如何在`Contact Us`表單的協助下，使用欄位和全域物件在伺服器上提交已處理的資料。

下列程式碼行：
`globals.functions.submitForm(globals.functions.exportData(), false);`用於在操作後提交表單資料。
* 第一個引數是要提交的資料。
* 第二個引數代表是否要在提交前驗證表單。 它是`optional`，預設為`true`。
* 第三個引數是提交的`contentType`，也是選擇性的，預設值為`multipart/form-data`。 其他值可以是`application/json`和`application/x-www-form-urlencoded`。

在自訂函式中新增下列程式碼（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中所述），以在伺服器上提交操作過的資料：

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

![在主控台視窗檢查資料](/help/forms/assets/custom-function-submit-data-console-data.png)

## 覆寫表單提交成功和錯誤處理常式

讓我們瞭解自訂函式如何在`Contact Us`表單的協助下，使用欄位和全域物件來覆寫提交處理常式。

新增下列程式碼行（如[create-custom-functionas](/help/forms/custom-function-core-component-create-function.md)區段中所述），以自訂表單提交的提交或失敗訊息，並在強制回應方塊中顯示表單提交訊息：

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

## 在可重複面板的特定執行個體中執行動作

使用可重複面板上的視覺化規則編輯器建立的規則會套用至可重複面板的最後一個例項。 若要為可重複面板的特定執行個體編寫規則，我們可以使用自訂函式。

讓我們建立另一個表格做為`Booking Form`，以收集前往目的地的旅行者相關資訊。 將旅行者面板新增為可重複的面板，使用者可在其中使用`Add Traveler`按鈕新增5個旅行者的詳細資料。

![旅行者資訊](/help/forms/assets/traveler-info-form.png)

新增下列程式碼行（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中所述），以於可重複面板的特定執行個體中執行動作，而非最後一個執行個體：

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

## 表單載入時使用值預先填寫欄位

讓我們瞭解自訂函式如何在`Booking Form`的協助下，使用欄位和全域物件來預先填入欄位。

新增下列程式碼行（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中所述），以在表單初始化時載入欄位中的預先填入值：

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

## 聚焦在特定欄位

讓我們瞭解自訂函式如何在`Booking Form`的協助下，使用欄位和全域物件來設定特定欄位的焦點。

新增下列程式碼行（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中所述），以便在按一下`Submit`按鈕時將焦點設定在指定的欄位上：

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

## 使用`dispatchEvent`屬性新增或刪除可重複的面板

讓我們瞭解自訂函式如何在`Booking Form`的協助下，使用`dispatchEvent`屬性使用欄位和全域物件來新增或刪除可重複的面板。

新增下列程式碼行（如[create-custom-function](/help/forms/custom-function-core-component-create-function.md)區段中所述），以在使用`dispatchEvent`屬性按一下`Add Traveler`按鈕時新增面板：

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

## 已知問題

* 自訂函式不支援JavaScript規則運算式常值。 在自訂函式中使用規則運算式常值會導致執行期間發生錯誤。 例如：
  `const pattern = /^abc$/;`

  若要確保相容性，請在自訂函式中使用RegExp建構函式。

  `const pattern = new RegExp("^abc$");`
重構規則運算式以使用RegExp建構函式，以確保一致且可靠的執行。

## 疑難排解

* 如果自訂提交處理常式無法在現有AEM專案或表單中按預期執行，請執行以下步驟：
   * 請確定[核心元件版本已更新至3.0.18和更新版本](https://github.com/adobe/aem-core-forms-components)。 不過，對於現有的AEM專案和表單，還有其他要遵循的步驟：

   * 對於AEM專案，使用者應使用`submitForm()`取代`submitForm('custom:submitSuccess', 'custom:submitError')`的所有執行個體，並透過Cloud Manager管道部署專案。

   * 針對現有表單，如果自訂提交處理常式無法正常運作，使用者需要使用規則編輯器在&#x200B;**提交**&#x200B;按鈕上開啟並儲存`submitForm`規則。 此動作將表單中`submitForm('custom:submitSuccess', 'custom:submitError')`的現有規則取代為`submitForm()`。

## 另請參閱

{{see-also-rule-editor}}
