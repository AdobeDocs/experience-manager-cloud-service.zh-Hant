---
title: 記錄檔案中支援的HTML標籤標籤
description: 產生記錄檔案現在支援HTML標籤標籤的參考指南，包括演算行為和協助工具考量事項
feature: Adaptive Forms
role: Developer, User
exl-id: 8481b0dc-aae7-4bd2-acfe-1f1b6d747683
source-git-commit: 1794ed6cac612ee4600c2f8e1ced18c6130b64a2
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 8%

---


# 記錄檔案中支援的HTML標籤標籤

## 此參考資料涵蓋哪些內容？

產生記錄檔案(DoR) PDF時，AEM Forms現在支援RTF欄位中的HTML標籤標籤。 本指南說明哪些HTML標籤標籤可以在最適化Forms中安全使用，以及這些標籤如何在產生的檔案中呈現。

如果您在表單中新增RTF內容（例如粗體格式、清單或連結），請務必瞭解支援的標籤及其限制。 此參考可協助您選擇適當的標籤，以確保您的內容可正確顯示並在記錄檔案中持續可供存取。

## 開始之前

### 先決條件

您應該熟悉：

- 基本HTML標籤語法
- [記錄檔案基本知識](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- 協助工具原則及WCAG准則
- PDF協助工具需求
- 接受HTML標籤的最適化表單元件

### 考量事項

記錄檔案(DoR)可以是已標籤的PDF，這有助於確保輔助技術的協助工具與正確結構。 若要啟用標籤的PDF輸出，[請將XCI屬性`config/present/pdf/tagged`設定為`true`](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file)。 產生PDF後，請務必確認協助工具標籤已正確套用。 您可以使用[Adobe Acrobat來檢查協助工具標籤](https://helpx.adobe.com/in/acrobat/using/create-verify-pdf-accessibility.html)，並確保您的檔案符合協助工具標準。

### 新增功能

記錄檔案支援RTF文字是最近的增強功能。 以前，RTF內容在產生的檔案中會顯示為純文字。 這項新功能可讓格式化內容在PDF輸出中正確呈現。

## HTML標籤支援參考

### 完全支援的標籤

建立適當的協助工具節點可完全支援這些標籤：

| HTML標籤 | 說明 | 記錄檔案支援 | 協助工具 | 範例 |
|----------|-------------|-------------|---------------|---------|
| `<p>` | 段落 | 是 | 完全支援 — 正確`<P>`節點 | `<p>This is a paragraph.</p>` |
| `<br/>` | 分行符號 | 是 | 完全支援 — `<P>`節點內 | `<p>Line 1<br/>Line 2</p>` |
| `<b>` | 粗體文字 | 是 | 完全支援 — `<P>`節點內 | `<b>bold text</b>` |
| `<i>` | 斜體文字 | 是 | 完全支援 — `<P>`節點內 | `<i>italic text</i>` |
| `<span>` | 通用內嵌容器 | 是 | 在區塊元素內 | `<span>styled text</span>` |
| `<sub>` | 下標 | 是 | 完全支援 — 在區塊元素內 | `H<sub>2</sub>O` |
| `<sup>` | 上標 | 是 | 完全支援 — 在區塊元素內 | `E=mc<sup>2</sup>` |
| `<a>` | 超連結 | 是 | 支援有限 — 需要適當的巢狀結構 | `<a href="url">link text</a>` |


#### 清單協助工具問題

目前的清單演算會建立`<P>`個節點，而非適當的清單結構：

```
Current: <P>1. First item
Current: <P>2. Second item

Expected: <L>
Expected:   <LI>
Expected:     <LBL>1.
Expected:     <LBody>First item
```

### 不支援的標籤

這些標籤不受支援，且將無法正確呈現：

| HTML標籤 | 說明 | 替代解決方案 |
|----------|-------------|---------------------|
| `<h1>` - `<h6>` | 標題標籤 | 使用樣式化的`<p>`標籤或設計層級標頭 |
| `<img>` | 影像 | 使用個別影像欄位或設計範本 |
| `<code>` | 程式碼區塊 | 使用等寬字型搭配`<span>`樣式 |
| `<blockquote>` | 區塊引號 | 使用具有縮排的樣式`<p>`標籤 |
| `<table>` | 表格 | 使用最適化表單元件 |

## 程式碼範例

### 基本文字格式

```html
<!--  Supported - renders correctly -->
<p>This paragraph contains <b>bold text</b> and <i>italic text</i>.</p>

<!--  Supported - combined formatting -->
<p>This text is <i><b>bold and italic</b></i>.</p>

<!--  Unsupported - headings don't work -->
<h1>This won't render as a heading</h1>
```

### 清單

```html
<!-- ⚠️ Partially supported - renders but not accessible -->
<ol>
  <li>First numbered item</li>
  <li>Second numbered item</li>
</ol>

<ul>
  <li>First bullet point</li>
  <li>Second bullet point</li>
</ul>
```

### 連結

```html
<!--  Supported - but must be within block elements -->
<p>Visit our <a href="https://example.com">website</a> for more information.</p>

<!--  Incorrect - link not properly nested -->
<a href="https://example.com">Standalone link</a>
```

### 科學記號

```html
<!--  Supported - but limited accessibility -->
<p>Water formula: H<sub>2</sub>O</p>
<p>Einstein's equation: E=mc<sup>2</sup></p>
```

## 相關內容


- [為最適化表單產生記錄文件](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- [產生核心元件的記錄檔案](/help/forms/generate-document-of-record-core-components.md)
- [記錄檔案範本自訂](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record)

