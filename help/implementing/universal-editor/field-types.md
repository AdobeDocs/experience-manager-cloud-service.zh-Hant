---
title: 模型定義、欄位和元件類型
description: 透過範例瞭解屬性邊欄中通用編輯器可編輯的欄位和元件型別。 瞭解如何建立模型定義並連結至元件，以裝備您自己的應用程式。
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
source-git-commit: c2dd0ed800739c2194ab20267f72b85461f3c5b8
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 10%

---


# 模型定義、欄位和元件類型 {#field-types}

透過範例瞭解屬性邊欄中通用編輯器可編輯的欄位和元件型別。 瞭解如何建立模型定義並連結至元件，以裝備您自己的應用程式。

## 概觀 {#overview}

調整您自己的應用程式以與通用編輯器搭配使用時，您必須檢測元件，並定義元件可在編輯器的屬性邊欄中操作的欄位和元件型別。 若要這麼做，請建立模型並從元件連結至模型。

本檔案提供模型定義、欄位和可用元件型別的概觀，以及設定範例。

>[!TIP]
>
>如果您不熟悉如何針對通用編輯器檢測您的應用程式，請參閱檔案 [適用於AEM開發人員的通用編輯器概觀。](/help/implementing/universal-editor/developer-overview.md)

## 模型定義結構 {#model-structure}

若要透過通用編輯器中的屬性邊欄設定元件，模型定義必須存在且連結至元件。

模型定義是JSON結構，從模型的陣列開始。

```json
[
  {
    "id": "model-id",        // must be unique
    "fields": []             // array of fields which shall be rendered in the properties rail
  }
]
```

