---
title: 引入自訂函式中的範圍物件
description: 表單支援自訂函式中的範圍物件，在執行規則時，這些物件會作為最後一個引數傳遞至函式。
keywords: 自訂函式中的範圍物件、全域物件、欄位物件。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 248c75a5-6335-41d2-aa0a-28a20a710f88
source-git-commit: e2bc958104bd9b75845ad2c213eec18d2560a3a4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# 自訂函數中的範圍物件

在Adaptive Forms中，執行規則時，範圍物件會作為最後一個引數傳給函式。 它可用來讀取表單/欄位屬性，以及從函式內修改表單。 範圍物件包含表單、觸發事件和目標欄位的唯讀Proxy物件。 可透過分別附加`$` （例如`scope.form.$id`和`scope.field.$id`）來使用範圍物件存取表單和欄位內容。

## 使用範圍物件的表單修改函式

範圍物件具有下清單單修改功能：

| 函數 | 語法 | 說明 | 程式碼範例 |
|-----------------|--------|-------------|-------------|
| **setProperty** | `setProperty(any $element, any $payload)` | 使用`$payload`在目標欄位上設定屬性。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule)檢視範例。 |
| **驗證** | `validate([any $element])` | 在目標欄位上執行驗證。 如果未提供目標，會在整個表單上執行驗證，並傳回一系列驗證錯誤。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#validate-the-field)檢視範例。 |
| **重設** *（已棄用）* | `reset([any $element])` | 已棄用。 請改用`dispatchEvent($target, 'reset')`。 重設目標欄位，如果未提供目標，則重設整個表單。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel)檢視範例。 |
| **importData** | `importData(any $payload)` | 將資料匯入表單，取代任何現有的表單資料。 若指定`qualifiedName`，資料只會匯入該容器欄位。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads)檢視範例。 |
| **exportData** | `exportData()` | 傳回表單資料。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server)檢視範例。 |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | 觸發表單提交。 您可以透過`$payload`引數指定要提交的內容，並透過`$contentType`引數設定內容型別。 資料預設為`multipart/form-data`提交。 選用的`$validateForm`引數指定是否應在提交前驗證表單（預設值： true）。 成功時引發`submitSuccess`；失敗時引發`submitError`。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server)檢視範例。 |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | 將焦點設定為目標欄位，可以是面板或表單欄位。 如果未提供目標，則焦點會設定為觸發規則的欄位。 選用的`$focusOption`引數指定相對於目標的下一個或上一個專案是否應聚焦。 支援的值： `'nextItem'`， `'previousItem'`。 如果與面板搭配使用，導覽會限制在該面板。 如果和欄位一起使用，導覽會在該欄位的父面板中發生。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field)檢視範例。 |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | 在由`$eventName`決定的專案上分派型別`$target`的事件。 如果未提供目標，則會在表單上傳送事件。 處理事件的運算式可以使用選用的`$payload`。 選用的`$dispatch`引數可控制事件傳播行為。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property)檢視範例。 |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | 將`$fieldIdentifier`所識別的欄位標籤為無效並顯示`$validationMessage`。 選用的`$option`引數指定`$fieldIdentifier`是否解譯為`id`、`dataRef`或`qualifiedName`。 預設值為`{useId: true}`。 支援的值： `{useId: true}`、`{useDataRef: true}`、`{useQualifiedName: true}`。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid)檢視範例。 |

## 另請參閱

{{see-also-rule-editor}}

