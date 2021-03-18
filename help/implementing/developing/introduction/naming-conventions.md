---
title: 命名慣例
description: 儲存庫中的節點受Java內容儲存庫的命名約定的約束
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# 命名慣例{#naming-conventions}

儲存庫中的節點受Java內容儲存庫的命名約定的約束。 但AEM是，頁面節點名稱會有進一步的約定。

## 頁面{#naming-conventions-for-pages}的命名慣例

這些命名慣例會在不同層級實作：

* JcrUtil:&lt;aAEM0/>JCR實用程式](#jcr-utilities)的實現。[
* PageManager:[頁面管理器](#page-manager)提供頁面層級操作的方法。
* 在AEMUI {#ui-behavior}中

### JCR實用程式{#jcr-utilities}

[JcrUtilis](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/jcr/JcrUtil.html) 實AEM施JCR實用程式。驗證名稱的特別感興趣的是它控制的字元映射和以下驗證：

* `isValidName`
   * 檢查名稱是否不為空，且僅包含有效字元。
   * 可用來檢查建議的名稱是否有效。
* `createValidName`
   * 這會從任意字串中建立有效的標籤。
   * 它可用來從標題建立名稱。

### 頁面管理員{#page-manager}

[PageManager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html) 根據 [JCRUtil提供頁面層級操作的](#jcr-utilities)方法。

### AEMUI行為{#ui-behavior}

管理內容時，AEMUI:

* 驗證名稱時，請根據PageManager所施加的限制：
   * 提供頁面標題以轉換為節點名稱
   * 提供了顯式節點名稱
