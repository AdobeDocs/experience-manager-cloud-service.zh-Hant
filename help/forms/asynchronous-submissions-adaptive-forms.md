---
title: 如何配置適應Forms的非同步提交？
description: 瞭解如何配置AdaptiveForms的非同步提交。 更深入地瞭解非同步提交在Adaptive Forms中的作用。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# 非同步提交自適應Forms {#asynchronous-submission-of-adaptive-forms}

傳統上，Web表單配置為同步提交。 在同步提交中，當用戶提交表單時，會將他們重定向到確認頁、感謝頁，或在提交失敗時，重定向到錯誤頁。 然而，單頁應用程式等現代Web體驗越來越受歡迎，在後台進行客戶端與伺服器交互時，網頁保持靜態。 您可以配置非同步提交，以便通過Adaptive Forms提供此體驗。

在非同步提交中，當用戶提交表單時，表單開發人員將插入單獨的體驗，例如重定向到網站的其他表單或單獨的部分。 作者還可以插入單獨的服務，如將資料發送到不同的資料儲存或添加自定義分析引擎。 在非同步提交時，Adaptive Form的行為與單頁應用程式類似，因為在伺服器上驗證提交的表單資料時，表單不會重新載入或其URL不會更改。

有關Adaptive Forms中非同步提交的詳細資訊，請閱讀。

## 配置非同步提交 {#configure}

要配置自適應表單的非同步提交，請執行以下操作：

1. 在自適應表單創作模式中，選擇「表單容器」對象，然後點擊 ![cmppr](assets/configure-icon.svg) 開啟其屬性。
1. 在 **[!UICONTROL 提交]** 屬性部分，啟用 **[!UICONTROL 使用非同步提交]**。
1. 在 **[!UICONTROL 提交時]** 部分，選擇要在成功提交表單時執行的以下選項之一。

   * **[!UICONTROL 重定向至URL]**:重定向到表單提交時指定的URL或頁面。 可以指定URL或瀏覽以在 **[!UICONTROL 重定向URL/路徑]** 的子菜單。
   * **[!UICONTROL 顯示消息]**:顯示表單提交消息。 您可以在以下文本欄位中寫入消息 **[!UICONTROL 顯示消息]** 的雙曲餘切值。 文本欄位支援富格文本格式。

1. 點擊 ![複選框1](assets/save_icon.svg) 的子菜單。

## 非同步提交的工作原理 {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] 為表單提交提供開箱即用的成功和錯誤處理程式。 處理程式是基於伺服器響應執行的客戶端函式。 當提交表單時，資料被傳輸到伺服器以進行驗證，伺服器返回對客戶端的響應，其中包含有關提交的成功或錯誤事件的資訊。 資訊作為參數傳遞給相關處理程式以執行該函式。

此外，表單作者和開發人員可以在表單級別編寫規則以覆蓋預設處理程式。 有關詳細資訊，請參見 [使用規則覆蓋預設處理程式](#custom)。

讓我們首先查看伺服器對成功和錯誤事件的響應。

### 伺服器對提交成功事件的響應 {#server-response-for-submission-success-event}

伺服器對提交成功事件的響應的結構如下：

```json
{oneOf: [
{  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouOption : {type : "string"}
   }},
  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouContent: {type: "string"}
   }
]

}
```

成功提交表單時的伺服器響應包括：

* 表單資料格式類型：XML或JSON
* XML或JSON格式的表單資料
* 選擇的選項可重定向到頁面或顯示在窗體中配置的消息
* 在表單中配置的頁面URL或消息內容

成功處理器讀取伺服器響應並相應地重定向到所配置的頁面URL或顯示消息。

### 伺服器對提交錯誤事件的響應 {#server-response-for-submission-error-event}

伺服器對提交錯誤事件的響應的結構如下：

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

在提交表單時出錯時，伺服器響應包括：

* 錯誤原因、驗證碼或伺服器端驗證失敗
* 錯誤對象清單，包括驗證失敗的欄位的SOM表達式和相應的錯誤消息

錯誤處理程式讀取伺服器響應，並相應地在表單上顯示錯誤消息。

## 使用規則覆蓋預設處理程式 {#custom}

表單開發人員和作者可以在表單級別編寫規則以覆蓋預設處理程式。 成功和錯誤事件的伺服器響應在窗體級別公開，開發人員可以使用 `$event.data` 在規則中。

執行以下步驟來編寫規則以處理成功和錯誤事件。

1. 在創作模式下開啟「自適應表單」，選擇任何表單對象，然後點擊 ![編輯規則1](assets/edit-rules-icon.svg) 開啟規則編輯器。
1. 選擇 **[!UICONTROL 窗體]** 在「表單對象」樹中按一下 **[!UICONTROL 建立]**。
1. 選擇 **[!UICONTROL 已成功提交]** 或 **[!UICONTROL 提交]** 從 **[!UICONTROL 選擇狀態]** 的子菜單。
1. 定義 **[!UICONTROL 然後]** 選定狀態的操作。 例如，選擇 **[!UICONTROL 導航至]** 然後鍵入或貼上URL。 也可以使用 **[!UICONTROL 函式]** 頁籤

   ![成功提交處理程式](assets/form-submission-handler.png)

1. 點擊 **[!UICONTROL 完成]** 來保存規則。
