---
title: 自訂 UI
description: 瞭解不同的擴充功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 6%

---


# 自訂 UI {#customizing-ui}

瞭解不同的擴充功能，這些功能可讓您自訂Universal Editor的UI，以支援內容作者的需求。

## 停用發佈 {#disable-publish}

某些編寫工作流程在發佈內容之前必須先進行稽核。 在這種情況下，任何作者都不能使用發佈選項。

此 **發佈** 因此，您可以新增下列中繼資料，在應用程式中完全隱藏按鈕。

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```
