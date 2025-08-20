---
title: 為 EDS Forms 建立自訂元件
description: 為 EDS Forms 建立自訂元件
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '623'
ht-degree: 100%

---

# 建立自訂元件

AEM Forms 適用的 Edge Delivery Services 讓您可以自訂[原生 HTML 表單元件](/help/edge/docs/forms/form-components.md)，並建立容易使用的互動式表單。它讓您能使用預先定義標記修改表單元件，如[表單欄位樣式](/help/edge/docs/forms/style-theme-forms.md)所述，使用自訂 CSS (階層樣式表) 和自訂程式碼來裝飾元件，進而增強最適化 Forms 區塊中表單欄位外觀。

![自訂元件](/help/edge/assets/custom-component-image.png)

本文件概述透過設定原生 HTML 表單元件的樣式來建立自訂元件的步驟，以改善使用者體驗並增加表單的視覺吸引力。

我們以在表單上顯示 `Estimated trip cost` 的 `range` 元件為例。`range` 元件顯示為一條直線，不顯示任何值，例如最小值、最大值或選取值。

![原生範圍元件](/help/edge/assets/native-range-component.png)

首先，使用 CSS 新增樣式並新增自訂函數來裝飾元件，開始自訂 `range` 欄位以顯示行上的最小值、最大值和選定值。

![自訂範圍元件](/help/edge/assets/custom-range-component.png)

在本文結束時，您將學會在 CSS 檔案和自訂函數中新增樣式來建立自訂元件。

## 必要條件

在開始建立自訂元件之前，您應該：

- 對於[原生 HTML 元件](/help/edge/docs/forms/form-components.md)有基本的認識。
- 瞭解如何[使用 CSS 選擇器根據欄位類型設定表單欄位的樣式](/help/edge/docs/forms/style-theme-forms.md)


## 建立自訂元件


![建立自訂元件的步驟](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

現在，我們來詳細瞭解每個步驟。

<!--Refer to the [enquiry spreadsheet](/help/edge/docs/forms/assets/enquiry.xlsx) to customize the `range` component, by following the steps as explained below.-->

### 新增自訂函數以裝飾元件

`[../Form Block/components]` 中新增的自訂函數包括：

- **函數宣告**：定義函數名稱及其參數。
- **邏輯實作**：寫入邏輯，新增元件的自訂行為。
- **函數匯出**：讓函數在 `[Form Block]` 中可供存取。

若要新增自訂函數：

1. 瀏覽至 `[../Form Block/components]`。
1. 找到一個名為 `range.js` 的檔案。如果不存在，則建立一個。
1. 新增以下程式碼行：

   ```javascript
   function updateBubble(input, element) {
   const step = input.step || 1;
   const max = input.max || 0;
   const min = input.min || 1;
   const value = input.value || 1;
   const current = Math.ceil((value - min) / step);
   const total = Math.ceil((max - min) / step);
   const bubble = element.querySelector('.range-bubble');
   // during initial render the width is 0. Hence using a default here.
   const bubbleWidth = bubble.getBoundingClientRect().width || 31;
   const left = `${(current / total) * 100}% - ${(current / total) * bubbleWidth}px`;
   bubble.innerText = `${value}`;
   const steps = {
   '--total-steps': Math.ceil((max - min) /    step),
   '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   // eslint-disable-next-line no-unused-vars
   export default function decorateRange(fieldDiv, field) {
   loadCSS('/blocks/form/components/range/range.css');
   const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 1;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper';
   input.after(div);
   const hover = document.createElement('span');
   hover.className = 'range-bubble';
   const rangeMinEl = document.createElement('span');
   rangeMinEl.className = 'range-min';
   const rangeMaxEl = document.createElement('span');
   rangeMaxEl.className = 'range-max';
   rangeMinEl.innerText = `${input.min || 1}`;
   rangeMaxEl.innerText = `${input.max}`;
   div.appendChild(hover);
   // move the input element within the wrapper div
   div.appendChild(input);
   div.appendChild(rangeMinEl);
   div.appendChild(rangeMaxEl);
   input.addEventListener('input', (e) => {
       updateBubble(e.target, div);
   });
   updateBubble(input, div);
   // as a best practice add a custom css class to apply custom styling
   fieldDiv.classList.add('decorated');
   return fieldDiv;    
   }
   ```

1. 儲存變更。

### 將裝飾器插入表單區塊中

`[Form Block]` 使用語義 HTML 來呈現表單欄位，包括輸入欄位、標籤和說明文字，且具有標準屬性以方便取用。若要讓 `[Form Block]` 對指定元件使用自訂裝飾器，請在 `mappings.js` 檔案中定義。`mappings.js` 檔案匯入一個函數，該函數會傳回負責裝飾特定元件的模組。此函數取得欄位屬性並傳回表單欄位的裝飾器函數。

在我們的案例中，該函數檢查欄位的 `fieldType` 屬性，並從 `[../Form Block/components]` 中的 `range.js` 檔案傳回自訂範圍裝飾器。

若要將裝飾器插入表單區塊中：

1. 前往 `[../Form Block/]` 並開啟 `mapping.js`。
1. 新增以下程式碼行：

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default(element,fd);
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. 儲存變更。

### 在 CSS 檔案中新增元件的樣式

您可以用 CSS 選擇器，根據欄位類型和欄位名稱設定表單欄位的外觀，依據需求呈現一致或獨特的樣式。若要設定元件樣式，請在 `form.css` 檔案中新增程式碼，以修改表單元件的外觀。

若要自訂 `range` 元件的樣式，請加入一個 CSS 程式碼片段，用於設定表單中 `range` 輸入元素及其關聯元件的樣式。這裡假設一個結構化的 HTML 版面配置，其中包含  `.form`  和  `.range-wrapper` 等類別。

若要在 CSS 檔案中加入元件的樣式：

1. 前往 `[../Form Block/]` 並開啟 `form.css`。
1. 新增以下程式碼行：

   ```javascript
       /** styling for range */
   main .form .range-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, var(--button-primary-color) calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #fff;
   border: 3px solid var(--button-primary-color);
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: var(--button-primary-color);
   }
   
   .range-wrapper.decorated .range-bubble {
   color: #17252e;
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   }
   
   .range-wrapper.decorated .range-min,
   .range-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-wrapper.decorated .range-max {
   float: right;
   }
   ```

1. 儲存變更。

### 部署檔案並建置專案

部署已更新的 `range.js`、`mapping.js` 和 `form.css` 檔案到您的 GitHub 專案，並驗證建置是否成功。

### 使用 AEM Sidekick 預覽表單

使用新實作的函數預覽您的表單，該函數可為 `range` 元件設定樣式。

![自訂元件樣式](/help/edge/assets/custom-componet-form.png)

`range` 元件的新樣式透過使用 CSS 新增樣式和包含元件裝飾器的自訂函數，顯示行上的最小值、最大值和選取值。


