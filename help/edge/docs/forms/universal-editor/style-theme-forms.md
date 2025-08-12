---
title: 自訂 AEM Forms 適用的 Edge Delivery Services 主題和樣式
description: 有效地自訂透過 Edge Delivery Services 交付的 AEM Forms 的主題和樣式，從而確保具有凝聚力和品牌化的使用者體驗。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 55%

---

# 自訂表單的外觀

適用於AEM Forms的Edge Delivery Services中的表單樣式設定需要對CSS自訂屬性、區塊型架構和元件特定鎖定目標策略有複雜的瞭解。 與傳統的表單樣式方法不同，最適化Forms區塊實作系統化的設計代號系統，在系統化設計主題的同時，維持Edge Delivery Services的效能和協助工具優勢。

最適化Forms區塊架構會在所有表單元件中產生標準化HTML結構，為CSS目標定位和自訂建立可預測的模式。 這種一致性可讓開發人員實作完整的樣式系統，這些系統可跨複雜的表單實作進行擴充，同時保留區塊式效能最佳化，讓Edge Delivery Services的執行速度異常快速。

本全方位指南涵蓋Edge Delivery Services生態系統內表單樣式的技術基礎，包括CSS自訂屬性系統、元件HTML結構模式和進階樣式技術。 本檔案提供建立複雜、品牌化表單體驗的理論與實務實作指引。

## 您將要掌握的內容

**CSS Custom Properties Mastery**：瞭解控制表單外觀的完整變數系統，包括色彩配置、印刷比例、間距系統和版面配置引數。 瞭解如何覆寫及擴充這些屬性，以實作完整的品牌主題。

**元件架構瞭解**：深入瞭解每個表單元件型別所使用的HTML結構模式，以啟用精確的CSS目標定位和自訂，而不會破壞基礎功能或協助工具功能。

**進階樣式技術**：實作複雜的樣式模式，包括狀態式樣式、回應式設計整合，以及效能最佳化的自訂策略，以維持Edge Delivery Services的快速載入特性。

**專業實作策略**：學習業界標準的表單樣式方法，包括設計系統整合、可維護的CSS架構以及疑難排解複雜樣式設定案例的技術。

## 了解表單欄位類型

在深入研究樣式之前，讓我們回顧一下最適化表單區塊支援的常見表單[欄位類型](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes)：

- 輸入欄位：包括文字輸入、電子郵件輸入、密碼輸入等。
- 核取方塊群組：用於選取多個選項。
- 單選按鈕群組：用於從一組選項中選取一個選項。
- 下拉式選單：也稱為選取方塊，用於從清單中選取一個選項。
- 面板/容器：用於將相關的表單元素組成群組。

## 基本樣式設定原則

