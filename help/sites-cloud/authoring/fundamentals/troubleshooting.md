---
title: 製作時疑難排解AEM
description: 使用AEM時可能會遇到的一些問題
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 10%

---

# 編寫{#troubleshooting-aem-when-authoring}時疑難排解AEM

以下章節說明使用AEM時可能會遇到的一些問題，以及如何疑難排解的建議。

## 已發佈網站上仍舊有的頁面版本{#old-page-version-still-on-published-site}

* **問題**:
   * 您已對頁面進行變更並將頁面發佈至發佈網站，但頁面的&#x200B;*old*&#x200B;版本仍顯示在發佈網站上。
* **原因**:
   * 這可能有數個原因，通常是快取（您的本機瀏覽器或Dispatcher），但有時可能是復寫佇列的問題。
* **解決方案**:
   * 這裡有各種可能性：
   * 確認頁面已正確復寫。 檢查頁面狀態，並在必要時檢查復寫佇列的狀態。
   * 清除本機瀏覽器中的快取，並再次存取您的頁面。
   * 將`?`新增至頁面URL的結尾。 例如：
      * `http://<host>:<port>/sites.html/content?`
      * 這會直接向AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。
   * 如果複製隊列出現問題，請與系統管理員聯繫。

## 工具欄{#component-actions-not-visible-on-toolbar}上不顯示元件操作

* **問題**:
   * 在製作環境上編輯內容頁面時，不會顯示完整的適用元件動作。
* **原因**:
   * 在少數情況下，先前的動作可能會影響工具列。
* **解決方案**:
   * 重新整理頁面。
