---
title: 為 EDS Forms 建立自訂元件
description: 為 EDS Forms 建立自訂元件
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 9664495d17ad8a8101c886408bee1584b3d48f1e
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 99%

---


# 在自適應表單區塊中建立自訂表單元件

Edge Delivery Services 表單可提供自訂，讓前端開發人員可以建置量身打造的表單元件。這些自訂元件可無縫整合到 WYSIWYG 製作體驗中，使表單作者能夠在表單編輯器中輕鬆地進行新增、設定和管理。使用自訂元件，作者即可提升功能，同時可確保平順、直覺的製作流程。

本文件概述透過設定原生 HTML 表單元件的樣式來建立自訂元件的步驟，以改善使用者體驗並增加表單的視覺吸引力。

## 架構概觀

表單區塊的自訂元件遵循 **MVC (Model-View-Controller)** 架構模式：

### 模型

- 由每個 `field/component` 的 JSON 結構描述所定義。

- 在對應的 JSON 檔案中指定可編寫的屬性 (請參閱區塊/表單/模型/表單 - 元件)。

- 表單建立工具中的作者可使用這些屬性，並且可作為欄位定義 (fd) 的一部分傳遞至元件。

### 檢視

- 在 form-field-types 中說明各欄位類別的 HTML 結構。

- 這是可延伸或可修改元件的基本結構。

- 各個 OOTB 元件的基本 HTML 結構會記錄在 form-field-types。

### 控制器/元件邏輯

- 以 OOTB (out-of-the-box) 或自訂元件的形式在 JavaScript 中進行實作。- 位於自訂元件的 `blocks/form/components`。

## OOTB 元件

**OOTB (out-of-the-box)** 元件為自訂開發奠定基礎：

- OOTB 元件位於 `blocks/form/models/form-components`。

- 每個 OOTB 元件均具備定義其可編寫屬性的 JSON 檔案 (例如：` _text-input.json`、`_drop-down.json`)。

- 表單建立工具中的作者可使用這些屬性，並且可作為欄位定義 (fd) 的一部分傳遞至元件。

- 各個 OOTB 元件的基本 HTML 結構會記錄在 form-field-types。

擴充現有的 OOTB 元件可讓您重複使用其基本結構、行為及屬性，並且對其進行自訂以符合需求。

- 自訂元件必須從預先定義的 OOTB 元件集開始擴充。

- 此系統會根據欄位 JSON 中的 `viewType` 屬性，識別要擴充的 OOTB 元件。

- 此系統會維護允許的自訂元件變體登錄。僅限使用此登錄中所列出的變體，例如`mappings.js` 的 `customComponents[]`。

- 轉譯表單時，此系統會檢查變體屬性或 `:type/fd:viewType`，並且如果其符合已註冊的自訂元件，則會從 `blocks/form/components` 資料夾中載入對應的 JS 和 CSS 檔案。

- 此自訂元件隨後會套用至 OOTB 元件的基本 HTML 結構，可讓您增強或覆寫其行為和外觀。

## 自訂元件的結構

若要建立自訂元件，您可以使用&#x200B;**支架 CLI**&#x200B;來設定元件所需的檔案和資料夾，然後新增自訂元件的程式碼。

- 自訂元件存放於 `blocks/form/components` 資料夾。

- 每個自訂元件均必須存放在自己的資料夾中，並以元件命名，例如 cards。在此資料夾中，下列檔案應為：

   - **_cards.json**：擴充 OOTB 元件之元件定義 JSON 檔案、定義其可編寫的屬性 (模型[])，以及載入時的內容結構 (定義[])。
   - **cards.js**：包括主要邏輯的 JavaScript 檔案。
   - **卡片.css**：可選用，適用於樣式。

- 此資料夾名稱與 JS/CSS 檔案必須相符。

### 重複使用和擴充自訂元件的欄位

在自訂元件的 JSON 中定義欄位時 (適用於任何欄位群組、基本、驗證、說明等)，請遵循下列可維護性和一致性的最佳做法：

- 參考現有的共用容器或欄位定義 (例如：`../form-common/_basic-input-placeholder-fields.json#/fields`、`../form-common/_basic- validation-fields.json#/fields`)，以重複使用標準/共用欄位。這可確保您繼承所有標準選項，而無須重複選項。

