---
title: ContextHub
description: ContextHub是儲存、控制和呈現上下文資料的架構
translation-type: tm+mt
source-git-commit: 75d6b51c0148a21ca401d98a5eaf644fc6b0e8cc
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# ContextHub {#contexthub}

ContextHub是儲存、控制和呈現上下文資料的架構。 它的主要功能是提供在模擬和切換各 [種角色時，檢視上下文資料的能力。](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub可讓您：

* [使用內容資料製作頁面時，呈現、檢視、切換角色](#presentation) ，並模擬使用者體驗。
* [將網站上的上下文資料](#persistence) ，以資料層表示形式保存。
* [管理選取上下文的區段](#segmentation) 。

用戶端Javascript API可讓您存取資料，以個人化內容。

## 簡報 {#presentation}

ContextHub工 [](/help/sites-cloud/authoring/personalization/contexthub.md) 具列可讓行銷人員和作者查看和控制儲存資料，以模擬在製作頁面時的使用者體驗。 工具列由UI模組群組組成，這些UI模組可存取 [ContextHub儲存區](#persistence) ，這些儲存區會保存用戶端上的ContextHub資料。

每個ContextHub UI模組都是預先定義模組類型的例項：

* ContextHub提供了幾 [種模組類型](sample-modules.md)。
* 使用AEM主控台 [新增UI模組](configuring-contexthub.md#adding-a-ui-module)，並 [在UI模式中分組](configuring-contexthub.md#adding-a-ui-mode)。
* 開發人員可 [以建立自訂模組類型](extending-contexthub.md#creating-contexthub-ui-module-types)。

開發人員需 [要將ContextHub元件新增至頁面](configuring-contexthub.md)。

## 永續性 {#persistence}

ContextHub會在用戶端上儲存持續的上下文資料。 ContextHub Javascript API可讓您存取商店，以視需要建立、更新和刪除資料。 因此，ContextHub代表您頁面上的資料層。

每個ContextHub儲存都是預定義儲存類型的實例：

* ContextHub提供數種 [範例商店類型](sample-stores.md)。
* 使用AEM主控台 [建立商店](configuring-contexthub.md#creating-a-contexthub-store)。
* 開發人員可 [以建立自訂商店類型](extending-contexthub.md#creating-custom-store-candidates)。
* 開發人員可 [以透過Javascript存取](configuring-contexthub.md#interacting-with-contexthub-stores) 儲存資料。

## Segmentation {#segmentation}

ContextHub包含區段引擎，可管理區段並判斷哪些區段可針對目前的上下文加以解析。 已定義數個區段。 您可以使用Javascript API來判斷已解 [決的區段](configuring-contexthub.md#determining-resolved-contexthub-segments)。
