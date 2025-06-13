---
title: 使用 Edge Delivery Services 專案進行所見即所得製作的內容模型
description: 了解使用 Edge Delivery Services 專案進行所見即所得製作的內容模型如何運作，以及如何對您自己的內容建立模型。
exl-id: e68b09c5-4778-4932-8c40-84693db892fd
feature: Edge Delivery Services
role: Admin, Architect, Developer
index: false
hide: true
hidefromtoc: true
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 使用 Edge Delivery Services 專案進行所見即所得製作的內容模型 {#content-modeling}

了解使用 Edge Delivery Services 專案進行所見即所得製作的內容模型如何運作，以及如何對您自己的內容建立模型。

## 先決條件 {#prerequisites}

使用 Edge Delivery Services 進行所見即所得製作的專案會繼承任何其他 Edge Delivery Services 專案的大部分機制，而且不受內容來源或[製作方法](/help/edge/wysiwyg-authoring/authoring.md)的影響。

在開始為專案的內容建立模式之前，請確保先閱讀以下文件。

* [快速入門 - 開發人員教學課程](/help/edge/developer/tutorial.md)
* [標記語言、區段、區塊和自動進行區塊](/help/edge/developer/markup-sections-blocks.md)
* [區塊集合](/help/edge/developer/block-collection.md)

為了提出一個引人注目的內容模型 (採用與內容來源無關的方式)，了解這些概念至關重要。本文件提供有關於專為所見即所得製作實作之機制的詳細資訊。

## 預設內容 {#default-content}

**預設內容**&#x200B;是作者直觀地放在頁面上而不加入任何額外語義的內容。這包括文字、標題、連結和影像。此類內容的功能和目的一目了然。

在 AEM 中，此內容是以非常簡單預定義模式的元件來實作，其中包括可以在 Markdown 和 HTML 中序列化的所有內容。

* **文字**：RTF 文字 (包括列表元素和粗體或斜體文字)
* **標題**：文字，類型 (h1-h6)
* **影像**：來源、描述
* **按鈕**：文字、標題、url、類型 (預設、主要、次要)

這些元件的模型屬於[使用 Edge Delivery Services 進行所見即所得製作之範本](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)的一部分。

## 區塊 {#blocks}

區塊是用來建立具有特定樣式和功能的更豐富內容。與預設內容相比，區塊確實需要額外的語義。

區塊本質上是由 JavaScript 修飾並使用樣式表設定樣式的內容片段。

### 區塊模式定義 {#model-definition}

在運用使用 Edge Delivery Services 進行所見即所得製作時，必須對區塊的內容建立明確的模式，以便為作者提供建立內容的介面。基本上，您需要建立一個模式，以便製作 UI 知道根據區塊向作者呈現哪些選項。

 [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) 檔案旨在定義區塊模式。元件模式中定義的欄位將作為屬性保留在 AEM 中，並呈現為構成區塊的表格儲存格。

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

請注意，並非每個區塊都必須有模式。有些區塊只是子系清單的[容器](#container) ，其中每個子系都有自己的模式。

還需要定義哪些區塊存在並可以使用通用編輯器新增到頁面中。[`component-definitions.json`](/help/implementing/universal-editor/component-definition.md) 檔案列有通用編輯器提供的元件。

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

多個區塊可能可使用一個模式。例如，有些區塊可以共享定義文字和影像的模式。

對於每個區塊，開發人員：

* 必須使用 `core/franklin/components/block/v1/block` 資源類型，這是在 AEM 中通用的區塊邏輯實作。
* 必須定義區塊名稱，該名稱將呈現在區塊標頭中。
   * 區塊名稱是用來擷取正確的樣式和指令碼來裝飾區塊。
* 可以定義[模式 ID](/help/implementing/universal-editor/field-types.md#model-structure)。
   * 模式 ID 是元件模式的參考編號，旨在定義作者在屬性面板中可用的欄位。
* 可以定義[篩選器 ID](/help/implementing/universal-editor/filtering.md)。
   * 篩選器 ID 是元件篩選器的參考編號，旨在允許變更製作行為，例如透過限制可以將哪些子系新增至區塊或區段，或啟用哪些 RTE 功能。

當將區塊新增至頁面時，所有這些資訊都會儲存在 AEM 中。如果缺少資源類型或區塊名稱，該區塊將不會在頁面上呈現。

>[!WARNING]
>
>雖然有可能，但沒有必要或不建議實作自訂 AEM 元件。AEM 提供的 Edge Delivery Services 元件已足夠，並提供了某些護欄以方便開發作業。
>
>AEM 提供的元件會在發佈到 Edge Delivery Services 時，呈現可供 [helix-html2md](https://github.com/adobe/helix-html2md) 使用的標記；以及在通用編輯器載入頁面時，呈現可供 [aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) 使用的標記。標記是 AEM 與系統其他部分之間的穩定契約，不允許進行自訂。因此，專案不得變更元件，也不得使用自訂元件。

### 區塊結構 {#block-structure}

區塊屬性是[在元件模式中定義](#model-definition)，並繼續保留在 AEM 中。屬性呈現為區塊表格類結構中的儲存格。

#### 簡單區塊 {#simple}

最簡單形式的區塊會依照屬性在模式中定義的順序呈現單行/列中的每個屬性。

在以下範例中，首先在模式中定義影像，然後定義文字。因此，會先呈現影像，然後呈現文字。

>[!BEGINTABS]

>[!TAB 資料]

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

>[!TAB 標記]

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

>[!TAB 表格]

```text
+---------------------------------------------+
| Hero                                        |
+=============================================+
| ![Helix - a shape like a corkscrew][image0] |
+---------------------------------------------+
| # Welcome to AEM                            |
+---------------------------------------------+
```

>[!ENDTABS]

您可能會注意到，有些類型的值允許推斷標記語言中的語義，並且屬性會合併到單一儲存格中。行為描述列於[「類型推斷」](#type-inference)區段中。

#### 鍵值區塊 {#key-value}

在許多情況下，建議裝飾所呈現的語義標記語言、新增 CSS 類別名稱、新增節點或在 DOM 中移動節點，以及套用樣式。

然而，在其他情況下，區塊被讀取為類似鍵值對的配定。

其中一個範例為[區段中繼資料](/help/edge/developer/markup-sections-blocks.md#sections)。在此使用案例中，可以將區塊設定為呈現為鍵值組表格。請參閱「[區段和區段中繼資料](#sections-metadata)」部份，了解更多資訊。

>[!BEGINTABS]

>[!TAB 資料]

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

>[!TAB 標記]

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

>[!TAB 表格]

```text
+-----------------------------------------------------------------------+
| Featured Articles                                                     |
+=======================================================================+
| source   | [/content/site/articles.json](/content/site/articles.json) |
+-----------------------------------------------------------------------+
| keywords | Developer,Courses                                          |
+-----------------------------------------------------------------------+
| limit    | 4                                                          |
+-----------------------------------------------------------------------+
```

>[!ENDTABS]

#### 容器區塊 {#container}

前面兩個結構都有一個維度：屬性清單。容器區塊允許新增子系 (通常具有相同類型或模式)，因此是二維度。這些區塊仍然支援將本身自有的屬性會先呈現為有單一欄的列。但這些區塊也允許新增子系，其中每個項目都呈現為列，每個屬性在列中呈現為欄。

在以下範例中，區塊接受連結圖示清單作為子系，其中每個連結圖示都有一個影像和連結。請注意區塊資料中設定的 [篩選器 ID](/help/implementing/universal-editor/filtering.md) ，以便引用篩選器設定。

>[!BEGINTABS]

>[!TAB 資料]

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

>[!TAB 標記]

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

>[!TAB 表格]

```text
+------------------------------------------------------------ +
| Our Partners                                                |
+=============================================================+
| Our community of partners is ...                            |
+-------------------------------------------------------------+
| ![Icon of Foo][image0] | [https://foo.com](https://foo.com) |
+-------------------------------------------------------------+
| ![Icon of Bar][image1] | [https://bar.com](https://bar.com) |
+-------------------------------------------------------------+
```

>[!ENDTABS]

### 為區塊建立語義內容模式 {#creating-content-models}

使用[所說明的區塊結構機制](#block-structure)，即有可能建立一個內容模式，將 AEM 持續擁有的內容一對一對應到傳遞層。

在每項專案早期，必須仔細考慮每個區塊的內容模式。模式必須與內容來源和製作體驗無關，以便允許作者在重複使用區塊實作和樣式時切換或組合這些實作。更多詳細資訊和一般指導可瀏覽 [David 模式 (第 2 步)](https://www.aem.live/docs/davidsmodel)。更具體地說，[區塊集合](/help/edge/developer/block-collection.md)包含廣泛的內容模式組，用於常見使用者介面模式的特定使用案例。

使用 Edge Delivery Services 進行所見即所得製作時，會有一個問題：當資訊是以由多個欄位組成的表單所製作，而不是在上下文中編輯語義標記語言 (如 RTF 文字) 時，如何提供令人信服的語義內容模型。

為了解決這個問題，可以使用三種方法來建立令人信服的內容模式：

* [類型推斷](#type-inference)
* [欄位摺疊](#field-collapse)
* [元素分組](#element-grouping)

>[!NOTE]
>
>區塊實作可以拆析內容並用用戶端呈現的 DOM 來取代區塊。雖然這對開發人員來說是有可能且直觀的，但這並不是 Edge Delivery Services 的最佳實務。

#### 類型推斷 {#type-inference}

若是有些值，我們可以從值本身推斷出語義意義。這類值包括：

* **影像** - 如果 AEM 中的資源參照是 MIME 類型並且是以 `image/` 為開頭的資產，參照會呈現為 `<picture><img src="${reference}"></picture>`。
* **連結** - 如果參照存在於 AEM 中且不是影像，或該值是以 `https?://` 或者 `#` 為開頭，則參照呈現為 `<a href="${reference}">${reference}</a>`。
* **RTF 文字** - 如果裁剪後的值以段落 (`p`, `ul`、`ol`、`h1` -`h6` 等) 為開頭，則該值呈現為 RTF 文字。
* **類別名稱** - `classes` 屬性被視為[區塊選項](/help/edge/developer/markup-sections-blocks.md#block-options)並呈現在[簡單區塊](#simple)的表格標頭中，或呈現為[容器區塊](#container)中項目的值清單。如果您希望[以不同的方式設計區塊](/help/edge/wysiwyg-authoring/create-block.md#block-options)，此功能即很實用，但不需要建立全新的區塊。
* **值清單** - 如果某個值是多值屬性，且第一個值不是前面的任何一個值，則所有值將連接為逗號分隔清單。

其他所有內容都將呈現為純文字。

#### 欄位摺疊 {#field-collapse}

欄位摺疊是一種基於使用尾碼 (`Title`、`Type`, `MimeType`、`Alt` 和 `Text`；全部區分大小寫) 的命名慣例且將多個欄位值組合成單一語義元素的機制。任何以這些尾碼結尾的屬性都不會被視為值，而是被視為另一個屬性 (property) 的屬性 (attribute)。

##### 影像 {#image-collapse}

>[!BEGINTABS]

>[!TAB 資料]

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

>[!TAB 標記]

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

>[!TAB 表格]

```text
![A red car on a road][image0]
```

>[!ENDTABS]

##### 連結和按鈕 {#links-buttons-collapse}

>[!BEGINTABS]

>[!TAB 資料]

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

>[!TAB 標記]

不是 `linkType` 或 `linkType=default`

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

>[!TAB 表格]

```text
[adobe.com](https://www.adobe.com "Navigate to adobe.com")
**[adobe.com](https://www.adobe.com "Navigate to adobe.com")**
_[adobe.com](https://www.adobe.com "Navigate to adobe.com")_
```

>[!ENDTABS]

##### 標題 {#headings-collapse}

>[!BEGINTABS]

>[!TAB 資料]

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

>[!TAB 標記]

```html
<h2>Getting started</h2>
```

>[!TAB 表格]

```text
## Getting started
```

>[!ENDTABS]

#### 元素分組 {#element-grouping}

[欄位摺疊](#field-collapse)是將多個屬性組合到單一語義元素中，而元素分組是將多個語義元素連接到單一儲存格中。這對於作者應該限制可以建立的元素類型和數量的使用案例特別有用。

例如，Teaser 元件可讓作者只建立副標題、標題和單一段落描述，並最多結合兩個召喚行動按鈕。將這些元素組合在一起會產生語義標記語言，無需進一步操作即可對其進行樣式設定。

元素分組會使用命名慣例，其中群組名稱會以底線來區別群組中的每個屬性。群組中屬性的欄位摺疊使用方法如前所述。

>[!BEGINTABS]

>[!TAB 資料]

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

>[!TAB 標記]

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

>[!TAB 表格]

```text
+-------------------------------------------------+
| Teaser                                          |
+=================================================+
| ![A group of people sitting on a stage][image0] |
+-------------------------------------------------+
| Adobe Experience Cloud                          |
| ## Meet the Experts                             |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## 區段和區段中繼資料 {#sections-metadata}

開發人員可以使用相同的方式定義多個[區塊](#blocks)並建立模式，這些可以定義不同的區段。

Edge Delivery Services 內容模式本來就是只允許單一巢狀層級，這是任預設內容或含有一個區段的區塊。這意味著為了擁有可以包含其他元件的更複雜視覺元件，必須將這些模式建立為區段，並使用自動封鎖用戶端合併在一起。這個的一般範例是標記和如手風琴般的可摺疊區段。

區段的定義方式與區塊相同，但資源類型為 `core/franklin/components/section/v1/section`。區段可以有一個名稱和一個[篩選器 ID，](/help/implementing/universal-editor/filtering.md) 限供 [Universal Editor](/help/implementing/universal-editor/introduction.md) 使用；以及有一個[模式 ID ](/help/implementing/universal-editor/field-types.md#model-structure)，可用於呈現區段中繼資料。這樣的模型式就是區段中繼資料區塊的模式，如果不是為空，此模式會自動作為鍵值區塊附加到區段中。

預設區段的[模式 ID](/help/implementing/universal-editor/field-types.md#model-structure) 和 [篩選器 ID](/help/implementing/universal-editor/filtering.md) 是 `section`。這可用於更改預設區段的行為。以下範例將一些樣式和背景影像新增至區段中繼資料模式。

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

以下範例是定義一個標記區段，然後透過在自動封鎖期間將連續區段與標記標題資料屬性合併為標記區塊，以便用來建立標記區塊。

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

## 頁面繼資料 {#page-metadata}

文件可以有[中繼資料區塊](https://www.aem.live/developer/block-collection/metadata)頁面，可用於定義要哪個 `<meta>` 元素呈現在頁面的 `<head>` 中。AEM as a Cloud Service 中的頁面屬性會對應到 Edge Delivery Services 現成可用的頁面屬性，例如 `title`, `description`、`keywords` 等。

在進一步探索如何定義自己的中繼資料之前，請先查看以下文件以了解頁面中繼資料的概念。

* [中繼資料](https://www.aem.live/developer/block-collection/metadata)
* [大量中繼資料](/help/edge/docs/bulk-metadata.md)

同時也可能以兩種方式定義附加頁面中繼資料。

### 中繼資料試算表 {#metadata-spreadsheets}

在 AEM as a Cloud Service 中，可能以類似表格的方式定義每個路徑或每個路徑模式的中繼資料。有一個類似 Excel 或 Google Sheets 的表格式資料適用的製作 UI。

如需進一步詳細資訊，請參閱文件：[使用試算表管理表格資料](/help/edge/wysiwyg-authoring/tabular-data.md)，以了解更多資訊。

### 頁面屬性 {#page-properties}

AEM 中提供的許多預設頁面屬性都會對應到文件中各別的頁面中繼資料。例如，這包括 `title`、`description`、`robots`、`canonical url` 或 `keywords`。有些 AEM 特定的屬性也可用：

* 以 `modified-time` (ISO8601 格式) 顯示的 `cq:lastModified`
* 文件最後發佈的時間為 `published-time` (ISO8601 格式)
* `cq:tags` 作為 `cq-tags` 以逗號分隔的標記 ID 清單。

也可以為自訂頁面中繼資料定義元件模型，使作者可以在通用編輯器中使用。

若要如此做，請使用 ID `page-metadata` 建立元件模型。

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

## 後續步驟 {#next-steps}

現在您已了解如何建立內容模型，接下來可以使用所見即所得製作專案為您自己的 Edge Delivery Services 建立區塊。

請參閱文件：[建立經檢測適用通用編輯器的區塊](/help/edge/wysiwyg-authoring/create-block.md)，了解如何在使用 Edge Delivery Services 專案的所見即所得製作中建立經檢測適用通用編輯器的區塊。

如果您已經熟悉如何建立區塊，請參閱文件：[使用 Edge Delivery Services 進行所見即所得製作的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)，協助您快速開始使用新的 Adobe Experience Manager 網站，使用 Edge Delivery Services 和通用編輯器進行內容製作。
