---
title: ContextHub
description: ContextHub是儲存、操控和呈現內容資料的架構
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub是儲存、操控和呈現內容資料的架構。 其主要功能是提供 [在模擬和切換各種角色時檢視內容資料。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub可讓您：

* [呈現、檢視、切換角色及模擬使用者體驗](#presentation) 使用內容資料編寫頁面時。
* [保留內容資料](#persistence) 作為資料層表示。
* [管理區段](#segmentation) 中。

用戶端Javascript API可讓您存取資料，以個人化內容。

## 簡報 {#presentation}

此 [ContextHub工具列](/help/sites-cloud/authoring/personalization/contexthub.md) 可讓行銷人員和作者查看和操控儲存資料，以模擬編寫頁面時的使用者體驗。 工具列包含提供存取權的UI模組群組 [ContextHub商店、](#persistence) 會保留用戶端上的ContextHub資料。

每個ContextHub UI模組都是預先定義模組類型的例項：

* ContextHub提供數個 [範例模組類型](sample-modules.md).
* 使用AEM主控台 [新增UI模組](configuring-contexthub.md#adding-a-ui-module)和 [在UI模式中將它們分組](configuring-contexthub.md#adding-a-ui-mode).
* 開發人員可 [建立自訂模組類型](extending-contexthub.md#creating-contexthub-ui-module-types).

開發人員需 [將ContextHub元件新增至頁面](configuring-contexthub.md).

## 持久性 {#persistence}

ContextHub會在用戶端上儲存保留的內容資料。 ContextHub Javascript API可讓您視需要存取儲存區，以建立、更新和刪除資料。 因此，ContextHub代表您頁面上的資料層。

每個ContextHub存放區都是預先定義的存放區類型的例項：

* ContextHub提供數個 [範例存放區類型](sample-stores.md).
* 使用AEM主控台 [建立儲存](configuring-contexthub.md#creating-a-contexthub-store).
* 開發人員可 [建立自訂商店類型](extending-contexthub.md#creating-custom-store-candidates).
* 開發人員可 [存取儲存資料](adding-contexthub.md#interacting-with-contexthub-stores) 透過JavaScript。

## Segmentation {#segmentation}

ContextHub包含區段引擎，可管理區段並判斷要針對目前內容解析哪些區段。 已定義數個區段。 您可以將Javascript API用於 [判斷已解析的區段](adding-contexthub.md#determining-resolved-contexthub-segments).
