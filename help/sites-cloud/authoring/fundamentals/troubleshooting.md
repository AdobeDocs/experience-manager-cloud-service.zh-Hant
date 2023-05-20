---
title: 創作時AEM故障排除
description: 使用時可能遇到的一些問AEM題
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 10%

---

# 創作時AEM故障排除 {#troubleshooting-aem-when-authoring}

以下部分介紹在使用時可能遇到的一些問題AEM，以及有關如何解決這些問題的建議。

## 舊頁面版本仍位於已發佈站點上 {#old-page-version-still-on-published-site}

* **問題**:
   * 您已對頁面進行了更改並將頁面發佈到發佈站點，但 *老* 該頁面的版本仍顯示在發佈網站上。
* **原因**:
   * 這可能有幾種原因，最常是快取（本地瀏覽器或Dispatcher），但有時可能是複製隊列的問題。
* **解決方案**:
   * 這裡有各種可能：
   * 確認已正確複製該頁。 檢查頁狀態以及複製隊列的狀態（如有必要）。
   * 清除本地瀏覽器中的快取，然後再次訪問頁面。
   * 添加 `?` 到 例如：
      * `http://<host>:<port>/sites.html/content?`
      * 這將直接從Dispatcher請求AEM該頁並繞過該Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。
   * 如果複製隊列有問題，請與系統管理員聯繫。

## 工具欄上不可見的元件操作 {#component-actions-not-visible-on-toolbar}

* **問題**:
   * 在作者環境上編輯內容頁面時，所有適用的元件操作都不可見。
* **原因**:
   * 在少數情況下，先前的操作可能會影響工具欄。
* **解決方案**:
   * 刷新頁面。
