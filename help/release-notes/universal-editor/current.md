---
title: 通用編輯器 2025.07.31 版發行說明
description: 以下是通用編輯器 2025.07.31 版的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 91799e32f363aca268a89a7eebcb5001c5295cc5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 61%

---


# 通用編輯器 2025.07.31 版發行說明 {#release-notes}

以下是通用編輯器 2025 年 7 月 31 日版的發行說明。

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* [如](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings)2025.07.09.[版所介紹，驗證標題工具列選項](/help/release-notes/universal-editor/2025/2025-07-09.md)仍會保留在功能切換之後
   * 不過現在預設為啟用。
* [RTE早期採用者的新功能](#new-rte)
   * 已新增深色模式支援。
   * 已新增文字對齊方式支援。
      * 預設為停用，僅適用於Headless專案
   * 新增縮排支援。
      * 預設為停用，僅適用於Headless專案
   * 現在會在shift+enter鍵上插入分隔符號(`<br>`)。

## 早期採用功能 {#early-adopter}

如果您有興趣測試這些即將推出的功能並分享意見回饋，請使用與您 Adobe ID 相關聯的電子郵件地址，傳送電子郵件給您的 Adobe 客戶成功經理。

### 新 RTE {#new-rte}

新的 ProseMirror RTE 在連結對話框中具備頁面選擇器，現在可以在右側面板中使用。

### 還原/取消復原 {#undo-redo}

通用編輯器內容作者現在可以進行還原和取消復原。

* 其中包括在內容中完成的編輯、透過屬性面板完成的編輯，以及新增 (或複製)、移動和刪除區塊。
* 還原和取消復原僅限於目前瀏覽器工作階段。

## 其他改良功能 {#other-improvements}

* 早期採用者RTE的修正
   * 按下Enter鍵現在會在清單中建立新的清單專案(`<li>`)。
* 使用遠端DAM時，視訊現在會正確更新。
* 為6.5 LTS新增服務支援。

## 棄用 {#deprecations}

* `text-input`和`text-area`元件已正式棄用[版本2025.07.09。](/help/release-notes/universal-editor/2025/2025-07-09.md)
   * 在 `model-definition.json` 中，使用文字元件可建立「屬性」面板的文字輸入。
