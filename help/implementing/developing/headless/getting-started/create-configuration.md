---
title: 《 Creating a Configuration Headless Quick Start Guide》（建立配置無頭快速入門手冊）
description: 在AEM中以Cloud Service的形式開始使用無頭功能的第一步，您需要建立設定。
translation-type: tm+mt
source-git-commit: 259d54a225f8dee5929f62b784e28f3fc2bb794a
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---


# 《 Creating a Configuration Headless Quick Start Guide {#creating-configuration}》

在AEM中以Cloud Service的形式開始使用無頭功能的第一步，您需要建立設定。

## 什麼是配置？{#what-is-a-configuration}

「設定瀏覽器」提供AEM中設定的一般設定API、內容結構、解析機制。

在AEM中無頭內容管理的環境中，請將設定想成AEM中的工作場所，您可在其中建立內容模型，以定義未來內容和內容片段的結構。 您可以有多種配置來分隔這些模型。

如果您熟悉完整堆疊AEM實作中的[頁面範本，](/help/sites-cloud/authoring/features/templates.md)內容模型管理組態的使用方式類似。

## 如何建立配置{#how-to-create-a-configuration}

管理員只需建立一次設定，或在組織內容模型時需要新工作區時，管理員可自行建立設定。 為了本快速入門手冊的目的，我們只需建立一個設定。

1. 以雲端服務的身分登入AEM，並從主功能表選擇「**工具->一般->組態瀏覽器**」。
1. 為您的配置提供&#x200B;**Title**&#x200B;和&#x200B;**Name**。
   * **Title**&#x200B;應為描述性。
   * **Name**&#x200B;將成為儲存庫中的節點名。
      * 系統會根據標題自動產生，並根據[AEM命名慣例進行調整。](/help/implementing/developing/introduction/naming-conventions.md)
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
