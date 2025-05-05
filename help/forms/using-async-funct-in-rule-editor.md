---
title: 如何在視覺化規則編輯器中使用非同步函式呼叫？
description: 視覺化規則編輯器中的非同步函式呼叫
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: a240ba26-a6d8-4643-8acb-1d8812dac61f
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# 根據核心元件在最適化表單中使用非同步函式

最適化Forms[&#128279;](/help/forms/rule-editor-core-components.md)中的規則編輯器支援非同步功能，可讓您整合和管理需要等待外部程式或資料擷取的作業，而不會中斷使用者與表單的互動。

## 使用非同步或同步功能取決於哪些因素？

有效管理使用者互動對於建立順暢的體驗至關重要。 處理操作的兩種常見方法是同步和非同步函式。

**同步功能**&#x200B;會逐一執行工作，導致應用程式等待每個作業完成後再繼續。 這可能會導致延遲和較少參與的使用者體驗，尤其是當任務涉及等待外部資源（例如檔案上傳或資料擷取）時。

例如，假設使用者上傳影像，整個表單會暫停，等候上傳完成。 此暫停會讓使用者無法與其他欄位互動，導致挫折感和延遲。 當他們等待影像處理時，如果導覽到別處或失去耐心，所輸入的任何資訊都可能會遺失，導致體驗繁瑣且效率低下。

**非同步函式**，另一方面，允許同時執行工作。 這表示在執行背景程式時，使用者可以繼續與應用程式互動。 非同步操作可增強回應能力，讓使用者能立即收到意見回饋，並保持參與而不受干擾。

相反地，使用者可以非同步方式上傳背景影像，同時繼續無縫填寫表單的其餘部分。 介面保持回應式，允許即時更新，並可在上傳過程中即時提供意見反應。 它可提升使用者參與度，確保暢通無阻的體驗。

![非同步和同步功能](/help/forms/assets/sync-async.png){align=center}

## 為Adaptive Forms實作非同步函式

您可以在規則編輯器中使用下列規則型別，實作最適化Forms的非同步函式：

* [非同步函式呼叫](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [函式輸出](#how-to-use-function-output-rule-type)

## 如何使用非同步函式呼叫規則型別？

您可以撰寫非同步作業的[自訂函式](/help/forms/custom-function-core-component-create-function.md)，並使用規則編輯器中的&#x200B;**[!UICONTROL 非同步函式呼叫]**&#x200B;規則型別來設定非同步函式。

### 透過使用案例探索Async函式呼叫規則型別

考慮在使用者輸入一次性密碼(OTP)的網站上建立登錄檔格。 只有在輸入正確的OTP後，才會顯示新增使用者詳細資訊的面板。 如果OTP不正確，面板會保持隱藏狀態，且熒幕上會顯示錯誤訊息。

![登入表單](/help/forms/assets/rule-editor-login-form.png) {width-50%}

在登錄檔單中，當使用者按一下&#x200B;**Confirm**&#x200B;按鈕時，將會以非同步方式呼叫`matchOTP()`函式以驗證輸入的OTP。 `matchOTP()`函式已實作為[自訂函式](/help/forms/custom-function-core-component-create-function.md)。 使用規則編輯器中的&#x200B;**[!UICONTROL 非同步函式呼叫]**&#x200B;規則型別，您可以在適用性表單的規則編輯器中設定`matchOTP()`函式。 您也可以在規則編輯器中實作成功和失敗回呼。

下圖說明使用&#x200B;**[!UICONTROL 非同步函式呼叫]**&#x200B;規則型別來叫用最適化Forms非同步函式的步驟：

![新增非同步函式的工作流程](/help/forms/assets/workflow-to-add-async-func.png){width=50%, align=center}

### 1.為JS檔案中的非同步作業寫入自訂函式

>[!NOTE]
>
> * 當您選取&#x200B;**非同步函式呼叫**&#x200B;規則型別時，表單的規則編輯器只會顯示傳回型別為`Promise`的函式。
> * 若要瞭解如何建立自訂函式，請參閱標題為[根據核心元件為最適化表單建立自訂函式](/help/forms/custom-function-core-component-create-function.md)的文章。

`matchOTP()`函式已實作為自訂函式。 下列程式碼會新增至自訂函式的JS檔案中：

```JavaScript
/**
 * generates the otp for success use case
 * @param {string} otp
 * @return {PROMISE}
 */
function matchOTP(otp) {
     return new Promise((resolve, reject) => {
        // Perform some asynchronous operation here
         asyncOperationForOTPMatch(otp, (error, result) => {
            if (error) {
                // On failure, call reject(error)
                reject(error);
            } else {
                // On success, call resolve(result)
                resolve(result);
            }
        });
    });
}

/**
 * generates the otp
 */
function asyncOperationForOTPMatch(otp, callback) {
    setTimeout(() => {
        if(otp === '111') {
            callback( null, {'valid':'true'});    
        } else {
            callback( {'valid':'false'}, null);
        }
    }, 1000);
}
```

程式碼定義函式`matchOTP()`，該函式會產生Promise以非同步方式驗證一次性密碼(OTP)。 它使用函式`asyncOperationForOTPMatch()`來模擬OTP比對程式。 此函式檢查提供的OTP是否等於`111`。 如果輸入的OTP正確，它會呼叫錯誤為null的回呼，以及指示OTP有效為`({'valid':'true'})`的物件。如果OTP無效，則會呼叫結果為null且錯誤物件為`({'valid':'false'})`的回呼。

### 2.在規則編輯器中設定非同步函式

執行以下步驟，在規則編輯器中設定非同步函式：

1. [使用Async Function呼叫規則型別建立規則以使用非同步函式](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [為非同步函式實作回呼](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1建立規則以使用非同步函式呼叫規則型別來使用非同步函式

若要建立規則以使用非同步作業，請使用&#x200B;**[!UICONTROL 非同步函式呼叫]**&#x200B;規則型別，請執行下列步驟：

1. 以編寫模式開啟最適化表單，選取表單元件，然後選取&#x200B;**[!UICONTROL 規則編輯器]**&#x200B;以開啟規則編輯器。
1. 選取「**[!UICONTROL 建立]**」。
1. 在規則的&#x200B;**When**&#x200B;區段中建立條件，以點選按鈕。 例如，按一下&#x200B;**When[Confirm]**。
1. 在&#x200B;**然後**&#x200B;區段中，從&#x200B;**選取動作**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 非同步函式呼叫]**。
當您選取&#x200B;**[!UICONTROL 非同步函式呼叫]**&#x200B;時，就會顯示具有`Promise`傳回型別的函式。
1. 從清單中選取非同步函式。 例如，選取`matchOTP()`函式，其回呼會顯示為`Add success callback`和`add failure callback`。
1. 現在選取&#x200B;**[!UICONTROL 輸入]**&#x200B;繫結。 例如，選取&#x200B;**[!UICONTROL 輸入]**&#x200B;作為`Form Object`，並將其與`OTP`欄位進行比較。

底下熒幕擷圖顯示規則：

![規則型別](/help/forms/assets/asyn-function-rule-type.png)

現在，您可以繼續實作`matchOTP`函式的`Success`和`Failure`回呼。

#### 2.2為非同步函式實作回呼

使用視覺化規則編輯器為非同步函式實作成功和失敗回呼方法。

**為`Add Success callback`方法建立規則**

如果OTP符合值`111`，讓我們建立規則以顯示`userdetails`面板。

1. 按一下&#x200B;**[!UICONTROL 新增成功回呼]**。
1. 按一下&#x200B;**[!UICONTROL 新增陳述式]**&#x200B;以建立規則。
1. 在規則的&#x200B;**When**&#x200B;區段中建立條件。
1. 選取&#x200B;**[!UICONTROL 函式輸出]** > **[!UICONTROL 取得事件承載]**。

   >[!NOTE]
   >
   > **[!UICONTROL Get Event Payload]**&#x200B;函式會擷取與特定事件相關的資料，以動態管理使用者互動。

1. 從&#x200B;**Input**&#x200B;區段選取其對應的繫結。 例如，選取&#x200B;**[!UICONTROL 字串]**&#x200B;並輸入`valid`。 比較輸入的字串與`true`。
1. 在&#x200B;**然後**&#x200B;區段中，從&#x200B;**選取動作**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 顯示]**。 例如，顯示`userdetails`面板。
1. 按一下&#x200B;**[!UICONTROL 新增陳述式]**。
1. 從&#x200B;**選取動作**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 隱藏]**。 例如，隱藏`error message`文字方塊。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

![成功呼叫](/help/forms/assets/rule-editor-success-callback.png){width=50%, height=50%}

請參考下方的熒幕擷圖，其中使用者以`111`身分進入OTP，且按一下`Confirm`按鈕時就會顯示`User Details`面板。

![成功](/help/forms/assets/success.gif)

**為`Add Failure callback`方法建立規則**

讓我們建立一個規則，在OTP不符合值`111`時顯示失敗訊息。

1. 按一下&#x200B;**[!UICONTROL 新增失敗回呼]**。

1. 按一下&#x200B;**[!UICONTROL 新增陳述式]**&#x200B;以建立規則。
1. 在規則的&#x200B;**When**&#x200B;區段中建立條件。
1. 選取&#x200B;**[!UICONTROL 函式輸出]** > **[!UICONTROL 取得事件承載]**。
1. 從&#x200B;**Input**&#x200B;區段選取其對應的繫結。 例如，選取&#x200B;**[!UICONTROL 字串]**&#x200B;並輸入`valid`。 比較輸入的字串與`false`。
1. 在&#x200B;**然後**&#x200B;區段中，從&#x200B;**選取動作**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 顯示]**。 例如，顯示`error message`文字方塊。
1. 按一下&#x200B;**[!UICONTROL 新增陳述式]**。
1. 從&#x200B;**選取動作**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 隱藏]**。 例如，隱藏`userdetails`面板。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

![失敗回呼方法](/help/forms/assets/rule-editor-failure-callback.png){width=50%, height=50%}

請參考下方的熒幕擷圖，其中使用者以`123`身分進入OTP，且按一下`Confirm`按鈕時會顯示錯誤訊息。

![失敗](/help/forms/assets/failure.gif)

下面的熒幕擷圖顯示使用&#x200B;**[!UICONTROL 非同步函式呼叫]**&#x200B;實作非同步函式的完整規則：

非同步函式呼叫的![規則](/help/forms/assets/rule-editor-async-callbacks.png)

您也可以按一下&#x200B;**[!UICONTROL 編輯成功回呼]**&#x200B;和&#x200B;**[!UICONTROL 編輯失敗回呼]**&#x200B;來編輯回呼。

## 如何使用函式輸出規則型別？

您也可以使用同步函式間接呼叫非同步函式。 同步函式是使用最適化表單的規則編輯器中的&#x200B;**[!UICONTROL 函式輸出]**&#x200B;規則型別執行。

檢視下列程式碼，瞭解如何使用&#x200B;**[!UICONTROL 函式輸出]**&#x200B;規則型別來叫用非同步函式：

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

在上述範例中，asyncFunction函式是`asynchronous function`。 它透過向`https://petstore.swagger.io/v2/store/inventory`發出`GET`請求來執行非同步操作。 它會使用`await`等待回應、使用`response.json()`將回應本文剖析為JSON，然後傳回資料。 `callAsyncFunction`函式是同步自訂函式，會叫用`asyncFunction`函式並在主控台中顯示回應資料。 雖然`callAsyncFunction`函式是同步的，但它會呼叫非同步asyncFunction函式，並以`then`和`catch`陳述式處理其結果。

若要檢視其運作情況，讓我們新增按鈕，並為按鈕建立規則，此規則會在按鈕按一下時叫用非同步函式。

![為非同步函式建立規則](/help/forms/assets/rule-for-async-funct.png){width=50%}

請參考下方主控台視窗的熒幕擷圖，以示範當使用者按一下`Fetch`按鈕時，會叫用自訂函式`callAsyncFunction`，進而呼叫非同步函式`asyncFunction`。 檢查主控台視窗以檢視按鈕點選的回應：

![主控台視窗](/help/forms/assets/async-custom-funct-console.png)

## 另請參閱

{{see-also-rule-editor}}
