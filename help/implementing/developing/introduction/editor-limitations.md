---
title: 編輯器限制
description: 啟用觸控的UI中的編輯器會使用覆蓋來與iframe中限制的內容互動。 此互動功能會對編輯器的使用以及開發人員造成一些限制。
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# 編輯器限制 {#editor-limitations}

啟用觸控的UI中的編輯器會使用覆蓋來與iframe中限制的內容互動。 此互動功能會對編輯器的使用以及開發人員造成一些限制。 本頁總結了這些限制，並盡可能提供解決方案或解決方法。

## 功能限制 {#functional-limitations}

使用編輯器來製作頁面時，作者可能會遇到下列功能限制。

### 連結未作用中 {#links-not-active}

編輯 [頁面時](/help/sites-cloud/authoring/fundamentals/editing-content.md)，連結不作用中。

* [切換至 **預覽** 模式](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) ，使用內容中的連結進行導覽。

### 結構頁面 {#structure-pages}

無法命名頁面 `structure`。 在頁面編輯器 `structure` 中無法編輯命名的頁面。

## CSS限制 {#css-limitations}

開發人員在編輯器與CSS的互動時可能會遇到下列限制。

### 絕對定位元素 {#absolutely-positioned-elements}

絕對定位的元素可能會導致其覆蓋位置發生問題。

* 如果發生此情況，請確定絕對定位元素的尺寸正確，因為編輯器會建立具有相同尺寸的覆蓋。

### Vh Units {#vh-units}

`vh` 不支援單位，因為iframe高度必須由AEM自動調整。

### 固定背景影像 {#fixed-background-images}

固定背景影像在捲動時可能不會顯示為固定，因為它內嵌在iframe中。

* 在標 **題列動作中選取「檢視頁面** 」為「已發佈」，會正確顯示頁面。

### 100% Height {#height}

頁面的主體元素不支援100%高度。

* 為了實現全屏機身，可進行如下「拉伸」機身元件：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 邊界收合 {#margin-collapsing}

如果主體元素的第一個子元素具有邊界，則可看到邊界折疊問題。

* 解決方案是在主體元素層級添加clearfix，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
