---
title: 自訂和擴充通用編輯器
description: 瞭解不同的擴充點和其他功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---


# 自訂和擴充通用編輯器 {#customizing-extending}

瞭解不同的擴充點和其他功能，這些功能可讓您自訂Universal Editor的撰寫體驗，以支援內容作者的需求。

## 概觀 {#overview}

Universal Editor允許兩種型別的調整，以滿足您專案的需求。

* [自訂通用編輯器](#customizing) — 可透過數個自訂設定調整通用編輯器的標準功能。
* [擴充通用編輯器UI](#extending) — 也可使用App Builder擴充通用編輯器的UI，以符合您的專案需求。

以下各節將詳細介紹這兩種型別。

## 自訂 Universal Editor {#customizing}

Universal Editor提供數個內建選項，可用於自訂其功能。

### 停用發佈 {#disable-publish}

某些編寫工作流程在發佈內容之前必須先進行稽核。 在這種情況下，任何作者都不能使用發佈選項。

因此，可以新增下列中繼資料，在應用程式中完全隱藏&#x200B;**Publish**&#x200B;按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### 篩選元件 {#filtering-components}

您可以使用元件篩選器，在通用編輯器中限制每個容器允許的元件。 如需詳細資訊，請參閱檔案[篩選元件](/help/implementing/universal-editor/filtering.md)。

### 有條件地顯示和隱藏屬性面板中的元件 {#conditionally-hide}

雖然元件通常可供作者使用，但在某些情況下卻可能沒有意義。 在這種情況下，您可以將`condition`屬性新增至元件模型](/help/implementing/universal-editor/field-types.md#fields)的[欄位，以隱藏屬性面板中的元件。

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

### 自訂預覽URL {#custom-preview-urls}

您可以透過`urn:adobe:aue:config:preview`中繼設定來指定自訂預覽URL，按一下[編輯器右上角工具列](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)中的&#x200B;**開啟頁面**&#x200B;按鈕時，將會開啟該設定。

這對於具有特定預覽需求的應用程式特別有用，例如那些將Edge Delivery Services與WYSIWYG編寫](/help/edge/wysiwyg-authoring/authoring.md)搭配使用的[。

若要這麼做，只需將所需的預覽URL加入所檢測應用程式的中繼標籤中，例如下列範例。

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

## 擴充通用編輯器UI {#extending}

作為Adobe Experience Cloud服務，Universal Editor的UI可以使用App Builder和Experience Manager進行擴充。

UI擴充功能是使用Adobe App Builder建置的JavaScript應用程式，可嵌入在Adobe Experience Cloud unified shell底下執行的UI應用程式（例如Universal Editor）中。 您可以將自己的按鈕和動作新增到頁首功能表和屬性面板，以及為通用編輯器建立自己的事件。

如果您想探索這些可能性，請參閱下列資源：

1. [UI擴充功能](https://developer.adobe.com/uix/docs/) — 這是UI擴充功能的開發人員檔案。
1. [UI擴充性指南](https://developer.adobe.com/uix/docs/guides/) — 如何開發您自己的擴充功能的逐步指示
1. [通用編輯器擴充點檔案](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) — 通用編輯器專用的擴充點檔案

>[!TIP]
>
>如果您偏好以範例學習，請參閱[AEM UI擴充性教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview)。 雖然重點在於擴充內容片段主控台，但在通用編輯器中實作UI擴充功能的概念是相同的。

[在AEM Sites中使用Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)，您可以根據每個執行個體來啟用或停用擴充功能、存取Adobe的第一方擴充功能（包括Universal Editor的擴充功能）等等。
