---
title: 《 Creating a Configuration Headless Quick Start Guide》（建立配置無頭快速入門手冊）
description: 建立設定，做為開始使用無頭功能的第一AEM步，做為Cloud Service。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---


# 《 Creating a Configuration Headless Quick Start Guide {#creating-configuration}》

作為開始將無頭引入作為Cloud Service的AEM第一步，您需要建立配置。

## 什麼是配置？{#what-is-a-configuration}

「配置瀏覽器」提供一般配置API、內容結構、中的配置解析機制AEM。

在無頭內容管理的范AEM圍中，將組態設為可建立內容模型的AEM工作場所，以定義未來內容和內容片段的結構。 您可以有多種配置來分隔這些模型。

如果您熟悉完整堆疊實作中的[頁面範本AEM,](/help/sites-cloud/authoring/features/templates.md)內容模型管理組態的使用方式類似。

## 如何建立配置{#how-to-create-a-configuration}

管理員只需建立一次設定，或在組織內容模型時需要新工作區時，管理員會非常自行地建立設定。 為了本快速入門手冊的目的，我們只需建立一個設定。

1. 以Cloud ServiceAEM身份登錄，從主菜單中選擇&#x200B;**工具->常規->配置瀏覽器**。
1. 為您的配置提供&#x200B;**Title**&#x200B;和&#x200B;**Name**。
   * **Title**&#x200B;應為描述性。
   * **Name**&#x200B;將成為儲存庫中的節點名。
      * 系統會根據標題自動產生，並根據[命AEM名慣例進行調整。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有需要，可加以調整。
1. 勾選下列選項：
   * **內容片段模型**
   * **GraphQL持久查詢**

   ![建立設定](../assets/create-configuration.png)

1. 點選或按一下&#x200B;**Create**

您可以視需要建立多種設定。 配置也可以嵌套。

>[!NOTE]
>
>視您的實作需求而定，可能需要&#x200B;**內容片段模型**&#x200B;和&#x200B;**GraphQL持久查詢**&#x200B;之外的配置選項。

## 後續步驟{#next-steps}

使用此配置，您現在可以移至入門指南的第二部分，並[建立內容片段模型。](create-content-model.md)

>[!TIP]
>
>有關配置瀏覽器的完整詳細資訊，請[參閱配置瀏覽器文檔。](/help/implementing/developing/introduction/configurations.md)
