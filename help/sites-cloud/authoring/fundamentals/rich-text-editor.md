---
title: 將Rich Text Editor用於作 [!DNL Adobe Experience Manager] 者內容。
description: 使用 [!DNL Experience Manager] Rich Text Editor來製作內容。
translation-type: tm+mt
source-git-commit: 5437329c55bd7da6d8b966a7f01c9e57ff1feb59
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---


# 使用Rich Text Editor來製作內容 {#use-rich-text-editor-to-author-content}

富格文本編輯器(RTE)是一個基本的構建塊，用於向其添加文本內容 [!DNL Adobe Experience Manager]。 此外，許多允許編寫的其他元件都基於RTE。 Experience Manager開發人員可自訂RTE，管理員可設定RTE供作者使用。

## 就地編輯 {#in-place-editing}

只要按一下，即可選取文字型元件，以顯示元件工 [具列](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)。

![元件工具列](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

再次按一下或以慢速按兩下方式初始選擇元件，將開啟就地編輯。 編輯模式包含工具列。 您可以編輯內容並變更基本格式。

![使用RTE就地編輯](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

通常，工具列提供下列選項：

* **格式**: 強調文字為粗體或斜體，或加上文字底線。
* **清單**: 建立項目清單或編號清單並設定縮排。
* **超連結**: 建立連結。
* **解除連結**: 移除超連結。
* **全螢幕**: 以全螢幕模式開啟編輯器。
* **關閉**: 停止編輯。
* **儲存**: 儲存變更。

## 全螢幕編輯 {#full-screen-editing}

對於基於文本的元件，按一下工具欄中的全屏模式 ![RTE全屏按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png)[](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) ，開啟富格文本編輯器並隱藏其餘的頁面內容。

全螢幕模式會顯示您可用於製作的所有已設定選項。 選項的可用性取決於配置。 <!--Full screen mode displays all the configured options that you can use for authoring. The availability of options [depends on the configuration](/help/sites-administering/rich-text-editor.md).-->

![全屏模式下的RTE](/help/sites-cloud/authoring/assets/rte-full-screen.png)

其他豐富式文字編輯器選項包括：

* **錨點**: 在文字中建立錨點，您稍後可以連結至或建立參考。
* **向左對齊文字**.
* **文字置中**.
* **向右對齊文字**.

按一下「最小化」以關閉全螢幕模式。

>[!Tip]
>
>將嵌套清單從複製 [!DNL Microsoft Word] 到RTE中可能會產生不一致的結果。 您可以改為貼上為文字，然後進行手動調整。

>[!MORELIKETHIS]
>
>* [設定豐富式文字編輯器](/help/implementing/developing/extending/rich-text-editor.md)

