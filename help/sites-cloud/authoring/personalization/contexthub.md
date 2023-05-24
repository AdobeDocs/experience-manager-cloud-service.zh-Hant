---
title: 使用 ContextHub 資料預覽頁面
description: ContextHub工具列會顯示ContextHub存放區中的資料，並可讓您變更存放區資料，且可用於預覽內容
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 3%

---

# 使用 ContextHub 資料預覽頁面  {#previewing-pages-using-contexthub-data}

ContextHub工具列會顯示ContextHub存放區中的資料，並可讓您變更存放區資料。 ContextHub工具列可用於預覽由ContextHub存放區中的資料所決定的內容。

工具列包含一系列包含一或多個UI模組的UI模式。

* UI模式是出現在工具列左側的圖示。 按一下或點選圖示時，工具列會顯示其中的UI模組。
* UI模組會顯示一或多個ContextHub存放區的資料。 有些UI模組也可讓您操控存放區資料。

ContextHub會安裝數個UI模式和UI模組。 您的管理員可能會 [已設定的ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) 以顯示不同的值。

## 顯示ContextHub工具列 {#revealing-the-contexthub-toolbar}

ContextHub工具列可在「預覽」模式下使用。 工具列僅在作者執行個體上可用，且僅當您的管理員啟用它時可用。

![contexthub工具列](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. 開啟頁面進行編輯時，在工具列上按一下或點選「預覽」。

   ![「預覽」按鈕](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. 若要顯示工具列，請按一下或點選ContextHub圖示。

   ![ContextHub按鈕](/help/sites-cloud/authoring/assets/contexthub-button.png)

## UI模組功能 {#ui-module-features}

提供的每個UI模組都是一組不同的功能，但以下型別的功能很常見。 由於UI模組是可擴充的，因此您的開發人員可以根據需要實作其他功能。

### 工具列內容 {#toolbar-content}

UI模組可以在工具列中顯示一或多個ContextHub存放區的資料。 UI模組使用圖示和標題來識別自身。

![ContextHub角色](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### 快顯內容 {#popup-content}

某些UI模組在點按或點選時會顯示快顯覆蓋圖。 通常，快顯視窗包含比工具列上顯示的資訊更多的資訊。

![contexthub設定檔資訊](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### 快顯視窗Forms {#popup-forms}

模組的彈出式覆蓋圖可包含可讓您變更ContextHub存放區中資料的表單元素。 如果頁面內容由商店資料決定，您可以使用表單並觀察頁面內容的變更。

### 全螢幕模式 {#fullscreen-mode}

彈出式覆蓋圖可包含您按一下或點選以展開彈出式內容的圖示，以涵蓋整個瀏覽器視窗或熒幕。

![全熒幕按鈕](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
