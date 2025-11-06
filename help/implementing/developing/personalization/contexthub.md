---
title: ContextHub
description: ContextHub是一種用於儲存、操控和呈現內容資料的架構
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
feature: Developing, Personalization
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub是一種用於儲存、操控和呈現內容資料的架構。 其主要功能是提供[檢視內容資料的功能，同時模擬和切換各種角色](/help/sites-cloud/authoring/personalization/contexthub.md)。

ContextHub允許您：

* 使用內容資料製作頁面時，[出現、檢視、切換角色和模擬使用者體驗](#presentation)。
* [將內容資料](#persistence)保留在您的網站上做為資料層表示。
* [管理所選內容的區段](#segmentation)。

使用者端JavaScript API可讓您存取個人化內容的資料。

## 簡報 {#presentation}

[ContextHub工具列](/help/sites-cloud/authoring/personalization/contexthub.md)可讓行銷人員和作者檢視並操控存放區資料，以模擬製作頁面時的使用者體驗。 工具列包含提供存取[ContextHub存放區](#persistence)的UI模組群組，這些模組會將ContextHub資料保留在使用者端上。

每個ContextHub UI模組都是預先定義模組型別的例項：

* ContextHub提供數個[範例模組型別](sample-modules.md)。
* 使用AEM主控台來[新增UI模組](configuring-contexthub.md#adding-a-ui-module)，並將它們以UI模式[分組](configuring-contexthub.md#adding-a-ui-mode)。
* 開發人員可以[建立自訂模組型別](extending-contexthub.md#creating-contexthub-ui-module-types)。

開發人員需要[將ContextHub元件新增至頁面](configuring-contexthub.md)。

## 持續性 {#persistence}

ContextHub會儲存使用者端上持續儲存的內容資料。 ContextHub JavaScript API可讓您視需要存取存放區以建立、更新和刪除資料。 因此，ContextHub代表頁面上的資料層。

每個ContextHub存放區都是預先定義的存放區型別例項：

* ContextHub提供數個[範例存放區型別](sample-stores.md)。
* 使用AEM主控台[建立存放區](configuring-contexthub.md#creating-a-contexthub-store)。
* 開發人員可以[建立自訂商店型別](extending-contexthub.md#creating-custom-store-candidates)。
* 開發人員可以[透過JavaScript存取存放區資料](adding-contexthub.md#interacting-with-contexthub-stores)。

## 細分 {#segmentation}

ContextHub包含區段引擎，可管理區段並決定針對目前內容解析哪些區段。 已定義數個區段。 您可以使用JavaScript API來[決定已解析的區段](adding-contexthub.md#determining-resolved-contexthub-segments)。
