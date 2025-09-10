---
title: 為 EDS Forms 建立自訂元件
description: 為 EDS Forms 建立自訂元件
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 1d59791561fc6148778adccab902c8e727adc641
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 4%

---


# 在調適型表單區塊中建立自訂表單元件

Edge Delivery Services 表單可提供自訂，讓前端開發人員可以建置量身打造的表單元件。這些自訂元件可無縫整合到 WYSIWYG 製作體驗中，使表單作者能夠在表單編輯器中輕鬆地進行新增、設定和管理。使用自訂元件，作者即可提升功能，同時可確保平順、直覺的製作流程。

本文件概述透過設定原生 HTML 表單元件的樣式來建立自訂元件的步驟，以改善使用者體驗並增加表單的視覺吸引力。

## 架構概觀

Forms區塊的自訂元件遵循&#x200B;**MVC （模型 — 檢視 — 控制器）**&#x200B;架構模式：

### 模型

- 由每個`field/component`的JSON結構描述定義。

- 可編寫的屬性會在對應的JSON檔案中指定（請參閱區塊/表單/模型/表單元件）。

- 這些屬性可供表單產生器中的作者使用，並作為欄位定義(fd)的一部分傳遞至元件。

### 檢視

- 各欄位型別的HTML結構在form-field-types中有說明。

- 這是可延伸或修改之元件的基礎結構。

- 各個OOTB元件的基本HTML結構會以表單欄位型別記錄。

### 控制器/元件邏輯

- 以OOTB （現成可用）或自訂元件的形式在JavaScript中實作。   — 位於自訂元件的`blocks/form/components`。

## OOTB元件

**OOTB （現成可用）**&#x200B;元件為自訂開發提供基礎：

- OOTB元件位於`blocks/form/models/form-components`。

- 每個OOTB元件都有定義其可編寫屬性（例如，` _text-input.json`，`_drop-down.json`）的JSON檔案。

- 這些屬性可供表單產生器中的作者使用，並作為欄位定義(fd)的一部分傳遞至元件。

- 各個OOTB元件的基本HTML結構會以表單欄位型別記錄。

擴充現有的OOTB元件可讓您重複使用其基本結構、行為和屬性，同時自訂它以符合您的需求。

- 自訂元件必須從預先定義的OOTB元件集延伸。

- 系統會根據欄位JSON中的`viewType`屬性識別要擴充的OOTB元件。

- 系統會維護允許的自訂元件變體的登入。 只能使用此登入中列出的變體，例如`customComponents[]`中的`mappings.js`。

- 轉譯表單時，系統會檢查變體屬性或`:type/fd:viewType`，如果它符合已註冊的自訂元件，則會從`blocks/form/components`資料夾載入對應的JS和CSS檔案。

- 自訂元件隨後會套用至OOTB元件的基本HTML結構，好讓您增強或覆寫其行為和外觀。

## 自訂元件的結構

若要建立自訂元件，您可以使用&#x200B;**Scaffolder CLI**&#x200B;來設定元件所需的檔案和資料夾，然後新增自訂元件的程式碼。

- 自訂元件位於`blocks/form/components`資料夾中。

- 每個自訂元件都必須放在自己的資料夾中，以元件命名，例如卡片。 在資料夾中，下列檔案應該是：

   - **_cards.json** — 延伸OOTB元件定義的JSON檔案，定義其可編寫的屬性（模型[]）和載入時的內容結構（定義[]）。
   - **cards.js** — 包含主要邏輯的JavaScript檔案。
   - **卡片.css** — 樣式為選用。

- 資料夾名稱與JS/CSS檔案必須相符。

### 重複使用和擴充自訂元件中的欄位

在自訂元件的JSON中定義欄位時（適用於任何欄位群組、基本、驗證、說明等），請遵循下列可維護性和一致性的最佳實務：

- 參考現有的共用容器或欄位定義（例如，`../form-common/_basic-input-placeholder-fields.json#/fields`、`../form-common/_basic- validation-fields.json#/fields`），以重複使用標準/共用欄位。 這可確保您繼承所有標準選項，而不需複製它們。

