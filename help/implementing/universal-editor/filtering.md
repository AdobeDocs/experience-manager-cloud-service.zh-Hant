---
title: 篩選器
description: 瞭解如何定義篩選器以限制編輯器中可用的選項，例如可用元件、RTE選項和資產選擇。
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 15%

---


# 篩選器 {#filters}

瞭解如何定義篩選器以限制編輯器中可用的選項，例如可用元件、RTE選項和資產選擇。

## 設定篩選器 {#configuring-filters}

使用通用編輯器時，您可以定義篩選器來限制特定功能允許的選項。 篩選器是特定前後關聯可用的專案或動作清單。 例如，您可以篩選可插入容器的可用元件，您可以[篩選RTE中可用的選項，](/help/implementing/universal-editor/configure-rte.md)以及您可以[篩選資產選取器中的可用資產](/help/implementing/universal-editor/configure-assets-selector.md)。

所有篩選器的定義都必須類似。

1. [新增指令碼標籤以指向篩選器定義](#add-tag)
1. [定義篩選器](#define-filter)
1. [參考篩選器](#reference-filter)

讓我們舉一個依容器元件篩選元件的範例。

## 參考篩選器定義 {#add-tag}

首先，引進其他指令碼標籤，指向篩選器定義。

在我們的範例中，為每一個容器篩選允許的元件，標籤看起來可能會像這樣。

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

## 定義篩選 {#define-filter}

篩選器定義包含的JSON具有篩選器唯一ID和篩選器准則。

在我們的範例中，若要篩選每個容器允許的元件，可能會如下所示，這會限制容器僅允許新增文字和影像。

```json
[
  {
    "id": "container-filter",
    "components": ["text", "image"]
   }
]
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

## 參考篩選器 {#reference-filter}

若要使用篩選器，您必須參考篩選器定義。 您可以透過以下方式進行：

* 透過新增屬性`data-aue-filter`，傳遞篩選的ID，從容器元件參照篩選。

  ```html
  data-aue-filter="container-filter"
  ```

* 從您的[元件定義參考篩選器，](/help/implementing/universal-editor/component-definition.md)傳遞篩選器的ID。

  ```json
  {
     "title":"My Container",
     "id":"my-container",
     "model": "my-model",
     "filter": "container-filter",
     ...
  }
  ```

## 其他資源 {#additional-resources}

參閱以下文件，了解通用編輯器能夠使用的其他自訂和擴充選項：

* [為通用編輯器設定RTE](/help/implementing/universal-editor/configure-rte.md)
* [設定Assets選擇器的篩選器](/help/implementing/universal-editor/configure-assets-selector.md)
* [自訂通用編輯器](/help/implementing/universal-editor/customizing.md)
* [擴充通用編輯器](/help/implementing/universal-editor/extending.md)