在設定特定表單欄位的樣式之前，了解[基本的 CSS 概念](https://www.w3schools.com/css/css_intro.asp)至關重要：

- [選取器](https://www.w3schools.com/css/css_selectors.asp)：CSS 選擇器可讓您針對特定的 HTML 元素進行樣式設定。您可以使用元素選擇器、類別選擇器或 ID 選擇器。
- [屬性](https://www.w3schools.com/css/css_syntax.asp)：CSS 屬性定義元素的外觀。用於設定表單欄位樣式的常見屬性包括顏色、背景顏色、邊框、邊框間距、邊界等。
- [方塊模型](https://www.w3schools.com/css/css_boxmodel.asp)：CSS 方塊模型會將 HTML 元素結構描述為由邊框間距、邊框和邊界包圍的內容區域
- Flexbox/Grid：CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) 和[ Grid 版面](https://www.w3schools.com/css/css_grid.asp)是建立回應式和靈活設計的強大工具。




## 使用CSS自訂屬性的完整表單樣式

最適化Forms區塊採用以自訂屬性（CSS變數）為基礎的複雜CSS架構，以便在所有表單元件間啟用系統化主題設定和一致的樣式。 瞭解此結構對於有效的表單自訂和品牌化至關重要。

### 瞭解forms.css架構

預設表單樣式位於`/blocks/form/form.css`的專案存放庫中，並遵循優先處理可維護性、一致性和自訂靈活性的結構化方法。 此架構包含數個關鍵元件：

**CSS Custom Properties Foundation**：樣式系統建置在`:root`層級定義的CSS自訂屬性上，提供可串連於所有表單元件的集中式主題系統。 這些變數會建立顏色、印刷樣式、間距和版面屬性的設計代號。

**區塊式CSS結構**： Edge Delivery Services採用區塊式架構，其中`.form`類別會作為所有表單相關樣式的主要名稱空間，確保正確的範圍隔離，並防止CSS與其他頁面元件衝突。

**元件特定樣式**：個別表單元件使用一致的包裝函式模式(`.{Type}-wrapper`)來設定樣式，為不同的欄位型別提供可預測的鎖定目標，同時維持整體設計系統的完整性。

### CSS自訂屬性參考與自訂

表單樣式系統包含超過50個CSS自訂屬性，這些屬性控制表單外觀和行為的每個方面。 瞭解這些屬性可全面自訂，同時維持設計的一致性。

+++ 顏色和主題設定變數

色彩系統透過精心整理的自訂屬性，為表單建立完整的視覺基礎：

```css
:root {
    /* Primary color system */
    --background-color-primary: #fff;
    --label-color: #666;
    --border-color: #818a91;
    --form-error-color: #ff5f3f;
    
    /* Button color system */
    --button-primary-color: #5F8DDA;
    --button-secondary-color: #666;
    --button-primary-hover-color: #035fe6;
    
    /* Form-specific color applications */
    --form-background-color: var(--background-color-primary);
    --form-input-border-color: var(--border-color);
    --form-invalid-border-color: #ff5f3f;
    --form-label-color: var(--label-color);
}
```

**實際自訂範例**：若要為表單實作深色主題，請覆寫基本顏色變數：

```css
:root {
    --background-color-primary: #1a1a1a;
    --label-color: #e0e0e0;
    --border-color: #404040;
    --form-error-color: #ff6b6b;
    --button-primary-color: #4a9eff;
}
```

此單一變更會傳播至所有表單元件，因為系統使用變數參照，而非硬式編碼值。

+++

+++ 印刷樣式和間距變數

印刷樣式和間距變數可全面控制文字表示和版面間距：

```css
:root {
    /* Font size system */
    --form-font-size-m: 22px;
    --form-font-size-s: 18px;
    --form-font-size-xs: 16px;
    
    /* Component-specific typography */
    --form-label-font-size: var(--form-font-size-s);
    --form-label-font-weight: 400;
    --form-title-font-weight: 600;
    --form-input-font-size: 1rem;
    
    /* Spacing system */
    --form-field-horz-gap: 40px;
    --form-field-vert-gap: 20px;
    --form-input-padding: 0.75rem 0.6rem;
    --form-padding: 0 10px;
}
```

**實用的自訂範例**：若要使用較小的印刷樣式建立更精簡的表單版面配置：

```css
:root {
    --form-font-size-m: 18px;
    --form-font-size-s: 14px;
    --form-font-size-xs: 12px;
    --form-field-horz-gap: 20px;
    --form-field-vert-gap: 15px;
    --form-input-padding: 0.5rem 0.4rem;
}
```

+++

+++ 版面配置與結構變數

版面配置變數可控制表單維度、格點行為和元件排列：

```css
:root {
    /* Form layout */
    --form-width: 100%;
    --form-columns: 12;
    --form-submit-width: 100%;
    
    /* Card-based components */
    --form-card-border-radius: 4px;
    --form-card-padding: 0.6rem 0.8rem;
    --form-card-shadow: 0 1px 2px rgb(0 0 0 / 3%);
    --form-card-hover-shadow: 0 2px 4px rgb(0 0 0 / 6%);
    
    /* Wizard-specific layout */
    --form-wizard-padding: 0px;
    --form-wizard-padding-bottom: 160px;
    --form-wizard-step-legend-padding: 10px;
}
```

**實際自訂範例**：若要建立具有增強視覺深度的卡片式表單：

```css
:root {
    --form-card-border-radius: 12px;
    --form-card-padding: 1.5rem 2rem;
    --form-card-shadow: 0 4px 12px rgb(0 0 0 / 8%);
    --form-card-hover-shadow: 0 8px 24px rgb(0 0 0 / 12%);
    --form-background-color: #f8f9fa;
}

.form {
    background: var(--form-background-color);
    border-radius: var(--form-card-border-radius);
    box-shadow: var(--form-card-shadow);
    padding: var(--form-card-padding);
    max-width: 600px;
    margin: 2rem auto;
}
```

+++

### CSS樣式模式和最佳作法

最適化Forms區塊會遵循特定的CSS模式，以確保所有元件的可維護、高效能且一致的樣式。

+++ 主要樣式模式

**區塊層級表單容器**：針對整體版面與背景樣式設定主要表單容器的目標：

```css
.form {
    /* Form-wide styles */
    max-width: 800px;
    margin: 0 auto;
    background-color: var(--form-background-color);
    padding: var(--form-padding);
    border-radius: var(--form-card-border-radius);
}
```

**元件包裝函式模式**：使用一致包裝函式類別的目標特定欄位型別：

```css
/* Text input fields */
.form .text-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
    border-radius: 4px;
    width: 100%;
}

/* Email input fields */
.form .email-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
}

/* Button styling */
.form .button-wrapper button {
    background-color: var(--form-button-background-color);
    color: var(--form-button-color);
    padding: var(--form-button-padding);
    border: var(--form-button-border);
    font-size: var(--form-button-font-size);
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

.form .button-wrapper button:hover {
    background-color: var(--form-button-background-hover-color);
}
```

+++

+++ 進階自訂模式

**欄位特定目標定位**：針對不重複樣式需求，依名稱定位個別欄位：

```css
/* Style specific fields */
.form .field-email input {
    background-image: url('data:image/svg+xml;...'); /* Email icon */
    background-repeat: no-repeat;
    background-position: right 12px center;
    padding-right: 40px;
}

.form .field-phone input {
    text-align: center;
    letter-spacing: 1px;
    font-family: monospace;
}
```

**以狀態為基礎的樣式**：實作驗證和互動狀態：

```css
/* Validation states */
.form .field-wrapper[data-valid="false"] input {
    border-color: var(--form-error-color);
    box-shadow: 0 0 0 2px rgba(255, 95, 63, 0.1);
}

.form .field-wrapper[data-valid="true"] input {
    border-color: #28a745;
    box-shadow: 0 0 0 2px rgba(40, 167, 69, 0.1);
}

/* Focus states */
.form .text-wrapper input:focus,
.form .email-wrapper input:focus {
    outline: none;
    border-color: var(--button-primary-color);
    box-shadow: 0 0 0 2px rgba(95, 141, 218, 0.2);
}
```

+++


## 元件結構

最適化表單區塊為各種表單元素提供一致的 HTML 結構，確保輕鬆進行樣式設定和管理。您可以使用 CSS 進行樣式設定，藉此操控元件。

+++ 一般元件 (不包含下拉式選單、單選按鈕群組和核取方塊群組)：

所有表單欄位 (不包含下拉式選單、單選按鈕群組和核取方塊群組) 都具有以下 HTML 結構：

#### 一般元件的 HTML 結構

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

- 類別：div 元素有幾個目標為特定元素和樣式的類別。您需要 `{Type}-wrapper` 或 `field-{Name}` 類別以開發 CSS 選取器來設定表單欄位樣式：
- {Type}：根據欄位類型識別元件。例如，text (text-wrapper)、number (number-wrapper)、date (date-wrapper)。
- {Name}：根據名稱識別元件。欄位名稱只能包含英數字元，名稱中的多個連續破折號將替換為單個破折號 `(-)`，並且將移除欄位名稱中的開頭和結尾的破折號。例如，first-name (field-first-name field-wrapper)。
- {FieldId}：自動產生的欄位唯一識別碼。
- {Required}：一個布林值，用於表示此欄位是否為必要欄位。
- 標籤：的 `label` 元素提供欄位的描述性文字，並使用 `for` 屬性將其與輸入元素相關聯。
- 輸入：`input` 元素定義要輸入的資料類型。例如，text、number、email。
- 描述 (選用)：`div` 與類別 `field-description` 會為使用者提供其他資訊或指示。

**HTML 結構範例**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

#### 一般元件的 CSS 選取器

```css
/* Primary Pattern: Target field wrapper by type */
.form .{Type}-wrapper {
    /* Container styling for specific field types */
    margin-bottom: 1rem;
    border-radius: 4px;
}

/* Primary Pattern: Target input fields within wrapper */
.form .{Type}-wrapper input {
    /* Input field styling using CSS custom properties */
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
}

/* Context-specific: Target element by field name when higher specificity needed */
.form .field-{Name} input {
    /* Field-specific customizations */
    /* Use this pattern for unique styling requirements */
}
```

- `.form .{Type}-wrapper`：根據欄位型別定位欄位包裝函式專案。 例如，`.form .text-wrapper`會鎖定所有文字欄位容器。
- `.form .{Type}-wrapper input`：以包裝函式中的實際輸入元素為目標。 這是設定表單輸入樣式的建議模式。
- `.form .field-{Name}`：根據特定欄位名稱的目標元素。 例如，`.form .field-first-name`會鎖定「名字」欄位容器。 使用`.form .field-{Name} input`以特定目標定位輸入專案。
- **避免**： `main .form form .{Type}-wrapper` — 這會建立不必要的CSS特殊性，且較難維護。

**一般元件的 CSS 選取器範例**

```css
/* Primary Pattern: Target all text input fields */
.form .text-wrapper input {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
    background-color: var(--form-input-background-color);
}

/* Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
    text-transform: capitalize;
    border-color: var(--button-primary-color);
}

/* Alternative with main context if needed */
main .form .text-wrapper input {
    /* Use only when you need higher specificity */
    color: var(--form-label-color);
}
```

+++

+++ 下拉式選單元件

對於下拉式選單，使用 `select` 元素而非 `input` 元素：

#### 下拉式選單元件的 HTML 結構

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**HTML 結構範例**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

#### 下拉式選單元件的 CSS 選擇器

以下 CSS 列出下拉式選單元件的一些範例 CSS 選擇器。

```css
/* Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
    /* Container layout using flexbox */
    display: flex;
    flex-direction: column;
    margin-bottom: var(--form-field-vert-gap);
}

/* Target the select element */
.form .drop-down-wrapper select {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    background-color: var(--form-input-background-color);
    font-size: var(--form-input-font-size);
    color: var(--form-label-color);
}

/* Style the label */
.form .drop-down-wrapper .field-label {
    margin-bottom: 5px;
    font-weight: var(--form-label-font-weight);
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
}
```

- 以包裝函式為目標：第一個選取器 (`.drop-down-wrapper`) 以外部包裝函式元素為目標，確保樣式套用至整個下拉式選單元件。
- Flexbox 版面：Flexbox 垂直排列標籤、下拉式選單和說明，以呈現簡潔的版面。
- 標籤樣式設定：標籤以較粗字體和些微邊界呈現醒目效果。
- 下拉式選單樣式設定：`select` 元素獲得邊框、邊框間距和圓角，具有精美的外觀。
- 背景顏色：設定一致的背景顏色讓視覺更為和諧。
- 箭頭自訂：選擇性樣式可隱藏預設下拉箭頭，並使用 Unicode 字元和定位建立自訂箭頭。

+++

+++ 單選按鈕群組

與下拉元件類似，單選按鈕群組也有自己的 HTML 結構和 CSS 結構：

#### 單選按鈕群組 HTML 結構

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**HTML 結構範例**

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

#### 單選按鈕群組的 CSS 選擇器

- 為欄位集進行目標定位

```css
/* Target radio group container */
.form .radio-group-wrapper {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    margin-bottom: var(--form-field-vert-gap);
}
```

此選擇器針對具有 radio-group-wrapper 類別的任何欄位集。這對於將通用樣式應用於整個單選按鈕群組非常有用。

- 為單選按鈕標籤進行目標定位

```css
/* Target radio button labels */
.form .radio-wrapper label {
    font-weight: var(--form-label-font-weight);
    margin-right: 10px;
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
    cursor: pointer;
}
```

- 根據名稱鎖定來針對欄位集中的所有單選按鈕標籤

```css
/* Target all radio button labels within a specific fieldset based on its name */
.form .field-color .radio-wrapper label {
    /* Field-specific radio label customizations */
    /* Add your custom styles here */
}
```

+++

+++ 核取方塊群組

#### 核取方塊群組的 HTML 結構

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="checkbox-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**HTML 結構範例**

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

#### 核取方塊群組的 CSS 選取器

- 以外部包裝函式為目標：這些選取器的目標為單選按鈕和核取方塊群組的最外層容器，讓您可將一般樣式套用至整個群組結構。這對於設定間距、對齊方式或其他版面相關的屬性非常有用。

```css
/* Primary Pattern: Targets radio group wrappers */
.form .radio-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between radio groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}

/* Primary Pattern: Targets checkbox group wrappers */
.form .checkbox-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}
```

- 以群組標籤為目標：此選取器的目標為單選按鈕和核取方塊群組包裝函式內的 `.field-label` 元素。這使您可以專門為這些群組設定標籤樣式，從而可能使它們更加醒目。

```css
/* Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
    font-weight: var(--form-title-font-weight); /* Makes the group label bold */
    margin-bottom: 0.5rem;
    font-size: var(--form-fieldset-legend-font-size);
    color: var(--form-fieldset-legend-color);
    padding: var(--form-fieldset-legend-padding);
    border: var(--form-fieldset-legend-border);
}
```

- 以個別輸入和標籤為目標：這些選取器可以對個別單選按鈕、核取方塊及其關聯的標籤進行更精細的控制。您可以使用它們來調整大小、間距或套用更獨特的視覺樣式。

```css
/* Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}

/* Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}
```

- 自訂單選按鈕和核取方塊的外觀：此技術隱藏預設輸入並使用 `:before` 和 `:after` 偽元素來建立自訂視覺效果，其根據「已選取」狀態來變更外觀。

```css
/* Hide the default radio button or checkbox */
.form .radio-group-wrapper input[type="radio"],
.form .checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
}

/* Create a custom radio button */
.form .radio-group-wrapper input[type="radio"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 50%;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .radio-group-wrapper input[type="radio"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    box-shadow: inset 0 0 0 3px var(--form-input-background-color);
}

/* Create a custom checkbox */
.form .checkbox-group-wrapper input[type="checkbox"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 2px;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><path fill="white" d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/></svg>');
    background-repeat: no-repeat;
    background-position: center;
}
```

+++

+++ 面板/容器元件

#### 面板/容器元件的 HTML 結構

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**HTML 結構範例**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

- Fieldset 元素可用作含有 panel-wrapper 類別和其他類別的面板容器，以便根據面板名稱 (field-login) 設定樣式。
- 圖例元素(`<legend>`)做為面板標題，包含「登入資訊」文字和類別欄位標籤。 data-visible=&quot;false&quot; 屬性可以與 JavaScript 一起用來控制標題的可見度。
- 在 fieldset 內部、多個。{Type}-wrapper 元素 (在本例中為 .text-wrapper 和 .password-wrapper) 代表面板中的個別表單欄位。
- 每個包裝函式皆包含一個標籤、輸入欄位及說明，與先前的範例類似。


#### 面板/容器元件的 CSS 選擇器範例

1. 為面板進行目標定位：

```CSS
  /- Target the entire panel container */
  main .form form .panel-wrapper {
    /- Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- `.panel-wrapper` 選擇器使用 panel-wrapper 類別來設定所有元素的樣式，為所有面板建立一致的外觀。

1. 為面板標題進行目標定位：

```CSS
  /- Target the legend element (panel title) */
  .panel-wrapper legend {
    /- Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /- Optional: create a separation line */
  }
```

- `.panel-wrapper legend` 選擇器設定面板內圖例元素的樣式，讓標題在視覺上脫穎而出。


1. 為面板中個別欄位進行目標定位：

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- `.panel-wrapper .{Type}-wrapper` 選擇器為面板中含有 `.{Type}-wrapper` 類別的所有包裝函式進行目標定位，可讓您設定表單欄位之間的間距樣式。

1. 為特定欄位 (選項) 進行目標定位：

```CSS
  /- Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /- Add your styles here (specific to username field) */
  }

  /- Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /- Add your styles here (specific to password field) */
  }
```

- 這些屬於選項的選擇器可讓您在面板中為特定欄位包裝函式進行獨特樣式的目標定位，例如醒目顯示使用者名稱欄位。


+++

+++ 可重複面板

#### 可重複面板的 HTML 結構

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**HTML 結構範例**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

每個面板都有與單一面板範例相同的結構，並含有附加屬性：

- data-repeatable=&quot;true&quot;：此屬性表示可使用 JavaScript 或框架以機動方式重複面板。

- 唯一 ID 和名稱：面板中的每個元素都有一個唯一 ID (例如 name-1、email-1) 和以面板索引為主的名稱屬性 (例如 name=&quot;contacts[0 ].name”)。這樣可以在提交多個面板時進行正確的資料收集。


#### 可重複面板的 CSS 選擇器

- 為所有可重複面板進行目標定位：

```CSS
  /- Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /- Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

選擇器會為所有可重複的面板進行樣式設定，確保有一致的外觀和感覺。


- 為面板中個別欄位進行目標定位：

```CSS
/- Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

此選擇器可為可重複面板中所有欄位包裝函式進行樣式設定，讓欄位之間的間距維持一致。

- 為特定欄位 (在面板內) 進行目標定位：

```CSS
/- Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /- Add your styles here (specific to first name field) */
}

/- Target all
```


+++


+++ 檔案附件

#### 檔案附件的 HTML 結構

```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**HTML 結構範例**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

- 類別屬性使用為檔案附件提供的名稱 (claim_form)。
- 輸入元素的 id 和名稱屬性與檔案附件名稱 (claim_form) 相符。
- 檔案清單區段一開始是空值。當檔案上傳時，此區段會以 JavaScript 機動式地填入。


#### 檔案附件元件的 CSS 選擇器

- 為全部檔案附件元件進行目標定位：

```CSS
/- Target the entire file attachment component */
main .form form .file-wrapper {
  /- Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

此選擇器為全部檔案附件元件設定樣式，包括圖例、拖曳區域、輸入欄位和清單。

- 為特定元素進行目標定位：

```CSS
/- Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /- Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/- Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /- Add your styles here (e.g., hide the default input) */
  display: none;
}

/- Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /- Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/- Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /- Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

這些選擇器可讓您為檔案附件元件的不同部分個別設定樣式。您可以調整樣式以符合您的設計偏好。

+++



## 設定元件樣式

您也可以根據表單欄位的特定類型 (`{Type}-wrapper`) 或個別名稱 (`field-{Name}`) 來設定表單欄位的樣式。這允許更精細地控制和自訂表單的外觀。

+++ 根據欄位類型設定樣式

您可以使用 CSS 選取器來以特定欄位類型為目標並一致地套用樣式。

#### HTML 結構

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**HTML 結構範例**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

- 每個欄位都包含在具有多個類別的 `div` 元素中：
   - `{Type}-wrapper`：識別欄位的類型。例如：`form-text-wrapper`、`form-number-wrapper`、`form-email-wrapper`。
   - `field-{Name}`：根據名稱識別欄位。例如：`form-name`、`form-age`、`form-email`。
   - `field-wrapper`：所有欄位包裝函式的通用類別。
- `data-required` 屬性表示該欄位是必填還是選擇性欄位。
- 每個欄位都有對應的標籤、輸入元素和潛在的附加元素 (例如預留位置和描述)。




#### CSS 選取器範例

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  /- Add your styles here */
  width: 100%;
  padding: var(--form-input-padding);
}

