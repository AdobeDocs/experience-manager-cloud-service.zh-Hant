---
title: 如何使用API從最適化Forms叫用表單資料模型服務？
description: 說明可用於從最適化表單欄位中叫用以WSDL撰寫的網頁服務的invokeWebServices API。
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# 從最適化Forms叫用表單資料模型服務的API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概觀 {#overview}

[!DNL AEM Forms] 可讓表單作者從調適型表單欄位叫用表單資料模型中設定的服務，進一步簡化及增強表單填寫體驗。 若要叫用資料模型服務，您可以在視覺化編輯器中建立規則，或使用 `guidelib.dataIntegrationUtils.executeOperation` 的程式碼編輯器中的API [規則編輯器](rule-editor.md).

本檔案著重於使用編寫JavaScript `guidelib.dataIntegrationUtils.executeOperation` 用於叫用服務的API。

## 使用API {#using-the-api}

此 `guidelib.dataIntegrationUtils.executeOperation` API會從最適化表單欄位中叫用服務。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

的結構 `guidelib.dataIntegrationUtils.executeOperation` API會指定服務作業的相關詳細資訊。 結構的語法如下。

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API結構會指定下列有關服務操作的詳細資訊。

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>用於指定表單資料模型識別碼、作業標題和作業名稱的結構</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>指定表單資料模型的存放庫路徑，包括其名稱</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>指定要執行的服務作業名稱</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>將一個或多個表單物件對應到服務操作的輸入引數</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>將一或多個表單物件對應至服務作業的輸出值，以填入表單欄位<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>根據服務操作的輸入引數傳回值。 此為選用引數，可作為回呼函式使用。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>如果success回呼函式無法根據輸入引數顯示輸出值，則顯示錯誤訊息。 此為選用引數，可作為回呼函式使用。<br /> </td>
  </tr>
 </tbody>
</table>

## 用於叫用服務的範例指令碼 {#sample-script-to-invoke-a-service}

以下範例指令碼使用 `guidelib.dataIntegrationUtils.executeOperation` 用於叫用的API `getAccountById` 服務作業設定於 `employeeAccount` 表單資料模型。

此 `getAccountById` 操作取得的值位於 `employeeID` 表單欄位作為 `empId` 引數並傳回對應員工的員工名稱、帳號及帳戶餘額。 輸出值會填入指定的表單欄位中。 例如，中的值 `name` 引數會填入 `fullName` 表單元素和值 `accountNumber` 中的引數 `account` 表單元素。

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## 搭配回呼函式使用API {#using-the-api-callback}

您也可以使用呼叫表單資料模型服務 `guidelib.dataIntegrationUtils.executeOperation` 具有回呼函式的API。 API語法如下：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回呼函式可以具有 `success` 和 `failure` 回呼函式。

### 包含成功和失敗回呼函式的範例指令碼 {#callback-function-success-failure}

以下範例指令碼使用 `guidelib.dataIntegrationUtils.executeOperation` 用於叫用的API `GETOrder` 服務作業設定於 `employeeOrder` 表單資料模型。

此 `GETOrder` 操作取得的值位於 `Order ID` 表單欄位作為 `orderId` 引數並傳回訂單數量值 `success` 回呼函式。  如果 `success` 回撥函式不會傳回訂單數量，而 `failure` 回呼函式會顯示 `Error occured` 訊息。

>[!NOTE]
>
> 如果您使用 `success` 回呼函式，則輸出值不會填入指定的表單欄位中。

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
