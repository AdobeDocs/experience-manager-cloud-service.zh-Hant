---
title: 元件定義
description: 詳細了解元件定義和通用編輯器之間的 JSON 協定。
feature: Developing
role: Admin, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: 022dea38f8597226c644fcdd8c2197a2299a1dfb
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 97%

---

# 元件定義 {#component-definition}

詳細了解元件定義和通用編輯器之間的 JSON 協定。

## 概觀 {#overview}

`component-definition.json` 檔案定義專案內容作者可用的元件。本文件將詳細說明此檔案的用途，以及通用編輯器如何使用此檔案向作者呈現頁面製作元件。

>[!TIP]
>
>關於內容建模程序的概觀，請參閱[使用 Edge Delivery Services 專案進行 WYSIWYG 製作的內容建模](https://www.aem.live/developer/component-model-definitions)文件。

>[!TIP]
>
>您不需要從頭開始建立自己的 `component-definition.json` 檔案。您用於[啟動專案](https://www.aem.live/developer/ue-tutorial)的專案樣板專案包含[功能完整的 `component-definition.json` 檔案](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json)，您可以根據自己的需求進行調整。

## 元件定義範例 {#example}

以下範例是完整但簡單的 `component-definition.json`。

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

`groups` 定義作者在通用編輯器中按一下編輯器屬性面板中的「**新增**」圖示，以便[在頁面中新增元件](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)時，所看到的元件群組。群組將元件進行分類整理。常見的群組可能是&#x200B;**通用元件**&#x200B;和&#x200B;**進階元件**。

* `title` 定義編輯器使用者介面中顯示之群組的文字說明。
* `id` 是群組的唯一識別。

## `components` {#components}

`components` 定義哪些元件屬於某個群組。

* `title` 定義使用者介面中顯示之元件的文字說明。
* `id` 是元件的唯一識別。
   * 相同 `id` 的[元件模型](/help/implementing/universal-editor/field-types.md#model-structure)會定義元件的欄位。
   * 因為這是唯一的，所以可以用於比如[篩選器定義](/help/implementing/universal-editor/filtering.md)，以確定可將哪些元件新增至容器。
* `model` 定義哪個[模型](/help/implementing/universal-editor/field-types.md#model-structure)與元件搭配使用。
   * 因此會在元件定義中集中維護模型，而不需要[指定檢測。](/help/implementing/universal-editor/field-types.md#instrumentation)
   * 這樣一來，您就可以在容器間移動元件。
* `filter` 定義哪個[篩選器](/help/implementing/universal-editor/filtering.md)應與元件搭配使用。

## `plugins` {#plugins}

`plugins` 定義哪個外掛程式負責保留元件。常見的外掛程式包括：

* `aem`適用於[AEM as a Cloud Service，](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service) [AEM 6.5.，](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65)和[AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts)
* [使用 AEM Sites 進行 Edge Delivery Services 編寫](https://www.aem.live/developer/ue-tutorial) 的 `xwalk`。
* `da`用於[檔案製作](https://docs.da.live/developers/reference/universal-editor)

## `page` 或 `cf` {#page-cf}

定義 `plugin` 後，您必須標明這是頁面相關或片段相關。

* `page` 表示該元件是目前頁面上的內容。
* `cf` 表示該元件與[內容片段](/help/assets/content-fragments/content-fragments.md)中的內容相關。

### `page` {#page}

如果元件是頁面上的內容，您可以提供以下資訊。

* `resourceType` 定義用於轉譯元件的 [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType`。
* `template` 定義要自動寫入新建立之元件的選用鍵/值，並定義應將哪個篩選器和/或模型套用至該元件。
   * 適用於解釋性、範例或預留位置文字。

#### `template` {#template}

藉由提供選用的鍵/值配對，`template` 可以自動將這些寫入新元件。此外，也可以指定下列選用值。

### `cf` {#cf}

如果元件與內容片段中的內容相關，則可以提供以下資訊。

* `name` 為新建立的元件定義儲存至 JCR 的選用名稱。
   * 僅供參考，不像 `title` 那樣通常會顯示在使用者介面中。
* `cfModel` 定義新建立之元件的[內容片段](/help/assets/content-fragments/content-fragments-models.md)模型。
* `cfFolder` 定義應在哪個資料夾建立內容片段。
* `title` 定義新內容片段的標題。
* `description` 定義新內容片段的說明。
* `template` 定義選用的鍵/值，以便自動寫入新建立的內容片段。
   * 適用於解釋性、範例或預留位置文字。

### `cf` 可以是隱含的 {#cf-implied}

如果頁面[經檢測](/help/implementing/universal-editor/getting-started.md#instrument-page)為指向一個參照欄位，便會假定使用 `cf`。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

於此情況下會假定使用 `cf`，因為 `data-aue-prop` 指向一個參照欄位。如果沒有 `data-aue-prop`，通用編輯器會假定使用 `page`，因為於此情況下，並沒有透過參照欄位連結元件。

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

元件只是資源下方的子節點。