/- Primary Pattern: Target all number input fields */
.form .number-wrapper input {
  /- Add your styles here */
  letter-spacing: 2px; /- Example for adding letter spacing to all number fields */
  text-align: center;
}
```

+++

+++ 根據欄位名稱設定樣式

您也可以根據名稱以個別欄位為目標來套用獨特的樣式。

#### HTML 結構

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**HTML 結構範例**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```


#### CSS 選取器範例

```CSS
/- Primary Pattern: Target specific field by name */
.form .field-otp input {
   letter-spacing: 2px;
   text-align: center;
   font-family: monospace;
}

/- Context-specific: Use higher specificity when needed */
main .form .field-otp input {
   /- Use only when you need to override other styles */
   font-weight: bold;
}
```

此 CSS 的目標是位於具有類別 `field-otp` 的元素內的所有輸入元素。Edge Delivery Services表單結構遵循最適化Forms區塊慣例，其中容器標示為欄位特定類別，例如「field-otp」（針對名稱為「otp」的欄位）。


## CSS檔案結構與實作

### **參考實作**

完整的表單樣式參考可在AEM Forms範本存放庫中取得：

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

此檔案可作為CSS自訂屬性系統的標準實作，並為所有表單樣式設定提供基礎。 其中包含所有CSS變數、元件樣式模式和回應式設計實施的完整定義。

