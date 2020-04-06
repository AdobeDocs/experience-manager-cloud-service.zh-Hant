---
title: AEM系統概觀
description: AEM系統概觀
translation-type: tm+mt
source-git-commit: aa6bb878ea4c58ba1e2fbf82d53effaa1a72d668

---


# AEM系統概觀 {#aem-system}

本頁說明Adobe Experience Manager(AEM)系統概觀。

## 背景 {#background}

此模式可用來識別提供AEM系統概觀的一般資訊。 資訊可包含下列項目：

AEM版本使用的AEM產品（網站、資產、表單等）節點計數（頁面、資產等）

## 模式資料 {#pattern-data}

模式的JSON表示法中包含下列物件：

* **item.message**:是指模式的訊息。
* **item.context**:參考概述資訊的其他資訊：
   * *類型*:上下文資料的類型，「aem.version」、「aem.product」或「node.count」。
   * *資料*:JSON物件包含與類型對應的資料：&quot;version&quot;（字串）、&quot;product&quot;（字串）或&quot;count&quot;（整數）。

### 可能的影響和風險 {#possible-implications}

不適用。

### 可能的解決方案 {#possible-solutions}

不適用。
