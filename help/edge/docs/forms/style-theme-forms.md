---
title: 自訂 AEM Forms Edge Delivery Service Form 的主題和樣式
description: 自訂 AEM Forms Edge Delivery Service Form 的主題和樣式
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e8fbe3efae7368c940cc2ed99cc9a352bbafbc22
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 90%

---


# 設定表單欄位的樣式

表單對於網站上的使用者互動至關重要，可讓使用者輸入資料。本指南說明在「 」中設定各種表單欄位樣式的基礎知識。 [最適化表單區塊](/help/edge/docs/forms/create-forms.md)，協助您建立吸引人且方便使用的表單。

## 了解表單欄位類型

開始研究樣式之前，請先檢閱最適化表單區塊支援的常見表單欄位型別：

* 輸入欄位：包括文字輸入、電子郵件輸入、密碼輸入等。
* 核取方塊群組：用於選取多個選項。
* 單選按鈕群組：用於只能在一組選項中進行單選。
* 下拉式選單：也稱為選取方塊，用於從清單中選取一個選項。
* 面板/容器：用於將相關的表單元素群組在一起。

## 基本樣式設定原則

在設定特定表單欄位的樣式之前，了解基本的 CSS 概念至關重要：

* 選取器：CSS 選擇器可讓您針對特定的 HTML 元素進行樣式設定。您可以使用元素選取器、類別選取器或 ID 選取器。
* 屬性：CSS 屬性定義元素的外觀。用於設定表單欄位樣式的常見屬性包括顏色、背景顏色、邊框、邊框間距、邊界等。
* 方塊模型：CSS 方塊模型描述 HTML 元素結構為由邊框間距、邊框和邊界包圍的內容區域。
* Flexbox/Grid：CSS Flexbox 和 Grid 版面是建立回應式和靈活性設計的強大工具。

## 為最適化表單區塊設定表單樣式

「最適化表單區塊」提供標準化的HTML結構，可簡化選擇與設定表單元件樣式的程式：

* **更新預設樣式**：您可以透過編輯 `/blocks/form/form.css file` 來修改表單的預設樣式。此檔案提供了表單的全面樣式，支援多步驟精靈表單。它著重在使用自訂 CSS 變數來輕鬆自訂、維護和跨表單的統一樣式。如需將最適化表單區塊新增至專案的指示，請參閱 [建立表單](/help/edge/docs/forms/create-forms.md).

* **自訂**：以預設 `forms.css` 為基礎，然後進行自訂以修改表單元件的外觀，使其具有視覺吸引力且方便使用。此檔案的結構鼓勵組織並維護表單的樣式，從而促進整個網站的設計一致。

## forms.css 結構分解

* **全域變數：** 定義於 `:root` 層級，這些變數 (`--variable-name`) 儲存整個樣式表中使用的值，以保持一致性並易於更新。這些變數定義顏色、字體大小、邊框間距和其他屬性。您可以宣告自己的全域變數或修改現有變數來變更表單的樣式。

* **通用選取器樣式：**&#x200B;此`*` 選取器符合表單中的每個元素，確保樣式預設套用於所有元件，包括將 `box-sizing` 屬性設定為 `border-box`。

* **表單樣式設定：**&#x200B;本區段重點在於使用選取器針對特定 HTML 元素來設定表單元件樣式。其定義了輸入欄位、文字區域、核取方塊、單選按鈕、檔案輸入、表單標籤和描述的樣式。

* **精靈樣式設定 (如果適用)：** 本區段專門設定精靈版面的樣式，這是多步驟表單，其中每個步驟一次顯示一個。其定義了精靈容器、欄位集、圖例、導覽按鈕和回應式版面的樣式。

* **媒體查詢：**&#x200B;其提供適用於不同螢幕尺寸的樣式，可相應地調整版面和樣式。

* **其他樣式設定：**：本區段包含成功或錯誤訊息、檔案上傳區域以及表單中其他元素的樣式。


## 元件結構

最適化表單區塊為各種表單元素提供一致的HTML結構，確保更輕鬆的樣式化和管理。 您可以使用 CSS 進行樣式設定，藉此操控元件。