+++

+++ 專案整合

在您的Edge Delivery Services專案中，透過以下結構化方法實施表單樣式：

```
/blocks/form/form.css          // Core form block styles (copied from boilerplate)
/styles/styles.css             // Global site styles and CSS variable overrides
/styles/lazy-styles.css        // Additional component enhancements
```

+++

+++ 實作策略

**CSS自訂屬性覆寫**：覆寫全域樣式中的表單變數，以實作品牌特定主題：

```css
/* In /styles/styles.css */
:root {
    /* Brand-specific overrides */
    --button-primary-color: #your-brand-color;
    --form-background-color: #your-background;
    --label-color: #your-text-color;
}
```

**元件特定自訂**：
新增元件專用樣式，同時維護CSS變數系統：

```css
/* Enhanced component styling */
.form .text-wrapper input {
    border-radius: var(--form-card-border-radius);
    transition: all 0.2s ease;
}

.form .text-wrapper input:focus {
    transform: translateY(-1px);
    box-shadow: 0 0 0 3px rgba(var(--button-primary-color), 0.1);
}
```

**回應式設計整合**：在媒體查詢中運用CSS自訂屬性，以取得一致的回應式行為：

```css
@media (max-width: 768px) {
    :root {
        --form-input-padding: 0.875rem;
        --form-field-vert-gap: 1rem;
        --form-padding: 1rem;
    }
}
```

