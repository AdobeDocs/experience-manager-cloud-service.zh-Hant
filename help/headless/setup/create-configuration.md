---
title: 建立設定 - Headless 設定
description: 建立設定是在 AEM as a Cloud Service 中開始使用 Headless 的第一步。
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 94%

---

# 建立設定 - Headless 設定 {#creating-configuration}

在 AEM as a Cloud Service 中開始使用 Headless 的第一步，您需要建立設定。

## 什麼是設定？ {#what-is-a-configuration}

設定瀏覽器提供一般 API、內容結構、解析機制用於 AEM 中的設定。

在 AEM Headless 內容管理的環境中，將設定視為 AEM 中的工作區，您可以在其中建立內容模型，該內容模型定義未來內容和內容片段的結構。您可以有多個設定來將這些模型分開。

如果您熟悉[全堆疊 AEM 實作中的頁面範本](/help/sites-cloud/authoring/features/templates.md)，用於管理內容模型之設定的用法是類似的。

## 如何建立設定 {#how-to-create-a-configuration}

系統管理員一次只需建立一個設定，或者在需要新工作區來組織內容模型時建立，這個情況很少發生。出於本快速入門指南的目的，我們只需要建立一個設定。

1. 登入AEMas a Cloud Service，並從主功能表選取 **「工具」>「一般」>「設定瀏覽器」**.
1. 提供設定的&#x200B;**標題**&#x200B;和&#x200B;**名稱**。
   * **標題** 應該是描述性的。
   * **名稱**&#x200B;會成為存放庫中的節點名稱。
      * 它會根據標題自動產生，並根據 [AEM 命名慣例](/help/implementing/developing/introduction/naming-conventions.md)進行調整。
      * 如有需要，可加以調整。
1. 檢查以下選項：
   * **內容片段模型**
   * **GraphQL 持續性查詢**

   ![建立設定](../assets/create-configuration.png)

1. 選取 **建立**

如果需要，您可以建立多個設定。設定也可以是巢狀。

>[!NOTE]
>
>除了 **內容片段模型**&#x200B;和&#x200B;**GraphQL 持續性查詢** 之外，有些設定選項可能是必要的，視您的實作要求而定。

## 後續步驟 {#next-steps}

使用此設定，您現在可以繼續閱讀快速入門指南的第二部分，並[建立內容片段模型。](create-content-model.md)

>[!TIP]
>
>如需設定瀏覽器的完整詳細資訊，[請參閱設定瀏覽器文件](/help/implementing/developing/introduction/configurations.md)。
