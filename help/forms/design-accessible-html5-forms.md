---
title: 設計無障礙的HTML5表單
description: HTML5表單使用ARIA HTML5協助工具標準。 這些表單支援標籤式導覽，並經過認證與常用熒幕閱讀器相容。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 設計無障礙的HTML5表單 {#designing-accessible-html-forms}

<span class="preview"> HTML5 Forms功能屬於Early Access方案的一部分。 若要要求存取權，請將您的正式（工作）電子郵件ID傳送電子郵件至aem-forms-ea@adobe.com。
</span>

HTML5表單使用ARIA HTML5協助工具標準來產生無障礙的HTML表單。 這些表單支援標籤式導覽（Mozilla FireFox除外），且經認證與一般熒幕閱讀器相容。 若要產生具備良好協助工具功能的HTML5表單，請根據一些基本設計准則來設計XFA表單範本。 設計准則包括設定正確的標籤順序，並為每個表單控制項提供「說文字」內容。 AEM Forms Designer支援這些表單控制項屬性的設定，以產生可存取的PDF和HTML5表單。

*注意：索引標籤導覽未涵蓋受保護欄位，例如顯示值總和的計算欄位。 若要讓熒幕助讀程式讀取受保護欄位的值，請在受保護欄位的頂端或旁邊，放置空白的唯讀欄位。 將受保護欄位的值指派給新的唯讀欄位。 熒幕助讀程式或索引標籤導覽可以挑選此唯讀欄位，並將其朗讀為受保護欄位的值。*

AEM Forms Designer包含數個可傳遞給熒幕助讀程式的說話文字選項。 對於表單中的每個物件，使用者可以為熒幕助讀程式文字指定下列其中一個設定：

* 自訂熒幕助讀程式文字，可使用「協助工具」浮動視窗進行設定。 作者可以標註按鈕和欄位的名稱及其用途。
* 工具提示，可在「協助工具」浮動視窗中設定。
* 表單上欄位的標題。
* 物件的名稱，如「繫結」標籤的「名稱」選項中所指定。

![協助工具](assets/accessibility.png)

當表單控制項上有工具提示、熒幕Reader文字和標題等多個選項可用時，熒幕Reader只會使用其中一個屬性。 預設順序為「自訂熒幕Reader文字」、「工具提示」、「標題」和「名稱」。 您可以使用協助工具浮動視窗中的熒幕Reader **優先順序**&#x200B;選項來覆寫預設順序。
