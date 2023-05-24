---
title: 疑難排解製作時的AEM
description: 使用AEM時可能會遇到的一些問題
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 10%

---

# 疑難排解製作時的AEM {#troubleshooting-aem-when-authoring}

下節涵蓋您在使用AEM時可能會遇到的一些問題，以及有關如何疑難排解這些問題的建議。

## 發佈網站上仍顯示舊的頁面版本 {#old-page-version-still-on-published-site}

* **問題**:
   * 您已變更頁面並將頁面發佈至發佈網站，但 *舊* 頁面版本仍會顯示在發佈網站上。
* **原因**:
   * 這可能有多種原因，最常見的是快取（本機瀏覽器或Dispatcher），不過有時復寫佇列可能會出現問題。
* **解決方案**:
   * 這裡有多種可能性：
   * 確認頁面已正確復寫。 檢查頁面狀態，並視需要檢查復寫佇列的狀態。
   * 清除本機瀏覽器中的快取，然後再次存取您的頁面。
   * 新增 `?` 到頁面URL的結尾。 例如：
      * `http://<host>:<port>/sites.html/content?`
      * 這會直接向AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。
   * 如果復寫佇列發生問題，請聯絡您的系統管理員。

## 元件動作在工具列上不可見 {#component-actions-not-visible-on-toolbar}

* **問題**:
   * 在作者環境中編輯內容頁面時，無法看到適用元件的完整動作範圍。
* **原因**:
   * 在極少數情況下，先前的動作可能會影響工具列。
* **解決方案**:
   * 重新整理頁面。
