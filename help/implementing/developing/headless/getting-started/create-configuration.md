---
title: 建立配置無頭快速入門手冊
description: 建立設定，這是開始使用AEM as aCloud Service中的無頭設定的第一步。
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# 建立配置無頭快速入門手冊{#creating-configuration}

若要開始使用AEM as aCloud Service中的無頭式裝置，您必須建立設定。

## 什麼是配置？{#what-is-a-configuration}

「設定瀏覽器」提供AEM中設定的一般設定API、內容結構、解析機制。

在AEM無頭式內容管理的情境中，請將設定視為AEM內可供您建立內容模型（定義未來內容和內容片段的結構）的工作場所。 您可以有多個設定來分隔這些模型。

如果您熟悉完整堆疊AEM實作中的[頁面範本，](/help/sites-cloud/authoring/features/templates.md)管理內容模型的設定使用方式類似。

## 如何建立配置{#how-to-create-a-configuration}

管理員只需建立一次設定，或在組織內容模型時需要新工作區時，非常自然。 為了使用本快速入門手冊，我們只需建立一個配置。

1. 以Cloud Service身分登入AEM，然後在主功能表中選取&#x200B;**工具 — >一般 — >設定瀏覽器**。
1. 為您的設定提供&#x200B;**Title**&#x200B;和&#x200B;**Name**。
   * **Title**&#x200B;應是描述性的。
   * **Name**&#x200B;將成為儲存庫中的節點名稱。
      * 系統會根據標題自動產生，並根據[AEM命名慣例進行調整。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有需要，可加以調整。
1. 勾選下列選項：
   * **內容片段模型**
   * **GraphQL持久查詢**

   ![建立設定](../assets/create-configuration.png)

1. 點選或按一下&#x200B;**建立**

您可以視需要建立多個設定。 配置也可嵌套。

>[!NOTE]
>
>視您的實作需求而定，除了&#x200B;**內容片段模型**&#x200B;和&#x200B;**GraphQL持久查詢**&#x200B;外，可能還需要設定選項。

## 後續步驟{#next-steps}

使用此配置，您現在可以轉到快速入門手冊的第二部分，並[建立內容片段模型。](create-content-model.md)

>[!TIP]
>
>有關配置瀏覽器的完整詳細資訊，請[參閱配置瀏覽器文檔。](/help/implementing/developing/introduction/configurations.md)
