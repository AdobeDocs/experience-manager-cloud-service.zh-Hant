---
title: 為 EDS Forms 建立自訂元件
description: 為 EDS Forms 建立自訂元件
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 98%

---

# 在 WYSIWYG 製作中建立自訂元件

Edge Delivery Services 表單可提供自訂，讓前端開發人員可以建置量身打造的表單元件。這些自訂元件可無縫整合到 WYSIWYG 製作體驗中，使表單作者能夠在表單編輯器中輕鬆地進行新增、設定和管理。使用自訂元件，作者即可提升功能，同時可確保平順、直覺的製作流程。

本文件概述透過設定原生 HTML 表單元件的樣式來建立自訂元件的步驟，以改善使用者體驗並增加表單的視覺吸引力。

## 必要條件

在開始建立自訂元件之前，您應該：

- 對於[原生 HTML 元件](/help/edge/docs/forms/form-components.md)有基本的認識。
- 瞭解如何[使用 CSS 選擇器根據欄位類型設定表單欄位的樣式](/help/edge/docs/forms/style-theme-forms.md)

## 建立自訂元件

在通用編輯器中新增自訂元件指在設計表單時為表單作者提供新元件。這包含註冊元件、定義其屬性以及設定其使用位置。建立自訂元件的步驟包括：