+++

### 完成樣式實施範例

本節將示範如何使用CSS自訂屬性來建立現代的品牌化表單。 實作會細分成清楚的子區段，以便輕鬆瞭解及導覽。



+++ 1.品牌主題變數

使用CSS自訂屬性定義您品牌的調色盤、間距和印刷樣式。

```css
/* Custom brand theme */
:root {
  /* Brand color system */
  --brand-primary: #2563eb;
  --brand-secondary: #64748b;
  --brand-success: #059669;
  --brand-error: #dc2626;
  --brand-background: #f8fafc;
  
  /* Override form variables */
  --background-color-primary: #ffffff;
  --button-primary-color: var(--brand-primary);
  --button-primary-hover-color: #1d4ed8;
  --form-error-color: var(--brand-error);
  --form-background-color: var(--brand-background);
  --label-color: var(--brand-secondary);
  --border-color: #d1d5db;
  
  /* Enhanced spacing */
  --form-input-padding: 1rem;
  --form-field-vert-gap: 1.5rem;
  --form-padding: 2rem;
  
  /* Modern typography */
  --form-font-size-s: 16px;
  --form-label-font-weight: 500;
}
```


+++

+++ 2.表單容器樣式

將現代化背景、邊框半徑和陰影套用至表單容器，以擁有視覺吸引力的版面。


