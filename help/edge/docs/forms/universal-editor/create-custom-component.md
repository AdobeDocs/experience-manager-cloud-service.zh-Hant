---
title: 為 EDS Forms 建立自訂元件
description: 為 EDS Forms 建立自訂元件
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d71c5d6488935de4a02c8d3828f287542b979d0f
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 5%

---


# 在WYSIWYG製作中建立自訂元件

Edge Delivery Services Forms提供自訂功能，可讓前端開發人員建立自訂的表單元件。 這些自訂元件可順暢地整合至WYSIWYG製作體驗，讓表單作者可在表單編輯器中輕鬆新增、設定和管理這些元件。 藉由自訂元件，作者可增強功能，同時確保製作程式順暢且直覺。

本文件概述透過設定原生 HTML 表單元件的樣式來建立自訂元件的步驟，以改善使用者體驗並增加表單的視覺吸引力。

## 必要條件

在開始建立自訂元件之前，您應該：

* 對於[原生 HTML 元件](/help/edge/docs/forms/form-components.md)有基本的認識。
* 瞭解如何[使用 CSS 選擇器根據欄位類型設定表單欄位的樣式](/help/edge/docs/forms/style-theme-forms.md)

## 建立自訂元件

在通用編輯器中新增自訂元件，表示讓表單作者可在設計表單時使用新元件。 這需要註冊元件、定義其屬性，以及設定可在何處使用它。 建立自訂元件的步驟如下：

