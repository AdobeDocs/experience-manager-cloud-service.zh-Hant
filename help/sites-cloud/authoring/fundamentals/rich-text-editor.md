---
title: 在中使用RTF編輯器 [!DNL Adobe Experience Manager] 來製作內容。
description: 使用 [!DNL Experience Manager] RTF編輯器來編寫內容。
exl-id: 15c175f8-11de-4475-87a9-920219a4c004
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 2%

---

# 使用RTF編輯器來製作內容 {#use-rich-text-editor-to-author-content}

RTF編輯器(RTE)是新增文字內容的基本建置區塊 [!DNL Adobe Experience Manager]. 此外，許多允許編寫的其他元件都是以RTE為基礎。 Experience Manager開發人員可自訂RTE，管理員可設定RTE供作者使用。

## 就地編輯 {#in-place-editing}

只要按一下即可選取文字型元件，即可顯示 [元件工具列](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar).

![元件工具列](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

再次按一下，或最初以慢速按兩下選取元件時，就地開啟編輯。 編輯模式包含工具列。 您可以編輯內容並變更基本格式。

![使用RTE就地編輯](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

工具列通常會提供下列選項：

* **格式**:強調文字為粗體或斜體，或將文字加底線。
* **清單**:建立項目符號或編號清單並設定縮進。
* **超連結**:建立連結。
* **取消連結**:刪除超連結。
* **全螢幕**:以全螢幕模式開啟編輯器。
* **關閉**:停止編輯。
* **儲存**:儲存變更。

## 全螢幕編輯 {#full-screen-editing}

若為文字型元件，請按一下全螢幕模式 ![RTE全螢幕按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png) 從 [工具列](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 開啟RTF編輯器並隱藏其餘的頁面內容。

全螢幕模式會顯示您可用於編寫的所有已設定選項。 可用選項 [取決於設定](/help/implementing/developing/extending/rich-text-editor.md).

![全螢幕模式中的RTE](/help/sites-cloud/authoring/assets/rte-full-screen.png)

其他RTF編輯器選項包括：

* **錨點**:在文本中建立錨點，以後可以連結到或建立引用。
* **向左對齊文字**.
* **文字置中**.
* **向右對齊文字**.

按一下「最小化」以關閉全螢幕模式。

>[!TIP]
>
>從複製嵌套清單 [!DNL Microsoft Word] 輸入RTE可能會產生不一致的結果。 請改為貼上為文字，並手動調整。

>[!MORELIKETHIS]
>
>* [設定RTF編輯器](/help/implementing/developing/extending/rich-text-editor.md)

