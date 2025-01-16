---
title: 篩選元件
description: 瞭解如何使用元件篩選器，限制通用編輯器中每個容器允許的元件。
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 48c1a109c060db4ce19bf645723357008d51c572
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# 篩選元件 {#filtering-components}

瞭解如何使用元件篩選器，限制通用編輯器中每個容器允許的元件。

## 篩選條件 {#filters}

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

然後，您可以新增屬性`data-aue-filter`，傳遞您先前定義的篩選器ID，以參照容器元件的篩選器定義。

```html
data-aue-filter="container-filter"
```

將篩選定義中的`components`屬性設定為`null`可允許所有元件，就像沒有篩選一樣。

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

>[!TIP]
>
>在檔案[自訂和擴充通用編輯器](/help/implementing/universal-editor/customizing.md)中瞭解通用編輯器可用的其他自訂和擴充選項。
