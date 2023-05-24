---
title: 使用RTF編輯器 [!DNL Adobe Experience Manager] 以創作內容。
description: 使用 [!DNL Experience Manager] 使用RTF編輯器創作內容。
exl-id: 15c175f8-11de-4475-87a9-920219a4c004
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 2%

---

# 使用RTF編輯器來編寫內容 {#use-rich-text-editor-to-author-content}

RTF編輯器(RTE)是新增文字內容的基本建置區塊 [!DNL Adobe Experience Manager]. 此外，許多允許編寫的其他元件也是以RTE為基礎。 Experience Manager開發人員可以自訂RTE，管理員也可以設定RTE以供作者使用。

## 就地編輯 {#in-place-editing}

按一下即可選取文字元件，以顯示 [元件工具列](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar).

![元件工具列](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

再次按一下或最初以緩慢連按兩下方式選取元件，會開啟就地編輯。 編輯模式包含工具列。 您可以編輯內容並進行基本格式變更。

![使用RTE就地編輯](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

通常，工具列會提供下列選項：

* **格式**：以粗體或斜體強調文字，或為文字加上底線。
* **清單**：建立專案符號或編號清單並設定縮排。
* **超連結**：建立連結。
* **取消連結**：移除超連結。
* **全熒幕**：以全熒幕模式開啟編輯器。
* **關閉**：停止編輯。
* **儲存**：儲存變更。

## 全熒幕編輯 {#full-screen-editing}

如果是文字元件，請按一下全熒幕模式 ![RTE全熒幕按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png) 從 [工具列](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 以開啟RTF編輯器並隱藏頁面內容的其餘部分。

全熒幕模式會顯示您可用來編寫的所有已設定選項。 選項可用性 [取決於設定](/help/implementing/developing/extending/rich-text-editor.md).

![全熒幕模式的RTE](/help/sites-cloud/authoring/assets/rte-full-screen.png)

其他RTF編輯器選項包括：

* **錨點**：在文字中建立可在稍後連結或參照的錨點。
* **向左對齊文字**.
* **文字置中**.
* **向右對齊文字**.

按一下「最小化」以關閉全熒幕模式。

>[!TIP]
>
>複製巢狀清單來源 [!DNL Microsoft Word] 到RTE中可能會產生不一致的結果。 請改為貼上成文字，然後手動調整。

>[!MORELIKETHIS]
>
>* [設定RTF編輯器](/help/implementing/developing/extending/rich-text-editor.md)

