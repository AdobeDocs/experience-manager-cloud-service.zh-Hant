---
title: 命名慣例
description: 儲存庫中的節點受Java內容儲存庫的命名約定的約束
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 命名慣例{#naming-conventions}

儲存庫中的節點受Java內容儲存庫的命名約定的約束。 不過，AEM會針對頁面節點的名稱，加入更多約定。

## 頁面的命名慣例 {#naming-conventions-for-pages}

這些命名慣例會在不同層級實作：

* JcrUtil:JCR公用程式的AEM [實作](#jcr-utilities)。
* PageManager:「頁 [面管理器](#page-manager) 」提供頁面層級操作的方法。
* 在AEM UI中 {#ui-behavior}

### JCR實用程式 {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) 是JCR實用程式的AEM實現。 驗證名稱的特別感興趣的是它控制的字元映射和以下驗證：

* `isValidName`
   * 檢查名稱是否不為空，且僅包含有效字元。
   * 可用來檢查建議的名稱是否有效。
* `createValidName`
   * 這會從任意字串中建立有效的標籤。
   * 它可用來從標題建立名稱。

### 頁面管理員 {#page-manager}

[PageManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 根據 [JCRUtil](#jcr-utilities)，提供頁面層級操作的方法。

### AEM UI行為 {#ui-behavior}

管理內容時，AEM UI:

* 驗證名稱時，請根據PageManager所施加的限制：
   * 提供頁面標題以轉換為節點名稱
   * 提供了顯式節點名稱