### 一般元件 (不包含下拉式選單、單選按鈕群組和核取方塊群組)：

所有表單欄位 (不包含下拉式選單、單選按鈕群組和核取方塊群組) 都具有以下 HTML 結構：

#### HTML 結構

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* 類別：div 元素有幾個目標為特定元素和樣式的類別。您需要 `form-{Type}-wrapper` 或 `form-{Name}` 類別以開發 CSS 選取器來設定表單欄位樣式：
   * {Type}：根據欄位類型識別元件。例如，文字 (form-text-wrapper)、數字 (form-number-wrapper)、日期 (form-date-wrapper)。
   * {Name}：根據名稱識別元件。欄位名稱只能包含英數字元，名稱中的多個連續破折號將替換為單個破折號 `(-)`，並且欄位名稱中的開頭和結尾破折號將被刪除。例如，名字 (form-first-name field-wrapper)。
   * {FieldId}：欄位的唯一識別碼，是自動產生的。
   * {Required}：它是一個布林值，表示該欄位是否為必填欄位。
* 標籤：的 `label` 元素提供欄位的描述性文字，並使用 `for` 屬性將其與輸入元素相關聯。
* 輸入：`input` 元素定義要輸入的資料類型。例如，文字、數字、電子郵件。
* 描述 (選擇性)：`div` 與類別 `field-description` 為使用者提供額外資訊或說明。

**HTML 結構範例**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

**一般元件的 CSS 選取器**

```CSS
.form-{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}


.form-{Name} input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

* `.form-{Type}-wrapper`：根據欄位類型以外部 `div` 元素為目標。例如，`.form-text-wrapper` 以所有文字輸入欄位為目標。
* `.form-{Name}`：根據特定欄位名稱進一步選取元素。例如，`.form-first-name` 以「名字」文字欄位為目標。

**一般元件的 CSS 選取器範例**

```CSS
/*Target all text input fields */

.form-text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/*Target all fields with name first-name*/

.form-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```


### 下拉式選單元件

對於下拉式選單，使用 `select` 元素而非 `input` 元素：


#### HTML 結構

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**HTML 結構範例**

```HTML
    <div class="form-drop-down-wrapper form-country field-wrapper" data-required="true">
      <label for="country" class="field-label">Country</label>
      <select id="country" name="country">
         <option value="">Select Country</option>
         <option value="US">United States</option>
         <option value="CA">Canada</option>
    </select>
   <div class="field-description" aria-live="polite" id="country-description">Please select your country of residence.</div>
   </div>
```

#### 下拉式選單的 CSS 選取器範例

```CSS
/* Target the outer wrapper */
.form-drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.form-drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.form-drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: white; /* Ensure a consistent background */
  /* Adjust arrow appearance as needed */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

/* Optional: Style the dropdown arrow */
.form-drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.form-drop-down-wrapper select::after {
  content: "\25BC";
  font-size: 12px;
  color: #ccc;
  /* Adjust positioning as needed */
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
}
```

* 以包裝函式為目標：第一個選取器 (`.form-drop-down-wrapper`) 以外部包裝函式元素為目標，確保樣式套用至整個下拉式選單元件。
* Flexbox 版面：Flexbox 垂直排列標籤、下拉式選單和說明，以呈現簡潔的版面。
* 標籤樣式設定：標籤以較粗字體和些微邊界呈現醒目效果。
* 下拉式選單樣式設定：所選元素獲得邊框、邊框間距和圓角，具有精美的外觀。
* 背景顏色：設定一致的背景顏色讓視覺更為和諧。
* 箭頭自訂：選擇性樣式可隱藏預設下拉箭頭，並使用 Unicode 字元和定位建立自訂箭頭。

### 單選按鈕和核取方塊群組

與下拉元件類似，單選按鈕和核取方塊群組也有自己的 HTML 結構和 CSS 考量事項：

#### 單選按鈕群組 HTML 結構

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```


