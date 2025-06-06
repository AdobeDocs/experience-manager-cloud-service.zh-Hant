---
title: 如何設定AEM Adaptive Forms的非同步提交？
description: 瞭解如何設定最適化Forms的非同步提交。 深入瞭解非同步提交如何適用於Adaptive Forms。
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 3%

---

# 設定AEM Adaptive Forms的非同步提交 {#asynchronous-submission-of-adaptive-forms}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/asynchronous-submissions-adaptive-forms.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |


傳統上，網路表單會設定為同步提交。 在同步提交中，當使用者提交表單時，系統會將他們重新導向至認可頁面、感謝頁面，或在提交失敗的情況下重新導向至錯誤頁面。 不過，單頁應用程式等現代網頁體驗越來越受歡迎，這是因為網頁會維持靜態，而使用者端與伺服器之間的互動會在背景進行。 您可以設定非同步提交，透過Adaptive Forms提供此體驗。

在非同步提交中，當使用者提交表單時，表單開發人員會插入單獨的體驗，例如重新導向到其他表單或網站的單獨區段。 作者也可以外掛個別的服務，例如傳送資料至不同的資料存放區，或新增自訂分析引擎。 在非同步提交的情況下，最適化表單的行為就像單頁應用程式，因為當在伺服器上驗證提交的表單資料時，表單不會重新載入或其URL不會變更。

請閱讀下文，瞭解最適化Forms中非同步提交的詳細資訊。

## 設定非同步提交 {#configure}

若要設定最適化表單的非同步提交：

1. 在調適型表單編寫模式中，選取表單容器物件，然後選取![cmppr1](assets/configure-icon.svg)以開啟其屬性。
1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;屬性區段中，啟用&#x200B;**[!UICONTROL 使用非同步提交]**。
1. 在&#x200B;**[!UICONTROL 於提交]**&#x200B;區段中，選取下列其中一個選項以在成功提交表單時執行。

   * **[!UICONTROL 重新導向至URL]**：在提交表單時，重新導向至指定的URL或頁面。 您可以指定URL或瀏覽，以在&#x200B;**[!UICONTROL 重新導向URL/路徑]**&#x200B;欄位中選擇頁面的路徑。
   * **[!UICONTROL 顯示訊息]**：在提交表單時顯示訊息。 您可以在&#x200B;**[!UICONTROL 顯示訊息]**&#x200B;選項下方的文字欄位中撰寫訊息。 文字欄位支援RTF格式。

1. 選取![check-button1](assets/save_icon.svg)以儲存屬性。

## 非同步提交的運作方式 {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms]為表單提交提供現成可用的成功和錯誤處理常式。 處理常式是根據伺服器回應執行的用戶端函數。提交表單時，資料會傳送至伺服器進行驗證，伺服器會傳回回應給使用者端，其中包含提交成功或錯誤事件的相關資訊。 此資訊會以引數形式傳遞至相關處理常式，以執行函式。

此外，表單作者和開發人員可在表單層級撰寫規則以覆寫預設處理常式。 如需詳細資訊，請參閱[使用規則](#custom)覆寫預設處理常式。

讓我們先檢閱伺服器回應，以瞭解成功和錯誤事件。

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

如果表單提交成功，伺服器回應會包括：

* 表單資料格式型別： XML或JSON
* XML或JSON格式的表單資料
* 選取此選項以重新導向至頁面，或依據表單的設定顯示訊息
* 頁面URL或訊息內容（如表單中所設定）

成功處理常式會讀取伺服器回應，並據以重新導向至設定的頁面URL或顯示訊息。

### 提交錯誤事件的伺服器回應 {#server-response-for-submission-error-event}

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

表單提交中發生錯誤時的伺服器回應包括：

* 錯誤的原因，驗證碼或伺服器端驗證失敗
* 錯誤物件清單，包括驗證失敗的欄位的SOM運算式和對應的錯誤訊息

錯誤處理常式會讀取伺服器回應，並在表單上顯示錯誤訊息。

## 使用規則覆寫預設處理常式 {#custom}

表單開發人員和作者可以在表單層級撰寫規則以覆寫預設處理常式。 成功和錯誤事件的伺服器回應會公開於表單層級，開發人員可在規則中使用`$event.data`進行存取。

執行以下步驟來撰寫規則以處理成功和錯誤事件。

1. 以編寫模式開啟最適化表單，選取任何表單物件，然後選取![edit-rules1](assets/edit-rules-icon.svg)以開啟規則編輯器。
1. 在表單物件樹狀結構中選取&#x200B;**[!UICONTROL 表單]**，然後選取&#x200B;**[!UICONTROL 建立]**。
1. 從&#x200B;**[!UICONTROL 選取狀態]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL 提交成功]**&#x200B;或&#x200B;**[!UICONTROL 提交失敗]**。
1. 為選取的狀態定義&#x200B;**[!UICONTROL Then]**&#x200B;動作。 例如，選取&#x200B;**[!UICONTROL 瀏覽至]**，然後輸入或貼上URL。 您也可以使用&#x200B;**[!UICONTROL 函式]**&#x200B;索引標籤將任何函式拖曳至規則。

   ![成功的提交處理常式](assets/form-submission-handler.png)

1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存規則。