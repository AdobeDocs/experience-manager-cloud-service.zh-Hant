---
title: Markdown
description: 瞭解內容片段編輯器如何使用Markdown語法，輕鬆建立頁面製作和Headless傳送的內容。
feature: Content Fragments
role: User
exl-id: 6fbf8128-3b7f-4eda-bbbd-3336578d2586
solution: Experience Manager Sites
source-git-commit: 278242e0be1da5c64abfa5d9ac174013688ff422
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 4%

---

# Markdown {#markdown}

當您[製作](/help/sites-cloud/administering/content-fragments/authoring.md#edit-multi-line-text-fields-plaintext-markdown)內容片段時，您可能會有[多行文字欄位](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)以&#x200B;**Markdown**&#x200B;的&#x200B;**預設型別**&#x200B;定義。 內容片段編輯器使用&#x200B;*Markdown*&#x200B;語法，可讓您輕鬆編寫頁面編寫和Headless傳送的內容：

編輯器中的![Markdown多行文字欄位](/help/sites-cloud/administering/content-fragments/assets/cf-markdown-field-edit.png)

您可以定義：

* [標題標籤法](/help/sites-cloud/administering/content-fragments/markdown.md#heading-notation)
* [段落和分行符號](/help/sites-cloud/administering/content-fragments/markdown.md#paragraphs-and-line-breaks)
* [連結](/help/sites-cloud/administering/content-fragments/markdown.md#links)
* [影像](/help/sites-cloud/administering/content-fragments/markdown.md#images)
* [區塊引號](/help/sites-cloud/administering/content-fragments/markdown.md#block-quotes)
* [清單](/help/sites-cloud/administering/content-fragments/markdown.md#lists)
* [強調](/help/sites-cloud/administering/content-fragments/markdown.md#emphasis)
* [程式碼片段](/help/sites-cloud/administering/content-fragments/markdown.md#code-blocks)
* [反斜線逸出](/help/sites-cloud/administering/content-fragments/markdown.md#backslash-escapes)

## 標題標籤法 {#heading-notation}

若要建立標題，請在標題前面放置雜湊標籤(#)。 一個雜湊標籤(#)表示H1，兩個雜湊標籤(##)表示H2，以此類推。 您最多可以使用6個雜湊標籤。 例如：

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

或者，您可以等號加底線來建立H1，減號加底線來建立H2。 例如：

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落和分行符號 {#paragraphs-and-line-breaks}

段落只是一行或多行連續的文字，以一行或多行空白行分隔。 空白行是隻包含空格或定位字元的行。 不應以空格或定位點縮排一般段落。

換行符號的建立方式，是先以兩個或多個空格結束一行，然後再返回一行。

## 連結 {#links}

您可以建立內嵌和參照連結。

在這兩種樣式中，連結文字會以方括弧`[]`分隔。

以下是內嵌連結的範例：

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example (non-standard) of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

參照連結的語法如下：

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 影像 {#images}

影像的語法與連結類似。 您可以建立內嵌和參照的影像。

例如，內嵌影像的語法如下：

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

語法包括：

* 驚歎號：！；
* 後面接著一組方括弧，其中包含影像的alt屬性文字；
* 後面接著一組括弧（包含影像的URL或路徑），以及一個以雙引號或單引號括起來的選用標題屬性。

參照樣式影像的語法如下：

    `![Alt text][id]`

其中「id」是定義的影像參考的名稱。 影像參照是使用與連結參照相同的語法來定義：

    `[id]: url/to/image "Optional title attribute"`

## 區塊引號 {#block-quotes}

您可以在文字前新增>符號來引用文字。 例如：

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

您可以有巢狀區塊引號。 例如：

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## 清單 {#lists}

您可以建立已排序和未排序清單。

若要建立未排序清單，請在清單中的專案前使用&amp;amp；ast；符號。 例如：

    `* item in list`

    `* item in list`

    `* item in list`

若要建立有序清單，請在清單中的每個專案前新增數字，然後加上句點。 例如：

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 強調 {#emphasis}

您可以新增斜體或粗體樣式至文字。

您可以新增斜體，如下所示：

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

您可以依照下列方式顯示粗體文字：

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

若要指出程式碼範圍，請以反勾號(&amp;amp；grave；)將程式碼換行。 和預先格式化的程式碼區塊不同，程式碼範圍表示一般段落中的程式碼。

例如：

    ``Use the `printf()` function.``

## 程式碼片段 {#code-blocks}

程式碼區塊通常用於說明原始程式碼。 您可以使用索引標籤縮排程式碼，或最少4個空格來建立程式碼區塊。 例如：

    `This is a normal paragraph.`

        `This is a code block.`

## 反斜線逸出 {#backslash-escapes}

您可以使用反斜線逸出產生在格式語法中也具有特殊意義的常值字元。 例如，如果您想以星號括住單字(而非HTML &lt;em>標籤)，可以在星號前使用反斜線，如下所示：

    `\\*literal asterisks\\*`

反斜線逸出適用於下列字元：

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
