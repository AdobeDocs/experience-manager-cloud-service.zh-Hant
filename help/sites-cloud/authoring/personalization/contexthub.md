---
title: 使用 ContextHub 資料預覽頁面
description: ContextHub工具列顯示來自ContextHub存放區的資料，並可讓您變更存放區資料，且對於預覽內容很實用
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 3%

---

# 使用 ContextHub 資料預覽頁面  {#previewing-pages-using-contexthub-data}

ContextHub工具列會顯示ContextHub存放區的資料，並讓您變更存放區資料。 ContextHub工具列可用來預覽由ContextHub商店中的資料所決定的內容。

工具列包含一系列包含一或多個UI模組的UI模式。

* UI模式是顯示在工具列左側的圖示。 當您按一下或點選圖示時，工具列會顯示其包含的UI模組。
* UI模組會顯示一或多個ContextHub存放區的資料。 有些UI模組也可讓您操控儲存資料。

ContextHub會安裝數個UI模式和UI模組。 您的管理員可能 [已設定的ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) 來顯示不同的。

## 顯示ContextHub工具列 {#revealing-the-contexthub-toolbar}

ContextHub工具列可在「預覽」模式中使用。 工具列僅適用於製作執行個體，且僅在管理員啟用時才可用。

![ContextHub工具列](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. 在開啟您的頁面進行編輯時，在工具列上按一下或點選「預覽」。

   ![預覽按鈕](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. 若要顯示工具列，請按一下或點選「ContextHub」圖示。

   ![ContextHub按鈕](/help/sites-cloud/authoring/assets/contexthub-button.png)

## UI模組功能 {#ui-module-features}

每個UI模組提供的功能集不同，但下列功能類型很常見。 因為UI模組是可擴充的，您的開發人員可視需要實作其他功能。

### 工具列內容 {#toolbar-content}

UI模組可以顯示工具列中一或多個ContextHub存放區的資料。 UI模組會使用圖示和標題來識別自己。

![ContextHub角色](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### 快顯內容 {#popup-content}

有些UI模組在按一下或點選時會顯示快顯覆蓋圖。 彈出式功能表通常包含的工具列上顯示的其他資訊以外的其他資訊。

![ContextHub設定檔資訊](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### 彈出式Forms {#popup-forms}

模組的快顯覆蓋可以包含表單元素，讓您能夠變更ContextHub存放區中的資料。 如果頁面內容由儲存資料決定，您可以使用表單並觀察頁面內容的變更。

### 全螢幕模式 {#fullscreen-mode}

彈出式覆蓋圖可包含您按一下或點選以展開彈出式內容的圖示，以覆蓋整個瀏覽器視窗或畫面。

![全螢幕按鈕](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
