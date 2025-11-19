---
title: 為通用編輯器設定RTE
description: 瞭解如何在通用編輯器中設定RTF編輯器(RTE)。
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: 0557379b8d70205043ed87e104d9576ed40a13ce
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# 為通用編輯器設定RTE {#configure-rte}

瞭解如何在通用編輯器中設定RTF編輯器(RTE)。

>[!NOTE]
>
>本檔案適用於通用編輯器的新RTE，可作為早期採用者功能使用。 如果您有興趣測試這項新功能，[請參閱發行說明以取得詳細資料。](/help/release-notes/universal-editor/current.md#new-rte)

## 概觀 {#overview}

通用編輯器在適當位置和屬性面板中提供RTF編輯器(RTE)，讓作者在編輯文字時套用格式變更。

此RTE可使用[元件篩選器來設定。](/help/implementing/universal-editor/filtering.md)本檔案說明可用的組態選項以及範例。

## 設定結構 {#structure}

RTE組態包含兩個部分：

* [`toolbar`](#toolbar)：工具列設定會控制UI中可用的編輯選項及其組織方式。
* [`actions`](#actions)：動作設定可讓您自訂個別編輯動作的行為和外觀。

這些組態可以定義為具有屬性[的](/help/implementing/universal-editor/filtering.md)元件篩選器`rte`的一部分。

```json
[
  {
    "id": "richtext",
    "rte": {
      "toolbar": {
        // Toolbar configuration
      },
      "actions": {
        // Action-specific configurations
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## 工具列設定 {#toolbar}

工具列設定會控制UI中可用的編輯選項及其組織方式。 以下為可用的區段

```json
{
  "toolbar": {
    // Text formatting options
    "format": ["bold", "italic", "underline", "strike"],
    // Text alignment options
    "alignment": ["left", "center", "right", "justify"],
    // Text direction options, right-to-left or left-to-right
    "direction": ["rtl", "ltr"],
    // Indentation controls
    "indentation": ["indent", "outdent"],
    // Block-level elements
    "blocks": ["paragraph", "h1", "h2", "h3", "h4", "h5", "h6", "code_block"],
    // List options
    "list": ["bullet_list", "ordered_list"],
    // Content insertion
    "insert": ["link", "unlink", "image"],
    // Superscript/subscript
    "sr_script": ["superscript", "subscript"],
    // Editor utilities
    "editor": ["removeformat"],
    // Section ordering (optional)
    "sections": ["format", "alignment", "list"]
  }
}
```

## 動作設定 {#actions}

動作設定可讓您自訂個別編輯動作的行為和外觀。 這些是可用的區段。

### 格式化動作 {#format}

格式動作可用來套用格式，並支援HTML標籤切換，以便在語意變體之間選擇。 可使用下列章節。

```json
{
  "actions": {
    "bold": {
      "tag": "strong",      // Use <strong> instead of <b>
      "shortcut": "Mod-B",  // Custom keyboard shortcut
      "label": "Make Bold"  // Custom button label 
    },
    "italic": {
      "tag": "em",          // Use <em> instead of <i>
      "shortcut": "Mod-I",
      "label": "Italicize"
    },
    "strike": {
      "tag": "del"          // Use <del> instead of <s>
    }
  }
}
```

### 清單動作 {#list}

清單動作支援內容包裝，可控制HTML結構。 可使用下列章節。

```json
{
  "actions": {
    "bullet_list": {
      "wrapInParagraphs": true,    // <ul><li><p>content</p></li></ul>
      "shortcut": "Mod-Shift-8",   // Custom shortcut
      "label": "Bullet List"       // Custom label
    },
    "ordered_list": {
      "wrapInParagraphs": false,   // <ol><li>content</li></ol> (default)
      "shortcut": "Mod-Shift-9"
    }
  }
}
```

### 連結動作 {#link}

連結動作支援目標屬性控制來管理連結行為。 可使用下列章節。

```json
{
  "actions": {
    "link": {
      "hideTarget": false,       // Show target attribute options (default)
      "shortcut": "Mod-K",       // Custom keyboard shortcut
      "label": "Insert Link"     // Custom button label
    },
    "unlink": {
      "shortcut": "Mod-Shift-K", // Custom keyboard shortcut
      "label": "Remove Link"     // Custom button label
    }
  }
}
```

#### 連結設定選項 {#link-options}

* `hideTarget`： `false` （預設） — 在連結中包含目標屬性，允許`_self`、`_blank`等
* `hideTarget`： `true` — 從連結中完全排除目標屬性

只有當游標位於現有連結中時，`unlink`動作才會出現。 它會移除連結格式，同時保留文字內容。

### 影像動作 {#image}

影像動作支援將圖片元素換行，以產生回應式影像標籤。 可使用下列章節。

```json
{
  "actions": {
    "image": {
      "wrapInPicture": false,     // Use <img> tag (default)
      "shortcut": "Mod-Shift-I",  // Custom keyboard shortcut
      "label": "Insert Image"     // Custom button label
    }
  }
}
```

#### 影像組態選項 {#image-options}

* `wrapInPicture`： `false` （預設） — 產生簡單`<img>`元素
* `wrapInPicture`： `true` — 將影像包裝在`<picture>`個元素中以用於回應式設計

### 其他動作 {#other}

所有其他動作都支援基本自訂。 可使用下列章節。

```json
{
  "actions": {
    "h1": {
      "shortcut": "Mod-Alt-1",
      "label": "Large Heading"
    },
    "paragraph": {
      "shortcut": "Mod-Alt-0",
      "label": "Normal Text"
    },
    "link": {
      "shortcut": "Mod-K",
      "label": "Insert Link",
      "hideTarget": false    // Show target attribute options (default: false)
    }
  }
}
```

## 完成範例 {#example}

以下是完整設定的範例。

```json
[
  {
    "id": "richtext",
    "rte": {
      // Configure which tools appear in toolbar
      "toolbar": {
        "format": [
          "bold",
          "italic"
        ],
        "blocks": [
          "paragraph",
          "h1",
          "h2"
        ],
        "list": [
          "bullet_list",
          "ordered_list"
        ],
        "insert": [
          "link",
          "unlink"
        ],
        "sections": [
          "format",
          "blocks",
          "list",
          "insert"
        ]
      },
      // Customize individual action behavior
      "actions": {
        // Format actions with HTML tag choices
        "bold": {
          "tag": "strong",
          "shortcut": "Mod-B",
          "label": "Bold"
        },
        "italic": {
          "tag": "em",
          "shortcut": "Mod-I"
        },
        // List actions with content wrapping
        "bullet_list": {
          "wrapInParagraphs": true,
          "label": "Bullet List"
        },
        "ordered_list": {
          "wrapInParagraphs": false
        },
        // Link actions with target control
        "link": {
          "hideTarget": false,
          "shortcut": "Mod-K",
          "label": "Add Link"
        },
        "unlink": {
          "label": "Remove Link"
        },
        // Other actions with basic customization
        "h1": {
          "shortcut": "Mod-Alt-1",
          "label": "Main Heading"
        }
      }
    }
  }
]
```

## 動作選項詳細資訊 {#action-details}

有數個選項包含其他重要須牢記的詳細資料。

### `wrapInParagraphs` {#wrapInParagraphs}

清單的`wrapInParagraphs`選項控制HTML結構。

#### `wrapInParagraphs: false` (預設) {#wrapInParagraphs-false}

```html
<ul>
  <li>Simple text content</li>
  <li>Another item</li>
</ul>
```

#### `wrapInParagraphs: true` {#wrapInParagraphs-true}

```html
<ul>
  <li><p>Text wrapped in paragraphs</p></li>
  <li><p>Supports rich formatting within items</p></li>
</ul>
```

當您需要下列專案時使用`wrapInParagraphs: true`：

* 清單專案中的豐富格式
* 每個清單專案有多個段落
* 一致的區塊層級樣式

### 連結目標選項 {#link-target}

連結的`hideTarget`選項會控制`target`屬性是否包含在產生的連結中，以及建立連結的對話方塊是否包含目標選取的欄位。

#### `hideTarget: false` (預設) {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### 標籤選項 {#tag}

格式動作可讓您在HTML變體之間切換。

| 動作 | 預設標籤 | 替代標籤 | 使用案例 |
|---|---|---|---|
| `bold` | `<strong>` | `<b>` | 語意與視覺強調 |
| `italic` | `<em>` | `<i>` | 語意與視覺樣式 |
| `strike` | `<del>` | `<s>` | 視覺化與語意刪除 |

選擇語意標籤(`<strong>`、`<em>`、`<del>`)，以獲得更好的協助工具和SEO。

### 鍵盤快速鍵 {#keyboard-shortcuts}

捷徑使用格式`Mod-Key`，其中：

* `Mod` = Mac上的`Cmd`，Windows/Linux上的`Ctrl`
* 範例： `Mod-B`， `Mod-Shift-8`， `Mod-Alt-1`
