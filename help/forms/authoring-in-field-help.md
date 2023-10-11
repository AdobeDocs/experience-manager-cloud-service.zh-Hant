---
title: 如何為AEM最適化Forms欄位新增說明文字？
description: AEM Forms可讓您將內容說明新增至最適化表單欄位和面板，做為文字或豐富媒體（包括影片）。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# 為表單欄位編寫內容內說明{#authoring-in-context-help-for-form-fields}

## 簡介 {#introduction}

有時候，填寫表單的使用者不確定如何在特定表單欄位中填寫詳細資訊。 為了解決這類問題，最適化Forms提供支援，以便在表單欄位中新增文字或RTF內容說明。 它有助於改善表單填寫體驗並避免一般使用者的任何歧義。

本文探討表單作者如何在編寫Adaptive Forms時新增內容相關說明。

## 新增內文中說明 {#add-in-context-help}

您可以使用側邊欄中「屬性」標籤的「說明內容」區段中的下列選項來指定內容內說明。

* [簡短說明](authoring-in-field-help.md#p-short-description-p)
* [詳細說明](authoring-in-field-help.md#p-long-description-p)

![表單欄位的內容中說明](assets/descriptions.png)

>[!NOTE]
>
>完整說明會覆寫簡短說明。 如果您同時指定兩者，則只會顯示完整說明。

### 簡短說明 {#short-description}

「簡短說明」欄位可提供有關填寫表單欄位的快速簡短提示。 將滑鼠懸停在簡短說明欄位中時，該欄位中指定的文字會顯示為工具提示。

![為表單欄位新增內容內說明的簡短說明](assets/tooltip.png)

>[!NOTE]
>
>選取 **一律顯示簡短說明** 以永久顯示欄位下方的說明文字。

![欄位下方的永久簡短內容說明](assets/short1.png)

### 詳細說明 {#long-description}

您可以使用「完整說明」欄位來指定完整文字或內嵌RTF內容（包括視訊），以做為內容說明。 例如，下圖說明如何將視訊內嵌為內容說明，

![新增多媒體作為表單欄位的內容內說明](assets/long-descriptions.png)

新增完整說明會顯示 **？** 圖示加以存取。 按一下圖示會顯示新增至詳細說明區段的內容。

![多媒體內容說明範例](assets/photoshop.png)

### 面板層級說明 {#panel-level-help}

除了表單欄位的內容中說明之外，您還可以在面板編輯對話方塊的「說明內容」標籤中，指定面板層級的說明。

![新增表單面板的內容內說明](assets/panel-level-help.png)

新增面板的說明顯示 **？** 圖示加以存取（位於面板說明旁）。 按一下圖示會顯示新增在面板編輯對話方塊的「說明內容」區段中的內容。

![表單面板層級的內容中說明範例](assets/photoshop-1.png)

