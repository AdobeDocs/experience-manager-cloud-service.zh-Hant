---
title: 編輯器限制
description: 啟用觸摸的UI中的編輯器利用疊加來與限定在iframe中的內容交互。 這個互動會對編輯器的使用以及開發人員造成一些限制。
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---

# 編輯器限制 {#editor-limitations}

啟用觸摸的UI中的編輯器利用疊加來與限定在iframe中的內容交互。 這個互動會對編輯器的使用以及開發人員造成一些限制。本頁概述了這些限制，並盡可能提供解決方案或變通辦法。

## 功能限制 {#functional-limitations}

使用編輯器編寫頁面時，作者可能會遇到以下功能限制。

### 連結不活動 {#links-not-active}

當 [編輯頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md)，連結不處於活動狀態。

* [切換到 **預覽** 模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) 使用內容中的連結導航。

### 結構頁 {#structure-pages}

無法命名頁面 `structure`。 命名的頁 `structure` 在頁面編輯器中不可編輯。

## CSS限制 {#css-limitations}

開發人員在編輯器與CSS的交互時可能會遇到以下限制。

### 絕對定位元素 {#absolutely-positioned-elements}

絕對定位的元素可能導致其覆蓋位置出現問題。

* 如果發生這種情況，請確保絕對定位元素的尺寸正確，因為編輯器將建立具有相同尺寸的覆蓋。

### VH單位 {#vh-units}

`vh` 不支援單位，因為iframe高度必須由自動調AEM整。

### 固定背景影像 {#fixed-background-images}

由於固定背景影像嵌入在iframe中，因此在滾動時不能顯示為固定背景影像。

* 選擇 **以已發佈形式查看頁面** 在標題欄中，操作可正確顯示頁面。

### 100%高 {#height}

頁面的正文元素不支援100%高度。

* 通過「拉伸」身體元件，可進行如下的周圍加工：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 邊距折疊 {#margin-collapsing}

如果主體元素的第一子元素具有邊距，則可看到邊距折疊問題。

* 解決方案是在主體元素級別添加清除符，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
