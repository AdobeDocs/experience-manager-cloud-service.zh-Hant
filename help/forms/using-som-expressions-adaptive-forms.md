---
title: SOM表達式在自適應Forms中的應用
seo-title: Using SOM expressions in Adaptive Forms
description: 瞭解如何提取自適應表單面板的SOM表達式。
seo-description: Learn how to extract SOM expressions of a panel of an Adaptive Form.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# SOM表達式在自適應Forms中的應用{#using-som-expressions-in-adaptive-forms}

自適應Forms被建模AEM為Page，表示為JCR內容結AEM構。 內容結構的關鍵元素是guideContainer節點。 在guideContainer下，可以有rootPanel，它可以包含嵌套的面板和欄位。

可以使用指令碼對象模型(SOM)來引用特定文檔對象模型(DOM)中的值、屬性和方法。 DOM在樹層次結構中組織記憶體對象和屬性。 SOM表達式引用「欄位」/「繪圖」元素和面板。

下圖描述了在向表單添加元件時，自適應表單將轉換為的節點結構。 例如，您可以向根面板添加一個面板，並在面板中添加一個單選按鈕，該按鈕在運行時轉換為DOM。 「自適應表單」中單選按鈕欄位的SOM表達式指定為 `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`。

![DOM樹](assets/hierarchy.png)

DOM樹

自適應表單中任何元素的SOM表達式的前置詞為 `guide[0].guide1[0]`。 元件在節點結構層次中的位置用於導出其SOM表達式。

![具有兩個單選按鈕的DOM樹](assets/hierarchy_radio_button.png)

具有兩個單選按鈕的DOM樹

當您更改自適應表單中單選按鈕的位置時，SOM表達式會發生更改。 在創作模式中，可以查看域或元素的SOM表達式 [!DNL AEM Forms] 使用「查看SOM表達式」選項。 該選項出現在面板上，並在按一下右鍵該欄位或元素時顯示。

![自適應形式的SOM表達式提取](assets/som-expressions.png)

自適應形式的SOM表達式提取

在面板中，可從面板工具欄訪問該特徵。 該功能便於Adaptive Form作者編寫指令碼。

![使用面板工具欄提取SOM表達式](assets/som-expression.png)

使用面板工具欄提取SOM表達式

中列出的某些API [導橋](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 使用元素的SOM表達式。 例如，要將焦點引入「自適應表單」中的特定欄位，請將相應的SOM表達式傳遞到 `getFocus`API在 `guideBridge`。
