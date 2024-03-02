---
title: 自訂 AEM Forms Edge Delivery Service Form 的主題和樣式
description: 自訂 AEM Forms Edge Delivery Service Form 的主題和樣式
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e8fbe3efae7368c940cc2ed99cc9a352bbafbc22
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 1%

---


# 設定表單欄位樣式

Forms對於使用者在網站上的互動至關重要，可讓他們輸入資料。 本指南說明在「 」中設定各種表單欄位樣式的基礎知識。 [最適化表單區塊](/help/edge/docs/forms/create-forms.md)，協助您建立吸引人且方便使用的表單。

## 瞭解表單欄位型別

開始研究樣式之前，請先檢閱最適化表單區塊支援的常見表單欄位型別：

* 輸入欄位：包括文字輸入、電子郵件輸入、密碼輸入等。
* 核取方塊群組：用於選取多個選項。
* 選項群組：僅用於從群組選取一個選項。
* 下拉式清單：也稱為選取方塊，用於從清單中選取一個選項。
* 面板/容器：用於將相關的表單元素分組在一起。

## 基本樣式原則

在設定特定表單欄位的樣式之前，瞭解基本CSS概念至關重要：

* 選取器： CSS選取器可讓您鎖定特定的HTML元素，以進行樣式設定。 您可以使用元素選取器、類別選取器或ID選取器。
* 屬性： CSS屬性會定義元素的視覺外觀。 樣式化表單欄位的常見屬性包括顏色、背景顏色、邊框、邊框間距、邊界等等。
* 方塊模型： CSS方塊模型將HTML元素的結構描述為由邊框間距、邊框和邊界包圍的內容區域。
* Flexbox/Grid： CSS Flexbox和Grid版面配置是建立回應式且彈性設計的強大工具。

## 為最適化表單區塊設定表單樣式

「最適化表單區塊」提供標準化的HTML結構，可簡化選擇與設定表單元件樣式的程式：

* **更新預設樣式**：您可以編輯表單的預設樣式 `/blocks/form/form.css file`. 此檔案提供表單的完整樣式，支援多步驟精靈表單。 它強調使用自訂CSS變數來輕鬆進行自訂、維護以及跨表單的統一樣式。 如需將最適化表單區塊新增至專案的指示，請參閱 [建立表單](/help/edge/docs/forms/create-forms.md).

* **自訂**：使用預設值 `forms.css` 作為基礎，並進行自訂，以修改表單元件的外觀與風格，使其視覺上吸引人且方便使用。 檔案的結構會鼓勵組織並維護表單的樣式，促進整個網站的設計一致。

## forms.css結構的劃分

* **全域變數：** 定義於 `:root` 層級，這些變數(`--variable-name`)會儲存整個樣式表所使用的值，以保持一致性及方便更新。 這些變數定義顏色、字型大小、邊框間距和其他屬性。 您可以宣告自己的全域變數或修改現有的變數來變更表單樣式。

* **通用選取器樣式：** 此 `*` 選取器符合表單中的每個元素，確保樣式預設會套用至所有元件，包括設定 `box-sizing` 屬性至 `border-box`.

* **表單樣式：** 本節著重於使用選取器來鎖定特定HTML元素，以設計表單元件的樣式。 它定義輸入欄位、文字區域、核取方塊、選項按鈕、檔案輸入、表單標籤和說明的樣式。

* **精靈樣式（如果適用）：** 此區段專用於設定精靈配置的樣式，這是一種多步驟表單，其中每個步驟一次顯示一個。 它會定義精靈容器、欄位集、圖例、導覽按鈕和回應式佈局的樣式。

* **媒體查詢：** 這些選項提供不同熒幕大小的樣式，並據此調整版面和樣式。

* **其他樣式：**：本節涵蓋成功或錯誤訊息的樣式、檔案上傳區域，以及您在表單中可能遇到的其他元素。


## 元件結構

最適化表單區塊為各種表單元素提供一致的HTML結構，確保更輕鬆的樣式化和管理。 您可以針對樣式設定目的使用CSS來操作元件。

### 一般元件（下拉選單、選項群組及核取方塊群組除外）：

除下拉清單、選項群組及核取方塊群組外，所有表單欄位的HTML結構如下：

#### HTML結構

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* 類別： div元素具有數個類別，可鎖定特定元素和樣式。 您需要 `form-{Type}-wrapper` 或 `form-{Name}` 用來開發CSS選取器以設定表單欄位樣式的類別：
   * {Type}：依欄位型別識別元件。 例如，文字(form-text-wrapper)、數字(form-number-wrapper)、日期(form-date-wrapper)。
   * {Name}：依名稱識別元件。 欄位名稱只能包含英數字元，名稱中的多個連續破折號會以單一破折號取代 `(-)`欄位名稱中的開頭和結尾破折號會遭到移除。 例如，名字(form-first-name field-wrapper)。
   * {FieldId}：這是自動產生之欄位的唯一識別碼。
   * {Required}：此為布林值，指出欄位是否為必要欄位。
