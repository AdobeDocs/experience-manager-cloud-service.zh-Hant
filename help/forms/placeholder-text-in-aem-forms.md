---
title: 中的預留位置文字 [!DNL AEM Forms]
description: 預留位置文字旨在在控制項沒有值時，協助使用者輸入資料。 可以是範例值或預期格式的簡短說明。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 中的預留位置文字 [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

佔位符文本表示一個單詞或短片語。 其目的是在控制項沒有值時，協助使用者輸入資料。 預留位置文字可以是範例值或預期格式的簡短說明。 佔位符文本在用戶輸入值之前顯示，在用戶輸入或選擇值時將刪除它。

>[!NOTE]
>
>如果指定，佔位符文本必須具有一個不包含新行字元的值。

![含有和不含預留位置文字的日期元件](assets/dat-picker-place-holder-text.png)

**答：** 含預留位置文字的日期元件 **B.** 沒有預留位置文字的日期元件

[!DNL AEM Forms] 「密碼」框、「日期選擇器」、「數值」框和文本框欄位的支援佔位符文本。\
原生HTML5日期介面工具集不支援預留位置文字。 要指定佔位符文本，請執行以下操作：

1. 以滑鼠右鍵按一下支援預留位置文字的元件，然後按一下 **編輯**. 將出現「編輯元件」(Edit component)對話框。

1. 開啟 **標題和文字** 標籤。
1. 在 **佔位符文本框**. 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>不支援預留位置文字 [!DNL Microsoft Internet Explorer 9].