- 在容器中明確新增欄位或自訂欄位。 這讓您的方案保持枯燥和專注。

- 移除或避免重複透過參考包含的欄位。 僅定義元件邏輯特有的欄位。

- 視需要參考說明容器和其他共用內容（例如`../form-common/_help-container.json`），以維持一致性和可維護性。

>[!TIP]
>
> - 此模式可讓您日後輕鬆更新或擴充邏輯，並確保自訂元件與表單系統其他部分保持一致。
> - 在新增共用容器或欄位定義之前，請務必檢查現有共用容器或欄位定義。

### 定義自訂元件的新屬性

- 如果您需要從作者擷取自訂元件的新屬性，可透過在元件的JSON中的元件的`fields[]`陣列中定義欄位來完成。

- 自訂元件使用:type屬性識別，可在JSON檔案中將其設為`fd:viewType` （例如`fd:viewType: cards`）。 這可讓系統識別並載入正確的自訂元件，因此對自訂元件而言是必要的

- 在JSON定義中新增的任何新屬性可在欄位定義中作為屬性使用。 元件JS邏輯中的`<propertyName>`

## 自訂元件JavaScript API

自訂元件JavaScript API定義如何控制自訂表單元件的行為、外觀和反應性。

### 裝飾函式

**裝飾**&#x200B;函式是自訂元件的進入點。 它會初始化元件、將元件連結至其JSON定義，並允許您操控其HTML結構和行為。

>[!NOTE]
>
> 自訂元件的JavaScript檔案必須將預設函式匯出為裝飾：

#### 函式簽章：

```javascript
export default function decorate(element, fieldJson, container, formId) {
// element: The HTML structure of the OOTB component you are extending
// fieldJson: The JSON field definition (all authorable properties)
// container: The parent element (fieldset or form)
// formId: The id of the form
// ... your logic here ...
}
```

它可以：

- **修改元素**：新增事件接聽程式、更新屬性或插入其他標籤。

- **存取JSON屬性**：使用`fd.properties.<propertyName>`讀取JSON結構描述中定義的值，並在元件邏輯中套用這些值。

## 訂閱函式

**subscribe**&#x200B;函式可讓您的元件對欄位值或自訂事件的變更做出反應。 這可確保元件與表單的資料模型保持同步，並可動態更新其UI。

### 函式簽章：

```JavaScript
import { subscribe } from '../../rules/index.js';

export default function decorate(fieldDiv, fieldJson, container, formId) {
// Access custom properties defined in the JSON
const { initialText, finalText, time } = fieldJson?.properties;
// ... setup logic ...
subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => { fieldModel.subscribe(() => {
// React to custom event (e.g., resetCardOption)
// ... logic ...
}, 'resetCardOption');
});
}
```

它可以：

- **登入回呼**：呼叫&#x200B;**subscribe(element， formId， callback)**&#x200B;會在欄位資料變更時，將您的回呼登入為執行。請使用兩個回呼引數：
   - **element**：代表欄位的HTML元素。
   - **fieldModel**：代表欄位狀態和事件API的物件。

- **接聽變更或事件**：每當值變更或觸發自訂事件時，請使用`fieldModel.subscribe((event) => { ... }, 'eventName')`執行邏輯。 事件物件包含有關變更內容的詳細資訊。

## 建立自訂元件

在本節中，您將瞭解透過擴充OOTB選項按鈕元件來建立&#x200B;**卡片自訂元件**&#x200B;的程式。

