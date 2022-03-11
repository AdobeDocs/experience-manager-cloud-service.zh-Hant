---
title: '佔位符文本 [!DNL AEM Forms] '
description: 佔位符文本用於在控制項沒有值時幫助用戶輸入資料。 它可以是示例值或預期格式的簡短說明。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 佔位符文本 [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

佔位符文本表示一個詞或短詞。 當控制項沒有值時，它旨在幫助用戶輸入資料。 佔位符文本可以是示例值或預期格式的簡短說明。 佔位符文本在用戶輸入值之前顯示，當用戶輸入或選擇值時，佔位符文本將被刪除。

>[!NOTE]
>
>如果指定，佔位符文本必須具有不包含新行字元的值。

![包含和不包含佔位符文本的日期元件](assets/dat-picker-place-holder-text.png)

**答：** 包含佔位符文本的日期元件 **B** 沒有佔位符文本的日期元件

[!DNL AEM Forms] 支援「密碼」框、「日期選取器」、「數字」框和文本框欄位的佔位符文本。\
本機HTML5日期小部件不支援佔位符文本。 要指定佔位符文本：

1. 按一下右鍵支援佔位符文本的元件，然後按一下 **編輯**。 將出現「編輯元件」(Edit component)對話框。

1. 開啟 **標題和文本** 頁籤。
1. 在 **佔位符文本框**。 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>上不支援佔位符文本 [!DNL Microsoft Internet Explorer 9]。

