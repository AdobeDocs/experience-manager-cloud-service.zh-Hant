---
title: 通用編輯器 2054.01.16 發行說明
description: 此文件為通用編輯器 2025.01.16 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 77%

---


# 通用編輯器 2025.01.16 發行說明 {#release-notes}

此為通用編輯器 2025 年 1 月 16 日版本的發行說明。

>[!TIP]
>
>如需Adobe Experience Manager as a Cloud Service目前的發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **停止支援 3.0.0** 以前版本的 CORS 資料庫 - 為了確保未來的相容性並增強安全性，通用編輯器現在專門支援 3.0.0 或更高版本
  `@Adobe Express/universal-editor-cors`。
   * 程式庫現在僅透過[`universal-editor-service.adobe.io/cors.js`](http://universal-editor-service.adobe.io/cors.js)傳遞。
   * 當使用者開啟使用舊版 CORS 資料庫的頁面時，系統會出現停止支援通知並提示更新。
* **登陸頁面的擴充功能點** - [新的擴充功能點](/help/implementing/universal-editor/customizing.md#extending)已經為了擴功能而採用，並且顯示在通用編輯器登入頁面的側邊欄中。
   * 現在，開發人員可以明確指出擴充功能是否適用於編輯器、登陸頁面或兩者，以便提供更佳自訂性和可用性。

## 其他改善功能 {#other-improvements}

* **修正登陸頁面上「最近」專案中的無效URL** — 已解決在Universal Editor登陸頁面上「最近」清單中顯示的URL損毀的問題。
* **Unified Shell 中的主題同步** - 通用編輯器現在可將主題與系統的 Unified Shell 設定為動態同步，並在淺色和深色模式之間自動調整。
   * 這樣可確保微前端 (包括片段和資產選擇器) 具有一致的視覺外觀。
