---
title: 如何透過傳送API存取您AEM的內容
description: 在「無頭開發人AEM員歷程」的這部分，瞭解如何使用GraphQL查詢來存取您的內容片段內容。
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 6097cb8961f604ec2d3f5f6d602c927efc7344d5
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---


# 如何透過傳送APIAEM存取您的內容{#access-your-content}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[無頭開發人AEM員歷程的這部分，](#overview.md)瞭解如何使用GraphQL查詢存取您的內容片段。

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，您已在[如何建模您的內容](model-your-content.md)中學習資料建模的基AEM本知識，您現在應：

* 瞭解設計內容時的重要規劃考量。
* 瞭解根據您的整合層級需求實作無頭的步驟。
* 設定必要的工具和AEM設定。
* 瞭解最佳實務，讓您的無頭體驗更順暢、讓內容製作更有效率，並確保內容能快速傳遞。

本文以這些基礎為基礎，讓您瞭解如何透過API存取現有的無頭AEM內容。

* **觀眾**:初學者
* **目標**:瞭解如何使用GraphQL查詢存取內容片段AEM的內容：
   * 介紹GraphQL。
   * 介紹AEMGraphQL API。
   * 深入瞭解GraphQL AEM API的詳細資訊。
   * 檢視一些範例查詢，瞭解實際運作的方式。

以Adobe Experience Manager(AEM)為Cloud Service，您可以搭配使用內容片段和AEMGraphQL API，無條理地提供結構化內容，以便用於您的應用程式。 自訂單一API查詢的功能可讓您擷取並傳送您想要／需要轉譯的特定內容（作為對單一API查詢的回應）。

>[!NOTE]
>GraphQL AEM API是以標準GraphQL為基礎的自訂實作。

## GraphQL —— 簡介{#graphql-introduction}

GraphQL是：

* &quot;*...API的查詢語言，以及使用您現有資料來完成這些查詢的執行階段。*&quot;。

   請參見&#x200B;*GraphQL*。

### GraphQL —— 類型{#graphql-types}

### GraphQL —— 方案{#graphql-schemas}

### GraphQL —— 查詢{#graphql-queries}

## AEM和GraphQL {#aem-graphql}

GraphQL用於以下各個位AEM置：

* 商務
   * 預留位置
* 內容片段
   * 已針對此使用案例開發自訂的API。
   * 這是GraphQL AEM API。

## AEM GraphQL API {#aem-graphql-api}

針對Adobe Experience as a Cloud Experience，我們開發了標準GraphQL API的自訂實作。

GraphQL AEM API可讓您對內容片段執行（複雜）查詢；每個查詢都根據特定的模型類型。 然後，您的應用程式就可以使用傳回的內容。

>[!NOTE]
>
>GraphQL AEM API實施基於GraphQL Java庫。

### GraphQL AEM API和內容片段{#aem-graphql-content-fragments}

## 用於GraphQL API AEM {#content-fragments-use-with-aem-graphql-api}的內容片段

內容片段可作為GraphQL查詢的基礎，如AEM下所示：

* 它們可讓您設計、建立、組織和發佈不受頁面限制的內容。
* 「內容片段模型」透過定義的資料類型提供所需的結構。
* 定義模型時可用的「片段參照」(Fragment Reference)可用於定義其他結構層。

### 內容片段 {#content-fragments}

內容片段:

* 包含結構化內容。

* 它們是以內容片段模型為基礎，內容片段模型會預先定義產生片段的結構。

### 內容片段模型 {#content-fragments-models}

這些內容片段模型：

* 一次&#x200B;**Enabled**，用於生成方案。

* 提供GraphQL所需的資料類型和欄位。 它們可確保您的應用程式只要求可能的項目，並接收預期的項目。

* 您的模型中可使用資料類型&#x200B;**片段參考**&#x200B;來參考其他內容片段，因此引入其他層級的結構。

### 片段參考{#fragment-references}

**片段參考**:

* 與GraphQL結合使用特別受到關注。

* 是定義內容片段模型時可使用的特定資料類型。

* 參照另一個片段，取決於特定的內容片段模型。

* 可讓您擷取結構化資料。

   * 當定義為&#x200B;**multifeed**&#x200B;時，素數片段可參考（擷取）多個子片段。

### JSON預覽{#json-preview}

若要協助您設計和開發內容片段模型，您可以預覽[JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)。

## 下一個{#whats-next}

[瞭解如何使用REST API存取和更新您的內容片段](/help/implementing/developing/headless-journey/update-your-content.md)。

## 其他資源 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [結構描述](https://graphql.org/learn/schema/)
   * [GraphQL Java庫](https://graphql.org/code/#java)
* [與內AEM容片段搭配使用的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [學習如何搭配使用GraphQL AEM —— 範例內容與查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [內容片段的AEM遠程GraphQL查詢驗證](/help/assets/content-fragments/graphql-authentication-content-fragments.md)
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)
