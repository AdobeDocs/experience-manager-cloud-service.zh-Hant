---
title: 建立設定 — Headless設定
description: 建立設定是在 AEM as a Cloud Service 中開始使用 Headless 的第一步。
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 68%

---

# 建立設定 — Headless設定 {#create-configuration}

在 AEM as a Cloud Service 中開始使用 Headless 的第一步，您需要建立設定。

## 什麼是設定？ {#what-is-a-configuration}

設定瀏覽器提供一般 API、內容結構、解析機制用於 AEM 中的設定。

在 AEM Headless 內容管理的環境中，將設定視為 AEM 中的工作區，您可以在其中建立內容模型，該內容模型定義未來內容和內容片段的結構。您可以有多個設定來將這些模型分開。

如果您熟悉完整棧疊AEM實作[中的](/help/sites-cloud/authoring/page-editor/templates.md)頁面範本，使用組態來管理內容模型的方式會類似。

## 如何建立設定 {#how-to-create-a-configuration}

系統管理員一次只需建立一個設定，或者在需要新工作區來組織內容模型時建立，這個情況很少發生。出於本快速入門指南的目的，我們只需要建立一個設定。

如需逐步詳細資訊，請參閱[在設定瀏覽器](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)中啟用內容片段功能。

>[!NOTE]
>
>除了 **內容片段模型**&#x200B;和&#x200B;**GraphQL 持續性查詢** 之外，有些設定選項可能是必要的，視您的實作要求而定。

## 後續步驟 {#next-steps}

使用此設定，您現在可以移至快速入門手冊的第二部分，並[建立內容片段模型](create-content-model.md)。

>[!TIP]
>
>如需有關組態瀏覽器的完整詳細資訊，請參閱[組態瀏覽器檔案](/help/implementing/developing/introduction/configurations.md)。
