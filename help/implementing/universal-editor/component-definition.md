---
title: 元件定義
description: 詳細瞭解元件定義與通用編輯器之間的JSON合約。
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 2%

---

# 元件定義 {#component-definition}

詳細瞭解元件定義與通用編輯器之間的JSON合約。

## 概觀 {#overview}

`component-definition.json`檔案定義了專案內容作者可用的元件。 本檔案將詳細說明此檔案的用途，以及Universal Editor如何使用它來向作者展示頁面製作元件。

>[!TIP]
>
>如需內容模型程式的概述，請參閱檔案[使用Edge Delivery Services專案進行WYSIWYG編寫的內容模型。](https://www.aem.live/developer/component-model-definitions)

>[!TIP]
>
>您不需要從頭開始建立自己的`component-definition.json`檔案。 您用來[啟動您的專案](https://www.aem.live/developer/ue-tutorial)的專案樣版包含[完整運作的`component-definition.json`檔案](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json)，您可以根據自己的需求加以調整。

## 元件定義範例 {#example}

以下是一個完整但簡單的`component-definition.json`範例。

```json
{
  "groups":[
    {
      "title":"General Components",
      "id":"general",
      "components":[
        {
          "title":"Text",
          "id":"text",
          "model": "text",
          "filter": "texts",
          "plugins":{
            "aem":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            },
            "aem65":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```

## `groups` {#groups}

`groups`定義作者在通用編輯器中按一下編輯器屬性面板中的&#x200B;**新增**&#x200B;圖示以[將新元件新增到頁面](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)時看到的元件群組。 群組有助於組織元件。 通用群組可能是&#x200B;**一般元件**&#x200B;和&#x200B;**進階元件**。

* `title`定義編輯器UI中所顯示群組的文字說明。
* `id`可唯一識別群組。

## `components` {#components}

`components`定義哪些元件屬於群組。

* `title`會定義UI中所顯示元件的文字說明。
* `id`可唯一識別元件。
   * 相同[的](/help/implementing/universal-editor/field-types.md#model-structure)元件模型`id`定義了元件的欄位。
   * 因為它是唯一的，所以例如可以在[篩選定義](/help/implementing/universal-editor/filtering.md)中使用它來決定哪些元件可以新增到容器中。
* `model`定義元件使用哪個[模型](/help/implementing/universal-editor/field-types.md#model-structure)。
   * 因此，模型會集中維護在元件定義中，而不需要[指定檢測。](/help/implementing/universal-editor/field-types.md#instrumentation)
   * 這樣一來，您就可以在容器間移動元件。
* `filter`定義元件應使用哪個[篩選器](/help/implementing/universal-editor/filtering.md)。

## `plugins` {#plugins}

`plugins`會定義負責儲存元件的外掛程式。 常見的外掛程式包括：

* AEM as a Cloud Service的`aem`。
* AEM 6.5的`aem5`。
* 用於AEM as a Cloud Service WYSIWYG製作的`xwalk`。

## `page` 或 `cf` {#page-cf}

定義`plugin`後，您需要指出它是與頁面相關還是與片段相關。

* `page`表示元件是目前頁面的內容。
* `cf`指出元件與[內容片段](/help/assets/content-fragments/content-fragments.md)中的內容有關。

### `page` {#page}

如果元件是頁面上的內容，您可以提供下列資訊。

* `resourceType`定義用於轉譯元件的[Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType`。
* `template`定義要自動寫入新建立元件的選用索引鍵/值，並定義應該套用至元件的篩選條件和/或模型。
   * 適用於說明、範例或預留位置文字。

#### `template` {#template}

藉由提供選用的索引鍵/值組，`template`可以自動將這些索引鍵/值組寫入新元件。 此外，也可以指定下列可選值。

### `cf` {#cf}

如果元件與內容片段中的內容相關，您可以提供下列資訊。

* `name`會為新建立的元件定義儲存至JCR的可選名稱。
   * 僅供參考，通常不會在UI中顯示為`title`。
* `cfModel`為新建立的元件定義[內容片段](/help/assets/content-fragments/content-fragments-models.md)模型。
* `cfFolder`會定義將在哪個資料夾中建立內容片段。
* `title`定義新內容片段的標題。
* `description`定義新內容片段的說明。
* `template`定義要自動寫入新建立內容片段的選用索引鍵/值。
   * 適用於說明、範例或預留位置文字。

### `cf`可以是隱含的 {#cf-implied}

如果頁面是[檢測](/help/implementing/universal-editor/getting-started.md#instrument-page)以指向參考欄位，則會假設`cf`。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

在這種情況下，假設為`cf`，因為`data-aue-prop`指向參考欄位。 如果沒有`data-aue-prop`，通用編輯器將會假設`page`，因為在這種情況下，元件不會透過參考欄位進行連結。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

元件只是資源下方的子節點。
