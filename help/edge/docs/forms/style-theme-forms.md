---
title: 自訂 AEM Forms 適用的 Edge Delivery Services 主題與樣式
description: 自訂 AEM Forms 適用的 Edge Delivery Services 主題與樣式
feature: Edge Delivery Services
exl-id: c214711c-979b-4833-9541-8e35b2aa8e09
role: Admin, Architect, Developer
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 98%

---


# 自訂表單的外觀

表單對於網站上的使用者互動至關重要，可讓使用者輸入資料。您可以使用階層式樣式表 (CSS) 來設定表單欄位的樣式、增強表單的視覺呈現效果，以及提升使用者體驗。

自適應表單區塊會讓所有表單欄位產生一致的結構。這樣的一致結構讓 CSS 選擇器的開發工作變得更簡單，您可以使用此選擇器根據欄位類型和欄位名稱來選取表單欄位並設定其樣式。

此文件概述各種表單元件的 HTML 結構，協助您了解如何為各種表單欄位建立 CSS 選擇器，以利設定自適應表單區塊的表單欄位樣式。

閱讀完文章後，您將：

- 了解自適應表單區塊中包含的預設 CSS 檔案的結構
- 了解自適應表單區塊提供的表單元件之 HTML 結構，包括一般元件和特定元件，例如下拉式選單、單選按鈕群組和核取方塊群組
- 了解如何使用 CSS 選擇器根據欄位類型和欄位名稱來設定表單欄位樣式，以便依照需求打造一致或獨特的樣式


## 了解表單欄位類型

在深入研究樣式之前，讓我們回顧一下最適化表單區塊支援的常見表單[欄位類型](/help/edge/docs/forms/form-components.md)：

- 輸入欄位：包括文字輸入、電子郵件輸入、密碼輸入等
- 核取方塊群組：用於選取多個選項
- 單選按鈕群組：用於從一組選項中選取一個選項
- 下拉式選單：也稱為選取方塊，用於從清單中選取一個選項
- 面板/容器：用於將相關的表單元素組成群組

## 基本樣式設定原則

