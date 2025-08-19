---
title: 使用內容片段搭配GraphQL (Assets — 內容片段)的Headless內容傳送
description: 瞭解將內容片段與AEM搭配使用以實現Headless內容傳送的GraphQLHeadless CMS的基本概念。
feature: Content Fragments
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
role: User
solution: Experience Manager Sites
source-git-commit: 0664e5dc4a7619a52cd28c171a44ba02c592ea3d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 27%

---

# 搭配GraphQL使用內容片段的Headless內容傳送 {#headless-content-delivery-using-content-fragments-with-graphQL}

透過內容片段和GraphQL API，您可以使用Adobe Experience Manager (AEM) as a Cloud Service當作Headless內容管理系統(CMS)。

這是使用內容片段及AEM GraphQL API (根據標準GraphQL的自訂實作)來達成，以無頭傳送結構化內容供您的應用程式使用。 自訂單一API查詢的功能可讓您擷取並傳遞您想要/需要呈現的特定內容（作為對單一API查詢的回應）。

>[!NOTE]
>
>另請參閱：
>
>* [什麼是Headless？](/help/headless/what-is-headless.md)了解 Headless 概念和術語。
>
>* [Headless與AEM](/help/headless/introduction.md)，瞭解AEM Sites as a Cloud Service的Headless開發簡介。

>[!NOTE]
>
>GraphQL 目前在 Adobe Experience Manager (AEM) as a Cloud Service 中用於兩個 (獨立) 情況：
>
>* [AEM Commerce透過GraphQL使用來自commerce平台的資料。](/help/commerce-cloud/cif-storefront/integrating/magento.md)
>* [AEM內容片段與AEM GraphQL API (根據標準GraphQL的自訂實作)搭配使用，提供結構化內容用於您的應用程式](/help/headless/graphql-api/content-fragments.md)。

## Headless CMS {#headless-cms}

Headless內容管理系統(CMS)是僅用於後端的內容管理系統，其明確作為內容存放庫而設計和建置，可透過API存取內容以在任何裝置上顯示。

在AEM中編寫內容片段方面，這表示：

* 您可以使用內容片段來編寫主要不打算在格式化頁面上直接發佈(1:1)的內容。

* 您的內容片段的內容以預先決定的方式結構化 — 根據內容片段模式。 這可簡化應用程式的存取，進而處理您的內容。

## GraphQL — 概觀 {#graphql-overview}

GraphQL 是：

* *...一種用於API和執行階段的查詢語言，以使用您現有的資料滿足這些查詢。*。

  請參閱 [GraphQL.org](https://graphql.org)

[AEM GraphQL API](#aem-graphql-api)可讓您對[內容片段](/help/assets/content-fragments/content-fragments.md)執行（複雜）查詢；每個查詢都根據特定的模型型別。 然後，您的應用程式可以使用傳回的內容。

## AEM GraphQL API {#aem-graphql-api}

針對Adobe Experience as a Cloud Experience，我們已開發標準GraphQL API的自訂實作。 如需詳細資訊，請參閱用於內容片段的[AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)。

AEM GraphQL API實作是以[GraphQL Java資料庫](https://graphql.org/code/#java)為基礎。

## 與 AEM GraphQL API 搭配使用的內容片段 {#content-fragments-use-with-aem-graphql-api}

[內容片段](#content-fragments)可作為AEM查詢的GraphQL基礎，如下所示：

* 它們可讓您設計、建立、策劃和發佈獨立於頁面的內容。
* [內容片段模型](#content-fragments-models)透過定義的資料型別提供所需的結構。
* 定義模型時可用的[片段參考](#fragment-references)可用來定義額外的結構層。

用於GraphQL的![內容片段](assets/cfm-nested-01.png "用於GraphQL的內容片段")

### 內容片段 {#content-fragments}

內容片段：

* 包含結構化內容。

* 它們以[內容片段模型](#content-fragments-models)為基礎，此模型預先定義了結果片段的結構。

### 內容片段模型 {#content-fragments-models}

這[個內容片段模型](/help/assets/content-fragments/content-fragments-models.md)：

* 用於產生[結構描述](https://graphql.org/learn/schema/)，一旦&#x200B;**啟用**。

* 提供 GraphQL 所需的資料類型和欄位。它們確保您的應用程式只要求可能的內容並接收預期的內容。

* **[片段參考](#fragment-references)**&#x200B;資料類型可在您的模型中用來參考另一個內容片段，從而引入額外的結構層。

### 片段參考 {#fragment-references}

**[片段參考](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**：

* 與GraphQL搭配使用特別令人感興趣。

* 是可在定義內容片段模式時使用的特定資料型別。

* 可參考另一個片段，取決於特定的內容片段模型。

* 可讓您擷取結構化資料。

   * 當定義為 **multifeed** 時，主片段可以參考 (擷取) 多個子片段。

### JSON 預覽 {#json-preview}

若要協助設計和開發您的內容片段模型，您可以預覽[JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)。

## 了解搭配使用 GraphQL 與 AEM - 範例內容和查詢 {#learn-graphql-with-aem-sample-content-queries}

請參閱[瞭解如何搭配AEM使用GraphQL — 範例內容和查詢](/help/headless/graphql-api/sample-queries.md)，以取得使用AEM GraphQL API的簡介。

## 教學課程 - AEM Headless 和 GraphQL 快速入門

正在尋找實作教學課程？查看 [AEM Headless 和 GraphQL 快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=zh-Hant)端對端教學課程，說明如何在 Headless CMS 情境下使用 AEM GraphQL API 建立和公開內容並供外部應用程式取用。
