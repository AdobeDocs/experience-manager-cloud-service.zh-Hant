---
title: 通用編輯器使用案例和學習路徑
description: 了解通用編輯器的主要使用案例，以及如何充分了解其用途，還有如何在自己的專案中實施。
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: ht
source-wordcount: '882'
ht-degree: 100%

---

# 通用編輯器使用案例和學習路徑 {#use-cases-learning-paths}

了解通用編輯器的主要使用案例，以及如何更加了解其用途，還有如何在自己的專案中實施。

## 概觀 {#overview}

通用編輯器是一個多功能視覺化編輯器，是 Adobe Experience Manager Sites 的一部分。作者可以使用此編輯器透過所見即所得 (WYSIWYG) 的方式編輯任何無周邊或有周邊體驗。

本文件將詳細解釋這兩個使用案例，並告訴您要如何更加了解其相關資訊，讓您可以在自己的專案中實施通用編輯器。

>[!TIP]
>
>若您還沒有閱讀，請檢閱[通用編輯器簡介](/help/implementing/universal-editor/introduction.md)文件，了解通用編輯器的完整概觀和價值。

## 使用案例 {#use-cases}

無論內容作者正在建立什麼類型的內容，通用編輯器都是方便又簡單易用的視覺化編輯器。兩個主要的使用案例如下：

* [WYSIWYG 製作](#wysiwyg-authoring) - 使用 AEM Sites 控制台來管理您的內容，以及在 AEM 中使用通用編輯器來製作頁面
* [無周邊製作](#headless-authoring) - 使用通用編輯器在自訂的無周邊應用程式中製作內容。

### WYSIWYG 製作 {#wysiwyg-authoring}

若您已經熟悉 AEM，可以使用 Sites 控制台建立和管理您的頁面，然後使用通用編輯器對其進行編輯。

透過這種方式，您不但能夠運用 Sites 控制台中提供的工具，例如頁面管理 (複製、貼上、移動) 和工作流程，還能夠使用現代的通用編輯器。

如果這是您的使用案例，緊接著下一步，請參閱以下文件，了解如何在 AEM 中設定和執行通用編輯器的完整概觀。

1. [使用 Edge Delivery Services 進行 WYSIWYG 製作的開發人員快速入門手冊](https://www.aem.live/developer/ue-tutorial) - 開始使用 AEM 中第一個通用編輯器專案
1. [建立已經過檢測以和通用編輯器一起使用的區塊](https://www.aem.live/developer/universal-editor-blocks) - 了解如何檢測區塊，讓您可以在通用編輯器中編輯內容
1. [Edge Delivery Services 專案進行 WYSIWYG 製作的內容建模](https://www.aem.live/developer/component-model-definitions) - 詳細了解區塊的結構，以便有效地為內容建模並供通用編輯器使用。

閱讀這些文件後，您可以返回此頁面，了解無周邊製作使用案例，以及通用編輯器的一般運作原理。

### 無周邊製作 {#headless-authoring}

若您已經擁有無周邊應用程式，可以使用通用編輯器製作應用程式的內容，並將其內容作為內容片段保留在 AEM 中。唯一需求是必須檢測應用程式，以便允許使用通用編輯器。

如果這是您的使用案例，緊接著下一步，請參閱以下文件，了解無周邊應用程式經過檢測而能使用通用編輯器的範例。

* [通用編輯器的 SecurBank 範例應用程式](/help/implementing/universal-editor/securbank.md)

閱讀該文件後，您可以返回此頁面，了解 WYSIWYG 製作使用案例，以及通用編輯器的一般運作原理。

{{ue-headless-auth}}

## 通用編輯器的運作原理 {#how-ue-works}

通用編輯器的強大功能在於能夠在原位置製作任何內容，無論內容是什麼，都能為內容作者提供簡單易用且統一的使用者介面。

通用編輯器的運作方式如下。

1. 開發人員檢測應用程式或頁面，以便能夠使用通用編輯器。此檢測可告知編輯器，哪些內容為可編輯以及如何保留。
   * 若您依循[使用 Edge Delivery Services 進行 WYSIWYG 製作的開發人員快速入門手冊](https://www.aem.live/developer/ue-tutorial)文件，您的頁面會自動經過檢測。
   * 如果是無周邊製作，您可以輕鬆地檢測應用程式。
1. 內容作者載入通用編輯器，然後通用編輯器會載入您的頁面進行編輯。由於經過檢測，所以編輯器知道哪些內容為可編輯，以及如何呈現和保留這些內容。
1. 內容作者在直覺式的 WYSIWYG 介面中編輯頁面內容，在原位置編輯。
1. 通用編輯器會自動將變更儲存回資料來源並保留。

若想了解更多關於通用編輯器架構的詳細資訊，請參閱[通用編輯器架構](/help/implementing/universal-editor/architecture.md)文件。

## 通用編輯器概念 {#concepts}

若要讓頁面或應用程式可以透過通用編輯器進行編輯，必須進行適當的檢測。

* [屬性與類型](/help/implementing/universal-editor/attributes-types.md) - 為了讓應用程式或頁面可由通用編輯器進行編輯，必須進行適當的檢測。這包括要加入適當的後設資料，讓編輯器可以編輯應用程式的內容。
* [模型定義、欄位與元件類型](/help/implementing/universal-editor/field-types.md) - 具備後設資料並能夠編輯元件後，您即可在編輯器的屬性面板中定義可以操作哪些欄位和元件類型。
* [通用編輯器事件](/help/implementing/universal-editor/events.md) - 您可以使用通用編輯器在內容或使用者介面互動時所發出的事件，增強應用程式中的編輯體驗，進一步自訂您的應用程式。

您也可以根據專案需求改造通用編輯器。

* [自訂通用編輯器](/help/implementing/universal-editor/customizing.md) - 您可以篩選編輯器的不同層面或擴充編輯器的功能，來改造通用編輯器體驗。
* [擴充通用編輯器](/help/implementing/universal-editor/extending.md) - 您可以擴充通用編輯器的使用者介面，藉此擴展其功能以滿足專案需求。
