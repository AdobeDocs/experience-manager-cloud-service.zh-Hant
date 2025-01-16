---
title: 通用編輯器 2054.01.16 發行說明
description: 此文件為通用編輯器 2025.01.16 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 14bc45917f56ecf358278848e7e830afb1fedccd
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 19%

---


# 通用編輯器 2025.01.16 發行說明 {#release-notes}

這些是2025年1月16日發行的Universal Editor的發行說明。

>[!TIP]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **棄用CORS程式庫&lt; 3.0.0** — 為了確保未來的相容性並增強安全性，通用編輯器現在僅支援3.0.0版或更新版本的
  `@Adobe Express/universal-editor-cors`資料庫。
   * 程式庫現在僅透過[`universal-editor-service.adobe.io/cors.js`.](http://universal-editor-service.adobe.io/cors.js)傳遞
   * 使用者開啟使用舊版CORS程式庫的頁面時，系統會顯示淘汰通知，提示使用者更新。
* **登陸頁面的擴充點** - [已引入新的擴充點](/help/implementing/universal-editor/customizing.md#extending)，擴充功能會顯示在Universal Editor登陸頁面的側邊欄中。
   * 現在，開發人員可指定擴充功能是否適用於編輯器、登陸頁面或兩者，以提供更優異的自訂和可用性。

## 其他改良功能 {#other-improvements}

* **修正登陸頁面上「最近」專案中的無效URL** — 已解決在Universal Editor登陸頁面上「最近」清單中顯示的URL損毀的問題。
* **Unified Shell中的佈景主題同步處理** — 通用編輯器現在會動態同步處理佈景主題與系統的Unified Shell設定，並自動在明暗模式之間進行調整。
   * 這可確保跨微前端（包括片段和資產選擇器）的一致視覺外觀。