#### 核取方塊群組 HTML 結構

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```

**單選按鈕和核取方塊群組的 CSS 選取器範例**

* 以外部包裝函式為目標：這些選取器的目標為單選按鈕和核取方塊群組的最外層容器，可讓您將一般樣式套用至整個群組結構。這對於設定間距、對齊方式或其他版面相關的屬性非常有用。


  ```CSS
     /* Targets all radio group wrappers */
  .form-radio-group-wrapper {
    margin-bottom: 20px; /* Adds space between radio groups */
  }
  
  /* Targets all checkbox group wrappers */
  .form-checkbox-group-wrapper {
    margin-bottom: 20px; /* Adds space between checkbox groups */
  }
  ```


* 以群組標籤為目標：此選取器的目標為單選按鈕和核取方塊群組包裝函式內的 `.field-label` 元素。這使您可以專門為這些群組設定標籤樣式，從而可能使它們更加醒目。

  ```CSS
  .form-radio-group-wrapper .field-label,
  .form-checkbox-group-wrapper .field-label {
   font-weight: bold; /* Makes the group label bold */
  }
  ```



* 以個別輸入和標籤為目標：這些選取器可以對個別單選按鈕、核取方塊及其關聯的標籤進行更精細的控制。您可以使用它們來調整大小、間距或套用更獨特的視覺樣式。

  ```CSS
  /* Styling radio buttons */
  .form-radio-group-wrapper input[type="radio"] {
    margin-right: 5px; /* Adds space between the input and its   label */
  } 
  
  /* Styling radio button labels */
  .form-radio-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  
  /* Styling checkboxes */
  .form-checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 5px;  /* Adds space between the input and its  label */ 
  }
  
  /* Styling checkbox labels */
  .form-checkbox-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  ```




* 自訂單選按鈕和核取方塊的外觀：此技術隱藏預設輸入並使用 :before 和 :after 偽元素來建立自訂視覺效果，其根據「已選取」狀態來變更外觀。

  ```CSS
  /* Hide the default radio button or checkbox */
  .form-radio-group-wrapper input[type="radio"],
  .form-checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0; 
    position: absolute; 
  }
  
  /* Create a custom radio button */
  .form-radio-group-wrapper input[type="radio"] + label::before { 
    content: "";
    display: inline-block;
    width: 16px; 
    height: 16px; 
    border: 2px solid #ccc; 
    border-radius: 50%;
    margin-right: 5px;
  }
  
  .form-radio-group-wrapper input[type="radio"]:checked +  label::before {
    background-color: #007bff; 
  }
  
  /* Create a custom checkbox */
  /* Similar styling as above, with adjustments for a square shape  */
  ```


## 設定元件樣式

您也可以根據表單欄位的特定類型或個別名稱來設定表單欄位的樣式。這允許更精細地控制和自訂表單的外觀。

### 根據欄位類型設定樣式

您可以使用 CSS 選取器來以特定欄位類型為目標並一致地套用樣式。

**HTML 結構範例**

```HTML
<div class="form-text-wrapper form-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="form-number-wrapper form-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="form-email-wrapper form-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

* 每個欄位都包含在具有多個類別的 `div` 元素中：
   * `form-{Type}-wrapper`：識別欄位的類型。例如：`form-text-wrapper`、`form-number-wrapper`、`form-email-wrapper`。
   * `form-{Name}`：根據名稱識別欄位。例如：`form-name`、`form-age`、`form-email`。
   * `field-wrapper`：所有欄位包裝函式的通用類別。
* `data-required` 屬性表示該欄位是必填還是選擇性欄位。
* 每個欄位都有對應的標籤、輸入元素和潛在的附加元素 (例如預留位置和描述)。

**CSS 選取器範例**

```CSS
/* Target all text input fields */
.form-text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.form-number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

### 根據欄位名稱設定樣式

您也可以根據名稱以個別欄位為目標來套用獨特的樣式。

**HTML 結構範例**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**CSS 選取器範例**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

此 CSS 的目標是位於具有類別 `form-otp` 的元素內的所有輸入元素。您的表單HTML結構遵循最適化表單區塊的慣例，這表示有一個標有「form-otp」類別的容器會儲存名為「otp」的欄位。


