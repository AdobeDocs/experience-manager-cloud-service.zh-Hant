---
title: 編輯器限制
description: 觸控式UI中的編輯器會使用覆蓋來與受限於iframe的內容互動。 這個互動會對編輯器的使用以及開發人員造成一些限制。
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---

# 編輯器限制 {#editor-limitations}

觸控式UI中的編輯器會使用覆蓋來與受限於iframe的內容互動。 這個互動會對編輯器的使用以及開發人員造成一些限制。本頁概述這些限制，並盡可能提供解決方案或解決方案。

## 功能限制{#functional-limitations}

使用編輯器來製作頁面時，作者可能會遇到下列功能限制。

### 連結不活動{#links-not-active}

當[編輯頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md)時，連結不處於活動狀態。

* [切換至「 **** ](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) 預覽模式」，使用內容中的連結進行導覽。

### 結構頁{#structure-pages}

無法為頁面命名`structure`。 命名為`structure`的頁面在頁面編輯器中無法編輯。

## CSS限制{#css-limitations}

開發人員在編輯器與CSS的互動中可能會遇到下列限制。

### 絕對定位的元素{#absolutely-positioned-elements}

絕對定位的元素可能會在其覆蓋圖的位置造成問題。

* 如果發生此情況，請確定絕對定位的元素的尺寸正確，因為編輯器將建立具有相同尺寸的覆蓋圖。

### Vh單位{#vh-units}

`vh` 不支援單位，因為iframe高度必須由AEM自動調整。

### 修正背景影像{#fixed-background-images}

由於背景影像內嵌於iframe中，因此捲動時，固定的背景影像可能無法顯示為固定。

* 在標題列動作中選取&#x200B;**以Published**&#x200B;檢視頁面，即可正確顯示頁面。

### 100%高 {#height}

頁面的內文元素不支援100%高度。

* 可以通過「拉伸」主體元素來實施全屏主體，如下所示：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 邊距折疊{#margin-collapsing}

如果主體元素的第一個子元素有邊距，則可以看到邊距折疊問題。

* 解決方案是在內文元素層級新增clearfix，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
