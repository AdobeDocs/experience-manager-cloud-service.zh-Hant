---
title: WYSIWYG和檔案式編寫的區塊
description: 瞭解如何建立可同時用於WYSIWYG編寫和檔案式編寫的區塊。
feature: Edge Delivery Services
role: User
source-git-commit: 3419fa943eb865d87467443527ea97fcd64909c2
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# WYSIWYG和檔案式編寫的區塊 {#wysiwyg-and-doc-blocks}

瞭解如何建立可同時用於WYSIWYG編寫和檔案式編寫的區塊。

## 概觀 {#overview}

在某些專案中，您可能會想要同時支援使用Universal Editor](/help/edge/wysiwyg-authoring/authoring.md)的[WYSIWYG撰寫以及[檔案式撰寫。](/help/edge/docs/authoring.md)為了將開發時間降到最低並確保相同的網站體驗，您可以建立一組區塊以支援這兩個使用案例。

為此，您必須對WYSIWYG製作設定和檔案式製作設定使用相同的內容模型方法。

## 方針 {#approach}

在AEM的WYSIWYG製作中，您可以[宣告模型](/help/edge/wysiwyg-authoring/content-modeling.md)並提供命名慣例。 然後使用Edge Delivery以類似表格的區塊結構呈現資料，其方式與使用檔案式撰寫手動建立表格的方式相同。

為此，會進行某些假設，例如，針對像Teaser這樣的簡單區塊，將所有屬性和屬性群組都呈現為1。n列，每列有單一欄。 針對具有1的區塊……n個專案（例如輪播和卡片），這些專案會附加在這些列之後，每個列會各一列，每個屬性/屬性群組各一欄。

如果您對檔案式製作採取相同方法，則可重複使用WYSIWYG區塊。
