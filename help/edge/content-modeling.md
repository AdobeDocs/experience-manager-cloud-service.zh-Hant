---
title: 使用Edge Delivery Services專案進行AEM製作的內容模型
description: 瞭解內容模型如何用於AEM與Edge Delivery Services專案的製作，以及如何模型化您自己的內容。
source-git-commit: 8f3c7524ae8ee642a9aee5989e03e6584a664eba
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 1%

---


# 使用Edge Delivery Services專案進行AEM製作的內容模型 {#content-modeling}

瞭解內容模型如何用於AEM與Edge Delivery Services專案的製作，以及如何模型化您自己的內容。

{{aem-authoring-edge-early-access}}

## 先決條件 {#prerequisites}

搭配Edge Delivery Services使用AEM編寫的專案會繼承任何其他Edge Delivery Services專案的大部分機制，這與內容來源或無關。 [製作方法。](/help/edge/authoring.md)

開始建立專案的模型內容之前，請務必先閱讀下列檔案。

* [快速入門 - 開發人員教學課程](/help/edge/developer/tutorial.md)
* [標記、區段、區塊和自動進行區塊](/help/edge/developer/markup-sections-blocks.md)
* [區塊集合](/help/edge/developer/block-collection.md)

為了提出在不受內容來源限制的情況下運作且引人入勝的內容模型，瞭解這些概念至關重要。 本檔案提供專為AEM編寫所實作之機制的詳細資訊。

## 預設內容 {#default-content}

**預設內容** 是作者直覺地放在頁面上而不新增任何其他語意的內容。 這包括文字、標題、連結和影像。 這些內容在功能和目的方面不言自明。

在AEM中，此內容會以非常簡單、預先定義模型的元件形式實作，其中包括可以在Markdown和HTML中序列化的所有內容。

* **文字**： RTF文字（包括清單元素和強式或斜體文字）
* **標題**：文字，型別(h1-h6)
* **影像**：來源，說明
* **按鈕**：文字、標題、URL、型別（預設、主要、次要）

這些元件的模型是 [使用Edge Delivery Services進行AEM編寫的樣板。](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)

## 區塊 {#blocks}

區塊可用來建立具有特定樣式和功能的更豐富內容。 和預設內容不同，區塊確實需要其他語意。 區塊可類比至 [AEM頁面編輯器中的元件。](/help/implementing/developing/components/overview.md)

區塊基本上是JavaScript裝飾的內容片段，並以樣式表樣式。

### 區塊模型定義 {#model-definition}

搭配Edge Delivery Services使用AEM製作時，必須明確將區塊內容模型化，才能為作者提供建立內容的介面。 基本上，您需要建立模型，讓編寫UI知道根據區塊要向作者呈現哪些選項。

此 [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) 檔案定義區塊的模型。 元件模型中定義的欄位會在AEM中保留為屬性，並在組成區塊的表格中呈現為儲存格。

```json
{
  "id": "hero",
  "fields": [
    {
      "component": "reference",
      "valueType": "string",
      "name": "image",
      "label": "Image",
      "multi": false
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "imageAlt",
      "label": "Alt",
      "value": ""
    },
    {
      "component": "text-area",
      "name": "text",
      "value": "",
      "label": "Text",
      "valueType": "string"
    }
  ]
}
```

請注意，並非每個區塊都必須有模型。 有些區塊只是 [容器](#container) 用於子項清單，其中每個子項都有自己的模型。

您也必須定義哪些區塊存在，以及可使用通用編輯器將其新增至頁面。 此 [`component-definitions.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) 檔案會列出Universal Editor所提供的元件。

```json
{
  "title": "Hero",
  "id": "hero",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Hero",
          "model": "hero"
        }
      }
    }
  }
}
```

您可以將一個模型用於許多區塊。 例如，某些區塊可能會共用定義文字和影像的模型。

對於每個區塊，開發人員會：

* 必須使用 `core/franklin/components/block/v1/block` 資源型別，AEM中區塊邏輯的一般實作。
* 必須定義區塊名稱，此名稱將在區塊的表格標頭中轉譯。
* 可以定義 [模型ID。](/help/implementing/universal-editor/field-types.md#model-structure)
* 可以定義 [篩選器ID。](/help/implementing/universal-editor/customizing.md#filtering-components)

將區塊新增至頁面時，所有這些資訊都會儲存在AEM中。

>[!WARNING]
>
>可能的話，就不需要實作自訂AEM元件。 AEM提供的Edge Delivery Services元件已足夠，並提供特定護欄，以便利開發。
>
>因此，Adobe不建議使用自訂AEM資源型別。

### 區塊結構 {#block-structure}

區塊的屬性為 [已在元件模型中定義](#model-definition) 並持續儲存在AEM中。 屬性會呈現為區塊類似表格結構中的儲存格。

#### 簡單區塊 {#simple}

在最簡單的形式中，區塊會依照屬性在模型中定義的順序，呈現單一列/欄中的每個屬性。

在下列範例中，首先在模型中定義影像，然後定義文字。 因此，它們會先以影像呈現，然後再以文字呈現。

##### 資料 {#data-simple}

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

##### 標記語言 {#markup-simple}

```html
<div class="hero">
  <div>
    <div>
      <picture>
        <img src="/content/dam/image.png" alt="Helix - a shape like a corkscrew">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <h1>Welcome to AEM</h1>
    </div>
  </div>
