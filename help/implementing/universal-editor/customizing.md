---
title: 自訂通用編輯器
description: 了解自訂通用編輯器的不同選項以支援內容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 68%

---


# 自訂通用編輯器 {#customizing}

了解自訂通用編輯器的不同選項以支援內容作者的需求。

>[!TIP]
>
>通用編輯器亦提供許多[擴充點，](/help/implementing/universal-editor/extending.md)讓您擴充其功能以滿足專案需求。

## 使用Meta設定標籤 {#meta-tags}

某些編寫工作流程可能需要使用通用編輯器的部分功能，而非其他功能。 為了支援這些多樣化的情況，中繼標籤可用於設定或停用編輯器的特定功能或按鈕。

在頁面的`<head>`區段中使用此標籤以停用一或多個功能：

```html
<meta name="urn:adobe:aue:config:disable" content="..." />
```

如果您想要停用多項功能，請提供以逗號分隔的值清單。

以下是`content`支援的值，也就是可以使用meta標籤停用的功能。

| 內容值 | 說明 |
|---|---|
| `publish` | 停用所有[發佈](/help/sites-cloud/authoring/universal-editor/publishing.md)功能，即[發佈按鈕](/help/sites-cloud/authoring/universal-editor/navigation.md#publish)和[取消發佈按鈕](/help/sites-cloud/authoring/universal-editor/navigation.md#ellipsis) |
| `publish-live` | 停用即時[發佈](/help/sites-cloud/authoring/universal-editor/publishing.md) |
| `publish-preview` | 停用預覽發佈（如果[預覽服務](/help/sites-cloud/authoring/sites-console/previewing-content.md)可用） |
| `unpublish` | 停用[取消發佈按鈕](/help/sites-cloud/authoring/universal-editor/publishing.md#unpublishing-content) |
| `copy` | 停用[複製和貼上按鈕](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) |
| `duplicate` | 停用[重複按鈕](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) |
| `header-open-page` | 停用[開啟頁面按鈕](/help/sites-cloud/authoring/universal-editor/navigation.md#open-page) |

## 變更您的端點 {#custom-endpoint}

如果您不想使用由 Adobe 託管的通用編輯器服務，而是使用您自己的託管版本，可以在後設標記中進行設定。如需詳細資訊，請參閱 [AEM 中通用編輯器快速入門](/help/implementing/universal-editor/getting-started.md##configuration-settings)文件。

## 篩選元件 {#filtering-components}

您可以使用元件篩選器限制通用編輯器中每個容器所允許的元件。如需詳細資訊，請參閱[篩選元件](/help/implementing/universal-editor/filtering.md)文件。

## 在屬性面板中依條件顯示和隱藏元件 {#conditionally-hide}

儘管元件通常可供作者使用，但在某些情況下這樣做可能並不合理。於此情況下，您可以在[元件模型欄位](/help/implementing/universal-editor/field-types.md#fields)中新增 `condition` 屬性，隱藏屬性面板中的元件。

可以使用 [JsonLogic 結構描述](https://jsonlogic.com/)定義條件。若條件為真，則顯示該欄位。若條件為假，則該欄位會隱藏。

>[!BEGINTABS]

>[!TAB 範例模型]

```json
 {
    "id": "conditionally-revealed-component",
    "fields": [
      {
        "component": "boolean",
        "label": "Shall the text field be revealed?",
        "name": "reveal",
        "valueType": "boolean"
      },
      {
        "component": "text-input",
        "label": "Hidden text field",
        "name": "hidden-text",
        "valueType": "string",
        "condition": { "===": [{"var" : "reveal"}, true] }
      }
    ]
 }
```

>[!TAB 條件為假]

![隱藏文字欄位](assets/hidden.png)

>[!TAB 條件為真]

![顯示文字欄位](assets/shown.png)

>[!ENDTABS]

## 自訂預覽 URL {#custom-preview-urls}

您可以透過 `urn:adobe:aue:config:preview` 後設設定指定自訂預覽 URL，當您按一下[編輯器右上角工具列](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)中的「**開啟頁面**」按鈕即會開啟此 URL。

只要將所需的預覽 URL 加入已檢測的應用程式之後設標記內，即可做到，如下列範例所示。

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