![卡片自訂元件](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### 1.程式碼設定

#### 1.1檔案和資料夾

第一步是設定自訂元件的必要檔案，並將其連線到存放庫中的程式碼。 此程式由&#x200B;**AEM Forms Scaffolder CLI**&#x200B;自動完成，因此可以更快速地架設及連線必要的檔案。

1. 開啟終端機，並導覽至表單專案的根目錄。
2. 執行以下命令：

```bash
npm install
npm run create:custom-component
```

![支架CLI](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

它會：

- **提示您為新元件命名**。 例如，在此案例中，使用卡片。
- **要求您選擇**&#x200B;基本元件（選取選項群組）

這會建立所有必要的資料夾和檔案，包括：

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

並與CLI輸出中所示的存放庫中的其餘程式碼連線。
它會自動執行下列功能：

- 將卡片新增至篩選器，以便在最適化表單區塊中新增。
- 更新`mappings.js`的允許清單以包含新卡片元件。
- 在通用編輯器的&#x200B;**自訂元件**&#x200B;清單下註冊卡片元件的定義。

>[!NOTE]
>
> 您也可以使用手動（舊版）方法建立自訂元件。 如需詳細資訊，請參閱[手動或舊版方法](#manual-or-legacy-method-to-create-custom-component)以建立自訂元件區段。

#### 1.2在通用編輯器中使用元件

1. **重新整理通用編輯器**：在通用編輯器中開啟您的表單並重新整理頁面，以確保它從存放庫載入最新的程式碼。

2. **新增自訂元件**

   1. 按一下表單畫布上的&#x200B;**新增(+)**&#x200B;按鈕。
   2. 捲動至自訂元件區段。
   3. 選取新建立的&#x200B;**卡片元件**&#x200B;以將其插入您的表單中。

      ![選取自訂元件](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

由於`cards.js`內沒有程式碼，因此自訂元件會呈現為選項群組。

#### 1.3本機預覽和測試

現在表單包含自訂元件，您可以代理表單並在本機進行變更，然後檢視變更：

1. 前往您的終端機並執行`aem up`。

2. 開啟在`http://localhost:3000/{path-to-your-form}`啟動的Proxy伺服器（路徑範例： `/content/forms/af/custom-component-form`）


### 2.對自訂元件實作自訂行為

#### 2.1設定自訂元件的樣式

讓我們將類別&#x200B;**卡片**&#x200B;新增至元件，以設定樣式，並為每個無線電新增影像，針對此使用下列程式碼。

**在cards.js中使用裝飾函式來設定自訂元件的樣式**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) { element.classList.add('card');
element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => { const image = createOptimizedPicture('https://main--afb--
jalagari.hlx.live/lab/images/card.png', 'card-image'); radioWrapper.appendChild(image);
});
return element;
}
```

**在cards.css中為自訂元件新增執行階段行為**

```javascript
.card .radio-wrapper { min-width: 320px;
/* or whatever width fits your design */ max-width: 340px;
background: #fff;
border-radius: 16px;
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
flex: 0 0 auto;
scroll-snap-align: start; padding: 24px 16px;
margin-bottom: 0;
position: relative;
transition: box-shadow 0.2s; display: flex;
align-items: flex-start; gap: 12px;
}
```

現在，卡片元件顯示如下：

![新增卡片css和js](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2使用訂閱函式新增動態行為

變更下拉式清單時，卡片會被擷取，並設定在選項群組的列舉中。 但目前的檢視無法處理此問題。 因此會呈現如下：

![訂閱函式](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

呼叫API時，它會設定欄位模型，而且必須監聽變更並據此呈現檢視。 這是使用&#x200B;**訂閱函式**&#x200B;達成的。

讓我們將先前步驟中的檢視程式碼轉換為函式，並在`cards.js`中的訂閱函式中呼叫此函式，如下所示：

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';  

import { subscribe } from '../../rules/index.js';  
function createCard(element, enums) {  

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {  

    if (enums[index]?.name) {  

      let label = radioWrapper.querySelector('label');  

      if (!label) {  

        label = document.createElement('label');  

        radioWrapper.appendChild(label);  

      }  

      label.textContent = enums[index]?.name;  

    }  

    const image = createOptimizedPicture(enums[index].image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png', 'card-image');  

   radioWrapper.appendChild(image);  

  });  

}  
export default function decorate(element, fieldJson, container, formId) {  

    element.classList.add('card');  

    createCard(element, fieldJson.enum);  

    subscribe(element, formId, (fieldDiv, fieldModel) => {  

        fieldModel.subscribe((e) => {  

            const { payload } = e;  

            payload?.changes?.forEach((change) => {  

                if (change?.propertyName === 'enum') {  

                    createCard(element, change.currentValue);  

                }  

            });  

        });  

    });  
    return element;  

} 
```

**使用Subscribe函式接聽卡片中的事件變更.js**

現在，當您變更下拉式清單時，卡片會填入，如下所示：

![訂閱函式](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3將檢視更新與欄位模型同步

若要將檢視變更同步到[模型]欄位，您必須設定所選卡片的值。 因此，請在cards.js中新增下列變更事件接聽程式，如下所示：

**在cards.js中使用欄位模型API**

```javascript
 

import { createOptimizedPicture } from '../../../../scripts/aem.js';  

import { subscribe } from '../../rules/index.js';  

  

  

function createCard(element, enums) {  

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {  

    if (enums[index]?.name) {  

      let label = radioWrapper.querySelector('label');  

      if (!label) {  

        label = document.createElement('label');  

        radioWrapper.appendChild(label);  

      }  

      label.textContent = enums[index]?.name;  

    }  

    radioWrapper.querySelector('input').dataset.index = index;  

    const image = createOptimizedPicture(enums[index].image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png', 'card-image');  

   radioWrapper.appendChild(image);  

  });  

}  
export default function decorate(element, fieldJson, container, formId) {  

    element.classList.add('card');  
    createCard(element, fieldJson.enum);  

    subscribe(element, formId, (fieldDiv, fieldModel) => {  

        fieldModel.subscribe((e) => {  

            const { payload } = e;  

            payload?.changes?.forEach((change) => {  

                if (change?.propertyName === 'enum') {  

                    createCard(element, change.currentValue);  

                }  

            });  

        });  
        element.addEventListener('change', (e) => {  

            e.stopPropagation();  

            const value = fieldModel.enum?.[parseInt(e.target.dataset.index, 10)];  

            fieldModel.value = value.name;  

        });  

    });  

    return element;  
} 
```

現在自訂卡片元件會出現，如下所示：

![卡片自訂元件](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

## 提交和推送變更

在您針對自訂元件實作JavaScript和CSS並在本機驗證後，請認可變更並將其推送至您的Git存放庫。

```bash
git add . && git commit -m "Add card custom component" && git push
```

您僅需幾個簡單步驟，即可成功建立複雜的自訂卡片選取元件。

## 建立自訂元件的手動或舊式方法

舊版的方法是手動遵循以下所述的步驟：

1. **選擇要擴充的OOTB元件** （例如，按鈕、下拉式清單、文字輸入等）。 在此情況下，請延伸選項元件。

2. **在**&#x200B;中建立資料夾`blocks/form/components`，並搭配您元件的名稱（在此案例中為卡片）。

3. **新增相同名稱的JS檔案**：
   - `blocks/form/components/cards/cards.js`。

4. （選擇性） **為自訂樣式新增CSS檔案**：
   - `blocks/form/components/cards/cards.css.`

5. **在與**&#x200B;元件JS檔案` _cards.json` (**)相同的資料夾中定義新的JSON檔案** （例如`blocks/form/components/cards/_cards.json`）。 此JSON應該擴充現有元件，並在其定義中，將`fd:viewType`設定為您的元件名稱（在此例中為卡片）：

   - 對於所有欄位群組（基本、驗證、說明等），請明確新增您的自訂欄位。

6. **實作JS和CSS邏輯：**
   - 匯出預設函式，如上所述。
   - 使用&#x200B;**element**&#x200B;引數修改基礎HTML結構。
   - 如果需要，請使用標準欄位資料的&#x200B;**fieldJson**&#x200B;引數。
   - 視需要使用&#x200B;**subscribe**&#x200B;函式接聽欄位變更或自訂事件。

     >[!NOTE]
     >
     >如上所述，實作自訂元件的JS和CSS邏輯。

7. 在表單產生器中將您的元件註冊為變體並設定變體屬性或
   將JSON中的`fd:viewType/:type`加到您的元件名稱，例如，從`fd:viewType`將`definitions[]`值新增為卡片到具有`id="form`之物件的元件陣列。

   ```javascript
   {
   "definitions": [
   {
   "title": "Cards",
   "id": "cards", "plugins": {
   "xwalk": {
   "page": {
   "resourceType":
   "core/fd/components/form/radiobutton/v1/radiobutton", "template": {
   "jcr:title": "Cards",
   "fieldType": "radio-button", "fd:viewType": "cards",
   "enabled": true, "visible": true}
   }
   } }
   }
   ]}
   ```

8. **更新mappings.js**：將元件名稱新增至&#x200B;**OOTBComponentDecorators** （針對OOTB樣式的元件）或&#x200B;**customComponents**&#x200B;清單，讓系統可識別並載入它。

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **更新_form.json**：將元件的名稱新增至`filters.components`陣列，以便將其放置在編寫UI中。

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **更新_component-definition.json**：在`models/_component-definition.json`中，以下列方式使用物件更新群組中具有`id custom-components`的陣列：

   ```javascript
   {
   "...":"../blocks/form/components/cards/_cards.json#/definitions"
   }
   ```

   這是為了提供將與其他元件一起建置的新卡片元件的參考

11. **執行組建:json指令碼**：執行`npm run build:json`，將所有元件JSON定義編譯並合併成單一檔案，由伺服器提供服務。 這可確保您的新元件的結構描述包含在合併的輸出中。

12. 提交變更並將其推播到您的Git存放庫。

現在，您可以將自訂元件新增至表單。

## 建立複合元件

複合元件是藉由結合多個元件而建立的。
例如，「條款與條件」複合元件由父項面板組成，其中包含：

- 用於顯示字詞的純文字欄位

- 擷取使用者合約的核取方塊

此組合結構在個別元件的JSON檔案中定義為範本。 下列範例說明如何定義條款與條件元件的範本：

```javascript
{ 

  "definitions": [ 

    { 

      "title": "Terms and conditions", 

      "id": "tnc", 

      "plugins": { 

        "xwalk": { 

          "page": { 

            "resourceType": "core/fd/components/form/termsandconditions/v1/termsandconditions", 

            "template": { 

              "jcr:title": "Terms and conditions", 

              "fieldType": "panel", 

              "fd:viewType": "tnc", 

              "text": { 

                "value": "Text related to the terms and conditions come here.", 

                "sling:resourceType": "core/fd/components/form/text/v1/text", 

                "fieldType": "plain-text", 

                "textIsRich": true 

              }, 

              "approvalcheckbox": { 

                "name": "approvalcheckbox", 

                "jcr:title": "I agree to the terms & conditions.", 

                "sling:resourceType": "core/fd/components/form/checkbox/v1/checkbox", 

                "fieldType": "checkbox", 

                "required": true, 

                "type": "string", 

                "enum": [ 

                  "true" 

                ] 

              } 

            } 

          } 

        } 

      } 

    } 

  ], 

  ... 

} 
```

## 最佳實務

建立您自己的自訂元件前，請記住以下重點：

- **讓元件邏輯保持焦點**：僅新增/覆寫自訂行為所需的專案

- **善用基底結構**：使用OOTB HTML作為起點

- **使用可編寫的屬性：**&#x200B;透過JSON結構描述公開可設定的選項

- **名稱空間您的CSS**：使用唯一的類別名稱來避免樣式衝突

## 參照

- form-field-types：所有欄位型別的基本HTML結構和屬性。 [按一下這裡](/help/edge/docs/forms/eds-form-field-properties)以檢視詳細的表單欄位結構和屬性。

- **區塊/表單/模型/表單元件**： OOTB和自訂元件屬性定義。

- **區塊/表單/元件**：放置您的自訂元件。 例如： `blocks/form/components/countdown-timer/_countdown-timer.json`顯示如何擴充基礎元件及新增屬性。
