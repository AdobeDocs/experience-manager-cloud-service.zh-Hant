---
title: 用於結構化內容傳遞和內容片段管理的AEM API
description: 瞭解可用於結構化內容傳遞和內容片段管理的API
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: 95aecd30-566a-42a9-b97a-7efe45fd389c
source-git-commit: 1995c84bb669fd52ecd53c7e695acc518a5226e8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 28%

---


# 用於傳遞和管理結構化內容的 AEM API {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager (AEM) as a Cloud Service 為內容片段的結構化內容傳遞和內容片段管理提供多個 API。關於特定 API 的更多詳細資訊，請參閱個別頁面。

* [透過 OpenAPI 傳遞 AEM 內容片段](/help/headless/aem-content-fragment-delivery-with-openapi.md)
   * 此 API 建立 JSON 回應，用於在 AEM 中傳遞來自內容片段的結構化內容。
   * 其使用內容片段的路徑做為端點。
   * 此 API 以 REST 為基礎。
   * 其針對內容傳遞包括 CDN 整合進行最佳化。
* [用於傳遞內容片段的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
   * 此 API 以結構描述為基礎。API 結構描述由內容片段模型呈現，其會定義內容結構。
   * 此 API 以 GraphQL 為基礎。
* [內容片段和內容片段模型的 OpenAPI](/help/headless/content-fragment-openapis.md)
   * 這些 API 是用來管理結構化內容。
   * 各 GET 運算子並未針對內容傳遞進行最佳化。
   * 此 API 以 REST 為基礎。

>[!NOTE]
>
>Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)中的[內容片段支援現在[已棄用](/help/release-notes/deprecated-removed-features.md)。 已由[使用OpenAPI的內容片段傳送](/help/headless/aem-content-fragment-delivery-with-openapi.md)以及[內容片段和內容片段模型管理OpenAPI](/help/headless/content-fragment-openapis.md)取代。

## REST與GraphQL {#rest-vs-graphql}

使用的API是開發人員的決定，AEM支援兩者。

線上提供許多比較資料，但REST的一些重點和優點包括：

* 簡單性

   * 開發人員通常（會）熟悉HTTP和REST。 根據API報告](https://www.postman.com/state-of-api/)的[Postman狀態，有高比例的開發人員使用REST。

   * 透過簡單而熟悉。 使用REST時，不會出現關於誰擁有查詢以及誰擁有應用程式的組織問題，而GraphQL則可能出現這些問題。

   * 熟悉度（通常是）帶來廣泛的社群和工具環境。 這不是GraphQL固有的缺點，但對於REST而言可能會更廣闊、更深層。

   * 更簡單的方法也可以讓安全性實作更容易。 使用REST時，用於決定要呈現所有內容在使用者端應用程式中進行的篩選。 透過GraphQL，這會發生在使用者端與伺服器之間的結構描述型查詢中。

* 彈性

   * 透過REST，開發人員可以`GET`任何資源。 使用GraphQL時，這些資源會限制在結構描述中定義的資源。

* 快取

   * REST `GET`要求的JSON回應本身可快取。 無法快取GraphQL `POST`要求，除非進行快取；例如，使用儲存在伺服器上，並且以類似REST的`GET`要求要求的AEM持續查詢。

GraphQL的優點包括：

* 內容傳遞效率

   * 焦點

      * 透過GraphQL使用者端應用程式，可請求轉譯所需的確切內容，而且不再需要。 此方法可以防止內容過度傳送、內容負載過多以及不必要的頻寬消耗。

   * 單一端點

      * 在REST中，每個API要求都是端點，但在GraphQL中，只有一個通用端點，而不同的內容要求會使用該通用端點以查詢形式表示。

* 快速原型製作

   * 透過GraphQL，只需一步驟就能在GraphQL查詢中將其整合，讓建立原型更加容易。 另一方面，REST是兩步驟流程：

      1. 使用API擷取內容。
      2. 在JSON回應中，決定要在使用者端應用程式中呈現的內容。
