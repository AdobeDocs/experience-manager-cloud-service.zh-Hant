---
title: 欄位型別
description: 透過如何檢測您自己的應用程式的範例，瞭解通用編輯器在元件邊欄中可以編輯的不同欄位型別。
source-git-commit: b1a188d01371665b4375087847625d89e47d8927
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 6%

---


# 欄位型別 {#field-types}

透過如何檢測您自己的應用程式的範例，瞭解通用編輯器在元件邊欄中可以編輯的不同欄位型別。

{{universal-editor-status}}

## 概觀 {#overview}

調整您自己的應用程式以搭配通用編輯器使用時，您必須檢測元件，並定義元件可在編輯器的元件邊欄中操作的資料型別。

本檔案提供您可以使用的欄位型別概覽以及設定範例。

>[!TIP]
>
>如果您不熟悉如何針對通用編輯器檢測您的應用程式，請參閱檔案 [適用於AEM開發人員的通用編輯器概觀。](/help/implementing/universal-editor/developer-overview.md)

## 布林值 {#boolean}

布林欄位會儲存轉譯為核取方塊的簡單true/false值。

### 範例 {#sample-boolean}

```json
{
  "fields": [   
   {
      "component": "boolean",
      "valueType": "boolean",
      "name": "field1",
      "label": "Boolean Field",
      "description": "This is a boolean field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "customErrorMsg": "This is an error."
      }
    }
  ]
}
```

## 核取方塊群組 {#checkbox-group}

與布林值類似，核取方塊群組允許選取多個true/false專案。

### 範例 {#sample-checkbox-group}

```json
{
  "fields": [   
   {
      "component": "checkbox-group",
      "valueType": "string-array",
      "name": "field1",
      "label": "Checkbox Group",
      "description": "This is a checkbox group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "First option", "value": "one" },
        { "name": "Second option", "value": "two" },
        { "name": "Third option", "value": "three" }
      ]
    }
  ]
}
```

## 日期時間 {#date-time}

日期時間欄位可指定日期或時間或是兩者的組合。

### 範例 {#sample-date-time}

```json
{
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

## 數字 {#number}

數字欄位允許輸入數字。

### 範例 {#sample-number}

```json
{
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
        "numberMin": null,
        "numberMax": null,
        "customErrorMsg": "Please don't do that."
      }
    }
  ]
}
```

## 選項按鈕群組 {#radio-group}

單選按鈕群組允許從多個選項中進行互斥選取，這些選項呈現為類似於核取方塊群組的群組。

### 範例 {#sample-radio-group}

```json
{
  "fields": [   
   {
      "component": "radio-group",
      "valueType": "string",
      "name": "field1",
      "label": "Radio Group",
      "description": "This is a radio group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ]
    }
  ]
}
```

## 參考 {#reference}

參照允許指定另一個資料物件作為目前物件的參照。

## 選擇 {#select}

選取「 」即可在下拉式選單中選取一或多個預先定義的選項。

### 範例 {#sample-select}

```json
{
  "fields": [   
   {
      "component": "select",
      "valueType": "string",
      "name": "field1",
      "label": "Select",
      "description": "This is a select.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ],
      "emptyOption": true
    }
  ]
}
```

## 文字區域 {#text-area}

文字區域允許多行文字輸入。

### 範例 {#sample-text-area}

```json
{
  "fields": [   
   {
      "component": "text-area",
      "valueType": "string",
      "name": "field1",
      "label": "Text Area",
      "description": "This is a text area.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "mimeType": "text/x-markdown"
    }
  ]
}
```

## 文字輸入 {#text-input}

文字輸入允許單行文字輸入。

### 範例 {#sample-text-input}

```json
{
  "fields": [   
   {
      "component": "text-input",
      "valueType": "string",
      "name": "field1",
      "label": "Text Input",
      "description": "This is a text input.",
      "required": true,
      "multi": true,
      "placeholder": null
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "field2",
      "label": "Another Text Input",
      "description": "This is a text input with validation.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "validation": {
        "minLength": 5,
        "maxLength": 10,
        "regExp": "^foo:.*",
        "customErrorMsg": "I'm sorry, Dave. I can't do that."
      }
    }
  ]
}
```

