---
title: 用於結構化內容傳遞和內容片段管理的AEM API
description: 瞭解可用於結構化內容傳遞和內容片段管理的API
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: 95aecd30-566a-42a9-b97a-7efe45fd389c
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# 用於傳遞和管理結構化內容的 AEM API {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager (AEM) as a Cloud Service提供多個API，用於內容片段和內容片段管理的結構化內容傳遞。 如需特定API的詳細資訊，請參閱個別頁面。

* [使用OpenAPI的AEM內容片段傳送](/help/headless/aem-content-fragment-delivery-with-openapi.md)
   * 此API會建立JSON回應，用於從AEM中的內容片段傳送結構化內容。
   * 它使用內容片段的路徑作為端點。
   * 此API以REST為基礎。
   * 它已針對內容傳遞（包括CDN整合）進行最佳化。
* [用於內容片段傳送的AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
   * 此API以結構描述為基礎。 API結構描述由內容片段模式表示，這些模式會定義內容結構。
   * 此API以GraphQL為基礎。
* [內容片段和內容片段模型的 OpenAPI](/help/headless/content-fragment-openapis.md)
   * 這些API旨在用於結構化內容管理。
   * 個別的GET運運算元未針對內容傳遞進行最佳化。
   * 此API以REST為基礎。
* [AEM Assets HTTP API中的內容片段支援](/help/assets/content-fragments/assets-api-content-fragments.md)
   * 用於AEM中結構化內容傳遞的JSON輸出的原始API。
      * 雖然此API健全且經過證明，但並未提供&#x200B;*完全水合的* JSON輸出。 參考僅輸出為路徑，需要次要API請求以擷取更多內容。
   * Assets HTTP API也可用來管理內容片段和內容片段模式(CRUD)。
   * 此API以REST為基礎。
   * Assets HTTP API中的內容片段支援未來將停止使用，因為Edge Delivery Services JSON REST API將成功提供支援。 時間刻度尚未決定。

<!--
## JSON vs HTML {#json-vs-HTML}

The content delivery format used is driven by frontend implementation. Unstructured content/HTML for full-stack implementations, structured content/JSON for headless implementations, or a combination of both in hybrid implementations. 

Key considerations include:

* Definition
  * JSON (JavaScript Object Notation) - used to represent, access and process structured data. 
  * HTML (HyperText Markup Language) - a markup language of tags and elements in a hierarchical structure.
* Primary Purpose
  * JSON is often used for transferring structure content between the server and client app.
  * HTML is the standard markup language for creating and rendering web pages in a browser.
-->

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
