---
title: 用於所見即所得和文件型製作的區塊
description: 了解如何建立可同時用於所見即所得製作和文件型製作的區塊。
feature: Edge Delivery Services
role: User
source-git-commit: 3419fa943eb865d87467443527ea97fcd64909c2
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---


# 用於所見即所得和文件型製作的區塊 {#wysiwyg-and-doc-blocks}

了解如何建立可同時用於所見即所得製作和文件型製作的區塊。

## 概觀 {#overview}

在某些專案中，您可能會希望同時支援[使用通用編輯器的所見即所得製作](/help/edge/wysiwyg-authoring/authoring.md)以及[文件型製作。](/help/edge/docs/authoring.md)為了盡量縮短開發時程並確保相同的網站體驗，您可以建立一組區塊來支援這兩種使用案例。

若要做到這一點，您必須對所見即所得製作設定和文件型製作設定使用相同的內容建模方法。

## 方法 {#approach}

在 AEM 的所見即所得製作中，[宣告模型](/help/edge/wysiwyg-authoring/content-modeling.md)並提供命名慣例。資料便會透過 Edge Delivery 呈現在類似表格的區塊結構中，就像使用文件型製作手動建立表格一樣。

為了達到這樣的結果，需要做出某些假設，例如對於像 Teaser 這樣的簡單區塊，所有的屬性和屬性群組都會以 1..n 列的形式呈現，每列只有一欄。對於具有 1..n 個項目的區塊 (例如輪播和卡片)，這些項目會附加在這些列之後，每列一個項目，每個屬性/屬性群組一欄。

如果您依照相同的方法進行文件型製作，可以重複使用所見即所得區塊。
