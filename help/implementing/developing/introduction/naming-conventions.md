---
title: 命名慣例
description: 存放庫中的節點會遵守Java內容存放庫的命名慣例
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# 命名慣例{#naming-conventions}

存放庫中的節點會遵守Java內容存放庫的命名慣例。 不過，AEM對頁面節點名稱實施進一步的慣例。

## 頁面的命名慣例 {#naming-conventions-for-pages}

這些命名慣例會在不同的層級實作：

* JcrUtil： [JCR公用程式](#jcr-utilities)的AEM實作。
* PageManager： [頁面管理員](#page-manager)提供頁面層級作業的方法。
* 在AEM UI中 {#ui-behavior}

### jcr公用程式 {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html)是JCR公用程式的AEM實作。 驗證名稱特別需要的是它控制的字元對應以及下列驗證：

* `isValidName`
   * 檢查名稱是否非空白且僅包含有效字元。
   * 可用來檢查建議的名稱是否有效。
* `createValidName`
   * 這會以任意字串建立有效的標籤。
   * 它可用來從標題建立名稱。

### 頁面管理員 {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html)提供基於[JCRUtil](#jcr-utilities)的頁面層級作業方法。

### AEM UI行為 {#ui-behavior}

管理內容時，AEM UI：

* 符合下列任一條件時，請根據PageManager的限制，驗證名稱：
   * 提供了頁面標題，以便轉換為節點名稱
   * 提供了明確的節點名稱
