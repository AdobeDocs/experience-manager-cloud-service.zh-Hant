---
title: Universal Visual Editor 簡介
description: 了解透過 Universal Visual Editor (即 Universal Editor) 如何實現所見即所得 (WYSIWYG) 編輯任何無周邊和有周邊體驗。了解它如何幫助內容作者提供卓越的體驗、提高其內容速度，以及如何提供最先進的開發人員體驗。
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
source-git-commit: 0f62245d31074ab7a64d86b97ef3b1a8d7533001
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 88%

---


# Universal Visual Editor 簡介 {#introduction}

了解透過 Universal Visual Editor (即 Universal Editor) 如何實現所見即所得 (WYSIWYG) 編輯任何無周邊和有周邊體驗。了解它如何幫助內容作者提供卓越的體驗、提高其內容速度，以及如何提供最先進的開發人員體驗。

## 背景 {#background}

AEM 內容作者最強大的工具就是頁面編輯器。頁面編輯器提供直觀、視覺化且與內容相關的 WYSIWYG 編寫體驗，只需一點培訓即可讓作者看見內容將如何顯示。

但是，頁面編輯器只能編輯 AEM 頁面內容、結構和其中包含的元件。但在現在，內容很少只來自同一個地方。Universal Editor 提供與頁面編輯器相同的就地編輯體驗，但適用於任意實施中任何方面的內容。

## 真正通用 {#universal}

Universal Editor 可以用於任何實施、任何內容和任何方面的內容。

![為何麼它可以通用](assets/universal.png)

### 任何實施 {#any-implementation}

由於體驗可以透過許多不同方式建置，因此任何實作都可以使用通用編輯器，以便作者執行內容內編輯。

使用者通常認為，Headless實作會將作者限制在表單式UI中編輯所有內容，但通用編輯器並非如此

實作使用通用編輯器的需求很簡單，並支援下列專案：

* **任何架構** - 伺服器端轉譯、邊緣端轉譯、用戶端轉譯等。
* **任何框架** - Vanilla AEM，或任何協力廠商框架，如 React、Next.js、Angular 等。
* **任何託管** - 可以在本機託管到 AEM，或託管在遠端網域上

### 任何內容 {#any-content}

內容作者也會擁有 AEM 頁面編輯器先前提供的強大編輯體驗。但是 Universal Editor 可讓內容作者在內容中視覺化編輯&#x200B;**任何**&#x200B;內容，並支援：

* **AEM 頁面結構** - `cq:Pages` 的嵌套`cq:Components`，包括體驗片段
* **AEM 內容片段** - 編輯出現在體驗內容中內容片段的內容.
* **文件** - 概念驗證表明 Word、Excel、Google 文件或 Markdown 文件也可以用相同的方式進行編輯 (這是 WIP)。

### 任何方面 {#any-aspect}

對於內容作者而言，內容不僅僅是包含的資訊，還包括呈現和接收資訊的方式。內容帶有額外的中繼資料和檢測規則，Universal Editor 可以理解和編輯這些規則，包括：

* **套用版面和樣式** - 透過使用樣式系統，行銷從業人員和內容作者可以將不同的樣式套用至其內容，並為內容建立不同的版面，例如欄、浮動切換、標籤、摺疊式功能表等。

## 值 {#value}

透過將內容編輯體驗與任何特定的內容交付系統分離，編輯器變得更通用和靈活，並可讓內容作者提供卓越的體驗，提高內容速度，並提供最先進的開發人員體驗。

![Universal Editor 的值](assets/value.png)

* **提供卓越的體驗**  — 為了讓從業人員建立吸引人的訪客體驗，通用編輯器允許從業人員在預覽環境中建立和編輯內容。 這可讓他們建立適合體驗設計的內容，並建構對造訪者有意義的旅程。
* **提高內容速度** - 為了簡化從業人員的管理工作流程，Universal Editor 可在預覽中編輯內容，透過僅顯示與該內容相關的選項來引導從業人員，並使工作流程獨立於內容來源。
* **最先進的開發人員體驗** - 為了支援真實生活的異質應用程式環境，Universal Editor 具備低耦合且與技術無關的特性，可讓開發人員使用他們喜歡的技術堆棧來實施體驗。

## Universal Visual Editor 和內容片段編輯器 {#universal-editor-content-fragment-editor}

乍看之下，Universal Visual Editor 和內容片段編輯器的編輯功能似乎很相似。然而，這些編輯器的功能大不相同，其完成的工作與行銷從業人員不同。

### 內容片段編輯器 {#content-fragment-editor}

行銷從業人員希望建立內容而不必關心其版面，以便它可以在多種體驗環境中重複使用。

* 要達成的基本工作是擴展內容策略。

### Universal Visual Editor {#universal-editor}

行銷從業人員會想建立根據指定內容版面量身定制的內容，以提供卓越的體驗。

* 要達成的基本工作是與讀者建立可靠的聯繫。

## 路線圖 {#road-map}

請務必注意，Universal Editor 還在開發中，本文件中列出的部分功能是最終編輯器的設想，不一定是目前擁有的功能。

請洽詢您的Adobe聯絡人，以取得有關為Universal Editor規劃的未來功能的詳細資訊。

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [使用 Universal Editor 編寫內容](authoring.md) - 了解內容作者使用 Universal Editor 建立內容有多簡單和直觀。
* [使用 Universal Editor 發佈內容](publishing.md) - 了解 Universal Visual Editor 如何發佈內容，和您的應用程式如何處理發佈的內容。
* [AEM 中 Universal Editor 快速入門](getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](authentication.md) - 了解 Universal Editor 如何進行驗證。