[1. 為新的自訂元件新增結構](#1-adding-structure-for-new-custom-component)
[2.定義自訂元件的屬性以供製作](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3.使您的自訂元件在 WYSIWYG 元件清單中可見](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4.註冊您的自訂元件](#4-registering-your-custom-component)
[5.為自訂元件新增執行階段行為](#5-adding-the-runtime-behaviour-for-your-custom-component)

讓我們以建立名為 **range** 的新自訂元件為例。該 range 元件會顯示為一條直線，並顯示最小值、最大值或選取值等值。

![範圍元件的視覺化展現方式顯示具有最小值和最大值的滑桿，以及選定值指示器](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

在本文結束時，您會了解如何從頭開始建立自訂元件。

### &#x200B;1. 為新的自訂元件新增結構

在使用自訂元件之前，必須先進行註冊，以便通用編輯器將其識別為可用選項。這會透過元件定義實現，元件定義包括唯一識別碼、預設屬性和元件的結構。執行下列步驟以使自訂元件可用於表單製作：

1. **新增資料夾和檔案**
在 AEM 專案中為新的自訂元件新增資料夾和檔案。
   1. 開啟您的 AEM 專案並瀏覽至 `../blocks/form/components/`。
   1. 在 `../blocks/form/components/<component_name>` 為您的自訂元件新增資料夾。在此範例中，我們會建立名為 `range` 的資料夾。
   1. 瀏覽到在 `../blocks/form/components/<component_name>` 新建立的資料夾。例如，瀏覽至 `../blocks/form/components/range`，並新增下列檔案：
      - `/blocks/form/components/range/_range.json`：包含自訂元件的定義。
      - `../blocks/form/components/range/range.css`：定義自訂元件的樣式。
      - `../blocks/form/components/range/range.js`：在執行階段自訂自訂元件。

        ![新增自訂元件以供製作](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > 確保 json 檔案的檔案名稱包括底線 (_) 作為前置詞。

1. 瀏覽至 `/blocks/form/components/range/_range.json` 檔案並新增自訂元件的元件定義。

1. **新增元件定義**

   若要新增定義，需要在 `_range.json` 檔案中新增下列欄位：

   - **title**：在通用編輯器中顯示的元件的標題。
   - **id**：元件的唯一識別碼。
   - **fieldType**：表單可支援各種 **fieldType** 來擷取特定類型的使用者輸入。您可以找到[支援的 fieldType (在 Extra Byte 區段中)](#supported-fieldtypes)。
   - **resourceType**：每個自訂元件都有一個以其 fieldType 為基礎的相關聯資源類型。您可以找到[支援的 resourceType (在 Extra Byte 區段中)](#supported-resourcetype)。
   - **jcr:title**：與標題類似，但儲存在元件的結構內。
   - **fd:viewType**：表示自訂元件的名稱。這是元件的唯一識別碼。需要為元件建立自訂檢視。

新增元件定義之後的 `_range.json` 檔案如下所示：

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
> 為通用編輯器新增區塊時，所有與表單相關的元件都會遵循與 Sites 相同的方法。如需更多資訊，您可參閱「[建立經檢測適用通用編輯器的區塊](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block)」一文。

### &#x200B;2. 定義自訂元件的屬性以供製作

自訂元件包括元件模型，該模型會指定表單作者可以設定哪些屬性。這些屬性隨即會出現在通用編輯器的「**屬性**」對話框中，讓作者可以調整標籤、驗證規則、樣式和其他屬性等設定。若要定義屬性：

1. 瀏覽至 `/blocks/form/components/range/_range.json` 檔案並新增自訂元件的元件模型。

1. **新增元件模型**

   若要定義自訂元件的元件模型，您需要將相關欄位新增至 `_range.json` 檔案。

   1. **建立新模型**

      - 在模型陣列中，新增物件並設定元件模型的 `id`，以和元件定義中之前所設定的 `fd:viewType` 屬性相符。
      - 在此物件內包括欄位陣列。

   2. **定義「屬性」對話框的欄位**

      - 欄位陣列中的每個物件都應該是 container-type 元件，使其可在「**屬性**」對話框中顯示為索引標籤。
      - 部分欄位可以參照 `models/form-common` 中可用的可重複使用屬性。

   3. **使用現有元件模型作為參考**

      - 您可以複製與您選擇的 `fieldType` 對應的現有元件模型，並根據需要進行修改。例如，`number-input` 元件會經過擴展以建立 **range** 元件，以便我們可以使用來自 `models/form-components/_number-input.json` 的模型陣列作為參考。

   新增元件模型之後的 `_range.json` 檔案如下所示：

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
   > 若要將新欄位新增至自訂元件的「**屬性**」對話框，需遵守[已定義的結構描述](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model)。

   您還可以[新增自訂屬性](#adding-custom-properties-for-your-custom-component)到自訂元件來擴展其功能。

#### 為自訂元件新增自訂屬性

自訂屬性可讓您根據元件的屬性對話框中設定的值定義特定行為。這有助於擴展元件的功能和自訂選項。

在此範例中，我們將 Step Value 作為自訂屬性新增到 Range 元件。

![Step Value 自訂屬性](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

若要新增 Step Value 自訂屬性，請在 ` _<component>.json` 檔案中使用下列程式碼附加元件模型：

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

JSON 片段為 **Range** 元件定義一個名為 **Step Value** 的自訂屬性。以下是各個欄位的分項說明：

- **component**：指定「屬性」對話框中使用的輸入欄位類型。於此範例中，「`number`」表示該欄位接受數值。
- **name**：屬性的識別碼，可在元件的邏輯中用來參照屬性。此處的「`stepValue`」代表 Range 的 Step Value 設定。
- **label**：「屬性」對話框中所見到的屬性顯示名稱。
- **valueType**：定義屬性預期的資料類型。「`number`」確保僅可以輸入數值。

您現在可以將 `stepValue` 用作 JSON 屬性 `range.js` 的自訂屬性，並根據其在執行階段的數值來執行動態行為。

因此，在新增元件定義、元件模型和自訂屬性後，最終的 `_range.json` 檔案如下所示：

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

![元件定義和模型](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### &#x200B;3. 使您的自訂元件在 WYSIWYG 元件清單中可見

篩選器會定義自訂元件可以用於通用編輯器中的哪個區段。這確保了元件僅能用於適當區段，同時保持結構和可用性。

為了確保自訂元件在 WYSIWYG 表單製作過程中出現在可用元件清單中：

1. 瀏覽至 `/blocks/form/_form.json` 檔案。
1. 在具有 `id="form"` 的物件中找到元件陣列。
1. 將 `definitions[]` 中的 `fd:viewType` 值新增到 `id="form"` 物件的元件陣列。

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

### &#x200B;4. 註冊您的自訂元件

若要讓表單區塊識別自訂元件，並在表單編寫期間載入元件模型中定義的屬性，請從元件定義新增`fd:viewType`值至`mappings.js`檔案。

若要註冊元件：

1. 瀏覽至 `/blocks/form/mappings.js` 檔案。
1. 找到 `customComponents[]` 陣列。
1. 將 `definitions[]` 陣列中的 `fd:viewType` 值新增到 `customComponents[]` 陣列。

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

完成上述步驟後，自訂元件隨即會出現在通用編輯器內的表單元件清單中。然後您即可將其拖曳到表單區段。

![通用編輯器元件面板的螢幕擷圖顯示可拖放至表單中的自訂範圍元件](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

下方的螢幕擷圖顯示 `range` 元件的屬性已新增至元件模型中，並指定表單製作者可以設定的屬性：

![通用編輯器屬性面板的螢幕擷圖顯示可設定的範圍元件設定，包括基本屬性、驗證規則及樣式選項](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

您現在可以透過新增樣式和功能來定義自訂元件的執行階段行為。

### &#x200B;5. 為自訂元件新增執行階段行為

您可以使用預先定義標記來修改自訂元件，如「[表單欄位的樣式](/help/edge/docs/forms/style-theme-forms.md)」中的說明。這可以透過自訂 CSS (階層式樣式表) 和自訂程式碼來實現，以美化元件的外觀。若要為元件新增執行階段行為：

1. 若要新增樣式，請瀏覽至 `/blocks/form/components/range/range.css` 檔案，並新增下列程式碼：

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% - var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% - var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /- Dark Blue */
   border: 3px solid #00008B; /- Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /- Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /- Dark Blue */
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

1. 若要新增功能，請瀏覽至 `/blocks/form/components/range/range.js` 檔案，並新增下列程式碼：

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
   const left = `${(current / total) - 100}% - ${(current / total) - bubbleWidth}px`;
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

   這會控制自訂元件如何與使用者輸入互動、處理資料以及和通用編輯器中的表單區塊整合。

   合併自訂樣式和功能後，range 元件的外觀和行為即會提升。更新後的設計會反映套用後的樣式，而新增的功能則可確保更動態和互動的使用者體驗。
下列螢幕擷圖提供更新後 range 元件的圖解。

![最終實際應用的範圍元件，顯示在通用編輯器中具有數值氣泡圖形且有樣式設計的滑桿以及互動功能](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## 常見問題

- **如果我要在 component.css 和 forms.css 中新增樣式，優先考慮哪一個？**
在 `component.css` 和 **forms.css** 中都有定義樣式時，優先考慮 `component.css`。這是因為元件層級樣式更為具體，並會覆寫 `forms.css` 的全域樣式。

- **我的自訂元件在通用編輯器中的可用元件清單中不可見。我要如何修正這個問題？**
如果您的自訂元件未出現，請檢查下列檔案，以確保元件已正確註冊：
   - **component-definition.json**：確認元件已正確定義。
   - **component-filters.json**：確保在適當區段中可允許該元件。
   - **component-models.json**：確認元件模型已正確設定。

## 最佳做法

- 建議您[設定本機 AEM 開發環境](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment)，以在本機開發自訂樣式和元件。


## Extra Byte

### 支援的 resourceType

| 欄位類型 | 資源類型 |
|--------------|------------------------------------------------------------------|
| 文字輸入 | core/fd/components/form/textinput/v1/textinput |
| 數字輸入 | core/fd/components/form/numberinput/v1/numberinput |
| 日期輸入 | core/fd/components/form/datepicker/v1/datepicker |
| 面板 | core/fd/components/form/panelcontainer/v1/panelcontainer |
| 核取方塊 | core/fd/components/form/checkbox/v1/checkbox |
| 下拉式清單 | core/fd/components/form/dropdown/v1/dropdown |
| 單選按鈕群組 | core/fd/components/form/radiobutton/v1/radiobutton |
| 純文字 | core/fd/components/form/text/v1/text |
| 檔案輸入 | core/fd/components/form/fileinput/v2/fileinput |
| 電子郵件 | core/fd/components/form/emailinput/v1/emailinput |
| 影像 | core/fd/components/form/image/v1/image |
| 按鈕 | core/fd/components/form/button/v1/button |

### 支援的 fieldTypes

表單支援的 fieldTypes 包括：

- 文字輸入
- 數字輸入
- 日期輸入
- 面板
- 核取方塊
- 下拉式清單
- 單選按鈕群組
- 純文字
- 檔案輸入
- 電子郵件
- 影像
- 按鈕

