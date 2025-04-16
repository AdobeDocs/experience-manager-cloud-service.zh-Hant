---
title: 如何使用AEM API更新您的內容
description: 在AEM Headless開發人員歷程的這一部分，瞭解如何使用可用的API來存取和更新內容片段的內容。
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 33%

---

# 如何使用AEM API更新您的內容 {#update-your-content}

在[AEM Headless開發人員歷程](overview.md)的這一部分，瞭解如何使用可用的API來存取和更新您的內容片段內容。

## 目前進度 {#story-so-far}

在 AEM Headless 歷程的上一份文件「[如何透過 AEM Delivery API 存取您的內容](access-your-content.md)」中，您已了解如何透過 AEM GraphQL API 存取 AEM 中的 Headless 內容，現在您應該：

* 對 GraphQL 有概略的了解。
* 了解 AEM GraphQL API 運作方式。
* 了解一些實際的範例查詢。

本文基於這些基礎之上，因此您瞭解如何透過可用的API在AEM中更新現有的Headless內容。

## 目標 {#objective}

* **客群**：進階
* **目標**：瞭解可用於存取和更新您的內容片段內容的API。

## 用於內容片段的AEM API {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service提供多個API，用於內容片段和內容片段管理的結構化內容傳遞。 如需特定API的詳細資訊，請參閱個別頁面。

* 使用OpenAPI的AEM內容片段傳送
   * 此API會建立JSON回應，用於從AEM中的內容片段傳送結構化內容。
   * 它使用內容片段的路徑作為端點。
   * 此API以REST為基礎。
   * 它已針對內容傳遞（包括CDN整合）進行最佳化。
* 用於內容片段傳送的AEM GraphQL API
   * 此API以結構描述為基礎。 API結構描述由內容片段模式表示，這些模式會定義內容結構。
   * 此API以GraphQL為基礎。
* 內容片段和內容片段模型的 OpenAPI
   * 這些API旨在用於結構化內容管理。
   * 個別的GET運運算元未針對內容傳遞進行最佳化。
   * 此API以REST為基礎。
* AEM Assets HTTP API中的內容片段支援
   * 用於AEM中結構化內容傳遞的JSON輸出的原始API。
      * 雖然此API健全且經過證明，但並未提供&#x200B;*完全水合的* JSON輸出。 參考僅輸出為路徑，需要次要API請求以擷取更多內容。
   * Assets HTTP API也可用來管理內容片段和內容片段模式(CRUD)。
   * 此API以REST為基礎。
   * Assets HTTP API中的內容片段支援未來將停止使用，因為Edge Delivery Services JSON REST API將成功提供支援。 時間刻度尚未決定。

## 下一步 {#whats-next}

您已完成此部分的 AEM Headless 開發人員歷程，您應該：

* 瞭解可用的AEM API。
* 瞭解這些API如何支援內容片段。

您應該繼續您的 AEM Headless 歷程，接下來查看文件[如何在 AEM Headless 中將您的應用程式和內容組合在一起](put-it-all-together.md)您將在其中熟悉 AEM 架構基本知識和將應用程式組合在一起所需的工具。

## 其他資源 {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [用於傳遞和管理結構化內容的 AEM API](/help/headless/apis-headless-and-content-fragments.md)
* [使用OpenAPI的AEM內容片段傳送](/help/headless/aem-content-fragment-delivery-with-openapi.md)
* [用於內容片段傳送的AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [內容片段和內容片段模型的 OpenAPI](/help/headless/content-fragment-openapis.md)
* [AEM Assets HTTP API中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)
* [使用內容片段](/help/sites-cloud/administering/content-fragments/overview.md)
* [AEM 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [CORS/AEM 說明](https://helpx.adobe.com/tw/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [影片 - 使用 AEM 開發 CORS](https://helpx.adobe.com/tw/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [AEM as a Headless CMS 簡介](/help/headless/introduction.md)
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM 中的 Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