```css
/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}
```




+++

+++ 3.輸入欄位樣式

設定文字、電子郵件和數字輸入欄位的樣式，以提供簡潔現代的外觀。


```css
/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}
```


+++

+++ 4.其他自訂

您可以視需要鎖定特定欄位、狀態或元件，以進一步擴充表單樣式。 如需進階模式，請參閱之前的章節。

```css
/* Custom brand theme */
:root {
    /* Brand color system */
    --brand-primary: #2563eb;
    --brand-secondary: #64748b;
    --brand-success: #059669;
    --brand-error: #dc2626;
    --brand-background: #f8fafc;
    
    /* Override form variables */
    --background-color-primary: #ffffff;
    --button-primary-color: var(--brand-primary);
    --button-primary-hover-color: #1d4ed8;
    --form-error-color: var(--brand-error);
    --form-background-color: var(--brand-background);
    --label-color: var(--brand-secondary);
    --border-color: #d1d5db;
    
    /* Enhanced spacing */
    --form-input-padding: 1rem;
    --form-field-vert-gap: 1.5rem;
    --form-padding: 2rem;
    
    /* Modern typography */
    --form-font-size-s: 16px;
    --form-label-font-weight: 500;
}

/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}

/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}

.form .text-wrapper input:focus,
.form .email-wrapper input:focus,
.form .number-wrapper input:focus {
    border-color: var(--brand-primary);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
    transform: translateY(-1px);
}

/* Enhanced button styling */
.form .button-wrapper button[type="submit"] {
    background: linear-gradient(135deg, var(--brand-primary) 0%, #1d4ed8 100%);
    color: white;
    border: none;
    border-radius: 8px;
    padding: 1rem 2rem;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    width: 100%;
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.form .button-wrapper button[type="submit"]:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4);
}
```

