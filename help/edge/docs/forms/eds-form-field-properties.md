---
title: 掌握最適化Forms區塊欄位屬性
description: 使用試算表及最適化Forms區塊欄位屬性，更快製作強大的表單！ 本指南列出EDS Forms Block支援的所有屬性。
feature: Edge Delivery Services
source-git-commit: ccc6439f68d8199154d4cd664b9cdb6428460a64
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---


# 最適化Forms區塊欄位屬性

本檔案概述JSON結構描述如何對應至`blocks/form/form.js`中轉譯的HTML，著重於如何識別和轉譯欄位、常見模式以及欄位特有的差異。

## 如何識別欄位(`fieldType`)？

JSON結構描述中的每個欄位都有`fieldType`屬性可決定其呈現方式。 `fieldType`可以是：

- **特殊型別**\
  範例： `drop-down`、`radio-group`、`checkbox-group`、`panel`、`plain-text`、`image`、`heading`等。
- **有效的HTML輸入型別**\
  範例： `text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file`等。
- **具有`-input`尾碼的型別**\
  範例： `text-input`、`number-input`等。 （已標準化為基底型別，例如`text`、`number`）。

如果`fieldType`符合特殊型別，則會使用&#x200B;**自訂轉譯器**。 否則，會將其視為&#x200B;**預設輸入型別**。

