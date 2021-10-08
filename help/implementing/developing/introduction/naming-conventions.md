---
title: 命名慣例
description: 儲存庫中的節點受Java內容儲存庫的命名慣例的約束
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 命名慣例{#naming-conventions}

儲存庫中的節點受Java內容儲存庫的命名慣例的約束。 不過，AEM會對頁面節點名稱實施進一步的慣例。

## 頁面的命名慣例 {#naming-conventions-for-pages}

這些命名慣例會在不同層級實作：

* JcrUtil:[JCR實用程式](#jcr-utilities)的AEM實施。
* PageManager:[頁面管理器](#page-manager)提供頁面層級操作的方法。
* 在AEM UI {#ui-behavior}內

### JCR實用程式 {#jcr-utilities}

[](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) JcrUtilis是JCR實用程式的AEM實施。要驗證名稱，特別需要的是它所控制的字元映射，以及以下驗證：

* `isValidName`
   * 檢查名稱是否非空白，且僅包含有效字元。
   * 可用來檢查建議的名稱是否有效。
* `createValidName`
   * 這會以任意字串建立有效標籤。
   * 它可用來從標題建立名稱。

### 頁面管理員 {#page-manager}

[](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) PageManager根據JCRUtil [提供頁面層級操作](#jcr-utilities)的方法。

### AEM UI行為 {#ui-behavior}

管理內容時，AEM UI:

* 在下列情況下，根據PageManager施加的限制驗證名稱：
   * 提供頁面標題以轉換為節點名稱
   * 提供了顯式節點名
