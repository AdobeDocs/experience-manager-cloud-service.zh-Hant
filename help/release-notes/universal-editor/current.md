---
title: 通用編輯器 2025.09.04 版發行說明
description: 以下是通用編輯器 2025.09.04 版的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 0c380e0faca1db0966d22d056dd1f824a731a7bc
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 78%

---


# 通用編輯器 2025.09.04 版發行說明 {#release-notes}

此為通用編輯器 2025 年 9 月 4 日版本的發行說明。

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* [早期採用者](#copy-paste)可以複製並貼上

### 還原/取消復原 {#undo-redo}

通用編輯器內容作者現在可以進行還原和取消復原。

* 其中包括在內容中完成的編輯、透過屬性面板完成的編輯，以及新增 (或複製)、移動和刪除區塊。
* 還原和取消復原僅限於目前瀏覽器工作階段。

## 早期採用功能 {#early-adopter}

如果您有興趣測試這些即將推出的功能並分享意見回饋，請使用與您 Adobe ID 相關聯的電子郵件地址，傳送電子郵件給您的 Adobe 客戶成功經理。

### 新 RTE {#new-rte}

新的 ProseMirror RTE 在連結對話框中具備頁面選擇器，現在可以在右側面板中使用。

### 複製/貼上 {#copy-paste}

內容作者現在可以在相同頁面內複製和貼上元件。

## 其他改良功能 {#other-improvements}

* 編輯器工具列的樣式已更新，以更符合即將推出的新RTE。
* 資產選擇器對話方塊中的篩選器已還原。

## 棄用 {#deprecations}

* [版本 2025.07.09](/help/release-notes/universal-editor/2025/2025-07-09.md) 正式棄用 `text-input` 和 `text-area` 元件。
   * 在 `model-definition.json` 中，使用文字元件來建立「屬性」面板的文字輸入。
