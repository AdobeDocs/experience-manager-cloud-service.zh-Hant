---
title: 從試算表到表單 - 掌握 Form 區塊欄位驗證
description: 使用試算表和 Form 區塊欄位更快地製作強大的表單！本指南可協助您為 EDS Forms 區塊欄位建立自訂驗證。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 24%

---


# 新增驗證至表單欄位

表單區塊內建驗證功能。 這些驗證會根據您選擇的欄位型別和其他屬性，自動套用至現代瀏覽器。

## 瞭解欄位型別與驗證

Form區塊支援各種功能 [HTML5輸入型別](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)，包括文字、電子郵件、數字、日期等。 也可隨附 [文字區域](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)、 select和fieldset，以及HTML-5固有的完整輸入驗證功能。

使用HTML欄位型別來定義使用者可輸入的資料型別。 不同的欄位型別有不同的內建驗證規則：

電子郵件：此欄位型別會自動根據通用電子郵件地址格式驗證使用者輸入。 使用者輸入無效的電子郵件時，將會看到錯誤訊息。
數字：此欄位型別僅允許數字輸入。 輸入非數字字元的使用者將會收到錯誤。
日期：此欄位型別會根據標準日期格式驗證使用者輸入。 超出合理範圍的日期也可能被標籤為無效。
URL：此欄位型別會根據有效的URL格式驗證使用者輸入。 輸入無效URL的使用者會看到錯誤訊息。
電話：此欄位型別是專為電話號碼所設計，可能會根據特定國家/地區格式（並非普遍支援）觸發驗證。


## 了解更多

* [建立並預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單來傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈到網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [改變主題和樣式風格](/help/edge/docs/forms/style-theme-forms.md)