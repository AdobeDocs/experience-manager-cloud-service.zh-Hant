---
title: 使用GraphQL的內容片段進行無頭內容傳遞
description: 瞭解使用GraphQL內容片段AEM實現無頭CMS的基本概念，以便無頭內容傳遞。
exl-id: ef48f737-a5b3-4913-9f37-6b9f681bc048
source-git-commit: 5663b1224dddcb2db9e0ca139bb8cf6b43787fab
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 1%

---

# 使用GraphQL的內容片段進行無頭內容傳遞 {#headless-content-delivery-using-content-fragments-with-graphQL}

使用內容片段和GraphQL API，您可以將Adobe Experience Manager(AEM)as a Cloud Service用作無頭內容管理系統(CMS)。

這是通過使用內容片段和AEMGraphQL API（基於標準GraphQL的定製實現）來無拘無束地提供結構化內容以供您的應用程式使用來實現的。 通過自定義單個API查詢，您可以檢索和傳遞您想要/需要呈現的特定內容（作為對單個API查詢的響應）。

>[!NOTE]
>
>另請參閱:
>
>* [什麼是無頭？](/help/headless/what-is-headless.md) 介紹無頭概念和術語。
>
>* [無頭AEM和](/help/headless/introduction.md) AEM Sitesas a Cloud Service的無頭開發簡介。


>[!NOTE]
>
>GraphQL目前在Adobe Experience Manager()as a Cloud Service的兩種(單獨AEM的)情形中使用：
>
>* [通AEM過GraphQL從商務平台消耗資料](/help/commerce-cloud/integrating/magento.md)。
>* [內AEM容片段與AEMGraphQL API（基於標準GraphQL的自定義實現）一起工作，以提供結構化內容供您的應用程式使用](/help/headless/graphql-api/content-fragments.md)。


## 無頭CMS {#headless-cms}

無頭內容管理系統(CMS)是僅用於後端的內容管理系統，它明確地設計和構建為內容儲存庫，使內容可通過API訪問，以便在任何設備上顯示。

就創作內容片段而言，AEM這意味著：

* 您可以使用內容片段來創作主要不打算在格式化頁面上直接發佈(1:1)的內容。

* 根據內容片段模型，內容片段的內容將以預定方式結構化。 這簡化了對應用程式的訪問，這將進一步處理您的內容。

## GraphQL — 概述 {#graphql-overview}

GraphQL為：

* &quot;*...API的查詢語言和用現有資料完成這些查詢的運行時。*。

   請參閱 [GraphQL.org](https://graphql.org)

的 [AEMGraphQL API](#aem-graphql-api) 允許您對 [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md);每個查詢都根據特定的模型類型。 然後，您的應用程式可以使用返回的內容。

## AEMGraphQL API {#aem-graphql-api}

對於Adobe Experience作為雲體驗，開發了標準GraphQL API的自定義實現。 請參閱 [用AEM於內容片段的GraphQL API](/help/headless/graphql-api/content-fragments.md) 的雙曲餘切值。

GraphQLAEM API實現基於 [GraphQL Java庫](https://graphql.org/code/#java)。

## 用於GraphQL API的內AEM容片段 {#content-fragments-use-with-aem-graphql-api}

[內容片段](#content-fragments) 可作為查詢的GraphQL的基礎，AEM如下：

* 它們使您能夠設計、建立、建立和發佈獨立於頁面的內容。
* 的 [內容片段模型](#content-fragments-models) 通過定義的資料類型提供所需的結構。
* 的 [片段引用](#fragment-references)定義模型時可用，可用於定義其它結構層。

![用於GraphQL的內容片段](assets/cfm-nested-01.png "用於GraphQL的內容片段")

### 內容片段 {#content-fragments}

內容片段:

* 包含結構化內容。

* 它們基於 [內容片段模型](#content-fragments-models)，它為生成的片段預定義結構。

### 內容片段模型 {#content-fragments-models}

這些 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md):

* 用於生成 [架構](https://graphql.org/learn/schema/)的 **已啟用**。

* 提供GraphQL所需的資料類型和欄位。 它們確保您的應用程式只請求可能的內容，並接收預期的內容。

* 資料類型 **[片段引用](#fragment-references)** 可在模型中使用以引用另一個內容片段，因此引入其他級別的結構。

### 片段引用 {#fragment-references}

的 **[片段引用](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* 與GraphQL結合使用尤其受關注。

* 是定義內容片段模型時可使用的特定資料類型。

* 引用另一段，取決於特定內容段模型。

* 允許您檢索結構化資料。

   * 定義為 **多饋**，多個子片段可以由素片段引用（檢索）。

### JSON預覽 {#json-preview}

要幫助設計和開發內容片段模型，可以預覽 [JSON輸出](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)。

## 學習將GraphQL與AEM樣例內容和查詢一起使用 {#learn-graphql-with-aem-sample-content-queries}

請參閱 [學習將GraphQL與AEM樣例內容和查詢一起使用](/help/headless/graphql-api/sample-queries.md) 以瞭解使用AEMGraphQL API的簡介。

## 教程 — 無頭和AEMGraphQL入門

想要實習教程嗎？ 簽出 [無頭和AEMGraphQL入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) 端到端教程，演示如何使用AEMGraphQL API構建和公開內容，並讓外部應用在無頭CMS方案中使用。
