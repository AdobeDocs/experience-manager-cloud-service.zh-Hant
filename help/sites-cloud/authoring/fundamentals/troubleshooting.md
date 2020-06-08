---
title: 編寫時疑難排解AEM
description: 使用AEM時可能會遇到的一些問題
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 10%

---


# 編寫時疑難排解AEM {#troubleshooting-aem-when-authoring}

下節涵蓋您使用AEM時可能遇到的一些問題，以及如何疑難排解的建議。

## 舊頁面版本仍在發佈網站上 {#old-page-version-still-on-published-site}

* **問題**:
   * 您已變更頁面並將頁面發佈至發佈網站，但 *舊版頁面* 仍會顯示在發佈網站上。
* **原因**:
   * 這可能有幾種原因，最常是快取（本地瀏覽器或Dispatcher），但有時可能是複製隊列的問題。
* **解決方案**:
   * 這裡有各種可能：
   * 確認頁面已正確複製。 檢查頁狀態以及複製隊列的狀態（如果需要）。
   * 清除本機瀏覽器中的快取，並再次存取您的頁面。
   * 新 `?` 增至頁面URL的結尾。 例如：
      * `http://<host>:<port>/sites.html/content?`
      * 這會直接從AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。
   * 如果複製隊列存在問題，請與系統管理員聯繫。

## 工具欄上不顯示元件操作 {#component-actions-not-visible-on-toolbar}

* **問題**:
   * 在作者環境中編輯內容頁面時，不會顯示完整的適用元件動作。
* **原因**:
   * 在少數情況下，先前的動作可能會影響工具列。
* **解決方案**:
   * 重新整理頁面。
