---
title: 使用 ContextHub 資料預覽頁面
description: ContextHub工具欄顯示ContextHub儲存中的資料，並允許您更改儲存資料，對預覽內容非常有用
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 3%

---

# 使用 ContextHub 資料預覽頁面  {#previewing-pages-using-contexthub-data}

ContextHub工具欄顯示ContextHub儲存中的資料，並允許您更改儲存資料。 ContextHub工具欄對預覽由ContextHub儲存中的資料確定的內容非常有用。

工具欄由包含一個或多個UI模組的一系列UI模式組成。

* UI模式是工具欄左側顯示的表徵圖。 按一下或點擊表徵圖時，工具欄將顯示其包含的UI模組。
* UI模組顯示來自一個或多個ContextHub儲存的資料。 某些UI模組還允許您操作儲存資料。

ContextHub安裝多個UI模式和UI模組。 您的管理員可能 [已配置ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) 來顯示不同的。

## 顯示ContextHub工具欄 {#revealing-the-contexthub-toolbar}

「預覽」模式下可使用ContextHub工具欄。 工具欄僅在作者實例上可用，並且僅當管理員啟用了它時才可用。

![ContextHub工具欄](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. 開啟頁面進行編輯時，在工具欄上按一下或點擊「預覽」。

   ![預覽按鈕](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. 要顯示工具欄，請按一下或點擊「上下文中心」表徵圖。

   ![「上下文中心」按鈕](/help/sites-cloud/authoring/assets/contexthub-button.png)

## UI模組功能 {#ui-module-features}

每個UI模組提供的功能集不同，但以下類型的功能是通用的。 因為UI模組是可擴展的，所以開發人員可以根據需要實現其他功能。

### 工具欄內容 {#toolbar-content}

UI模組可以顯示工具欄中一個或多個ContextHub儲存中的資料。 UI模組使用表徵圖和標題來標識自己。

![ContextHub角色](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### 彈出內容 {#popup-content}

某些UI模組在按一下或點擊時顯示彈出式覆蓋。 通常，彈出菜單包含的資訊比工具欄上顯示的資訊還要多。

![ContextHub配置檔案資訊](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### 彈出式Forms {#popup-forms}

模組的彈出式覆蓋可以包括表單元素，這些元素使您能夠更改ContextHub儲存中的資料。 如果頁面內容由儲存資料確定，則可以使用表單並觀察頁面內容的更改。

### 全螢幕模式 {#fullscreen-mode}

彈出式疊加可以包含一個表徵圖，您按一下或點擊該表徵圖可展開彈出式內容以覆蓋整個瀏覽器窗口或螢幕。

![全屏按鈕](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