請參閱 **[欄位](#fields)** 一節，以取得如何定義 `fields` 陣列。

若要將模型定義與元件一起使用， `data-aue-model` 屬性可供使用。

```html
<div data-aue-resource="urn:datasource:/content/path" data-aue-type="component"  data-aue-model="model-id">Click me</div>
```

## 載入模型定義 {#loading-model}

建立模型後，可作為外部檔案參照。

```html
<script type="application/vnd.adobe.aue.model+json" src="<url-of-model-definition>"></script>
```

或者，您也可以線上上定義模型。

```html
<script type="application/vnd.adobe.aue.model+json">
  { ... model definition ... }
</script>
```

## 欄位 {#fields}

欄位物件具有下列型別定義。

| 設定 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `component` | `ComponentType` | 元件的轉譯器 | 是 |
| `name` | `string` | 應儲存資料的屬性 | 是 |
| `label` | `FieldLabel` | 欄位標籤 | 是 |
| `description` | `FieldDescription` | 欄位說明 | 否 |
| `placeholder` | `string` | 欄位預留位置 | 否 |
| `value` | `FieldValue` | 預設值 | 否 |
| `valueType` | `ValueType` | 標準驗證，可以是 `string`， `string[]`， `number`， `date`， `boolean` | 否 |
| `required` | `boolean` | 欄位是否為必填欄位 | 否 |
| `readOnly` | `boolean` | 欄位是否為唯讀 | 否 |
| `hidden` | `boolean` | 預設為隱藏欄位 | 否 |
| `condition` | `RulesLogic` | 顯示或隱藏欄位的規則，根據 [條件](/help/implementing/universal-editor/customizing.md#conditionally-hide) | 否 |
| `multi` | `boolean` | 此欄位是否為多個欄位 | 否 |
| `validation` | `ValidationType` | 欄位的驗證規則 | 否 |
| `raw` | `unknown` | 元件可使用的原始資料 | 否 |

### 元件型別 {#component-types}

以下是可用於呈現欄位的元件型別。

| 說明 | 元件類型 |
|---|---|
| [AEM標籤](#aem-tag) | `aem-tag` |
| [AEM內容](#aem-content) | `aem-content` |
| [布林值](#boolean) | `boolean` |
| [核取方塊群組](#checkbox-group) | `checkbox-group` |
| [容器](#container) | `container` |
| [日期時間](#date-time) | `date-time` |
| [多選](#multiselect) | `multiselect` |
| [數字](#number) | `number` |
| [選項按鈕群組](#radio-group) | `radio-group` |
| [參考](#reference) | `reference` |
| [RTF文字](#rich-text) | `rich-text` |
| [選取](#select) | `select` |
| [標籤](#tab) | `tab` |
| [文字](#text) | `text` |

#### AEM標籤 {#aem-tag}

AEM標籤元件型別會啟用AEM標籤選擇器，其可用來將標籤附加至元件。

>[!BEGINTABS]

>[!TAB 範例]

```json
{
  "id": "aem-tag-picker",
  "fields": [
    {
      "component": "aem-tag",
      "label": "AEM Tag Picker",
      "name": "cq:tags",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![AEM標籤元件型別的熒幕擷圖](assets/component-types/aem-tag-picker.png)

>[!ENDTABS]

#### AEM內容 {#aem-content}

AEM內容元件型別會啟用AEM內容選擇器，其可用於設定內容參照。

>[!BEGINTABS]

>[!TAB 範例]

```json
{
  "id": "aem-content-picker",
  "fields": [
    {
      "component": "aem-content",
      "name": "reference",
      "value": "",
      "label": "AEM Content Picker",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![AEM內容元件型別的熒幕擷圖](assets/component-types/aem-content-picker.png)

>[!ENDTABS]

#### 布林值 {#boolean}

布林值元件型別會儲存簡單的true/false值，呈現為切換按鈕。 它提供額外的驗證型別。

| 驗證類型 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `customErrorMsg` | `string` | 如果輸入的值不是布林值，則會顯示的訊息 | 否 |

>[!BEGINTABS]

>[!TAB 範例1]

```json
{
  "id": "boolean",
  "fields": [
    {
      "component": "boolean",
      "label": "Boolean",
      "name": "boolean",
      "valueType": "boolean"
    }
  ]
}
```

>[!TAB 範例2]

```json
{
  "id": "another-boolean",
  "fields": [
    {
      "component": "boolean",
      "label": "Boolean",
      "name": "boolean",
      "valueType": "boolean",
      "validation": {
        "customErrorMsg": "Think, McFly. Think!"
      }
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![布林值元件型別的熒幕擷圖](assets/component-types/boolean.png)

>[!ENDTABS]

#### 核取方塊群組 {#checkbox-group}

與布林值類似，核取方塊群組元件型別允許選取多個true/false專案，呈現為多個核取方塊。

>[!BEGINTABS]

>[!TAB 範例]

```json
{
  "id": "checkbox-group",
  "fields": [
    {
      "component": "checkbox-group",
      "label": "Checkbox Group",
      "name": "checkbox",
      "valueType": "string[]",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![核取方塊群組元件型別的熒幕擷圖](assets/component-types/checkbox-group.png)

>[!ENDTABS]

#### 容器 {#container}

容器元件型別允許將元件分組。 它提供額外設定。

| 設定 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `collapsible` | `boolean` | 容器是否可摺疊 | 否 |

>[!BEGINTABS]

>[!TAB 範例]

```json
 {
  "id": "container",
  "fields": [
    {
      "component": "container",
      "label": "Container",
      "name": "container",
      "valueType": "string",
      "collapsible": true,
      "fields": [
        {
          "component": "text-input",
          "label": "Simple Text 1",
          "name": "text",
          "valueType": "string"
        },
        {
          "component": "text-input",
          "label": "Simple Text 2",
          "name": "text2",
          "valueType": "string"
        }
      ]
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![容器元件型別的熒幕擷圖](assets/component-types/container.png)

>[!ENDTABS]

#### 內容片段 {#content-fragment}

內容片段選擇器可用來選取 [內容片段](/help/sites-cloud/authoring/fragments/content-fragments.md) 及其變數（如有需要）。 它提供額外設定。

| 設定 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `variationName` | `string` | 儲存所選變數的變數名稱。 如果未定義，則不會顯示變數選擇器 | 否 |

>[!BEGINTABS]

>[!TAB 範例1]

```json
[
  {
    "id": "aem-content-fragment",
    "fields": [
      {
        "component": "aem-content-fragment",
        "name": "picker",
        "label": "Content Fragment Picker",
        "valueType": "string",
        "variationName": "contentFragmentVariation"
      }
    ]
  }
]
```

>[!TAB 熒幕擷圖]

![內容片段選擇器的熒幕擷圖](assets/component-types/aem-content-fragment.png)

>[!ENDTABS]

#### 日期時間 {#date-time}

日期時間元件型別可指定日期、時間或其組合。 它提供其他設定。

| 設定 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `displayFormat` | `string` | 日期字串顯示格式 | 是 |
| `valueFormat` | `string` | 儲存日期字串的格式 | 是 |

此外，還提供其他驗證型別。

| 驗證類型 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `customErrorMsg` | `string` | 訊息將在發生以下情況時顯示 `valueFormat` 不符合 | 否 |

>[!BEGINTABS]

>[!TAB 範例1]

```json
{
  "id": "date-time",
  "fields": [
    {
      "component": "date-time",
      "label": "Date & Time",
      "name": "date",
      "valueType": "date"
    }
  ]
}
```

>[!TAB 範例2]

```json
{
  "id": "another-date-time",
  "fields": [
    {
      "component": "date-time",
       "valueType": "date-time",
      "name": "field1",
      "label": "Date Time",
      "description": "This is a date time field that stores both date and time.",
      "required": true,
      "placeholder": "YYYY-MM-DD HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Marty! You have to come back with me!"
      }
    },
    {
      "component": "date-time",
      "valueType": "date",
      "name": "field2",
      "label": "Another Date Time",
      "description": "This is another date time field that only stores the date.",
      "required": true,
      "placeholder": "YYYY-MM-DD",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Back to the future!"
      }
    },
    {
      "component": "date-time",
      "valueType": "time",
      "name": "field3",
      "label": "Yet Another Date Time",
      "description": "This is another date time field that only stores the time.",
      "required": true,
      "placeholder": "HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Great Scott!"
      }
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![日期時間元件型別的熒幕擷圖](assets/component-types/date-time.png)

>[!ENDTABS]

#### 體驗片段 {#experience-fragment}

體驗片段選擇器可用來選取 [體驗片段](/help/sites-cloud/authoring/fragments/experience-fragments.md) 及其變數（如有需要）。 它提供額外設定。

| 設定 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `variationName` | `string` | 儲存所選變數的變數名稱。 如果未定義，則不會顯示變數選擇器 | 否 |

>[!BEGINTABS]

>[!TAB 範例1]

```json
[
  {
    "id": "aem-experience-fragment",
    "fields": [
      {
        "component": "aem-experience-fragment",
        "name": "picker",
        "label": "Experience Fragment Picker",
        "valueType": "string",
        "variationName": "experienceFragmentVariation"
      }
    ]
  }
]
```

>[!TAB 熒幕擷圖]

![體驗片段選擇器的熒幕擷圖](assets/component-types/aem-experience-fragment.png)

>[!ENDTABS]


#### 多選 {#multiselect}

多選元件型別會在下拉式選單中顯示多個可供選取的專案，包括將可選取元素分組的功能。

>[!BEGINTABS]

>[!TAB 範例1]

```json
{
  "id": "multiselect",
  "fields": [
    {
      "component": "multiselect",
      "name": "multiselect",
      "label": "Multi Select",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

>[!TAB 範例2]

```json
{
  "id": "multiselect-grouped",
  "fields": [
    {
      "component": "multiselect",
      "name": "property",
      "label": "Multiselect field",
      "valueType": "string",
      "required": true,
      "maxSize": 2,
      "options": [
        {
          "name": "Theme",
          "children": [
            { "name": "Light", "value": "light" },
            { "name": "Dark",  "value": "dark" }
          ]
        },
        {
          "name": "Type",
          "children": [
            { "name": "Alpha", "value": "alpha" },
            { "name": "Beta", "value": "beta" },
            { "name": "Gamma", "value": "gamma" }
          ]
        }
      ]
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![多選元件型別的熒幕擷圖](assets/component-types/multiselect.png)
![包含群組的多重選取元件型別熒幕擷圖](assets/component-types/multiselect-group.png)

>[!ENDTABS]

#### 數字 {#number}

數字元件型別允許輸入數字。 它提供額外的驗證型別。

| 驗證類型 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `numberMin` | `number` | 允許的最小數量 | 否 |
| `numberMax` | `number` | 允許的最大數量 | 否 |
| `customErrorMsg` | `string` | 訊息將在發生以下情況時顯示 `numberMin` 或 `numberMax` 不符合 | 否 |

>[!BEGINTABS]

>[!TAB 範例1]

```json
{
  "id": "number",
  "fields": [
    {
      "component": "number",
      "name": "number",
      "label": "Number",
      "valueType": "number",
      "value": 0
    }
  ]
}
```

>[!TAB 範例2]

```json
{
  "id": "another-number",
  "fields": [
   {
      "component": "number",
      "valueType": "number",
      "name": "field1",
      "label": "Number Field",
      "description": "This is a number field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "numberMin": 0,
        "numberMax": 88,
        "customErrorMsg": "You also need 1.21 gigawatts."
      }
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![數字元件型別的熒幕擷圖](assets/component-types/number.png)

>[!ENDTABS]

#### 選項按鈕群組 {#radio-group}

單選按鈕群組元件型別允許從多個選項中進行互斥選取，這些選項呈現為類似於核取方塊群組的群組。

>[!BEGINTABS]

>[!TAB 範例]

```json
{
  "id": "radio-group",
  "fields": [
    {
      "component": "radio-group",
      "label": "Radio Group",
      "name": "radio",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![選項群組元件型別的熒幕擷圖](assets/component-types/radio.png)

>[!ENDTABS]

#### 參考 {#reference}

參照元件型別允許參照目前物件中的其他資料物件。

>[!BEGINTABS]

>[!TAB 範例]

```json
{
  "id": "reference",
  "fields": [
    {
      "component": "reference",
      "label": "Reference",
      "name": "reference",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![參考元件型別的熒幕擷圖](assets/component-types/reference.png)

>[!ENDTABS]

#### RTF {#rich-text}

RTF允許多行RTF輸入。 它提供額外的驗證型別。

| 驗證類型 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `maxSize` | `number` | 允許的最大字元數 | 否 |
| `customErrorMsg` | `string` | 訊息將在發生以下情況時顯示 `maxSize` 已超過 | 否 |

>[!BEGINTABS]

>[!TAB 範例1]

```json
{
  "id": "richtext",
  "fields": [
    {
      "component": "richtext",
      "name": "rte",
      "label": "Rich Text",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 範例2]

```json
{
  "id": "another-richtext",
  "fields": [
    {
      "component": "richtext",
      "name": "rte",
      "label": "Rich Text",
      "valueType": "string",
      "validation": {
        "maxSize": 1000,
        "customErrorMsg": "That's about as funny as a screen door on a battleship."
      }
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![文字區域元件型別的熒幕擷圖](assets/component-types/richtext.png)

>[!ENDTABS]

#### 選取 {#select}

選取元件型別可讓您從下拉式選單中的預先定義選項清單中選取單一選項。

>[!BEGINTABS]

>[!TAB 範例]

```json
{
  "id": "select",
  "fields": [
    {
      "component": "select",
      "label": "Select",
      "name": "select",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![選取元件型別的熒幕擷圖](assets/component-types/select.png)

>[!ENDTABS]

#### 標籤 {#tab}

索引標籤元件型別可讓您將其他輸入欄位分組在多個索引標籤上，以改善作者的版面配置組織。

A `tab` 可將定義視為陣列中的分隔符號 `fields`. 之後的一切 `tab` 將會放在該索引標籤上，直到新的 `tab` 之後，會將下列專案放置在新標籤上。

如果您希望專案出現在所有標籤的上方，必須在任何標籤之前定義它們。

>[!BEGINTABS]

>[!TAB 範例]

```json
{
  "id": "tab",
  "fields": [
    {
      "component": "tab",
      "label": "Tab 1",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "label": "Text 1",
      "name": "text1",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Tab 2",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "label": "Text 2",
      "name": "text2",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![索引標籤元件型別的熒幕擷圖](assets/component-types/tab.png)

>[!ENDTABS]

#### 文字 {#text}

文字允許單行文字輸入。  它包含其他驗證型別。

| 驗證類型 | 數值類型 | 說明 | 必填 |
|---|---|---|---|
| `minLength` | `number` | 允許的最小字元數 | 否 |
| `maxLength` | `number` | 允許的最大字元數 | 否 |
| `regExp` | `string` | 輸入文字必須符合的規則運算式 | 否 |
| `customErrorMsg` | `string` | 訊息將在發生以下情況時顯示 `minLength`， `maxLength`、和/或 `regExp` 違反了 | 否 |

>[!BEGINTABS]

>[!TAB 範例1]

```json
{
  "id": "simpletext",
  "fields": [
    {
      "component": "text",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string"
    }
  ]
}
```

>[!TAB 範例2]

```json
{
  "id": "another simpletext",
  "fields": [
    {
      "component": "text",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string",
      "description": "This is a text input with validation.",
      "required": true,
      "validation": {
        "minLength": 1955,
        "maxLength": 1985,
        "regExp": "^foo:.*",
        "customErrorMsg": "Why don't you make like a tree and get outta here?"
      }
    }
  ]
}
```

>[!TAB 熒幕擷圖]

![文字元件型別的熒幕擷圖](assets/component-types/simpletext.png)

>[!ENDTABS]
