---
title: 如何透過 AEM API 更新您的內容
description: 在 AEM Headless 開發人員歷程的這一部分中，了解如何透過可用的 API 存取和更新內容片段的內容。
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: 8a3ee333a0bd5904c43c424967a7b9c752fd38c2
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 99%

---

# 如何透過 AEM API 更新您的內容 {#update-your-content}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，了解如何透過可用的 API 存取和更新內容片段的內容。

## 目前進度 {#story-so-far}

在 AEM Headless 歷程的上一份文件「[如何透過 AEM Delivery API 存取您的內容](access-your-content.md)」中，您已了解如何透過 AEM GraphQL API 存取 AEM 中的 Headless 內容，現在您應該：

* 對 GraphQL 有概略的了解。
* 了解 AEM GraphQL API 運作方式。
* 了解一些實際的範例查詢。

本文章以這些基本知識為基礎，以便您了解如何透過可用的 API 在 AEM 更新您的現有 Headless 內容。

## 目標 {#objective}

* **客群**：進階
* **目標**：了解可用來存取和更新內容片段之內容的 API。

## 與內容片段搭配使用的 AEM API {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service 為內容片段的結構化內容傳遞和內容片段管理提供多個 API。關於特定 API 的更多詳細資訊，請參閱個別頁面。

* 透過 OpenAPI 傳遞 AEM 內容片段
   * 此 API 建立 JSON 回應，用於在 AEM 中傳遞來自內容片段的結構化內容。
   * 其使用內容片段的路徑做為端點。
   * 此 API 以 REST 為基礎。
   * 其針對內容傳遞包括 CDN 整合進行最佳化。
* 用於傳遞內容片段的 AEM GraphQL API
   * 此 API 以結構描述為基礎。API 結構描述由內容片段模型呈現，其會定義內容結構。
   * 此 API 以 GraphQL 為基礎。
* 內容片段和內容片段模型的 OpenAPI
   * 這些 API 是用來管理結構化內容。
   * 各 GET 運算子並未針對內容傳遞進行最佳化。
   * 此 API 以 REST 為基礎。

>[!NOTE]
>
>[Assets HTTP API 中支援內容片段](/help/assets/content-fragments/assets-api-content-fragments.md)的功能現在[已棄用](/help/release-notes/deprecated-removed-features.md)。目前已由[透過 OpenAPI 傳遞 AEM 內容片段](/help/headless/aem-content-fragment-delivery-with-openapi.md)以及[內容片段與內容片段模型管理 OpenAPI](/help/headless/content-fragment-openapis.md) 取代上述功能。

## 下一步 {#whats-next}

您已完成此部分的 AEM Headless 開發人員歷程，您應該：

* 了解可用的 AEM API。
* 了解這些 API 如何支援內容片段。

您應該繼續您的 AEM Headless 歷程，接下來查看文件[如何在 AEM Headless 中將您的應用程式和內容組合在一起](put-it-all-together.md)您將在其中熟悉 AEM 架構基本知識和將應用程式組合在一起所需的工具。

## 其他資源 {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [用於傳遞和管理結構化內容的 AEM API](/help/headless/apis-headless-and-content-fragments.md)
* [透過 OpenAPI 傳遞 AEM 內容片段](/help/headless/aem-content-fragment-delivery-with-openapi.md)
* [用於傳遞內容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [內容片段和內容片段模型的 OpenAPI](/help/headless/content-fragment-openapis.md)
* [AEM Assets HTTP API 中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)
* [使用內容片段](/help/sites-cloud/administering/content-fragments/overview.md)
* [AEM 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [CORS/AEM 說明](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
* [影片 - 使用 AEM 開發 CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
* [AEM as a Headless CMS 簡介](/help/headless/introduction.md)
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM 中的 Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
