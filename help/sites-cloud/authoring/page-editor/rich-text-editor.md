---
title: 在 [!DNL Adobe Experience Manager] 中使用RTF編輯器來編寫內容。
description: 使用 [!DNL Experience Manager] RTF編輯器來編寫內容。
exl-id: 15c175f8-11de-4475-87a9-920219a4c004
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 使用RTF編輯器創作內容 {#use-rich-text-editor-to-author-content}

RTF編輯器(RTE)是新增文字內容至[!DNL Adobe Experience Manager]的基本建置區塊。 此外，許多允許編寫的其他元件也是以RTE為基礎。 Experience Manager開發人員可以自訂RTE，管理員則可以設定RTE以供作者使用。

## 就地編輯 {#in-place-editing}

按一下選取文字型元件以顯示[元件工具列](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)。

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

對於文字型元件，請從[工具列](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)按一下全熒幕模式![RTE全熒幕按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png)以開啟RTF編輯器，並隱藏頁面內容的其餘部分。

全熒幕模式會顯示所有可用於編寫的已設定選項。 選項[的可用性取決於組態](/help/implementing/developing/extending/rich-text-editor.md)。

全熒幕模式中的![RTE](/help/sites-cloud/authoring/assets/rte-full-screen.png)

其他RTF編輯器選項包括：

* **錨點**：在文字中建立錨點，以便稍後連結或建立參照。
* **文字靠左對齊**。
* **文字置中**。
* **文字靠右對齊**。

按一下「最小化」以關閉全熒幕模式。

>[!TIP]
>
>將巢狀清單從[!DNL Microsoft Word]複製到RTE可能會產生不一致的結果。 請改為貼上文字並進行手動調整。

>[!MORELIKETHIS]
>
>* [設定RTF編輯器](/help/implementing/developing/extending/rich-text-editor.md)
