---
title: 自訂 UI
description: 瞭解不同的擴充功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 1bc65e65e6ce074a050e21137ce538b5c086665f
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 3%

---


# 自訂 UI {#customizing-ui}

瞭解不同的擴充功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。

## 停用發佈 {#disable-publish}

某些編寫工作流程在發佈內容之前必須先進行稽核。 在這種情況下，任何作者都不能使用發佈選項。

此 **發佈** 因此，您可以新增下列中繼資料，在應用程式中完全隱藏按鈕。

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
