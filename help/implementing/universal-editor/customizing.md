---
title: 自訂通用編輯器
description: 了解自訂通用編輯器的不同選項以支援內容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 32b3a125d6370dd591252fde342843d5f9e33cf1
workflow-type: ht
source-wordcount: '409'
ht-degree: 100%

---


# 自訂通用編輯器 {#customizing}

了解自訂通用編輯器的不同選項以支援內容作者的需求。

>[!TIP]
>
>通用編輯器亦提供許多[擴充點，](/help/implementing/universal-editor/extending.md)讓您擴充其功能以滿足專案需求。

## 停用發佈 {#disable-publish}

某些製作工作流程會要求在發佈內容之前先進行審閱。於此情況下，任何作者應該無法使用發佈的選項。

因此，您可以新增以下後設資料，在應用程式內完全隱藏「**發佈**」按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## 停用發佈至預覽的功能 {#publish-preview}

某些製作工作流程可能會防止發佈至[預覽服務](/help/sites-cloud/authoring/sites-console/previewing-content.md) (若適用)。

因此，您可以新增以下後設資料，在應用程式內完全隱藏發佈視窗中的「**預覽**」選項。

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## 停用開啟頁面 {#open-page}

您可以新增以下後設資料，在應用程式內完全隱藏「**開啟頁面**」按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## 停用重複按鈕 {#duplicate-button}

某些製作工作流程可能需要限制內容作者複製元件的能力。您可以新增以下後設資料來停用「[重複圖示](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate)」。

```html
<meta name="urn:adobe:aue:config:disable" content="duplicate"/>
```

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
