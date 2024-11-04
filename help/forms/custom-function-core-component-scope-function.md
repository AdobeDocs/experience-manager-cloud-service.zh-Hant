---
title: 引入自訂函式中的範圍物件
description: 表單支援自訂函式中的範圍物件，在執行規則時，這些物件會作為最後一個引數傳遞至函式。
keywords: 自訂函式中的範圍物件、全域物件、欄位物件。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: af211649a4f22d06f4e8669335a8267ee948a408
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# 自訂函式中的範圍物件

在Adaptive Forms中，執行規則時，範圍物件會作為最後一個引數傳給函式。 它可用來讀取表單/欄位屬性，以及從函式內修改表單。 範圍物件包含表單、觸發事件和目標欄位的唯讀Proxy物件。 可透過分別附加`$` （例如`scope.form.$id`和`scope.field.$id`）來使用範圍物件存取表單和欄位內容。

## 使用範圍物件的表單修改函式

範圍物件具有下清單單修改功能：

| 函數 | 語法 | 說明 | 程式碼範例 |
|-----------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------|
| **setProperty** | `setProperty(any $element, any $payload)` | 使用`$payload`設定`$element`的屬性。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule)檢視範例。 |
| **驗證** | `validate([any $element])` | 在`$element`上執行驗證。 如果未提供元素，則會驗證整個表單。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#validate-the-field)檢視範例。 |
| **重設** | `reset([any $element])` | 重設`$element`。 如果未提供元素，則會重設整個表單。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel)檢視範例。 |
| **importData** | `importData(any $payload)` | 將資料匯入表單，取代任何現有的表單資料。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads)檢視範例。 |
| **exportData** | `exportData()` | 傳回表單資料。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server)檢視範例。 |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | 觸發表單提交。 `$data`引數指定要提交的內容，且`$submit_as`會定義內容型別（預設為「multipart/form-data」）。 選用的`$validate_form`決定是否應驗證表單（預設值： true）。 成功時引發`submitSuccess`；失敗時引發`submitError`。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server)檢視範例。 |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | 將焦點設定為`$element`，可以是面板或欄位。 如果未提供元素，則焦點會設定為觸發規則的欄位。 選用的`$focusOption`引數（屬於列舉型別`FocusOption`）指定是否將焦點放在相對於`$element`的&#39;nextItem&#39;或&#39;previousItem&#39;上。 如果指定面板，導覽會限制在該面板；如果欄位，導覽會在父面板中進行。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field)檢視範例。 |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | 在`$element`所指定的專案上分派型別`$eventName`的事件。 如果未提供元素，則會在表單上傳送事件。 選擇性`$payload`可供處理事件的運算式使用。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property)檢視範例。 |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | 將`$fieldIdentifier`所識別的欄位標籤為無效，並將驗證訊息設定為`$validationMessage`。 選用的`$option`引數指定`$fieldIdentifier`是否解譯為`id`、`name`或`dataRef`。 預設值為`{useId: true}`，支援的值包括`{useId: true}`、`{useDataRef: true}`和`{useQualifiedName: true}`。 | [按一下這裡](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid)檢視範例。 |

## 另請參閱

{{see-also-rule-editor}}