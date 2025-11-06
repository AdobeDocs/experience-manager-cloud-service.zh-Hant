---
title: 分析內容片段
description: 瞭解您的內容片段的結構。 如此可提供與Headless傳送和頁面製作相關的資訊。
feature: Content Fragments
role: User, Developer
exl-id: d9268c1a-bfe6-4df7-bad9-6007dd79e0aa
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 3%

---

# 分析內容片段結構 {#analyzing-content-fragments-structure}

內容片段是專為使用GraphQL[的](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)Headless傳遞所設計。 這表示它們可以具有多層結構。

Experience Manager (AEM)提供數種檢視和分析片段結構的方法。

## 參照 {#references}

多層結構是使用「參照」建立的：

* [參考的資料型別在內容片段模型中定義](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* 編寫時，您可以：
   * [管理這些參考資料](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [尋找片段的父參照](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## 結構樹 {#structure-tree}

從編輯器工具列開啟&#x200B;**結構樹狀結構**&#x200B;標籤，以顯示內容片段及其參照的階層結構。 使用連結圖示開啟參照。

例如：

![內容片段編輯器 — 結構樹狀結構](assets/cf-authoring-structure-tree.png)
