---
title: 篩選元件
description: 了解如何使用元件篩選器限制通用編輯器中每個容器所允許的元件。
feature: Developing
role: Admin, Architect, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: cdad4954b13f5582bebfd604220da90529231ccd
workflow-type: ht
source-wordcount: '153'
ht-degree: 100%

---

# 篩選元件 {#filtering-components}

了解如何使用元件篩選器限制通用編輯器中每個容器所允許的元件。

## 篩選器 {#filters}

使用通用編輯器時，您可以限制每個容器元件所允許的元件。為了做到這點，您必須額外引進指向篩選器定義的指令碼標記。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

篩選器定義可能如下所示，其會限制容器僅能允許新增文字和影像。

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

然後，您可以新增 `data-aue-filter` 屬性，把先前定義的篩選器 ID 傳遞出去，便可以參照來自容器元件的篩選器定義。

```html
data-aue-filter="container-filter"
```

將篩選器定義中的 `components` 屬性設定為 `null`，會允許所有元件，如同沒有篩選器一般。

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
>參閱以下文件，了解通用編輯器能夠使用的其他自訂和擴充選項：
>
>* [自訂通用編輯器](/help/implementing/universal-editor/customizing.md)
>* [擴充通用編輯器](/help/implementing/universal-editor/extending.md)
