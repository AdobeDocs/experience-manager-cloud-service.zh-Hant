---
title: 在中使用富格文本編輯器 [!DNL Adobe Experience Manager] 建立內容。
description: 使用 [!DNL Experience Manager] 富格文本編輯器，用於編寫內容。
exl-id: 15c175f8-11de-4475-87a9-920219a4c004
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 2%

---

# 使用富格文本編輯器創作內容 {#use-rich-text-editor-to-author-content}

富格文本編輯器(RTE)是向中添加文本內容的基本構造塊 [!DNL Adobe Experience Manager]。 另外，許多允許創作的其他元件都基於RTE。 Experience Manager開發人員可以自定義RTE，管理員可以配置RTE供作者使用。

## 就地編輯 {#in-place-editing}

按一下選取基於文本的元件以顯示 [元件工具欄](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)。

![元件工具欄](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

再次按一下或初始選擇元件時按兩下速度較慢，則開啟就地編輯。 編輯模式包含工具欄。 您可以編輯內容並進行基本格式更改。

![使用RTE就地編輯](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

通常，工具欄提供以下選項：

* **格式**:將文本強調為粗體或斜體或加下划線。
* **清單**:建立項目符號清單或編號清單並設定縮進。
* **超連結**:建立連結。
* **取消連結**:刪除超連結。
* **全屏**:以全屏模式開啟編輯器。
* **關閉**:停止編輯。
* **保存**:保存更改。

## 全屏編輯 {#full-screen-editing}

對於基於文本的元件，按一下全屏模式 ![RTE全屏按鈕](/help/sites-cloud/authoring/assets/editing-full-screen.png) 從 [工具欄](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) 開啟富格文本編輯器並隱藏其餘頁面內容。

全屏模式顯示可用於創作的所有已配置選項。 選項的可用性 [取決於配置](/help/implementing/developing/extending/rich-text-editor.md)。

![全屏模式下的RTE](/help/sites-cloud/authoring/assets/rte-full-screen.png)

更多的富格文本編輯器選項包括：

* **錨點**:在文本中建立一個錨點，以後可以連結到或建立引用。
* **向左對齊文字**.
* **文字置中**.
* **向右對齊文字**.

按一下「最小化」關閉全屏模式。

>[!TIP]
>
>從複製嵌套清單 [!DNL Microsoft Word] 在RTE中會產生不一致的結果。 而應貼上為文本並進行手動調整。

>[!MORELIKETHIS]
>
>* [配置富格文本編輯器](/help/implementing/developing/extending/rich-text-editor.md)

