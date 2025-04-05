---
title: 通用編輯器 2025.03.10 發行說明
description: 以下是通用編輯器 2025.03.10 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: beab4f94dc6d78c2b1ad87a02b9fe46dd0438bcc
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 68%

---


# 通用編輯器 2025.03.10 發行說明 {#release-notes}

以下是通用編輯器 2025 年 3 月 10 日版本的發行說明。

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **移動元件：** [在容器之間移動元件](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components)現在會遵守目標容器的元件篩選器條件。
   * 要在容器之間移動元件，目標以及目的地容器不再需具有相同的[篩選器定義](/help/implementing/universal-editor/filtering.md)。
* **鎖定頁面：**&#x200B;通用編輯器服務會遵守[頁面鎖定狀態](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page)，且只會寫入未鎖定或由使用者鎖定的頁面。

## 通用編輯器的新擴充功能 {#extensions}

已在[Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)上為Universal Editor發行許多新擴充功能，以強化撰寫體驗。

* **MSM延伸模組**：您現在可以中斷元件/區塊的繼承，並使用此延伸模組將其重新例項化。
* **頁面屬性擴充功能**：使用此擴充功能，直接從Universal Editor存取頁面的頁面屬性視窗。
* **工作流程擴充功能**：在頁面上使用此擴充功能檢測的工作流程及內容片段。
* **頁面鎖定擴充功能**：使用此擴充功能直接從通用編輯器鎖定及解除鎖定頁面。

## 其他改良功能 {#other-improvements}

* 已進行相關修正，確保 Headless 畫布的驗證正確。

## 停止支援 {#deprecation}

* 應停止使用透過 npm 或 `https://unviersal-editor-service.experiencecloud.live/corslib/*` 提供的 `universal-editor-cors` 程式庫。
   * 應改用指向 `https://universal-editor-service.adobe.io/cors.js` 的指令碼標記。
   * 若要了解如何正確設置頁面，以便與通用編輯器搭配使用的詳細資訊，請參閱「[AEM 開發人員的通用編輯器概觀](/help/implementing/universal-editor/developer-overview.md)」。
   * 如果使用錯誤的方法，使用者每天會看到一則停止支援的訊息。