此全方位方法示範CSS自訂屬性如何在維持最適化Forms區塊系統的結構完整性和協助工具功能的同時，啟用複雜的主題。

+++

## 疑難排解CSS問題

+++ CSS特殊性問題

```css
/- ❌ Problem: Styles not applying */
.text-wrapper input {
  color: red;
}

/- ✅ Solution: Match or exceed existing specificity */
.form .text-wrapper input {
  color: red;
}

/- ✅ Alternative: Use higher specificity when needed */
main .form .text-wrapper input {
  color: red;
}
```

+++

+++ css變數覆寫問題

```css
/- ❌ Problem: Variables not working */
.form {
  --form-border-color: blue; /- Local scope only */
}

/- ✅ Solution: Define in root scope */
:root {
  --form-border-color: blue; /- Global scope */
}
```

+++

+++ 表單狀態樣式

```css
/- Validation states */
.form .field-wrapper.error input {
  border-color: var(--form-error-color);
}

.form .field-wrapper.success input {
  border-color: var(--form-success-color);
}

/- Loading state */
.form[data-submitting="true"] {
  opacity: 0.7;
  pointer-events: none;
}

/- Disabled state */
.form input:disabled {
  background-color: var(--form-input-disabled-background);
  cursor: not-allowed;
}
```

+++

+++ 常見選擇器錯誤

```css
/- ❌ Incorrect: Assumes direct nesting */
.form form input {
  /- This might miss inputs in wrappers */
}

/- ✅ Correct: Target actual structure */
.form .text-wrapper input {
  /- Targets actual HTML structure */
}

/- ❌ Avoid: Unnecessary specificity */
main .form form .text-wrapper input {
  /- Too specific, harder to override */
}

/- ✅ Preferred: Balanced specificity */
.form .text-wrapper input {
  /- Easier to maintain and override */
}
```

+++



### **元件特定最佳實務**


+++ 按鈕樣式

```css
/- Primary buttons */
.form .button-wrapper button[type="submit"] {
  background-color: var(--form-focus-color);
  color: white;
  border: none;
  padding: var(--form-input-padding);
  border-radius: var(--form-border-radius);
}

/- Secondary buttons */
.form .button-wrapper button[type="reset"] {
  background-color: transparent;
  color: var(--form-text-color);
  border: 1px solid var(--form-border-color);
}
```

+++

+++ 回應式表單設計

```css
/- Mobile-first approach */
.form {
  width: 100%;
  padding: 1rem;
}

/- Tablet and up */
@media (min-width: 768px) {
  .form {
    max-width: var(--form-max-width);
    padding: var(--form-padding);
  }
}
```

+++

## 最佳實務摘要

1. **使用CSS自訂屬性**：利用變數來設定一致的主題
2. **遵循區塊式架構**：使用`.form`作為主要區塊選擇器
3. **避免過度特殊性**：除非必要，否則請勿使用`main .form form`
4. **目標包裝函式**：使用`.{Type}-wrapper`模式進行元件目標定位
5. **維持一致性**：在整個專案中使用相同的選取器模式
6. **跨裝置測試**：確保表單在行動裝置、平板電腦和桌上型電腦上運作正常
7. **驗證協助工具**：確保樣式不會干擾熒幕閱讀程式或鍵盤導覽


