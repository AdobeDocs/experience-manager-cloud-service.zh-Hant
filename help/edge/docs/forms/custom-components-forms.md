---
title: 為 EDS Forms 建立自訂元件
description: 為 EDS Forms 建立自訂元件
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# 建立自訂元件

AEM FormsEdge Delivery Services可讓您自訂[原生HTML表單元件](/help/edge/docs/forms/form-components.md)，並建立好記且互動式的表單。 它可讓您使用預先定義的標籤來修改表單元件，如表單欄位的[樣式](/help/edge/docs/forms/style-theme-forms.md)中所述，使用自訂CSS （階層式樣式表）和自訂程式碼來裝飾元件，進而增強最適化Forms區塊中表單欄位的外觀。

![自訂元件](/help/edge/assets/custom-component-image.png)

本檔案概述如何透過設計原生HTML表單元件的樣式來建立自訂元件，以改善使用者體驗並提高表格的視覺吸引力。

讓我們舉一個在表單上顯示`Estimated trip cost`的`range`元件為例。 `range`元件會以直線顯示，不會顯示任何值，例如最小值、最大值或選取的值。

![原生範圍元件](/help/edge/assets/native-range-component.png)

讓我們開始自訂`range`欄位，以使用CSS新增樣式並新增自訂函式來裝飾元件，藉此顯示行上的最小、最大和選定值。

![自訂範圍元件](/help/edge/assets/custom-range-component.png)

本文結束時，您將瞭解如何在CSS檔案和自訂函式中新增樣式，以建立自訂元件。

## 必要條件

開始建立自訂元件之前，您應該：

* 具備[原生HTML元件](/help/edge/docs/forms/form-components.md)的基本知識。
* 瞭解如何使用CSS選取器根據欄位型別[樣式化表單欄位](/help/edge/docs/forms/style-theme-forms.md)


## 建立自訂元件


建立自訂元件的![步驟](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

現在來詳細瞭解每個步驟。

請參考[查詢試算表](/help/edge/docs/forms/assets/enquiry.xlsx)以自訂`range`元件，請遵循以下說明的步驟。

### 新增自訂函式以裝飾元件

在`[../Form Block/components]`中新增的自訂函式包含：

* **函式宣告**：定義函式名稱及其引數。
* **邏輯實作**：寫入邏輯以新增元件的自訂行為。
* **函式匯出**：讓函式可在`[Form Block]`中存取。

讓我們建立名為`range.js`的JavaScript檔案來設定範圍元件的樣式。 若要新增自訂函式：

1. 前往Google Drive或SharePoint上的AEM專案資料夾。
1. 瀏覽至`[../Form Block/components]`。
1. 新增名為`range.js`的新檔案。
1. 新增下列程式碼行：

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

### 在表單區塊中插入裝飾程式

`[Form Block]`使用語意HTML來轉譯表單欄位，包括輸入欄位、標籤和說明文字，以及協助工具的標準屬性。 若要讓`[Form Block]`為指定的元件使用自訂裝飾程式，請在`mappings.js`檔案中定義它。 `mappings.js`檔案匯入的函式會傳回負責裝飾特定元件的模組。 此函式接受欄位屬性並傳回表單欄位的裝飾器函式。

在此案例中，函式會檢查欄位的`fieldType`屬性，並從`[../Form Block/components]`中存在的`range.js`檔案傳回自訂範圍裝飾程式。

若要在表單區塊中插入裝飾器：

1. 前往`[../Form Block/]`並開啟`mapping.js`。
1. 新增下列程式碼行：

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default;
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. 儲存變更。

### 在CSS檔案中新增元件的樣式

您可以使用CSS選取器，根據欄位型別和欄位名稱變更表單欄位的外觀，以根據需求允許一致或唯一的樣式。 若要設定元件的樣式，請在`form.css`檔案中新增程式碼，以修改表單元件的外觀。

若要自訂`range`元件的樣式，請在表單中加入CSS程式碼片段，以便為`range`輸入元素及其相關元件設定樣式。 這會假設結構化HTML配置具有類別，例如`.form`和`.range-wrapper`。

若要在CSS檔案中為元件新增樣式：
1. 前往`[../Form Block/]`並開啟`form.css`。
1. 新增下列程式碼行：

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

將更新的`range.js`、`mapping.css`和`form.css`檔案部署至您的GitHub專案，並驗證建置是否成功。

### 使用AEM Sidekick預覽表單

使用[AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)，使用新實作的函式預覽`range`元件的樣式。

![自訂元件表單](/help/edge/assets/custom-componet-form.png)

`range`元件的新樣式會使用CSS和包含元件裝飾器的自訂函式新增樣式，以顯示線條上的最小、最大和選取值。


## 另請參閱

{{see-more-forms-eds}}



