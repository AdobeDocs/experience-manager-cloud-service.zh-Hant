---
title: 透過GraphQL使用內容片段的Headless內容傳送
description: 瞭解透過GraphQL使用內容片段實現AEM Headless CMS以進行Headless內容傳送的基本概念。
feature: Content Fragments, GraphQL API
role: User
exl-id: ef48f737-a5b3-4913-9f37-6b9f681bc048
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 29%

---

# 透過GraphQL使用內容片段的Headless內容傳送 {#headless-content-delivery-using-content-fragments-with-graphQL}

透過內容片段和GraphQL API，您可以將Adobe Experience Manager (AEM) as a Cloud Service用作Headless內容管理系統(CMS)。

這是使用內容片段和AEM GraphQL API (根據標準GraphQL的自訂實施)來達成，以無頭傳送結構化內容供您的應用程式使用。 自訂單一API查詢的功能可讓您擷取並傳遞您想要/需要呈現的特定內容（作為對單一API查詢的回應）。

>[!NOTE]
>
>另請參閱:
>
>* [什麼是Headless？](/help/headless/what-is-headless.md)了解 Headless 概念和術語。
>
>* [Headless和AEM](/help/headless/introduction.md) 介紹AEM Sites的Headless開發as a Cloud Service。

>[!NOTE]
>
>GraphQL 目前在 Adobe Experience Manager (AEM) as a Cloud Service 中用於兩個 (獨立) 情況：
>
>* [AEM Commerce透過GraphQL使用來自Commerce平台的資料](/help/commerce-cloud/integrating/magento.md).
>* [AEM內容片段與AEM GraphQL API (根據標準GraphQL的自訂實施)搭配使用，提供結構化內容用於您的應用程式](/help/headless/graphql-api/content-fragments.md).

## Headless CMS {#headless-cms}

Headless內容管理系統(CMS)是僅用於後端的內容管理系統，其明確作為內容存放庫而設計和建置，使內容可透過API存取並在任何裝置上顯示。

在AEM中編寫內容片段時，這表示：

* 您可以使用內容片段來撰寫主要不打算在格式化頁面上直接發佈(1:1)的內容。

* 您的內容片段的內容以預先決定的方式建構 — 根據內容片段模式。 這可簡化應用程式的存取，進而處理您的內容。

## GraphQL — 概觀 {#graphql-overview}

GraphQL 是：

* &quot;*...一種API和執行階段的查詢語言，可使用您的現有資料滿足這些查詢。*「。

  請參閱 [GraphQL.org](https://graphql.org)

此 [AEM GRAPHQL API](#aem-graphql-api) 可讓您對執行（複雜）查詢 [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)；每個查詢都根據特定的模型型別。 然後，您的應用程式可以使用傳回的內容。

## AEM GraphQL API {#aem-graphql-api}

針對Adobe Experience as a Cloud Experience，我們已開發標準GraphQL API的自訂實作。 另請參閱 [用於內容片段的AEM GraphQL API](/help/headless/graphql-api/content-fragments.md) 以取得詳細資訊。

AEM GraphQL API實作是根據 [GraphQL Java程式庫](https://graphql.org/code/#java).

## 與 AEM GraphQL API 搭配使用的內容片段 {#content-fragments-use-with-aem-graphql-api}

[內容片段](#content-fragments) 可作為AEM查詢GraphQL的基礎，如下所示：

* 它們可讓您設計、建立、組織和發佈獨立於頁面的內容。
* 此 [內容片段模型](#content-fragments-models) 透過定義的資料型別提供所需的結構。
* 此 [片段參考](#fragment-references)定義模型時可用的，可用來定義其他結構層。

![與GraphQL搭配使用的內容片段](assets/cfm-nested-01.png "與GraphQL搭配使用的內容片段")

### 內容片段 {#content-fragments}

內容片段:

* 包含結構化內容。

* 它們是根據 [內容片段模型](#content-fragments-models)，會預先定義產生片段的結構。

### 內容片段模型 {#content-fragments-models}

這些 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)：

* 用於產生 [結構描述](https://graphql.org/learn/schema/)，一次 **已啟用**.

* 提供 GraphQL 所需的資料類型和欄位。它們確保您的應用程式只要求可能的內容並接收預期的內容。

* **[片段參考](#fragment-references)**&#x200B;資料類型可在您的模型中用來參考另一個內容片段，從而引入額外的結構層。

### 片段參考 {#fragment-references}

**[片段參考](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**：

* 與GraphQL搭配使用時特別感興趣。

* 是可在定義內容片段模型時使用的特定資料型別。

* 可參考另一個片段，取決於特定的內容片段模型。

* 可讓您擷取結構化資料。

   * 當定義為 **multifeed** 時，主片段可以參考 (擷取) 多個子片段。

### JSON 預覽 {#json-preview}

若要協助設計和開發您的內容片段模型，您可以預覽 [JSON輸出](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md).

## 了解搭配使用 GraphQL 與 AEM - 範例內容和查詢 {#learn-graphql-with-aem-sample-content-queries}

另請參閱 [瞭解如何將GraphQL與AEM搭配使用 — 範例內容和查詢](/help/headless/graphql-api/sample-queries.md) 瞭解如何使用AEM GraphQL API。

## 教學課程 - AEM Headless 和 GraphQL 快速入門

正在尋找實作教學課程？查看[AEM Headless 和 GraphQL 快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端對端教學課程，說明如何在 Headless CMS 情境下使用 AEM GraphQL API 建立和公開內容並供外部應用程式取用。
