---
title: 自訂 Universal Editor
description: 瞭解自訂Universal Editor的各種選項，以支援內容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 32b3a125d6370dd591252fde342843d5f9e33cf1
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---


# 自訂 Universal Editor {#customizing}

瞭解自訂Universal Editor的各種選項，以支援內容作者的需求。

>[!TIP]
>
>Universal Editor也提供許多[擴充點，](/help/implementing/universal-editor/extending.md)可讓您擴充其功能以滿足您的專案需求。

## 停用發佈 {#disable-publish}

某些編寫工作流程在發佈內容之前必須先進行稽核。 在這種情況下，任何作者都不能使用發佈選項。

因此，可以新增下列中繼資料，在應用程式中完全隱藏&#x200B;**發佈**&#x200B;按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## 停用發佈以預覽 {#publish-preview}

某些編寫工作流程可能會排除發行至[預覽服務](/help/sites-cloud/authoring/sites-console/previewing-content.md) （如果有的話）。

因此，可以新增下列中繼資料，在應用程式中完全隱藏發佈視窗中的&#x200B;**預覽**&#x200B;選項。

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## 停用開啟頁面 {#open-page}

新增下列中繼資料，可完全在應用程式中隱藏&#x200B;**開啟頁面**&#x200B;按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## 停用複製按鈕 {#duplicate-button}

某些編寫工作流程可能需要限制內容作者複製元件的能力。 您可以新增下列中繼資料，以停用[重複圖示](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate)。

```html
<meta name="urn:adobe:aue:config:disable" content="duplicate"/>
```

## 變更您的端點 {#custom-endpoint}

如果您不想使用由Adobe託管但您自己託管版本的通用編輯器服務，可以在中繼標籤中設定此專案。 如需詳細資訊，請參閱檔案[AEM中的通用編輯器快速入門](/help/implementing/universal-editor/getting-started.md##configuration-settings)。

## 篩選元件 {#filtering-components}

您可以使用元件篩選器，在通用編輯器中限制每個容器允許的元件。 如需詳細資訊，請參閱檔案[篩選元件](/help/implementing/universal-editor/filtering.md)。

## 有條件地顯示和隱藏屬性面板中的元件 {#conditionally-hide}

雖然元件通常可供作者使用，但在某些情況下卻可能沒有意義。 在這種情況下，您可以將`condition`屬性新增至元件模型[的](/help/implementing/universal-editor/field-types.md#fields)欄位，以隱藏屬性面板中的元件。

可以使用[JsonLogic結構描述](https://jsonlogic.com/)定義條件。 如果條件為true，則會顯示欄位。 如果條件為false，則會隱藏欄位。

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

>[!TAB 條件False]

![隱藏的文字欄位](assets/hidden.png)

>[!TAB 條件True]

![顯示的文字欄位](assets/shown.png)

>[!ENDTABS]

## 自訂預覽URL {#custom-preview-urls}

您可以透過`urn:adobe:aue:config:preview`中繼設定來指定自訂預覽URL，按一下&#x200B;**編輯器右上角工具列**&#x200B;中的[開啟頁面](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)按鈕時，將會開啟該設定。

若要這麼做，只需將所需的預覽URL加入所檢測應用程式的中繼標籤中，例如下列範例。

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