</div>
```

您可能會注意到，某些型別的值允許推斷標籤中的語義，而且屬性會合併到單一儲存格中。 一節將說明此行為 [型別推斷。](#type-inference)

#### 索引鍵值區塊 {#key-value}

在許多情況下，建議裝飾演算後的語意標籤、新增CSS類別名稱、新增節點或在DOM中移動節點，以及套用樣式。

但在其他情況下，區塊會讀取為機碼值組的類似設定。

以下是這方面的範例： [區段中繼資料。](/help/edge/developer/markup-sections-blocks.md#sections) 在此使用案例中，區塊可設定為呈現為機碼值組表格。 請參閱區段 [章節和章節中繼資料](#sections-metadata) 以取得詳細資訊。

##### 資料 {#data-key-value}

```json
{
  "name": "Featured Articles",
  "model": "spreadsheet-input",
  "key-value": true,
  "source": "/content/site/articles.json",
  "keywords": ['Developer','Courses'],
  "limit": 4
}
```

##### 標記語言 {#markup-key-value}

```html
<div class="featured-articles">
  <div>
    <div>source</div>
    <div><a href="/content/site/articles.json">/content/site/articles.json</a></div>
  </div>
  <div>
    <div>keywords</div>
    <div>Developer,Courses</div>
  <div>
  <div>
    <div>limit</div>
    <div>4</div>
  </div>
</div>
```

#### 容器區塊 {#container}

先前的兩個結構都有單一維度：屬性清單。 容器區塊允許新增子項（通常是相同型別或模型），因此是二維的。 這些區塊仍支援其自身的屬性，這些屬性會先呈現為具有單一欄的列。 但它們也允許新增子項，每個專案會呈現為列，而每個屬性會呈現為該列中的欄。

在下列範例中，區塊會接受作為子項的連結圖示清單，其中每個連結圖示都有影像和連結。 請注意 [篩選器ID](/help/implementing/universal-editor/customizing.md#filtering-components) 在區塊的資料中設定，以參考篩選器設定。

##### 資料 {#data-container}

```json
{
  "name": "Our Partners",
  "model": "text-only",
  "filter": "our-partners",
  "text": "<p>Our community of partners is ...</p>",
  "item_0": {
    "model": "linked-icon",
    "image": "/content/dam/partners/foo.png",
    "imageAlt": "Icon of Foo",
    "link": "https://foo.com/"
  },
  "item_1": {
    "model": "linked-icon"
    "image": "/content/dam/partners/bar.png",
    "imageAlt": "Icon of Bar",
    "link": "https://bar.com"
  }
}
```

##### 標記語言 {#markup-container}

```html
<div class="our-partners">
  <div>
    <div>
        Our community of partners is ...
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/foo.png" alt="Icon of Foo">
      </picture>
    </div>
    <div>
      <a href="https://foo.com">https://foo.com</a>
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/bar.png" alt="Icon of Bar">
      </picture>
    </div>
    <div>
      <a href="https://bar.com">https://bar.com</a>
    </div>
  </div>
