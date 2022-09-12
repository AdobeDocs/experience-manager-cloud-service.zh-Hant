---
title: 建立配置 — 無頭設定
description: 在AEM as a Cloud Service中建立設定，這是開始使用無頭設定的第一步。
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---

# 建立配置 — 無頭設定 {#creating-configuration}

在AEM as a Cloud Service中開始使用無頭功能的第一步，您需要建立設定。

## 什麼是配置？ {#what-is-a-configuration}

「設定瀏覽器」提供AEM中設定的一般設定API、內容結構、解析機制。

在AEM無頭式內容管理的情境中，請將設定視為AEM內可供您建立內容模型（定義未來內容和內容片段的結構）的工作場所。 您可以有多個設定來分隔這些模型。

如果您熟悉 [完整堆疊AEM實作中的頁面範本，](/help/sites-cloud/authoring/features/templates.md) 配置在管理內容模型時的用法類似。

## 如何建立設定 {#how-to-create-a-configuration}

管理員只需建立一次設定，或在組織內容模型時需要新工作區時，非常自然。 為了使用本快速入門手冊，我們只需建立一個配置。

1. 登入AEMas a Cloud Service，然後從主功能表選取 **工具 — >常規 — >配置瀏覽器**.
1. 提供 **標題** 和 **名稱** 的URL。
   * 此 **標題** 應是描述性的。
   * 此 **名稱** 會成為存放庫中的節點名稱。
      * 根據標題自動產生並根據 [AEM命名慣例。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有需要，可加以調整。
1. 勾選下列選項：
   * **內容片段模型**
   * **GraphQL持續查詢**

   ![建立設定](../assets/create-configuration.png)

1. 點選或按一下 **建立**

您可以視需要建立多個設定。 配置也可嵌套。

>[!NOTE]
>
>除了 **內容片段模型** 和 **GraphQL持續查詢** 視您的實作需求而定，可能是必要的。

## 後續步驟 {#next-steps}

使用此設定，您現在可以繼續前往快速入門手冊的第二部分，以及 [建立內容片段模型。](create-content-model.md)

>[!TIP]
>
>如需設定瀏覽器的完整詳細資訊， [請參閱設定瀏覽器檔案。](/help/implementing/developing/introduction/configurations.md)
