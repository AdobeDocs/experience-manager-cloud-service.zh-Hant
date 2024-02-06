---
title: 自訂通用編輯器編寫體驗
description: 瞭解不同的擴充點和其他功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: f04ab32093371ff425c4e196872738867d9ed528
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# 自訂通用編輯器編寫體驗 {#customizing-ue}

瞭解不同的擴充點和其他功能，這些功能可讓您自訂Universal Editor的撰寫體驗，以支援內容作者的需求。

## 停用發佈 {#disable-publish}

某些編寫工作流程在發佈內容之前必須先進行稽核。 在這種情況下，任何作者都不能使用發佈選項。

此 **發佈** 因此，您可以新增下列中繼資料，完全抑制應用程式中的按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## 篩選元件 {#filtering-components}

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

## 有條件地顯示和隱藏屬性邊欄中的元件 {#conditionally-hide}

雖然元件通常可供作者使用，但在某些情況下卻可能沒有意義。 在這種情況下，您可以新增「 」，以隱藏屬性邊欄中的元件 `condition` 屬性至 [元件模型的欄位。](/help/implementing/universal-editor/field-types.md#fields)

可使用以下專案定義條件 [JsonLogic結構描述。](https://jsonlogic.com/) 如果條件為true，則會顯示欄位。 如果條件為false，則會隱藏欄位。

### 範例模型 {#sample-model}

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

#### 條件False {#false}

![隱藏文字欄位](assets/hidden.png)

#### 條件True {#true}

![顯示的文字欄位](assets/shown.png)
