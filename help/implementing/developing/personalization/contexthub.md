---
title: ContextHub
description: ContextHub是用於儲存、操作和呈現上下文資料的框架
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# 上下文中心 {#contexthub}

ContextHub是用於儲存、操作和呈現上下文資料的框架。 它的主要功能是提供 [在模擬和切換各種角色時查看上下文資料。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub允許您：

* [呈現、查看、切換角色和模擬用戶體驗](#presentation) 使用上下文資料建立頁面時。
* [保留上下文資料](#persistence) 作為資料層表示。
* [管理段](#segmentation) 的子菜單。

客戶端Javascript API使您能夠訪問資料以個性化內容。

## 簡報 {#presentation}

的 [ContextHub工具欄](/help/sites-cloud/authoring/personalization/contexthub.md) 使營銷人員和作者能夠查看和操作儲存資料，以在創作頁面時模擬用戶體驗。 工具欄由UI模組組組成，這些模組提供對 [ContextHub儲存，](#persistence) 將ContextHub資料保留在客戶端上。

每個ContextHub UI模組都是預定義模組類型的實例：

* ContextHub提供了 [示例模組類型](sample-modules.md)。
* 使用控AEM制台 [添加UI模組](configuring-contexthub.md#adding-a-ui-module), [在UI模式下對它們進行分組](configuring-contexthub.md#adding-a-ui-mode)。
* 開發人員可以 [建立自定義模組類型](extending-contexthub.md#creating-contexthub-ui-module-types)。

開發人員需要 [將ContextHub元件添加到頁面](configuring-contexthub.md)。

## 持久性 {#persistence}

ContextHub在客戶端上儲存持續的上下文資料。 ContextHub Javascript API使您能夠訪問儲存，以根據需要建立、更新和刪除資料。 因此，ContextHub表示頁面上的資料層。

每個ContextHub儲存都是預定義儲存類型的實例：

* ContextHub提供了 [示例儲存類型](sample-stores.md)。
* 使用控AEM制台 [建立儲存](configuring-contexthub.md#creating-a-contexthub-store)。
* 開發人員可以 [建立自定義儲存類型](extending-contexthub.md#creating-custom-store-candidates)。
* 開發人員可以 [訪問儲存資料](adding-contexthub.md#interacting-with-contexthub-stores) 通過Javascript。

## Segmentation {#segmentation}

ContextHub包括分段引擎，用於管理段並確定為當前上下文解析哪些段。 定義了若干段。 可以使用Javascript API [確定已解析的段](adding-contexthub.md#determining-resolved-contexthub-segments)。
