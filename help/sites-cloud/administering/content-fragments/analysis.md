---
title: 分析內容片段
description: 瞭解您的內容片段的結構和內容傳送。 如此可提供Headless傳送和頁面編寫的相關資訊。
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 2%

---


# 分析內容片段結構 {#analyzing-content-fragments-structure}

內容片段是專為 [使用GraphQL的Headless傳遞](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). 這表示它們可以具有多層結構。

Experience Manager (AEM)提供數種檢視和分析片段結構的方法。

## 參考 {#references}

結構是使用「參照」建立的：

* [參考的資料型別在內容片段模型中定義](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* 編寫時，您可以：
   * [管理這些參考資料](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [尋找片段的父參照](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## 樹狀結構 {#structure-tree}

開啟 **樹狀結構** 標籤以顯示內容片段的階層結構及其參考。 使用連結圖示開啟參照。

例如：

![內容片段編輯器 — 結構樹](assets/cf-authoring-structure-tree.png)