---
title: 掌握自適應表單區塊欄位屬性
description: 使用試算表和自適應表單區塊欄位屬性，更快速地製作功能強大的表單！本指南列出 EDS 表單區塊支援的所有屬性。
feature: Edge Delivery Services
exl-id: e86ccc36-bda0-4e9d-8d65-ae7cb3fa79b7
source-git-commit: 41dd61425ce3b7536ee805580f3841e32e40ee99
workflow-type: ht
source-wordcount: '930'
ht-degree: 100%

---

# 自適應表單區塊欄位屬性

本文件概述 JSON 結構描述如何對應至 `blocks/form/form.js` 中轉譯的 HTML，重點介紹如何識別和轉譯欄位、常見模式，以及欄位特定的差異。

## 如何識別欄位 (`fieldType`)？

JSON 結構描述中的每個欄位都具備 `fieldType` 屬性，用於決定其轉譯方式。`fieldType` 可能是：

- **特殊類型**\
  範例：`drop-down`、`radio-group`、`checkbox-group`、`panel`、`plain-text`、`image`、`heading` 等。
- **有效的 HTML 輸入類型**\
  範例：`text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file` 等。
- **具有 `-input` 尾碼的類型**\
  範例：`text-input`、`number-input` 等。(已標準化為 `text`、`number` 等基底類型)。

如果 `fieldType` 符合特殊類型，就會使用&#x200B;**自訂轉譯器**。否則，會將其視為&#x200B;**預設輸入類型**。

請參閱以下各區段，了解各個欄位類型的[完整 HTML 結構和屬性](#common-html-structure)。

## 欄位常用的屬性

以下為大部分欄位使用的屬性：

- `id`：指定元素 ID 並支援無障礙功能。
- `name`：定義輸入、選取或欄位集元素的 `name` 屬性。
- `label.value`、`label.richText`、`label.visible`：指定標籤/圖例文字、HTML 內容和可見度。
- `value`：代表欄位目前的值。
- `required`：新增 `required` 屬性或驗證資料。
- `readOnly`、`enabled`：控制欄位為可編輯或停用。
- `description`：在欄位下方顯示說明文字。
- `tooltip`：設定輸入的 `title` 屬性。
- `constraintMessages`：提供自訂錯誤訊息作為資料屬性。

## 常見的 HTML 結構

大部分欄位是在包含標籤和選用說明文字的包裝函式內進行轉譯。下列片段展現出其結構：

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

對於群組 (單選按鈕/核取方塊) 和面板，會使用搭配 `<legend>` 的 `<fieldset>`，而非 `<div>/<label>`。說明文字 <div> 只有在已設定說明時才會出現。

## 錯誤訊息顯示

錯誤訊息會顯示在與說明文字所用的相同 `.field-description` 元素中 (該元素會動態更新)。

**欄位無效時**：

- 包裝函式 (例如 `.field-wrapper`) 會獲指派 `.field-invalid` 類別。
- `.field-description` 內容會替換為相應的錯誤訊息。

**欄位變為有效時**：

- `.field-invalid` 類別會移除。
- `.field-description` 會回復為原始說明文字 (如適用)；若無任何原始說明文字，則會將其移除。

可於 JSON 中使用 `constraintMessages` 屬性定義自訂錯誤訊息。\
這些訊息會在包裝函式上新增為 `data-<constraint>ErrorMessage` 屬性 (例如 `data-requiredErrorMessage`)。

## 預設輸入類型 (HTML 輸入或 `*-input`)

如果 `fieldType` 不是特殊類型，就會將其視為標準 HTML 輸入類型，或視為 `<type>-input`，例如 `text`、`number`、`email`、`date`、`text-input`、`number-input`。

- 尾碼 `-input` 會刪除，且基底類型會作為輸入的 `type` 屬性。
- 這些類型預設是在 `renderField()` 中進行處理。
常見的預設輸入類型為 `text`、`number`、`email`、`date`、`password`、`tel`、`range`、`file` 等。這些類型也接受 `text-input`、`number-input` 等已標準化為基底類型的內容。

## 預設輸入類型的限制式

限制式會根據 JSON 屬性，在輸入元素上新增為屬性。

| JSON 屬性 | HTML 屬性 | 適用於 |
|--------------|---------------|------------|
| maxLength | maxlength | text、email、password、tel |
| minLength | minlength | text、email、password、tel |
| pattern | pattern | text、email、password、tel |
| maximum | max | number、range、date |
| minimum | min | number、range、date |
| step | step | number、range、date |
| accept | accept | file |
| multiple | multiple | file |
| maxOccur | data-max | panel |
| minOccur | data-min | panel |

>[!NOTE]
>
> `multiple` 為布林值屬性。若為真，就會新增 `multiple` 屬性。

這些屬性會根據欄位的 JSON 定義，由表單轉譯器自動設定。

## 範例：含有限制式的 HTML 結構

下列範例示範如何使用驗證限制式和錯誤處理屬性來轉譯數字欄位。

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

HTML 結構的每個部分都在資料繫結、驗證及顯示說明或錯誤訊息方面扮演著其角色。

## 欄位特定屬性及其 HTML 結構

### 下拉式清單

**額外屬性：**

- `enum`/`enumNames`：定義下拉式清單的選項值及其顯示標籤。
- `type`：若設定為 `array`，就會啟用多重選取。
- `placeholder`：新增停用的預留位置選項，在使用者選取之前給予指引。

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

- `richText`：若為真，就會在段落中轉譯 HTML。

範例：

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### 核取方塊

**額外屬性**：

- `enum`：定義核取方塊之已核取和未核取狀態的值。
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

- `buttonType`：設定按鈕的類型 (按鈕、提交或重設)，藉此指定按鈕的行為。

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
- `maxLength`：指定在文字或文字區域輸入中允許的最大字元數。
- `pattern`：定義規則運算式；輸入值必須與其相符才能視為有效。
- `placeholder`：在輸入或文字區域中顯示預留位置文字，直到輸入值為止。

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
- `minOccur`：設定必要之面板執行個體的最小數量。maxOccur：設定允許之面板執行個體的最大數量。
- `properties.variant`：定義面板的視覺樣式或變體。
- `properties.colspan`：指定面板在網格版面中涵蓋的欄數。
- `index`：指出面板在其上層容器中的位置。
- `fieldset`：以圖例或標籤將 `<fieldset>` 元素之下的相關欄位分組。

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

### 單選按鈕

**額外屬性**：

- `enum`：定義單選按鈕欄位的允許值集合，作為每個選項按鈕選項的值屬性。

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

- `enum`：定義單選按鈕群組的選項值清單，作為每個選項按鈕的值。
- `enumNames`：提供選項按鈕的顯示標籤，且對應列舉順序。

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

- `enum`：定義核取方塊群組的選項值清單，作為每個核取方塊的值。
- `enumNames`：提供核取方塊的顯示標籤，且對應列舉順序。
- `minItems`：設定必須選取的核取方塊最小數量；選取此數量才能視為有效。
- `maxItems`：設定可選取的核取方塊最大數量；超過此數量便會觸發錯誤。

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

- `value / properties['fd:repoPath']`：定義用於轉譯影像的影像來源路徑或存放庫路徑。
- `altText`：提供影像的替代文字 (替代屬性)，藉此改善無障礙功能。

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

- `value`：指定要顯示於標題元素中的文字內容 (例如 `<h2>`)。

範例：

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

如需更多詳細資訊，請參閱 `blocks/form/form.js` 和 `blocks/form/util.js` 中的實作。


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