- 在容器中僅限明確新增新欄位或自訂欄位。這可讓您的結構描述保持簡潔和專注。

- 移除或避免重複已透過參考所包含的欄位。僅限定義元件邏輯獨有的欄位。

- 根據需要參考說明容器和其他共用內容 (例如 `../form-common/_help-container.json`)，以確保一致性和可維護性。

>[!TIP]
>
> - 此模式可讓您將來輕鬆進行更新或擴充邏輯，並確保自訂元件與表單系統其他部分保持一致。
> - 在新增共用容器或欄位定義之前，請務必檢查現有內容。

### 定義自訂元件的新屬性

- 若您需要從作者擷取自訂元件的新屬性，可透過在 JSON 元件中的元件 `fields[]` 陣列中定義欄位來完成。

- 使用在 JSON 檔案中 (例如 `fd:viewType: cards`) 可設為 `fd:viewType` 的 :type 屬性，以識別自訂元件。此步驟可讓系統進行識別並載入正確的自訂元件，因此對自訂元件而言是必要的。

- 在 JSON 定義中新增的任何新屬性，均可在欄位定義中作為屬性使用。元件 JS 邏輯中的 `<propertyName>`

## 自訂元件 JavaScript API

自訂元件 JavaScript API 定義如何控制自訂表單元件的行為、外觀及反應能力。

### 裝飾函數

**裝飾** 函數是自訂元件的入口點。此函數會將元件初始化，將元件連結至其 JSON 定義，並讓您操作其 HTML 結構和行為。

>[!NOTE]
>
> 此自訂元件的 JavaScript 檔案必須將預設函數匯出為裝飾：

#### 函數簽名：

```javascript
export default function decorate(element, fieldJson, container, formId) 
{
  // element: The HTML structure of the OOTB component you are extending
  // fieldJson: The JSON field definition (all authorable properties)
  // container: The parent element (fieldset or form)
  // formId: The id of the form

  // ... your logic here ...
}
```

功能：

- **修改元素**：新增事件監聽程式、更新屬性或插入其他標記。

- **存取 JSON 屬性**：使用 `fd.properties.<propertyName>` 來讀取 JSON 結構描述中定義的值，並將其套用於元件邏輯中。

## 訂閱函數

**訂閱**&#x200B;函數可讓您的元件欄位值或自訂事件的變更作出反應。可確保元件和表單的資料模型保持同步，並可動態更新其使用者介面。

### 函數簽名：

```javascript
import { subscribe } from '../../rules/index.js';
export default function decorate(fieldDiv, fieldJson, container, formId) {
  // Access custom properties defined in the JSON
  const { initialText, finalText, time } = fieldJson?.properties;

  // ... setup logic ...

  subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => {
    fieldModel.subscribe(() => {
      // React to custom event (e.g., resetCardOption)
      // ... logic ...
    }, 'resetCardOption');
  });
}
```

功能：

- **註冊回呼**：呼叫&#x200B;**訂閱 (元素、formId、回呼)** 會註冊您的回呼，使其在欄位資料變更時執行。請使用兩個回呼參數：
   - **元素**：代表此欄位的 HTML 元素。
   - **fieldModel**：代表欄位狀態和事件 API 的物件。

- **監聽變更或事件**：值變更或自訂事件觸發時，使用 `fieldModel.subscribe((event) => { ... }, 'eventName')` 來執行邏輯。此事件物件包含有關變更內容的詳細資訊。

## 建立自訂元件

在本節中，您將了解透過擴充 OOTB 選項按鈕元件來建立&#x200B;**卡片自訂元件**&#x200B;的程式。

