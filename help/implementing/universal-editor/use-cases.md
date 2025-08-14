---
title: 通用編輯器使用案例和學習路徑
description: 瞭解Universal Editor的主要使用案例，以及如何最好地瞭解其使用方式，以及如何在您自己的專案中實作。
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# 通用編輯器使用案例和學習路徑 {#use-cases-learning-paths}

瞭解通用編輯器的主要使用案例，以及如何充分瞭解其使用方式，以及如何在您自己的專案中實作。

## 概觀 {#overview}

通用編輯器是多功能的視覺化編輯器，屬於Adobe Experience Manager Sites的一部分。 它可讓作者對任何Headless或Headful體驗執行「所見即所得」(WYSIWYG)編輯。

本檔案將詳細說明這兩個使用案例，並說明如何深入瞭解這些案例，以便在您自己的專案中實作通用編輯器。

>[!TIP]
>
>若尚未提供，請檢閱檔案[通用編輯器簡介](/help/implementing/universal-editor/introduction.md)，以取得通用編輯器的完整概觀和值。

## 使用案例 {#use-cases}

Universal Editor為您的內容作者提供方便、直觀的視覺編輯器，無論他們建立什麼型別的內容。 兩個主要使用案例為：

* [WYSIWYG製作](#wysiwyg-authoring) — 使用AEM Sites主控台，使用通用編輯器在AEM中管理您的內容和製作頁面
* [Headless製作](#headless-authoring) — 使用通用編輯器在您自己的自訂Headless應用程式中製作內容。

### WYSIWYG 編寫 {#wysiwyg-authoring}

如果您已熟悉AEM，您可以使用Sites主控台建立和管理您的頁面，然後使用通用編輯器進行編輯。

透過這種方式，您可以從Sites Console中提供的工具(例如頁面管理（複製、貼上、移動）和工作流程)中受益，也可以從現代的通用編輯器中受益。

如果您的使用案例是這樣的，作為緊接著的下一步，請參閱以下檔案以取得有關如何在AEM中啟動並執行通用編輯器的完整概觀。

1. [使用Edge Delivery Services編寫WYSIWYG的開發人員快速入門手冊](https://www.aem.live/developer/ue-tutorial) — 開始使用AEM中的第一個Universal Editor專案
1. [建立已檢測成可與通用編輯器搭配使用的區塊](https://www.aem.live/developer/universal-editor-blocks) — 瞭解如何檢測區塊，使您的內容可在通用編輯器中編輯
1. [使用Edge Delivery Services專案進行WYSIWYG製作的內容模型化](https://www.aem.live/developer/component-model-definitions) — 瞭解區塊結構的詳細資訊，以有效地模型化您的內容以供搭配通用編輯器使用。

閱讀這些檔案後，您可以返回本頁，瞭解Headless編寫使用案例以及Universal Editor的一般運作方式。

### Headless製作 {#headless-authoring}

如果您已有Headless應用程式，可以使用Universal Editor來編寫應用程式的內容，並將其內容以AEM內容片段的形式持續存在。 唯一的要求是應用程式必須檢測為允許使用通用編輯器。

如果您的使用案例是這樣的，作為緊接著的下一步，請參閱以下檔案以瞭解使用通用編輯器的Headless應用程式範例。

* [通用編輯器的SecurBank範例應用程式](/help/implementing/universal-editor/securbank.md)

閱讀該檔案後，您可以返回本頁瞭解WYSIWYG編寫使用案例以及Universal Editor的一般運作方式。

{{ue-headless-auth}}

## 通用編輯器的運作方式 {#how-ue-works}

Universal Editor的強大功能是能夠就地撰寫任何內容，因此無論內容為何，都可為內容作者提供完全直覺式且統一的UI。

Universal Editor的運作方式如下。

1. 開發人員會測試應用程式或頁面，以使用通用編輯器。 此檢測會告知編輯器哪些內容可編輯以及如何將其保留。
   * 如果您使用Edge Delivery Services[檔案遵循WYSIWYG製作的](https://www.aem.live/developer/ue-tutorial)開發人員快速入門手冊，您的頁面會自動進行檢測。
   * 針對Headless編寫，可輕鬆檢測您的應用程式。
1. 內容作者會載入通用編輯器，接著再載入您的頁面進行編輯。 由於是儀器式的，因此它知道哪些內容可以編輯，以及如何表示和持續儲存內容。
1. 內容作者可在直覺式的WYSIWYG介面中編輯頁面內容，就地編輯。
1. Universal Editor會自動將變更儲存回資料來源。

如果您想深入瞭解通用編輯器的架構，請參閱檔案[通用編輯器架構](/help/implementing/universal-editor/architecture.md)。

## Universal Editor概念 {#concepts}

若要讓通用編輯器可編輯頁面或應用程式，必須正確檢測該頁面或應用程式。

* [屬性和型別](/help/implementing/universal-editor/attributes-types.md) — 若要讓通用編輯器可編輯應用程式或頁面，必須正確檢測它。 這包括包含適當的中繼資料，以便編輯器可以編輯應用程式的內容。
* [模型定義、欄位和元件型別](/help/implementing/universal-editor/field-types.md) — 當中繼資料顯示以啟用元件編輯功能後，您即可在編輯器的屬性面板中定義它們可以操作的欄位和元件型別。
* [通用編輯器事件](/help/implementing/universal-editor/events.md) — 您可以透過使用通用編輯器在內容或UI互動上發出的事件，來增強應用程式中的編輯體驗，進而自訂您的應用程式。

通用編輯器也可以根據您的專案需求進行調整。

* [自訂Universal Editor](/help/implementing/universal-editor/customizing.md) - Universal Editor體驗可以透過篩選編輯器的不同方面或擴充編輯器的功能來調整。
* [擴充通用編輯器](/help/implementing/universal-editor/extending.md) — 可擴充通用編輯器的UI，以擴充其功能來滿足您的專案需求。
