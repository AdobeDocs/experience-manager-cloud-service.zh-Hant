---
title: 如何設定最適化Forms的非同步提交？
description: 瞭解如何設定Adaptive Forms的非同步提交。 深入瞭解非同步提交如何適用於Adaptive Forms。
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

傳統上，網路表單會設定為同步提交。 在同步提交中，當使用者提交表單時，系統會將他們重新導向至認可頁面、感謝頁面，或在提交失敗的情況下重新導向至錯誤頁面。 不過，單頁應用程式等現代網頁體驗越來越熱門，這是因為網頁在背景執行使用者端與伺服器互動時，網頁會維持靜態。 您可以設定非同步提交，透過Adaptive Forms提供此體驗。

在非同步提交中，當使用者提交表單時，表單開發人員會插入個別體驗，例如重新導向到其他表單或網站的個別區段。 作者也可以外掛程式個別服務（例如傳送資料至不同的資料存放區），或新增自訂分析引擎。 在非同步提交的情況下，最適化表單的行為就像單頁應用程式，因為提交表單資料在伺服器上驗證時，表單不會重新載入或其URL不會變更。

請閱讀下文，瞭解最適化Forms中非同步提交的詳細資訊。

## 設定非同步提交 {#configure}

若要設定最適化表單的非同步提交：

1. 在調適型表單製作模式中，選取「表單容器」物件並點選 ![cmppr1](assets/configure-icon.svg) 以開啟其屬性。
1. 在 **[!UICONTROL 提交]** 屬性區段，啟用 **[!UICONTROL 使用非同步提交]**.
1. 在 **[!UICONTROL 提交時]** 區段，選取下列其中一個選項以在成功提交表單時執行。

   * **[!UICONTROL 重新導向至URL]**：在提交表單時重新導向至指定的URL或頁面。 您可以指定URL或瀏覽來選擇 **[!UICONTROL 重新導向URL/路徑]** 欄位。
   * **[!UICONTROL 顯示訊息]**：在表單提交上顯示訊息。 您可以在下方的文字欄位中撰寫訊息 **[!UICONTROL 顯示訊息]** 選項。 文字欄位支援RTF格式設定。

1. 點選 ![check-button1](assets/save_icon.svg) 以儲存屬性。

## 非同步提交如何運作 {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] 為表單提交提供現成可用的成功和錯誤處理常式。 處理常式是根據伺服器回應執行的使用者端功能。 提交表單時，資料會傳輸到伺服器進行驗證，伺服器會傳回回應給使用者端，其中包含提交成功或錯誤事件的相關資訊。 此資訊會以引數形式傳遞至相關處理常式，以執行函式。

此外，表單作者和開發人員可以在表單層級撰寫規則來覆寫預設處理常式。 如需詳細資訊，請參閱 [使用規則覆寫預設處理常式](#custom).

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

成功提交表單時的伺服器回應包括：

* 表單資料格式型別： XML或JSON
* XML或JSON格式的表單資料
* 選取此選項以重新導向至頁面，或依據表單的設定顯示訊息
* 頁面URL或訊息內容，如表單中所設定

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

* 錯誤原因、驗證碼或伺服器端驗證失敗
* 錯誤物件清單，其中包括驗證失敗的欄位的SOM運算式以及對應的錯誤訊息

錯誤處理常式會讀取伺服器回應，並在表單上顯示錯誤訊息。

## 使用規則覆寫預設處理常式 {#custom}

表單開發人員和作者可以在表單層級撰寫規則以覆寫預設處理常式。 成功和錯誤事件的伺服器回應會公開於表單層級，開發人員可透過此層級存取： `$event.data` 在規則中。

執行以下步驟來撰寫規則以處理成功和錯誤事件。

1. 在撰寫模式下開啟最適化表單，選取任何表單物件，然後點選 ![edit-rules1](assets/edit-rules-icon.svg) 以開啟規則編輯器。
1. 選取 **[!UICONTROL 表單]** 在「表單物件」樹狀結構中，點選 **[!UICONTROL 建立]**.
1. 選擇 **[!UICONTROL 已成功提交]** 或 **[!UICONTROL 提交失敗]** 從 **[!UICONTROL 選取狀態]** 下拉式清單。
1. 定義 **[!UICONTROL 則]** 所選狀態的動作。 例如，選取 **[!UICONTROL 導覽至]** 然後輸入或貼上URL。 您也可以使用拖曳任何函式 **[!UICONTROL 函式]** 標籤移至規則。

   ![提交處理常式成功](assets/form-submission-handler.png)

1. 點選 **[!UICONTROL 完成]** 以儲存規則。
