---
title: 命名約定
description: 儲存庫中的節點受Java內容儲存庫的命名約定的約束
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 命名約定{#naming-conventions}

儲存庫中的節點受Java內容儲存庫的命名約定的約束。 但AEM是會對頁節點名稱作進一步約定。

## 頁面命名約定 {#naming-conventions-for-pages}

這些命名約定在不同級別實施：

* JcrUtil:執AEM行 [JCR實用程式](#jcr-utilities)。
* PageManager:這樣 [頁面管理器](#page-manager) 提供了頁級操作的方法。
* 在UIAEM內 {#ui-behavior}

### JCR實用程式 {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) 是JCR實AEM用程式的實現。 對驗證名稱特別感興趣的是它控制的字元映射和以下驗證：

* `isValidName`
   * 檢查名稱是否不為空且僅包含有效字元。
   * 可用於檢查建議的名稱是否有效。
* `createValidName`
   * 這將從任意字串中建立有效標籤。
   * 它可用於從標題建立名稱。

### 頁面管理器 {#page-manager}

[頁面管理器](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) 提供基於的頁級操作方法 [JCRUtil](#jcr-utilities)。

### UIAEM行為 {#ui-behavior}

管理內容時，AEMUI:

* 根據PageManager施加的限制驗證名稱，當以下任一時間：
   * 提供頁標題以轉換為節點名稱
   * 提供了顯式節點名稱