</div>
```

### 建立區塊的語意內容模型 {#creating-content-models}

使用 [區塊結構的力學說明，](#block-structure) 您可以建立內容模型，將AEM中儲存的內容一對一對應至傳送階層。

在每個專案早期，必須仔細考慮每個區塊的內容模型。 它必須和內容來源及編寫體驗無關，這樣作者就能在重複使用區塊實作和樣式時切換或結合它們。 如需詳細資訊和一般指引，請參閱 [David模型（取兩塊）。](https://www.aem.live/docs/davidsmodel) 更具體地說， [區塊集合](/help/edge/developer/block-collection.md) 包含一組廣泛的內容模型，適用於常見使用者介面模式的特定使用案例。

針對使用Edge Delivery Services進行AEM編寫，這會產生一個問題，即當資訊是使用由多個欄位組成的表單進行編寫時，如何提供引人入勝的語意內容模型，而不是像RTF文字一樣在內容中編輯語意標籤。

有三種方法可協助建立吸引人的內容模型，以解決此問題：

* [型別推斷](#type-inference)
* [欄位摺疊](#field-collapse)
* [元素分組](#element-grouping)

>[!NOTE]
>
>區塊實施可解構內容並以使用者端轉譯的DOM取代區塊。 雖然這對開發人員而言既可行又直覺，但對Edge Delivery Services而言並非最佳實務。

#### 型別推斷 {#type-inference}

對於某些值，我們可以從值本身推斷語意意義。 這些值包括：

* **影像**  — 如果AEM中的資源參考是具有MIME型別（從開始）的資產 `image/`，參考呈現為 `<picture><img src="${reference}"></picture>`.
* **連結**  — 如果參照存在於AEM中且不是影像，或值開頭為 `https?://`  或 `#`，參考呈現為 `<a href="${reference}">${reference}</a>` .
* **RTF文字**  — 如果裁剪的值以段落開頭(`p`， `ul`， `ol`， `h1`-`h6`，以此類推)，值會呈現為RTF文字。
* **類別名稱** - `classes` 屬性會被視為區塊選項，並在的表格標頭中轉譯 [簡單區塊，](#simple) 或當做中專案的值清單 [容器區塊。](#container)
* **值清單**  — 如果值是多值屬性，且第一個值不是先前的值，則所有值都會串連為逗號分隔清單。

其他所有內容都將呈現為純文字。

#### 欄位摺疊 {#field-collapse}

欄位收合是根據命名慣例，使用尾碼將多個欄位值合併為單一語意元素的機制 `Title`， `Type`， `Alt`、和 `Text` （區分大小寫）。 任何以這些尾碼結尾的屬性都不會被視為值，而是另一個屬性的屬性。

##### 影像 {#image-collapse}

###### 資料 {#data-image}

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

###### 標記語言 {#markup-image}

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

##### 連結和按鈕 {#links-buttons-collapse}

###### 資料 {#data-links-buttons}

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

###### 標記語言 {#markup-links-buttons}

否 `linkType`，或 `linkType=default`

```html
<a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
```

`linkType=primary`

```html
<strong>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</strong>
```

`linkType=secondary`

```html
<em>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</em>
```

##### 標題 {#headings-collapse}

###### 資料 {#data-headings}

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

###### 標記語言 {#markup-headings}

```html
<h2>Getting started</h2>
```

#### 元素分組 {#element-grouping}

當 [欄位摺疊](#field-collapse) 是將多個屬性合併成單一語意元素，元素分組是將多個語意元素串連成單一儲存格。 在使用案例中，如果作者應限制他們可以建立的元素的型別和數量，這會特別有用。

例如，作者應僅建立子標題、標題和單一段落說明，以及最多兩個號召性用語按鈕的組合。 將這些元素分組在一起會產生語義標示，無需進一步操作即可設定樣式。

##### 資料 {#data-grouping}

```json
{
  "name": "teaser",
  "model": "teaser",
  "image": "/content/dam/teaser-background.png",
  "imageAlt": "A group of people sitting on a stage",
  "teaserText_subtitle": "Adobe Experience Cloud"
  "teaserText_title": "Meet the Experts"
  "teaserText_titleType": "h2"
  "teaserText_description": "<p>Join us in this ask me everything session...</p>"
  "teaserText_cta1": "https://link.to/more-details",
  "teaserText_cta1Text": "More Details"
  "teaserText_cta2": "https://link.to/sign-up",
  "teaserText_cta2Text": "RSVP",
  "teaserText_cta2Type": "primary"
}
```

##### 標記語言 {#markup-grouping}

```html
<div class="teaser">
  <div>
    <div>
      <picture>
        <img src="/content/dam/teaser-background.png" alt="A group of people sitting on a stage">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <p>Adobe Experience Cloud</p>
      <h2>Meet the Experts</h2>
      <p>Join us in this ask me everything session ...</p>
      <p><a href="https://link.to/more-details">More Details</a></p>
      <p><strong><a href="https://link.to/sign-up">RSVP</a></strong></p>
    </div>
  </div>
</div>
```

## 章節和章節中繼資料 {#sections-metadata}

和開發人員定義並模型化多個專案的方式相同 [個區塊，](#blocks) 它們可以定義不同的區段。

Edge Delivery Services的內容模型特意只允許單一層級的巢狀，這是區段包含的任何預設內容或區塊。 這表示為了擁有可包含其他元件的更複雜視覺元件，這些元件必須模型化為區段，並使用自動封鎖使用者端組合在一起。 典型的範例是標籤和可摺疊區段，例如摺疊式功能表。

區段可透過區塊相同的方式定義，但資源型別為 `core/franklin/components/section/v1/section`. 區段可以有名稱和 [篩選器ID、](/help/implementing/universal-editor/customizing.md#filtering-components) ，由 [通用編輯器](/help/implementing/universal-editor/introduction.md) 僅限，以及 [模型ID、](/help/implementing/universal-editor/field-types.md#model-structure) 用於呈現區段中繼資料。 此模型以這種方式建立區段中繼資料區塊的模型，如果區段不是空的，系統會自動將其附加至區段作為索引鍵值區塊。

此 [模型ID](/help/implementing/universal-editor/field-types.md#model-structure) 和 [篩選器ID](/help/implementing/universal-editor/customizing.md#filtering-components) 預設區段的 `section`. 它可用來改變預設區段的行為。 下列範例會將一些樣式和背景影像新增至區段中繼資料模型。

```json
{
  "id": "section",
  "fields": [
    {
      "component": "multiselect",
      "name": "style",
      "value": "",
      "label": "Style",
      "valueType": "string",
      "options": [
        {
          "name": "Fade in Background",
          "value": "fade-in"
        },
        {
          "name": "Highlight",
          "value": "highlight"
        }
      ]
    },
    {
      "component": "reference",
      "valueType": "string",
      "name": "background",
      "label": "Image",
      "multi": false
    }
  ]
}
```

下列範例會定義定位點區段，在自動封鎖期間，透過將連續區段與定位點標題資料屬性結合到定位點區塊中，可用來建立定位點區塊。

```json
{
  "title": "Tab",
  "id": "tab",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/section/v1/section",
        "template": {
          "name": "Tab",
          "model": "tab",
          "filter": "section"
        }
      }
    }
  }
}
```

## 頁面中繼資料 {#page-metadata}

檔案可以有一個頁面 [中繼資料區塊，](/help/edge/authoring.md#metadata--seo) 用於定義哪些 `<meta>` 元素會呈現於 `<head>` 的頁面。 AEMas a Cloud Service中頁面的頁面屬性對應至可立即用於Edge Delivery Services的頁面，例如 `title`， `description`， `keywords`等

在進一步探索如何定義您自己的中繼資料之前，請先檢閱以下檔案以先瞭解頁面中繼資料的概念。

* [中繼資料](https://www.aem.live/developer/block-collection/metadata)
* [大量中繼資料](/help/edge/docs/bulk-metadata.md)

您也可以以兩種方式定義其他頁面中繼資料。

### 中繼資料試算表 {#metadata-spreadsheets}

在AEMas a Cloud Service中，可以類似表格的方式為每個路徑或每個路徑模式基礎定義中繼資料。 有編寫UI可供使用類似於Excel或Google Sheets的表格資料。

若要建立這類表格，請建立頁面，並在Sites Console中使用中繼資料範本。

>[!NOTE]
>
>編輯中繼資料試算表時，請務必切換至 **預覽** 模式，因為編寫作業會在頁面本身上進行，而不是在編輯器內進行。

在試算表的頁面屬性中，定義您需要的中繼資料欄位以及URL。 然後為每個頁面路徑或頁面路徑模式新增中繼資料，其中URL欄位與對應的公用路徑相關，而不是AEM中的內容路徑。

在發佈之前，請確定試算表已新增至路徑對應。

```text
mappings:
  - /content/site/:/
  - /content/site/metadata:/metadata.json
```

### 頁面內容 {#page-properties}

您也可以為頁面中繼資料定義元件模型，以供作者做為AEM Sites頁面屬性對話方塊的索引標籤使用。

若要這麼做，請使用ID建立元件模型 `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text-input",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

有些欄位名稱具有特殊意義，在提供編寫對話方塊UI時會略過：

* **`cq:tags`**  — 根據預設， `cq:tags` 不會新增至中繼資料。 將它們新增至 `page-metadata` 模型會將標籤ID新增為以逗號分隔的清單，如下所示 `tags` meta標籤到標題。
* **`cq:lastModified`** - `cq:lastModified` 會將其資料新增為 `last-modified` 頭部。