在設定特定表單欄位的樣式之前，了解[基本的 CSS 概念](https://www.w3schools.com/css/css_intro.asp)至關重要：

- [選取器](https://www.w3schools.com/css/css_selectors.asp)：CSS 選擇器可讓您針對特定的 HTML 元素進行樣式設定。您可以使用元素選擇器、類別選擇器或 ID 選擇器
- [屬性](https://www.w3schools.com/css/css_syntax.asp)：CSS 屬性定義元素的外觀。用於設定表單欄位樣式的常見屬性包括顏色、背景顏色、邊框、邊框間距、邊界等
- [方塊模型](https://www.w3schools.com/css/css_boxmodel.asp)：CSS 方塊模型會將 HTML 元素結構描述為由邊框間距、邊框和邊界包圍的內容區域
- Flexbox/Grid：CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) 和 [Grid 版面](https://www.w3schools.com/css/css_grid.asp)是建立回應式和靈活設計的強大工具

## 為最適化表單區塊設定表單樣式

最適化區塊提供了標準化的 HTML 結構，簡化了選取表單元件和設定表單元件樣式的程序：

- **更新預設樣式**：您可以透過編輯 `/blocks/form/form.css` 檔案來修改表單的預設樣式。此檔案提供了表單的全面樣式，支援多步驟精靈表單。其著重在使用自訂 CSS 變數，讓自訂、維護和統一表單樣式的工作變得簡單。有關如何將最適化表單區塊新增至專案的說明，請參閱「[建立表單](/help/edge/docs/forms/create-forms.md)」。

- **自訂**：以預設的 `forms.css` 為基礎，然後再進行自訂以修改表單元件外觀，使其具有視覺吸引力且簡單易用。此檔案的結構會鼓勵組織並維護表單的樣式，進而促進整個網站的一致性設計。

## forms.css 結構分項說明

- **全域變數：** 定義於 `:root` 層級，這些變數 (`--variable-name`) 儲存整個樣式表中使用的值，以保持一致性並易於更新。這些變數定義顏色、字體大小、邊框間距和其他屬性。您可以宣告自己的全域變數或修改現有變數來變更表單的樣式。

- **通用選取器樣式：**&#x200B;此`*` 選取器符合表單中的每個元素，確保樣式預設套用於所有元件，包括將 `box-sizing` 屬性設定為 `border-box`。

- **表單樣式設定：**&#x200B;本區段重點在於使用選取器針對特定 HTML 元素來設定表單元件樣式。其定義了輸入欄位、文字區域、核取方塊、單選按鈕、檔案輸入、表單標籤和描述的樣式。

- **精靈樣式設定 (如果適用)：** 本區段專門設定精靈版面的樣式，這是多步驟表單，其中每個步驟一次顯示一個。其定義了精靈容器、欄位集、圖例、導覽按鈕和回應式版面的樣式。

- **媒體查詢：**&#x200B;其提供適用於不同螢幕尺寸的樣式，可相應地調整版面和樣式。

- **其他樣式設定：**&#x200B;此區段包含成功或錯誤訊息、檔案上傳區域，以及表單中其他元素的樣式。


## 元件結構

最適化表單區塊為各種表單元素提供一致的 HTML 結構，確保輕鬆進行樣式設定和管理。您可以使用 CSS 進行樣式設定，藉此操控元件。

### 一般元件 (不包含下拉式選單、單選按鈕群組和核取方塊群組)：

所有表單欄位 (不包含下拉式選單、單選按鈕群組和核取方塊群組) 都具有以下 HTML 結構：

+++ 一般元件的 HTML 結構

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be a minimum of 3 characters and a maximum of 10 characters.
   </div>
</div>
```

- 類別：div 元素有幾個目標為特定元素和樣式的類別。您需要 `{Type}-wrapper` 或 `field-{Name}` 類別以開發 CSS 選取器來設定表單欄位樣式：
   - {Type}：根據欄位類型識別元件。例如，text (text-wrapper)、number (number-wrapper)、date (date-wrapper)
   - {Name}：根據名稱識別元件。欄位名稱只能包含英數字元；名稱中的多個連續破折號會更換為單個破折號 `(-)`，而且欄位名稱中開頭和結尾的破折號會被移除。例如，first-name (field-first-name field-wrapper)
   - {FieldId}：這是欄位的唯一識別碼，會自動產生
   - {Required}：表示欄位是否為必要欄位的布林值
- 標籤：`label` 元素會提供描述欄位的文字，並使用 `for` 屬性將其與輸入元素相關聯
- 輸入：`input` 元素定義要輸入的資料類型。例如，text、number、email
- 描述 (選用)：`div` 與類別 `field-description` 會為使用者提供其他資訊或指示

**HTML 結構範例**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

+++

+++ 一般元件的 CSS 選取器

```CSS
/* Target all input fields within any .{Type}-wrapper */
.{Type}-wrapper {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all input fields within any .{Type}-wrapper */
.{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target any element with the class field-{Name} */
.field-{Name} {
  /* Add your styles here */
  /* This could be used for styles specific to all elements with field-{Name} class, not just inputs */
}
```

- `.{Type}-wrapper`：根據欄位類型以外部 `div` 元素為目標。例如，`.text-wrapper` 以所有文字欄位為目標
- `.field-{Name}`：根據特定欄位名稱進一步選取元素。例如，`.field-first-name` 以「名字」文字欄位為目標。雖然此選擇器可用來針對具有 field-{Name} 類別的元素，但請謹慎使用。在這種特定情況下，這對於設定輸入欄位的樣式並不是很有用，因為其不僅以輸入本身為目標，而且還會以標籤和描述元素為目標。建議使用比較具體的選擇器，例如用於針對文字輸入欄位 (.text-wrapper input) 的選擇器

**一般元件的 CSS 選取器範例**

```CSS
/* Target all text input fields */
.text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all fields with name first-name */
.field-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

+++

### 下拉式選單元件

對於下拉式選單，使用 `select` 元素而非 `input` 元素：

+++ 下拉式選單元件的 HTML 結構

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">Country</label>
   <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Please select your country from the list.
   </div>
</div>
```

**HTML 結構範例**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

+++

+++ 下拉式選單元件的 CSS 選擇器

```CSS
/* Target the outer wrapper */
.drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.drop-down-wrapper select {
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
.drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.drop-down-wrapper select::after {
  content: "\25BC";
}
```

+++

### 單選按鈕群組

與下拉元件類似，單選按鈕群組也有自己的 HTML 結構和 CSS 結構：

+++ 單選按鈕群組 HTML 結構

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

#### HTML 結構範例

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

+++

+++ 單選按鈕群組的 CSS 選擇器

- 為欄位集進行目標定位

```CSS
  .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```

此選擇器針對具有 radio-group-wrapper 類別的任何欄位集。這對於將通用樣式應用於整個單選按鈕群組非常有用。

- 為單選按鈕標籤進行目標定位

```CSS
.radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

- 根據名稱鎖定來針對欄位集中的所有單選按鈕標籤

```CSS
.field-color .radio-wrapper label {
  /* Your styles here */
}
```

+++

### 核取方塊群組

+++ 核取方塊群組的 HTML 結構

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

#### HTML 結構範例

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

+++

+++ 核取方塊群組的 CSS 選擇器

- 以外部包裝函式為目標：這些選取器的目標為單選按鈕和核取方塊群組的最外層容器，可讓您將一般樣式套用至整個群組結構。這對於設定間距、對齊方式或其他版面相關的屬性非常有用。


  ```CSS
     /* Targets radio group wrappers */
       .radio-group-wrapper {
       margin-bottom: 20px; /* Adds space between radio groups */  
     }
  
     /* Targets checkbox group wrappers */
     .checkbox-group-wrapper {
     margin-bottom: 20px; /* Adds space between checkbox groups */
     }
  ```


- 以群組標籤為目標：此選取器的目標為單選按鈕和核取方塊群組包裝函式內的 `.field-label` 元素。這使您可以專門為這些群組設定標籤樣式，從而可能使它們更加醒目。

  ```CSS
   .radio-group-wrapper legend,
   .checkbox-group-wrapper legend {
     font-weight: bold; /* Makes the group label bold */
   }
  ```



- 以個別輸入和標籤為目標：這些選取器可以對個別單選按鈕、核取方塊及其關聯的標籤進行更精細的控制。您可以使用它們來調整大小、間距或套用更獨特的視覺樣式。

  ```CSS
  /* Styling radio buttons */
   .radio-group-wrapper input[type="radio"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling radio button labels */
   .radio-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  
  /* Styling checkboxes */
   .checkbox-group-wrapper input[type="checkbox"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling checkbox labels */
   .checkbox-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  ```




- 自訂單選按鈕和核取方塊的外觀：此技術隱藏預設輸入並使用 `:before` 和 `:after` 偽元素來建立自訂視覺效果，其根據「已選取」狀態來變更外觀。

  ```CSS
  /* Hide the default radio button or checkbox */
     .radio-group-wrapper input[type="radio"],
     .checkbox-group-wrapper input[type="checkbox"] {
       opacity: 0;
       position: absolute;
     }
  
     /* Create a custom radio button */
     .radio-group-wrapper input[type="radio"] + label::before {
       /* ... styles for custom radio button ... */
     }
  
     .radio-group-wrapper input[type="radio"]:checked + label::before {
       /* ... styles for checked radio button ... */
     }
  
     /* Create a custom checkbox */
     /* Similar styling as above, with adjustments for a square shape  */
     .checkbox-group-wrapper input[type="checkbox"] + label::before {
       /* ... styles for custom checkbox ... */
     }
  
     .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
       /* ... styles for checked checkbox ... */
     }
  ```

+++

### 面板/容器元件

+++ 面板/容器元件的 HTML 結構

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**HTML 結構範例**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

- Fieldset 元素可用作含有 panel-wrapper 類別和其他類別的面板容器，以便根據面板名稱 (field-login) 設定樣式。
- 圖例元素(`<legend>`)做為面板標題，包含「登入資訊」文字和類別欄位標籤。 data-visible=&quot;false&quot; 屬性可以與 JavaScript 一起用來控制標題的可見度。
- 在欄位集中，多個。{Type}-wrapper 元素 (在本例中為 .text-wrapper 和 .password-wrapper) 代表面板中的個別表單欄位。
- 每個包裝函式皆包含一個標籤、輸入欄位及說明，與先前的範例類似。

+++

+++ 面板/容器元件的 CSS 選擇器範例

1. 為面板進行目標定位：

```CSS
  /* Target the entire panel container */
  .panel-wrapper {
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- `.panel-wrapper` 選擇器使用 panel-wrapper 類別來設定所有元素的樣式，為所有面板建立一致的外觀。

1. 為面板標題進行目標定位：

```CSS
  /* Target the legend element (panel title) */
  .panel-wrapper legend {
    /* Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /* Optional: create a separation line */
  }
```

- `.panel-wrapper legend` 選擇器設定面板內圖例元素的樣式，讓標題在視覺上脫穎而出。


1. 為面板中個別欄位進行目標定位：

```CSS
/* Target all form field wrappers within a panel */
.panel-wrapper .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- `.panel-wrapper .{Type}-wrapper` 選擇器為面板中含有 `.{Type}-wrapper` 類別的所有包裝函式進行目標定位，可讓您設定表單欄位之間的間距樣式。

1. 為特定欄位 (選項) 進行目標定位：

```CSS
  /* Target the username field wrapper */
  .panel-wrapper .text-wrapper.field-username {
    /* Add your styles here (specific to username field) */
  }

  /* Target the password field wrapper */
  .panel-wrapper .password-wrapper.field-password {
    /* Add your styles here (specific to password field) */
  }
```

- 這些屬於選項的選擇器可讓您在面板中為特定欄位包裝函式進行獨特樣式的目標定位，例如醒目顯示使用者名稱欄位。

+++

### 可重複面板

+++ 可重複面板的 HTML 結構

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**HTML 結構範例**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

每個面板都有與單一面板範例相同的結構，並含有附加屬性：

- data-repeatable=&quot;true&quot;：此屬性表示可使用 JavaScript 或框架以機動方式重複面板。

- 唯一 ID 和名稱：面板中的每個元素都有一個唯一 ID (例如 name-1、email-1) 和以面板索引為主的名稱屬性 (例如 name=&quot;contacts[0 ].name”)。這樣可以在提交多個面板時進行正確的資料收集。

+++

+++ 可重複面板的 CSS 選擇器

- 為所有可重複面板進行目標定位：

```CSS
  /* Target all panels with the repeatable attribute */
  .panel-wrapper[data-repeatable="true"] {
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

選擇器會為所有可重複的面板進行樣式設定，確保有一致的外觀和感覺。


- 為面板中個別欄位進行目標定位：

```CSS
/* Target all form field wrappers within a repeatable panel */
.panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

此選擇器可為可重複面板中所有欄位包裝函式進行樣式設定，讓欄位之間的間距維持一致。

- 為特定欄位 (在面板內) 進行目標定位：

```CSS
/* Target the name field wrapper within the first panel */
.panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /* Add your styles here (specific to first name field) */
}

/* Target all
```

+++

### 檔案附件

+++ 檔案附件的 HTML 結構

```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**HTML 結構範例**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

- 類別屬性使用為檔案附件提供的名稱 (claim_form)。
- 輸入元素的 id 和名稱屬性與檔案附件名稱 (claim_form) 相符。
- 檔案清單區段一開始是空值。當檔案上傳時，此區段會以 JavaScript 機動式地填入。

+++

+++ 檔案附件元件的 CSS 選擇器

- 為全部檔案附件元件進行目標定位：

```CSS
/* Target the entire file attachment component */
.file-wrapper {
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

此選擇器為全部檔案附件元件設定樣式，包括圖例、拖曳區域、輸入欄位和清單。

- 為特定元素進行目標定位：

```CSS
/* Target the drag and drop area */
.file-wrapper .file-drag-area {
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/* Target the file input element */
.file-wrapper input[type="file"] {
  /* Add your styles here (e.g., hide the default input) */
  display: none;
}

/* Target individual file descriptions within the list (populated dynamically) */
.file-wrapper .files-list .file-description {
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/* Target the file name within the description */
.file-wrapper .files-list .file-description .file-description-name {
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
}

/* Target the file size within the description */
.file-wrapper .files-list .file-description .file-description-size {
  /* Add your styles here (e.g., font-size) */
  font-size: 0.8em;
}

/* Target the remove button within the description */
.file-wrapper .files-list .file-description .file-description-remove {
  /* Add your styles here (e.g., background color, hover effect) */
  background-color: transparent;
  border: none;
  cursor: pointer;
}
```

這些選擇器可讓您為檔案附件元件的不同部分個別設定樣式。您可以調整樣式以符合您的設計偏好。

+++


## 設定元件樣式

您也可以根據表單欄位的特定類型 (`{Type}-wrapper`) 或個別名稱 (`field-{Name}`) 來設定表單欄位的樣式。這允許更精細地控制和自訂表單的外觀。

### 根據欄位類型設定樣式

您可以使用 CSS 選取器來以特定欄位類型為目標並一致地套用樣式。

+++ HTML 結構

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**HTML 結構範例**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

- 每個欄位都包含在具有多個類別的 `div` 元素中：
   - `{Type}-wrapper`：識別欄位的類型。例如：`form-text-wrapper`、`form-number-wrapper`、`form-email-wrapper`。
   - `field-{Name}`：根據名稱識別欄位。例如：`form-name`、`form-age`、`form-email`。
   - `field-wrapper`：所有欄位包裝函式的通用類別。
- `data-required` 屬性表示該欄位是必填還是選擇性欄位。
- 每個欄位都有對應的標籤、輸入元素和潛在的附加元素 (例如預留位置和描述)。


+++


+++ CSS 選取器範例

```CSS
/* Target all text input fields */
.text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

+++

### 根據欄位名稱設定樣式

您也可以根據名稱以個別欄位為目標來套用獨特的樣式。

+++ HTML 結構

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**HTML 結構範例**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

+++

+++ CSS 選取器範例

```CSS
.field-otp input {
   letter-spacing: 2px
}
```



此 CSS 的目標是位於具有類別 `field-otp` 的元素內的所有輸入元素。您表單的 HTML 結構遵循最適化表單區塊的慣例，這表示有一個標有「field-otp」類別的容器包含名為「otp」的欄位。

+++

