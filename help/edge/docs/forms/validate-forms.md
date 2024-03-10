---
title: 從試算表到Forms — 掌握最適化Forms區塊欄位驗證
description: 使用試算表及最適化Forms區塊欄位，更快製作強大的表單！ 本指南可協助您為 EDS Forms 區塊欄位建立自訂驗證。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 80%

---

# 新增驗證至表單欄位

最適化Forms區塊有內建驗證功能。 這些驗證功能會根據所選欄位類型和您提供的其他屬性自動套用在現代瀏覽器中。

## 了解欄位類型和驗證

最適化Forms區塊支援多種方式 [HTML5輸入型別](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)，包括文字、電子郵件、數字、日期等。 它還容納 [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)、select 和 fieldset，以及 HTML-5 固有的全面輸入驗證功能。

使用 HTML 欄位類型來定義使用者可以輸入的資料類型。不同的欄位類型有不同的內建驗證規則：

電子郵件：此欄位類型會自動根據常見電子郵件地址格式驗證使用者輸入。輸入無效電子郵件的使用者將看到錯誤訊息。
數字：此欄位類型僅允許輸入數字。輸入非數字字元的使用者將收到錯誤訊息。
日期：此欄位類型根據標準日期格式驗證使用者輸入。超出合理範圍的日期也可能被標記為無效。
URL：此欄位類型根據有效的 URL 格式驗證使用者輸入。輸入無效 URL 的使用者將看到錯誤訊息。
電話：此欄位類型專為電話號碼而設計，可能會觸發系統根據特定國家/地區格式進行驗證 (未受到普遍支援)。



