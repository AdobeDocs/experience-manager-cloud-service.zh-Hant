---
title: 建立 API 要求 - Headless 設定
description: 了解如何使用 GraphQL API Headless 傳遞內容片段，以及如何使用 AEM Assets REST API 管理內容片段。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 88%

---

# 建立 API 要求 - Headless 設定 {#accessing-delivering-content-fragments}

了解如何使用 GraphQL API Headless 傳遞內容片段，以及如何使用 AEM Assets REST API 管理內容片段。

## 什麼是 GraphQL 和 Assets REST API？ {#what-are-the-apis}

[現在您已建立一些內容片段](create-content-fragment.md)，您可以使用AEM的API來無頭傳送。

* [GraphQL API](/help/headless/graphql-api/content-fragments.md) 可讓您建立存取和傳遞內容片段的要求。這個 API 提供了一組最強大的功能來查詢和取用內容片段內容。
   * 若要使用 API，[在 AEM 中定義和啟用端點](/help/headless/graphql-api/graphql-endpoint.md)，如果需要，[安裝 GraphiQL 介面](/help/headless/graphql-api/graphiql-ide.md)。
* 結構化內容傳遞和管理[的](/help/headless/apis-headless-and-content-fragments.md)AEM API可供內容片段使用。

本指南的其餘部分著重在 GraphQL 存取和內容片段傳遞。

## 啟用 GraphQL 端點 {#enable-graphql-endpoint}

必須建立 GraphQL 端點，才能使用 GraphQL API。

如需詳細資訊，請參閱[在AEM中管理GraphQL端點](/help/headless/graphql-api/graphql-endpoint.md)。

## 使用 GraphQL 和 GraphiQL 查詢內容

資訊架構師會為他們的管道端點設計查詢，以便傳遞內容。只需要為每個模型的每個端點考慮一次這些查詢。出於本快速入門指南的目的，您只需要建立一個。

GraphiQL 是包含在您 AEM 環境中的 IDE，在[設定您的端點](#enable-graphql-endpoint)後，即可存取/看見它。

如需詳細資訊，請參閱[使用GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)。

GraphQL 支援結構化查詢，這些查詢不僅可以針對特定資料集或個別資料物件，還可以傳遞物件的特定元素、巢狀結果、支援查詢變數等等。

GraphQL 可以避免反覆 API 要求和過度傳遞，而是允許大量傳遞轉譯作業所需的內容，作為對單一 API 查詢的回應。產生的 JSON 可用於將資料傳遞到其他網站或應用程式。

## 後續步驟 {#next-steps}

就是這樣！您現在對 AEM Headless 內容管理有基本的了解。還有更多資源可供您深入研究以全面了解可用的功能。

* **[內容片段](/help/sites-cloud/administering/content-fragments/managing.md)** - 詳細說明如何建立和管理內容片段
* **[AEM Assets HTTP API 支援內容片段](/help/assets/content-fragments/assets-api-content-fragments.md)** - 詳細說明如何運用 CRUD 操作 (建立、讀取、更新、刪除) 透過 HTTP API 直接存取 AEM 內容。
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)** - 詳細說明如何以 Headless 方式傳遞內容片段

>[!NOTE]
>
>也提供[內容片段和內容片段模型 OpenAPI](/help/headless/content-fragment-openapis.md)。
