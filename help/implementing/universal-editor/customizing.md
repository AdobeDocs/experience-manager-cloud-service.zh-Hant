---
title: 自訂和擴充通用編輯器
description: 瞭解不同的擴充點和其他功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: bdd67fb383bf20399eacaf9b9c086ea8468ea742
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---


# 自訂和擴充通用編輯器 {#customizing-extending}

瞭解不同的擴充點和其他功能，這些功能可讓您自訂Universal Editor的撰寫體驗，以支援內容作者的需求。

## 概觀 {#overview}

Universal Editor允許兩種型別的調整，以滿足您專案的需求。

* [自訂通用編輯器](#customizing)  — 可透過數個自訂設定調整通用編輯器的標準功能。
* [擴充通用編輯器UI](#extending)  — 也可使用App Builder擴充通用編輯器的UI，以符合您的專案需求。

以下各節將詳細介紹這兩種型別。

## 自訂 Universal Editor {#customizing}

Universal Editor提供數個內建選項，可用於自訂其功能。

### 停用發佈 {#disable-publish}

某些編寫工作流程在發佈內容之前必須先進行稽核。 在這種情況下，任何作者都不能使用發佈選項。

此 **發佈** 因此，您可以新增下列中繼資料，完全抑制應用程式中的按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### 篩選元件 {#filtering-components}

使用通用編輯器時，您可以限制每個容器元件允許的元件。 若要這麼做，您必須引入其他指令碼標籤，該標籤會指向篩選定義。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

篩選定義可能如下所示，將容器限製為僅允許新增文字和影像。

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

然後，您可以新增屬性，從容器元件參照篩選器定義 `data-aue-filter`，傳遞您先前定義之篩選器的ID。

```html
data-aue-filter="container-filter"
```

設定 `components` 篩選定義中的屬性至 `null` 會允許所有元件，就像沒有篩選器一樣。

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

### 有條件地顯示和隱藏屬性邊欄中的元件 {#conditionally-hide}

雖然元件通常可供作者使用，但在某些情況下卻可能沒有意義。 在這種情況下，您可以新增「 」，以隱藏屬性邊欄中的元件 `condition` 屬性至 [元件模型的欄位。](/help/implementing/universal-editor/field-types.md#fields)

可使用以下專案定義條件 [JsonLogic結構描述。](https://jsonlogic.com/) 如果條件為true，則會顯示欄位。 如果條件為false，則會隱藏欄位。

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

![隱藏文字欄位](assets/hidden.png)

>[!TAB 條件True]

![顯示的文字欄位](assets/shown.png)

>[!ENDTABS]

## 擴充通用編輯器UI {#extending}

作為Adobe Experience Cloud服務，Universal Editor的UI可以使用App Builder和Experience Manager來擴充。

UI擴充功能是以AdobeApp Builder建置的JavaScript應用程式，可嵌入在Adobe Experience Cloud統一殼層（例如Universal Editor）下執行的UI應用程式中。 您可以將自己的按鈕和動作新增到頁首功能表和屬性邊欄，並為通用編輯器建立自己的事件。

如果您想探索這些可能性，請參閱下列資源：

1. [UI擴充性](https://developer.adobe.com/uix/docs/)  — 這是UI擴充功能的開發人員檔案。
1. [UI擴充性指南](https://developer.adobe.com/uix/docs/guides/)  — 如何開發您自己的擴充功能的逐步指示
1. [Universal Editor延伸點](https://developer.adobe.com/uix/docs/services/aem-universal-editor/)  — 通用編輯器專用的擴充點檔案

>[!TIP]
>
>如果您偏好以範例學習，請參閱 [AEM UI擴充性教學課程。](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) 雖然重點在於擴充內容片段主控台，但在通用編輯器中實作UI擴充功能的概念是相同的。

[在AEM Sites中使用Extension Manager，](https://developer.adobe.com/uix/docs/extension-manager/) 您可以根據執行個體來啟用或停用擴充功能、存取Adobe的第一方擴充功能，包括通用編輯器的擴充功能等等。