![卡片自訂元件](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. 程式碼設定

#### 1.1 檔案和資料夾

第一步是設定自訂元件的必要檔案，並將其連線至存放庫中的程式碼。透過可更快速架設和連接必要檔案的 **AEM Forms 支架 CLI** 自動完成此流程。

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. 開啟終端機，並導覽至表單專案的根目錄。
2. 執行以下命令：

```bash
npm install
npm run create:custom-component
```

![支架 CLI](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

將會：

- 針對新元件&#x200B;**提示您進行命名**。例如，在此案例中使用卡片。
- **要求您選擇**&#x200B;基本元件 (選取按鈕群組)

此動作會建立所有必要的資料夾和檔案，包括：

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

並將其與存放庫中其他的程式碼進行連接，如 CLI 輸出所示。
它會自動執行以下功能：

- 將卡片新增至篩選器，以便在自適應表單區塊中進行新增。
- 更新 `mappings.js` 允許清單，以包含新卡片元件。
- 在通用編輯器的&#x200B;**自訂元件**&#x200B;清單註冊卡片元件的定義。

>[!NOTE]
>
> 您亦可使用手動 (舊版) 方法來建立自訂元件。請參閱[手動或舊版方法](#manual-or-legacy-method-to-create-custom-component)，以建立自訂元件區段或了解詳細資訊。

#### 1.2 在通用編輯器中使用元件

1. **重新整理通用編輯器**：在通用編輯器中開啟您的表單，並重新整理頁面，以確保從存放庫載入最新的程式碼。

2. **新增自訂元件**

   1. 按一下表單畫布上的「**新增 (+)**」按鈕。
   2. 捲動至自訂元件區段。
   3. 選取新建的&#x200B;**卡片元件**，以將其插入您的表單中。

      ![選取自訂元件](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

由於 `cards.js` 內沒有程式碼，因此自訂元件會顯示為按鈕群組。

#### 1.3 本機預覽和測試

此表單現已包含自訂元件，您可以代理此表單並在本機進行變更，然後查看此變更：

1. 前往您的終端機，並執行`aem up`。

2. 開啟在 `http://localhost:3000/{path-to-your-form}` 啟動的 Proxy 伺服器 (路徑範例：`/content/forms/af/custom-component-form`)


### &#x200B;2. 針對自訂元件實作自訂行為

#### 2.1 自訂元件的樣式設定

請將&#x200B;**卡片**&#x200B;類別新增至元件以設定樣式，並針對每個按鈕新增影像，使用下列程式碼以完成此動作。

**使用card.js設定元件樣式**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => {
    const image = createOptimizedPicture(
      'https://main--afb--jalagari.hlx.live/lab/images/card.png',
      'card-image'
    );
    radioWrapper.appendChild(image);
  });

  return element;
}
```

**使用cards.css新增執行階段行為**

```javascript
.card .radio-wrapper {
  min-width: 320px; /* or whatever width fits your design */
  max-width: 340px;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  flex: 0 0 auto;
  scroll-snap-align: start;
  padding: 24px 16px;
  margin-bottom: 0;
  position: relative;
  transition: box-shadow 0.2s;
  display: flex;
  align-items: flex-start;
  gap: 12px;
}
```

現在，此卡片元件顯示如下：

![新增 card css 和 card js](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 使用訂閱函數新增動態行為

下拉式清單已變更時，會擷取卡片，並將其設定於按鈕群組的列舉中。但目前的檢視無法處理此問題。因此其顯示如下：

![訂閱函數](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

呼叫 API 時，此函數會設定欄位模型，且必須監聽變更並據此顯示檢視。使用&#x200B;**訂閱函數**&#x200B;即可完成。

請將先前步驟中的檢視程式碼轉換成函數，並在 `cards.js` 中的訂閱函數中呼叫此函數，如下所示：

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

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

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

**使用訂閱函數來監聽 cards.js 中的事件變更**

現在，當您變更下拉式清單時，卡片會如下所示填入：

![訂閱函數](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 將檢視更新與欄位模型同步

若要將此檢視變更同步至模型欄位，您必須設定已選取卡片的值。因此，請在 cards.js 中新增下列變更事件監聽程式，如下所示：

**在 cards.js 中使用欄位模型 API**

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

    // Attach index to input element for later reference
    radioWrapper.querySelector('input').dataset.index = index;

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

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

現在，自訂卡片元件會如下所示顯示：

![卡片自訂元件](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;3. 認可並推送變更

您已針對自訂元件實作 JavaScript 和 CSS 並在本機驗證後，請認可並推送此變更至您的 Git 存放庫。

```bash
git add . && git commit -m "Add card custom component" && git push
```

僅需進行數個簡易步驟，即可成功建立複雜的自訂卡片選取元件。

+++ **建立自訂元件的手動或舊版方法**

舊版方法是手動遵循以下所述的步驟：

1. **選擇 OOTB 元件**&#x200B;進行擴充 (例如：按鈕、下拉式清單、文字輸入等)。在此情況下，請擴充按鈕元件。

2. 請使用您的元件名稱 (此情況的卡片) 在`blocks/form/components` 中&#x200B;**建立資料夾**。

3. 以相同名稱 **新增 JS 檔案**：
   - `blocks/form/components/cards/cards.js`。

4. (選用) **新增自訂樣式的 CSS 檔案**：
   - `blocks/form/components/cards/cards.css.`

5. 在與您的&#x200B;**元件 JS 檔案** (`blocks/form/components/cards/_cards.json`) 所在的相同的資料夾中，**定義新的 JSON 檔案** (例如 ` _cards.json`)。此 JSON 應該擴充現有元件，並在其定義中將 `fd:viewType` 設定為您的元件名稱 (在此案例中為卡片)：

   - 針對所有欄位群組 (基本、驗證、說明等)，請明確新增您的自訂欄位。

6. **實作此 JS 和 CSS 邏輯：**
   - 如上所述匯出預設函數。
   - 使用此&#x200B;**元素**&#x200B;參數來修改基本 HTML 結構。
   - 如有需要，請使用標準欄位資料的 **fieldJson** 參數。
   - 如有需要，請使用&#x200B;**訂閱**&#x200B;函數來監聽欄位變更或自訂事件。

     >[!NOTE]
     >
     >如上所述，實作自訂元件的 JS 和 CSS 邏輯。

7. 在表單建立工具中將您的元件註冊為變體，並設定變體屬性或
   將 JSON 中的 `fd:viewType/:type` 設定為您的元件名稱，例如，從 `fd:viewType` 中，將 `definitions[]` 值新增為卡片至具有 `id="form` 物件的元件陣列。

   ```
       {
     "definitions": [
       {
         "title": "Cards",
         "id": "cards",
         "plugins": {
           "xwalk": {
             "page": {
               "resourceType": "core/fd/components/form/radiobutton/v1/radiobutton",
               "template": {
                 "jcr:title": "Cards",
                 "fieldType": "radio-button",
                 "fd:viewType": "cards",
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

8. **更新 mappings.js**：將您的元件名稱新增至 **OOTBComponentDecorators** (適用於 OOTB 樣式元件)，或 **customComponents** 清單，故系統可進行識別並將其載入。

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **Update _form.json**：將您的元件名稱新增至 `filters.components` 陣列，因此可將其拖放至製作 UI 中。

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **Update _component-definition.json**：在 `models/_component-definition.json` 中，以下列方式使用物件，將具有 `id custom-components` 群組內的陣列進行更新：

   ```javascript
   {
   "...":"../blocks/form/components/cards/_cards.json#/definitions"
   }
   ```

   其目的在於為將與其他元件一起建置的新卡片元件提供參考

11. **執行建置 :json 指令碼**：執行 `npm run build:json`，將所有元件 JSON 定義進行編譯並合併為單一檔案，再由伺服器提供服務。這可確保您新元件結構描述包含在已合併的輸出中。

12. 認可變更並將其推送至您的 Git 存放庫。

現在可以將自訂元件新增至您的表單。

+++

## 建立複合元件

複合元件是透過合併多個元件所建立。
例如，「條款與條件」複合元件由上層面板組成，其中包含：

- 用於顯示詞彙的純文字欄位

- 擷取使用者協議的核取方塊

此組成結構在個別元件的 JSON 檔案中定義為範本。下列範例顯示如何定義條款與條件元件的範本：

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

## 最佳做法

建立您自己的自訂元件前，請記住以下重點：

- **保持元件邏輯專一性**：僅新增/覆寫自訂行為所需的內容

- **善用基本結構**：使用 OOTB HTML 作為您的起點

- **使用可編寫的屬性：**&#x200B;透過 JSON 結構描述顯示可設定的選項

- **以名稱空間標記您的 CSS**：透過使用唯一的類別名稱來避免樣式衝突

## 參照

- [form-field-types](/help/edge/docs/forms/eds-form-field-properties.md)：所有欄位型別的基礎HTML結構和屬性。

- **區塊/表單/模型/表單元件**：OOTB 和自訂元件屬性定義。

- **區塊/表單/元件**：放置自訂元件的位置。例如：`blocks/form/components/countdown-timer/_countdown-timer.json` 顯示如何擴充基本元件並新增屬性。