* 標籤： `label` 要素會提供欄位的描述性文字，並使用 `for` 屬性。
* 輸入： `input` 元素會定義要輸入的資料型別。 例如，文字、數字、電子郵件。
* 說明（選用）： `div` 與類別 `field-description` 為使用者提供其他資訊或指示。

**HTML結構範例**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

**一般元件的CSS選取器**

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

* `.form-{Type}-wrapper`：鎖定外部 `div` 欄位型別為基礎的元素。 例如， `.form-text-wrapper` 鎖定所有文字輸入欄位。
* `.form-{Name}`：進一步根據特定欄位名稱選取元素。 例如， `.form-first-name` 定位「名字」文字欄位。

**一般元件的CSS選取器範例**

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


### 下拉式清單元件

對於下拉式功能表， `select` 會使用元素，而非 `input` 元素：


#### HTML結構

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**範例HTML結構**

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

#### 下拉式元件的CSS選取器範例

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

* 將目標定位包裝函式：第一個選取器(`.form-drop-down-wrapper`)鎖定外部包裝函式元素，確保樣式套用至整個下拉式清單元件。
* Flexbox版面配置： Flexbox會垂直排列標籤、下拉式清單和說明，以利使用簡潔的版面配置。
* 標籤樣式：標籤會以較粗的字型粗細和細微邊界突出顯示。
* 下拉式清單樣式：選取的元素會接收邊框、邊框間距和圓角，以提供拋光的外觀。
* 背景顏色：一致的背景顏色是為了視覺和諧而設定的。
* 箭頭自訂：選用的樣式會隱藏預設的下拉箭頭，並使用Unicode字元和位置建立自訂箭頭。

### 選項和核取方塊群組

與下拉式清單元件類似，單選按鈕和核取方塊群組也有自己的HTML結構和CSS考量事項：

#### 選項群組HTML結構

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


#### 核取方塊群組HTML結構

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

**選項和核取方塊群組的CSS選取器範例**

* 鎖定外部包裝函式：這些選取器會鎖定選項和核取方塊群組最外層的容器，讓您套用一般樣式至整個群組結構。 這對於設定間距、對齊方式或其他配置相關屬性非常有用。


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


* 目標群組標籤：此選取器會將 `.field-label` 選項和核取方塊群組包裝函式中的元素。 這可讓您設定這些群組專屬的標籤樣式，讓這些群組更加引人注目。

  ```CSS
  .form-radio-group-wrapper .field-label,
  .form-checkbox-group-wrapper .field-label {
   font-weight: bold; /* Makes the group label bold */
  }
  ```



* 鎖定個別輸入和標籤：這些選取器可讓您更精細地控制個別選項按鈕、核取方塊及其相關標籤。 您可以使用這些專案來調整大小、間距，或套用更多不同的視覺樣式。

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




* 自訂選項按鈕和核取方塊的外觀：此技術會隱藏預設輸入，並使用：before和：after虛擬元素來建立自訂視覺效果，以根據「已核取」狀態變更外觀。

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


## 樣式化元件

您也可以根據表單欄位的特定型別或個別名稱來設定表單欄位的樣式。 這可讓您更精細地控制及自訂表單的外觀。

### 根據欄位型別設定樣式

您可以使用CSS選取器來鎖定特定欄位型別，並一致地套用樣式。

**範例HTML結構**

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

* 每個欄位都包裝在 `div` 具有數個類別的元素：
   * `form-{Type}-wrapper`：識別欄位型別。 例如， `form-text-wrapper`， `form-number-wrapper`， `form-email-wrapper`.
   * `form-{Name}`：依名稱識別欄位。 例如 `form-name`， `form-age`， `form-email`.
   * `field-wrapper`：所有欄位包裝函式的泛型類別。
* 此 `data-required` 屬性指出欄位是必要欄位還是選用欄位。
* 每個欄位都有對應的標籤、輸入元素和潛在的其他元素，例如預留位置和說明。

**CSS選取器範例**

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

您也可以依名稱鎖定個別欄位，以套用唯一樣式。

**範例HTML結構**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**範例CSS選取器**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

此CSS會鎖定位於具有類別的元素中的所有輸入元素 `form-otp`. 您的表單HTML結構遵循最適化表單區塊的慣例，這表示有一個標有「form-otp」類別的容器會儲存名為「otp」的欄位。


