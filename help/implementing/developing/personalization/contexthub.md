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

ContextHub是儲存、操控和呈現內容資料的架構。 其主要功能是提供在模擬和切換各種角色時[查看上下文資料的功能。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub可讓您：

* [使用內容資料製作頁面時，呈現、檢視、切換角](#presentation) 色及模擬使用者體驗。
* [將網站](#persistence) 上的內容資料保留為資料層表示。
* [管理](#segmentation) 所選內容的區段。

用戶端Javascript API可讓您存取資料，以個人化內容。

## 簡報 {#presentation}

[ContextHub工具列](/help/sites-cloud/authoring/personalization/contexthub.md)可讓行銷人員和作者查看和操控存放區資料，以模擬製作頁面時的使用者體驗。 工具列由提供[ContextHub存放區存取權的UI模組組成，](#persistence)會保留用戶端上的ContextHub資料。

每個ContextHub UI模組都是預先定義模組類型的例項：

* ContextHub提供數種[範例模組類型](sample-modules.md)。
* 使用AEM主控台來[新增UI模組](configuring-contexthub.md#adding-a-ui-module)，以及在UI模式](configuring-contexthub.md#adding-a-ui-mode)中將它們分組。[
* 開發人員可以[建立自訂模組類型](extending-contexthub.md#creating-contexthub-ui-module-types)。

開發人員需要[將ContextHub元件新增至頁面](configuring-contexthub.md)。

## 持久性 {#persistence}

ContextHub會在用戶端上儲存保留的內容資料。 ContextHub Javascript API可讓您視需要存取儲存區，以建立、更新和刪除資料。 因此，ContextHub代表您頁面上的資料層。

每個ContextHub存放區都是預先定義的存放區類型的例項：

* ContextHub提供數種[範例存放區類型](sample-stores.md)。
* 使用AEM主控台建立[儲存](configuring-contexthub.md#creating-a-contexthub-store)。
* 開發人員可以[建立自訂商店類型](extending-contexthub.md#creating-custom-store-candidates)。
* 開發人員可以透過Javascript存取[儲存資料](adding-contexthub.md#interacting-with-contexthub-stores)。

## Segmentation {#segmentation}

ContextHub包含區段引擎，可管理區段並判斷要針對目前內容解析哪些區段。 已定義數個區段。 您可以使用Javascript API來[判斷已解析的區段](adding-contexthub.md#determining-resolved-contexthub-segments)。
