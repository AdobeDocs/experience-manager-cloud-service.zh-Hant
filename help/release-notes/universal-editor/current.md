---
title: 通用編輯器 2025.03.10 發行說明
description: 此文件為通用編輯器 2025.03.10 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b3c98f5e41dbc5e1714d0ed418a317199c735b73
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 23%

---


# 通用編輯器 2025.03.10 發行說明 {#release-notes}

這些是2025年3月10日發行的Universal Editor的發行說明。

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **移動元件：** [在容器之間移動元件](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components)現在會觀察目標容器的元件篩選。
   * 不再要求目標與目的地容器必須具備相同的[篩選器定義](/help/implementing/universal-editor/filtering.md)，才能在容器之間移動元件。
* **鎖定的頁面：** Universal Editor Service會觀察頁面](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page)的[鎖定狀態，並只寫入未鎖定或被使用者鎖定的頁面。

## 其他改善功能 {#other-improvements}

* 已進行修正以修正Headless畫布的驗證。

## 淘汰 {#deprecation}

* 不應再使用透過npm或`https://unviersal-editor-service.experiencecloud.live/corslib/*`提供的`universal-editor-cors`資料庫。
   * 應該改用指向`https://universal-editor-service.adobe.io/cors.js`的指令碼標籤。
   * 如需如何正確檢測您的頁面以與通用編輯器搭配使用的詳細資訊，請參閱[AEM開發人員的通用編輯器總覽](/help/implementing/universal-editor/developer-overview.md)。
   * 如果使用錯誤的方法，使用者每天會看到一次棄用訊息。