[1. 正在加入新自訂元件](#1-adding-structure-for-new-custom-component)的結構
[2。 定義用於編寫](#2-defining-the-properties-of-your-custom-component-for-authoring)的自訂元件屬性
[3。  讓您的自訂元件顯示在WYSIWYG元件清單中](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4。 正在登入您的自訂元件](#4-registering-your-custom-component)
[5。 正在新增自訂元件](#5-adding-the-runtime-behaviour-for-your-custom-component)的執行階段行為

讓我們以建立名為&#x200B;**range**&#x200B;的新自訂元件為例。 範圍元件會顯示為直線，並顯示最小值、最大值或選取值等值。

![範圍元件樣式](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

在本文結束時，您將瞭解如何從頭開始建立自訂元件。

### 1.新增新自訂元件的結構

您必須先註冊自訂元件，以便Universal Editor將其辨識為可用選項，才能使用該自訂元件。 這是透過元件定義來達成，該定義包含唯一識別碼、預設屬性和元件結構。執行下列步驟，讓自訂元件可用於表單撰寫：

1. **新增資料夾和檔案**
在AEM專案中為新的自訂元件新增資料夾和檔案。
   1. 開啟您的AEM專案，並導覽至`../blocks/form/components/`。
   1. 在`../blocks/form/components/<component_name>`為您的自訂元件新增資料夾。 在此範例中，我們會建立名為`range`的資料夾。
   1. 導覽至`../blocks/form/components/<component_name>`新建立的資料夾。 例如，瀏覽至`../blocks/form/components/range`，然後新增下列檔案：
      * `/blocks/form/components/range/_range.json`：包含自訂元件的定義。
      * `../blocks/form/components/range/range.css`：定義自訂元件的樣式。
      * `../blocks/form/components/range/range.js`：在執行階段自訂自訂元件。

        ![正在新增用於編寫的自訂元件](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > 請確定json檔案的檔案名稱中包含底線(_)當作首碼。

1. 導覽至`/blocks/form/components/range/_range.json`檔案，並新增自訂元件的元件定義。

1. **新增元件定義**

   若要新增定義，`_range.json`檔案中必須新增的欄位為：

   * **title**：在通用編輯器中顯示的元件標題。
   * **id**：元件的唯一識別碼。
   * **fieldType**： Forms支援各種&#x200B;**fieldType**，以擷取特定型別的使用者輸入。 您可以在[額外位元組]區段](#supported-fieldtypes)中找到[支援的fieldType。
   * **resourceType**：每個自訂元件都有根據其fieldType的關聯資源型別。 您可以在[額外位元組]區段](#supported-resourcetype)中找到[支援的resourceType。
   * **jcr：title**：它類似於標題，但儲存在元件的結構中。
   * **fd：viewType**：它代表自訂元件的名稱。 這是元件的唯一識別碼。 必須為元件建立自訂檢視。

新增元件定義後，`_range.json`檔案如下：

```javascript
{
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ]
}
```

>[!NOTE]
>
> 將區塊新增至通用編輯器時，所有表單相關元件會遵循與Sites相同的方法。 如需詳細資訊，請參考[Creating Blocks Instrumented for use with the Universal Editor](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block)一文。

### 2.定義用於編寫的自訂元件的屬性

自訂元件包括元件模型，指定哪些屬性可由表單作者設定。 這些屬性會顯示在Universal Editor的&#x200B;**屬性**&#x200B;對話方塊中，可讓作者調整標籤、驗證規則、樣式和其他屬性等設定。 若要定義屬性，請執行下列動作：

1. 導覽至`/blocks/form/components/range/_range.json`檔案，並為自訂元件新增元件模型。

1. **新增元件模型**

   若要定義自訂元件的元件模型，您必須將相關欄位新增至`_range.json`檔案。

   1. **建立新模型**

      * 在模型陣列中，新增物件並設定元件模型的`id`以符合元件定義中先前設定的`fd:viewType`屬性。
      * 在此物件中包含欄位陣列。

   2. **定義屬性對話方塊的欄位**

      * 欄位陣列中的每個物件都應該是一個容器型別元件，以便在&#x200B;**屬性**&#x200B;對話方塊中顯示為索引標籤。
      * 某些欄位可參照`models/form-common`中可用的可重複使用屬性。

   3. **使用現有的元件模型作為參考**

      * 您可以複製與您所選`fieldType`對應的現有元件模型的內容，並視需要加以修改。 例如，`number-input`元件已延伸以建立&#x200B;**範圍**&#x200B;元件，因此我們可以從`models/form-components/_number-input.json`使用模型陣列作為參考。

   新增元件模型後的`_range.json`檔案如下：

   ```javascript
   "models": [
   {
     "id": "range",
     "fields": [
       {
         "component": "container",
         "name": "basic",
         "label": "Basic",
         "collapsible": false,
         "...": "../../../../models/form-common/_basic-input-fields.json"
       },
       {
         "...": "../../../../models/form-common/_help-container.json"
       },
       {
         "component": "container",
         "name": "validation",
         "label": "Validation",
         "collapsible": true,
         "...": "../../../../models/form-common/_number-validation-fields.json"
       }
     ]
   }
   ]
   ```
   >[!NOTE]
   >
   > 若要新增欄位到自訂元件的&#x200B;**屬性**&#x200B;對話方塊，請遵循[定義的結構描述](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model)。

   您也可以[新增自訂屬性](#adding-custom-properties-for-your-custom-component)至自訂元件，以擴充其功能。

#### 新增自訂元件的自訂屬性

自訂屬性可讓您根據元件的「屬性」對話方塊中設定的值來定義特定行為。 這有助於擴充元件的功能和自訂選項。

在此範例中，我們將「步驟值」作為自訂屬性新增到Range元件中。

![步驟值自訂屬性](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

若要新增Step Value自訂屬性，請在` _<component>.json`檔案中附加元件模型，並使用下列幾行程式碼：

```javascript
    {
    "component": "number",
    "name": "stepValue",
    "label": "Step Value",
    "valueType": "number"
    }
    ```
The JSON snippet defines a custom property called **Step Value** for a **Range** component. Below is a breakdown of each field:

* **component**: Specifies the type of input field used in the Property dialog. In this case, `number` indicates that the field accepts numeric values.
* **name**: The identifier for the property, used to reference it in the component’s logic. Here, the `stepValue` represents the step value setting for the range.
* **label**: The display name of the property as seen in the Property dialog. 
* **valueType**: Defines the data type expected for the property. The `number` ensures that only numeric inputs are allowed.

You can now use `stepValue` as a custom property in the JSON properties of `range.js` and implement dynamic behavior based on its value at runtime.

Hence, the final `_range.json` file, after adding the component definition, component model and custom properties, is as follows:

```javascript
 {
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ],
  "models": [
    {
      "id": "range",
      "fields": [
        {
          "component": "container",
          "name": "basic",
          "label": "Basic",
          "collapsible": false,
          "...": "../../../../models/form-common/_basic-input-fields.json"
         {
           "component": "number",
           "name": "stepValue",
            "label": "Step Value",
             "valueType": "number"
}
        },
        {
          "...": "../../../../models/form-common/_help-container.json"
        },
        {
          "component": "container",
          "name": "validation",
          "label": "Validation",
          "collapsible": true,
          "...": "../../../../models/form-common/_number-validation-fields.json"
        }
      ]
    }
  ]
}
```

![元件定義與模型](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### 3.在WYSIWYG元件清單中顯示自訂元件

篩選器會定義自訂元件可在通用編輯器中使用的區段。 這樣可確保元件僅能在適當的區段中使用，並保持結構和可用性。

若要確保自訂元件在WYSIWYG表單製作期間會顯示在可用元件清單中：

1. 瀏覽至`/blocks/form/_form.json`檔案。
1. 在具有`id="form"`的物件中找出元件陣列。
1. 從`definitions[]`將`fd:viewType`值新增至具有`id="form"`之物件的元件陣列。

```javascript
 "filters": [
    {
      "id": "form",
      "components": [
        "captcha",
        "checkbox",
        "checkbox-group",
        "date-input",
        "drop-down",
        "email",
        "file-input",
        "form-accordion",
        "form-button",
        "form-fragment",
        "form-image",
        "form-modal",
        "form-reset-button",
        "form-submit-button",
        "number-input",
        "panel",
        "plain-text",
        "radio-group",
        "rating",
        "telephone-input",
        "text-input",
        "tnc",
        "wizard",
        "range"
      ]
    }
  ]
```

![元件篩選器](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### 4.註冊您的自訂元件

若要讓表單區塊識別自訂元件，並在表單編寫期間載入元件模型中定義的屬性，請從元件定義新增`fd:viewType`值至`mappings.js`檔案。
註冊元件：
1. 瀏覽至`/blocks/form/mappings.js`檔案。
1. 找到`customComponents[]`陣列。
1. 從`definitions[]`陣列新增`fd:viewType`值至`customComponents[]`陣列。

```javascript
let customComponents = ["range"];
const OOTBComponentDecorators = ['file-input',
                                 'wizard', 
                                 'modal', 'tnc',
                                'toggleable-link',
                                'rating',
                                'datetime',
                                'list',
                                'location',
                                'accordion'];
```

![元件對應](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

完成上述步驟後，自訂元件會出現在通用編輯器的表單元件清單中。 然後您可以將其拖放到表單區段中。

![範圍元件](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

您現在可以透過新增樣式和功能來定義自訂元件的執行階段行為。

### 5.新增自訂元件的執行階段行為

您可以使用預先定義的標示來修改自訂元件，如表單欄位[樣式](/help/edge/docs/forms/style-theme-forms.md)中所述。 這可透過自訂CSS （階層式樣式表）和自訂程式碼來完成，以增強元件的外觀。 若要新增元件的執行階段行為：

1. 若要新增樣式，請導覽至`/blocks/form/components/range/range.css`檔案並新增下列程式碼行：

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /* Dark Blue */
   border: 3px solid #00008B; /* Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /* Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /* Dark Blue */
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   font-weight: bold;
   }
   
   .range-widget-wrapper.decorated .range-min,
   .range-widget-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-widget-wrapper.decorated .range-max {
   float: right;
   }
   ```
   程式碼可協助您定義自訂元件的樣式和視覺外觀。

1. 若要新增功能，請瀏覽至`/blocks/form/components/range/range.js`檔案並新增下列程式碼行：

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
       '--total-steps': Math.ceil((max - min) / step),
       '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   
   export default async function decorate(fieldDiv, fieldJson) {
   console.log('RANGE DIV: ', fieldDiv);
   console.log('RANGE JSON: fieldJson', fieldJson);
    const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 10;
   input.max = input.max || 1000;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper decorated';
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
   return fieldDiv;
   }
   ```

   它會控制自訂元件與使用者輸入互動、處理資料以及與通用編輯器中的表單區塊整合的方式。

   結合自訂樣式和功能後，範圍元件的外觀和行為會增強。 更新後的設計會反映套用的樣式，而新增的功能可確保提供更動態、互動式的使用者體驗。
以下熒幕擷圖說明更新的範圍元件。

![範圍元件樣式](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## 常問的問題

* **如果我同時在component.css和forms.css中新增樣式，哪一個優先？**
同時在`component.css`和&#x200B;**forms.css**&#x200B;中定義樣式時，`component.css`優先順序。 這是因為元件層級樣式比較具體，而且會覆寫來自`forms.css`的全域樣式。

* **我的自訂元件在通用編輯器的可用元件清單中不可見。 如何解決此問題？**
如果您的自訂元件未出現，請檢查以下檔案，確保元件已正確註冊：
   * **component-definition.json**：確認元件已正確定義。
   * **component-filters.json**：請確定在適當的區段中允許該元件。
   * **component-models.json**：確認元件模型已正確設定。

## 最佳做法

* 建議[設定本機AEM開發環境](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment)，以便在本機開發自訂樣式和元件。


## 額外的位元組

### 支援的resourceType

| 欄位型別 | 資源類型 |
|--------------|------------------------------------------------------------------|
| 文字輸入 | core/fd/components/form/textinput/v1/textinput |
| 數字輸入 | core/fd/components/form/numberinput/v1/numberinput |
| 日期輸入 | core/fd/components/form/datepicker/v1/datepicker |
| 面板 | core/fd/components/form/panelcontainer/v1/panelcontainer |
| 核取方塊 | core/fd/components/form/checkbox/v1/checkbox |
| 下拉式清單 | core/fd/components/form/dropdown/v1/dropdown |
| radio-group | core/fd/components/form/radiobutton/v1/radiobutton |
| 純文字 | core/fd/components/form/text/v1/text |
| 檔案輸入 | core/fd/components/form/fileinput/v2/fileinput |
| 電子郵件 | core/fd/components/form/emailinput/v1/emailinput |
| 影像 | core/fd/components/form/image/v1/image |
| 按鈕 | core/fd/components/form/button/v1/button |

### 支援的fieldType

表單支援的fieldTypes包括：
* 文字輸入
* 數字輸入
* 日期輸入
* 面板
* 核取方塊
* 下拉式清單
* radio-group
* 純文字
* 檔案輸入
* 電子郵件
* 影像
* 按鈕

## 另請參閱

{{see-more-forms-eds}}