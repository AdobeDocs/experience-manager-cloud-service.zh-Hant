---
title: 如何為適用性Forms設定非同步提交？
description: 了解如何為適用性Forms設定非同步提交。 深入了解非同步提交如何適用於適用性Forms。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# 非同步提交最適化Forms {#asynchronous-submission-of-adaptive-forms}

傳統上，網路表單的設定是同步提交。 在同步提交中，當使用者提交表單時，系統會將他們重新導向至確認頁面、感謝頁面，或在提交失敗時，重新導向至錯誤頁面。 不過，單頁應用程式等現代化網頁體驗正日益普及，當用戶端與伺服器互動於背景時，網頁會維持靜態。 您可以設定非同步提交，以透過適用性Forms提供此體驗。

在非同步提交中，當使用者提交表單時，表單開發人員會插入不同的體驗，例如重新導向至網站的其他表單或個別區段。 作者也可以外掛個別服務，例如傳送資料至不同的資料存放區，或新增自訂分析引擎。 非同步提交時，適用性表單的行為類似於單頁應用程式，因為表單不會重新載入，或提交的表單資料在伺服器上通過驗證時，其URL不會變更。

如需Adaptive Forms中非同步提交的詳細資訊，請參閱。

## 設定非同步提交 {#configure}

若要設定適用性表單的非同步提交：

1. 在適用性表單製作模式中，選取「表單容器」物件並點選 ![cmppr1](assets/configure-icon.svg) 來開啟其屬性。
1. 在 **[!UICONTROL 提交]** 屬性部分，啟用 **[!UICONTROL 使用非同步提交]**.
1. 在 **[!UICONTROL 提交時]** 部分，選擇以下選項之一，以在成功提交表單時執行。

   * **[!UICONTROL 重新導向至URL]**:重新導向至表單提交時指定的URL或頁面。 您可以指定URL或瀏覽，以選擇 **[!UICONTROL 重新導向URL/路徑]** 欄位。
   * **[!UICONTROL 顯示消息]**:在表單提交時顯示訊息。 您可以在 **[!UICONTROL 顯示消息]** 選項。 文字欄位支援RTF格式。

1. 點選 ![check-button1](assets/save_icon.svg) 以儲存屬性。

## 非同步提交如何運作 {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] 為表單提交提供現成可用的成功和錯誤處理常式。 處理常式是根據伺服器回應執行的用戶端函式。 提交表單時，將資料發送到伺服器進行驗證，伺服器會向客戶端返回一個響應，其中包含有關提交成功或錯誤事件的資訊。 資訊會以參數形式傳遞至相關處理常式，以執行函式。

此外，表單作者和開發人員可以在表單層級撰寫規則，以覆寫預設處理常式。 如需詳細資訊，請參閱 [使用規則覆蓋預設處理程式](#custom).

讓我們先檢閱伺服器對成功和錯誤事件的回應。

### 提交成功事件的伺服器回應 {#server-response-for-submission-success-event}

提交成功事件的伺服器回應結構如下：

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

成功提交表單時的伺服器回應包括：

* 表單資料格式類型：XML或JSON
* XML或JSON格式的表單資料
* 已選取重新導向至頁面或顯示訊息的選項（如表單中所設定）
* 頁面URL或訊息內容，如表單中設定

成功處理常式會讀取伺服器回應，並因此重新導向至設定的頁面URL或顯示訊息。

### 提交錯誤事件的伺服器響應 {#server-response-for-submission-error-event}

提交錯誤事件的伺服器回應結構如下：

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

提交表單時發生錯誤時的伺服器回應包括：

* 錯誤原因、驗證碼失敗或伺服器端驗證
* 錯誤對象清單，包括驗證失敗的欄位的SOM表達式和相應的錯誤消息

錯誤處理程式讀取伺服器回應，並因此在表單上顯示錯誤訊息。

## 使用規則覆蓋預設處理程式 {#custom}

表單開發人員和作者可以在表單層級撰寫規則，以覆寫預設處理常式。 成功和錯誤事件的伺服器回應會在表單層級公開，開發人員可使用 `$event.data` 在規則中。

執行下列步驟來編寫規則以處理成功和錯誤事件。

1. 在製作模式中開啟「最適化表單」，選取任何表單物件，然後點選 ![edit-rules1](assets/edit-rules-icon.svg) 來開啟規則編輯器。
1. 選擇 **[!UICONTROL 表單]** 在「表單對象」樹中，並點選 **[!UICONTROL 建立]**.
1. 選擇 **[!UICONTROL 已成功提交]** 或 **[!UICONTROL 提交失敗]** 從 **[!UICONTROL 選擇狀態]** 下拉式清單。
1. 定義 **[!UICONTROL 然後]** 動作。 例如，選取 **[!UICONTROL 導覽至]** 然後輸入或貼上URL。 您也可以使用 **[!UICONTROL 函式]** 標籤。

   ![提交處理常式](assets/form-submission-handler.png)

1. 點選 **[!UICONTROL 完成]** 來儲存規則。