請參閱下列各節，瞭解每種欄位型別的[完整HTML結構和屬性](#common-html-structure)。

## 欄位使用的通用屬性

以下是大部分欄位使用的屬性：

- `id`：指定專案ID並支援協助工具。
- `name`：定義輸入、選取或fieldset專案的`name`屬性。
- `label.value`、`label.richText`、`label.visible`：指定標籤/圖例文字、HTML內容和可見度。
- `value`：代表欄位目前的值。
- `required`：新增`required`屬性或驗證資料。
- `readOnly`， `enabled`：控制欄位是否可編輯或停用。
- `description`：在欄位下方顯示說明文字。
- `tooltip`：設定輸入的`title`屬性。
- `constraintMessages`：提供自訂錯誤訊息作為資料屬性。

## 通用HTML結構

大部分欄位都會在包含標籤和選用說明文字的包裝函式中轉譯。 下列程式碼片段會示範結構：

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

對於群組（無線電/核取方塊）和面板，會使用具有`<fieldset>`的`<legend>`，而非`<div>/<label>`。 說明文字 <div> 只有在已設定說明時才會出現。

## 錯誤訊息顯示

錯誤訊息會顯示在用於說明文字（動態更新）的相同`.field-description`元素中。

**當欄位無效時**：

- 包裝函式（例如，`.field-wrapper`）被指派為`.field-invalid`類別。
- `.field-description`內容已取代為對應的錯誤訊息。

**欄位生效時**：

- 已移除`.field-invalid`類別。
- `.field-description`已還原為原始說明文字（如果有的話），如果沒有的話，則會移除。

可使用JSON中的`constraintMessages`屬性來定義自訂錯誤訊息。\
這些在包裝函式上新增為`data-<constraint>ErrorMessage`屬性（例如，`data-requiredErrorMessage`）。

## 預設輸入型別(HTML輸入或`*-input`)

如果`fieldType`不是特殊型別，則會將其視為標準HTML輸入型別或視為`<type>-input`，例如`text`、`number`、`email`、`date`、`text-input`、`number-input`。

- 尾碼`-input`已移除，基底型別會做為輸入的`type`屬性。
- 這些型別預設在`renderField()`中處理。
常見的預設輸入型別為`text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file`等。  它們也接受`text-input`、`number-input`等，這些已標準化為基底型別。

## 預設輸入型別的限制

會根據JSON屬性，將限制新增為輸入元素上的屬性。

| JSON屬性 | HTML屬性 | 套用至 |
|--------------|---------------|------------|
| maxLength | maxlength | 文字，電子郵件，密碼，電話 |
| minlength | minlength | 文字，電子郵件，密碼，電話 |
| 圖樣 | 圖樣 | 文字，電子郵件，密碼，電話 |
| 最大 | 最大值 | 數字、範圍、日期 |
| 最小值 | 分鐘 | 數字、範圍、日期 |
| 步驟 | 步驟 | 數字、範圍、日期 |
| 接受 | 接受 | 檔案 |
| 多個 | 多個 | 檔案 |
| maxOccure | data-max | 面板 |
| minOccure | data-min | 面板 |

>[!NOTE]
>
> `multiple`是布林值屬性。 如果為true，則會新增`multiple`屬性。

這些屬性會由表單轉譯器根據欄位的JSON定義自動設定。

## 範例：含有限制的HTML結構

下列範例示範如何使用驗證限制和錯誤處理屬性來呈現數字欄位。

```html
<div class="number-wrapper field-wrapper field-age" data-id="age"
data-required="true"
data-minimumErrorMessage="Too small" data-maximumErrorMessage="Too large">
<label for="age" class="field-label">Age</label>
<input type="number"
id="age" name="age"
value="30" required min="18"
max="99" step="1"
placeholder="Enter your age" />
<div class="field-description" id="age-description"> Description or error message
</div>
</div>
```

HTML結構的每個部分在資料繫結、驗證和顯示說明或錯誤訊息方面都扮演一個角色。

## 欄位特定屬性及其HTML結構

### 下拉式清單

**額外屬性：**

- `enum` / `enumNames`：定義下拉式清單的選項值及其顯示標籤。
- `type`：若設為`array`，則啟用多重選取範圍。
- `placeholder`：新增停用的預留位置選項，以在選取之前引導使用者。

範例：

```html
<div class="drop-down-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="This field is required">
<label for="<id>" class="field-label">Label</label>
<select id="<id>" name="<name>" required title="Tooltip" multiple>
<option disabled selected value="">Placeholder</option>
<option value="opt1">Option 1</option>
<option value="opt2">Option 2</option>
</select>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### 純文字

**額外屬性**：

- `richText`：如果為true，會在段落中轉譯HTML。

範例：

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### 核取方塊

**額外屬性**：

- `enum`：定義核取方塊的已核取與未核取狀態的值。
- `properties.variant / properties.alignment`：指定切換樣式核取方塊的視覺樣式和對齊方式。

範例：

```html
<div class="checkbox-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="Please check this box">
<label for="<id>" class="field-label">Label</label>
<input type="checkbox"
id="<id>"
name="<name>" value="on"
required
data-unchecked-value="off" />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### 按鈕

**額外屬性**：

- `buttonType`：透過設定按鈕的型別（按鈕、提交或重設）來指定按鈕的行為。

範例：

```html
<div class="button-wrapper field-wrapper field-<name>" data-id="<id>">
<button id="<id>" name="<name>" type="submit" class="button"> Label
</button>
</div>
```

### 多行輸入

**額外屬性**：

- `minLength`：指定在文字或文字區域輸入中允許的最小字元數。
- `maxLength`：指定文字或文字區域輸入中允許的字元數目上限。
- `pattern`：定義輸入值必須符合才能視為有效的規則運算式。
- `placeholder`：在輸入值之前，在輸入或文字區域中顯示預留位置文字。

範例：

```html
<div class="multiline-wrapper field-wrapper field-<name>" data-id="<id>"
data-minLengthErrorMessage="Too short" data-maxLengthErrorMessage="Too long">
<label for="<id>" class="field-label">Label</label>
<textarea id="<id>"
name="<name>" required
minlength="2"
maxlength="100"
pattern="[A-Za-z]+"
placeholder="Type here..."></textarea>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### 面板

**額外屬性**：

- `repeatable`：指定面板是否可以動態重複。
- `minOccur`：設定所需的面板執行個體數目下限。   maxOccur：設定允許的面板例項數目上限。
- `properties.variant`：定義面板的視覺樣式或變體。
- `properties.colspan`：指定面板在格線版面配置中跨越的欄數。
- `index`：表示面板在其上層容器中的位置。
- `fieldset`：以圖例或標籤將`<fieldset>`元素下的相關欄位分組。

範例：

```html
<fieldset class="panel-wrapper field-wrapper field-<name>" data-id="<id>"
name="<name>"
data-repeatable="true" data-index="0">
<legend class="field-label">Label</legend>
<!-- Nested fields here -->
<button type="button" class="add">Add</button>
<button type="button" class="remove">Remove</button>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### 選項

**額外屬性**：

- `enum`：定義選項欄位的允許值集，做為每個選項按鈕選項的值屬性。

範例：

```html
<div class="radio-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<label for="<id>" class="field-label">Label</label>
<input type="radio" id="<id>" name="<name>" value="opt1" required />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### 單選按鈕群組

**額外屬性**：

- `enum`：定義選項群組的選項值清單，做為每個選項按鈕的值。
- `enumNames`：提供符合列舉順序之選項按鈕的顯示標籤。

範例：

```html
<fieldset class="radio-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<legend class="field-label">Label</legend>
<div>
<input type="radio" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="radio" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### **核取方塊群組**

**額外屬性**：

- `enum`：定義核取方塊群組的選項值清單，做為每個核取方塊的值。
- `enumNames`：提供符合列舉順序的核取方塊顯示標籤。
- `minItems`：設定必須為有效性選取的核取方塊數目下限。
- `maxItems`：設定觸發錯誤前可選取的核取方塊數目上限。

範例：

```html
<fieldset class="checkbox-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true" data-minItems="1"
data-maxItems="3">
<legend class="field-label">Label</legend>
<div>
<input type="checkbox" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="checkbox" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### 影像

**額外屬性**：

- `value / properties['fd:repoPath']`：定義影像來源路徑或呈現影像的存放庫路徑。
- `altText`：提供影像的替代文字（替代屬性）以改善協助工具。

範例：

```html
<div class="image-wrapper field-wrapper field-<name>" data-id="<id>">
<picture>
<img src="..." alt="..." />
<!-- Optimized sources -->
</picture>
</div>
```

### 標題

**額外屬性**：

- `value`：指定要顯示在標題元素內的文字內容（例如，`<h2>`）。

範例：

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

如需詳細資訊，請參閱`blocks/form/form.js`和`blocks/form/util.js`中的實作。


<!--Each form field is represented as a dedicated row in the spreadsheet, analogous to fields in a database table. The column headers act as labels for the various properties supported by the form field block.

Think of your form as a table in a spreadsheet, where each line represents a different question or piece of information you want to collect. The table headings tell you what kind of answers you can expect for each section.

The below table lists all the properties that are supported by the Adaptive Forms Block.

**Master Your Forms with These Adaptive Forms Block Field Properties:**

This table details all the properties you can use to customize your Adaptive Forms Block fields:

| Property | Description | Example |
|---|---|---|
| **Type** | [HTML input type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) (text, email, number, etc.), [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select), [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) | `text`, `email`, `radio`, `select` |
| **Name** | This defines the unique identifier for submitted data (e.g., 'email' for an email address field).  Choose a clear and unique name for each field, as the name serves as internal field identifier used for data mapping during submission. | `user_name`, `email_address` |
| **Label** | User-friendly field label | `"Full Name"`, `"Choose your country"` |
| **Value** | Default value displayed | `"John Doe"`, `"United States"` |
| **Placeholder** | Hint text within the field | `"Enter your email address"` |
| **Description** | Help text for users | `"Please enter a valid email address"` |
| **Visible** | Show/hide the field initially | `true`, `false` |
| **Mandatory** | Require a value from the user | `true`, `false` |
| **Min/Max** | Set minimum/maximum values (number, date, text length) | `18` (age), `2025-12-31` (date) |
| **Accept** | Allowed file types for file upload | `"image/jpeg,image/png"` |
| **Multiple** | Allow multiple file selections | `true`, `false` |
| **Options** | Comma-separated list for dropdown menus | `"Option 1, Option 2, Option 3"` |
| **Checked** | Default-selected radio button/checkbox | `true`, `false` |
| **Fieldset** | Group fields together | Fieldset name (e.g., `"Personal Information"`) |-->

