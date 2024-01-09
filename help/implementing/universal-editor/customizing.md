---
title: 自訂UI
description: 瞭解不同的擴充功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。
source-git-commit: 65893c0c0dee37bed8ecfbb06a12e7c093c4397c
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# 自訂UI {#customizing-ui}

瞭解不同的擴充功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。

## 停用發佈 {#disable-publish}

某些編寫工作流程在發佈內容之前必須先進行稽核。 在這種情況下，任何作者都不能使用發佈選項。

此 **發佈** 因此，您可以新增下列中繼資料，在應用程式中完全隱藏按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```
