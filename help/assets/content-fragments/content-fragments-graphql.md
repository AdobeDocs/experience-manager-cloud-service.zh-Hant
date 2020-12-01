---
title: 使用內容片段與GraphQL進行無頭內容傳送
description: 瞭解如何將Adobe Experience Manager(AEM)中的內容片段當做雲端服務與GraphQL搭配使用，以進行無頭內容傳送。
translation-type: tm+mt
source-git-commit: ae918d074d4bacfc207d4dca2c67f41a3118aff4
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# 使用內容片段與GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}進行無頭內容傳送

>[!CAUTION]
>
>AEM GraphQL API（針對內容片段傳送）將於2021年初發行。
>
>相關檔案已可供預覽使用。

以Adobe Experience Manager(AEM)為雲端服務，您可以搭配使用內容片段和AEM GraphQL API（以標準GraphQL為基礎的自訂實作），來提供結構化內容，以便用於您的應用程式。

## 無頭CMS {#headless-cms}

無頭內容管理系統(CMS)是：

* &quot;*無頭內容管理系統或無頭CMS是從頭構建的純後端內容管理系統(CMS)，它是內容儲存庫，可通過API訪問內容，以便在任何設備上顯示。*

   *「無頭」一詞源於「主體」（後端，即內容存放庫）的截擊「頭」（前端，即網站）的概念*。

   請參閱[Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system)。

就在AEM中製作內容片段而言，這表示：

* 您可以使用「內容片段」來製作並非主要用來直接發佈在格式化頁面(1:1)的內容。

* 內容片段的內容將依照內容片段模型以預先確定的方式建構。 如此可簡化應用程式的存取，進一步處理您的內容。

>[!NOTE]
>
>如需AEM Sites的雲端服務無頭開發簡介，請參閱[無頭和AEM](/help/implementing/developing/headless/introduction.md)。

## GraphQL —— 概述{#graphql-overview}

GraphQL是：

* &quot;*...API的查詢語言，以及使用您現有資料完成這些查詢的執行時期。 GraphQL提供您API中資料的完整且易於理解的描述，讓客戶能夠要求確切的所需內容，而不需要其他內容，讓API隨著時間推移而更容易發展，並提供功能強大的開發人員工具。*&quot;。

   請參閱[GraphQL.org](https://graphql.org)

* &quot;*...開放式規格，以提供有彈性的API圖層。 將GraphQL置於您現有的後端，以前所未有的速度建立產品…….*&quot;。

   請參閱[瀏覽GraphQL](https://www.graphql.com)。 &quot;*Explore GraphQL由Apollo團隊維護。 我們的目標是為全球的開發人員和技術領導者提供他們瞭解和採用GraphQL所需的所有工具。*」。

[AEM GraphQL API](#aem-graphql-api)可讓您對[內容片段](/help/assets/content-fragments/content-fragments.md)執行（複雜）查詢；每個查詢都根據特定的模型類型。 然後，您的應用程式就可以使用傳回的內容。

### GraphQL術語{#graphql-terminology}

GraphQL使用下列功能：

* **[查詢](https://graphql.org/learn/queries/)**

* **[方案和類型](https://graphql.org/learn/schema/)** -使用這些，GraphQL顯示GraphQL允許用於AEM實施的類型和操作。

* **[欄位](https://graphql.org/learn/queries/#fields)**

* **GraphQL端點** - AEM中回應GraphQL查詢並提供GraphQL架構存取權的路徑。

有關詳細資訊，請參閱[(GraphQL.org)GraphQL](https://graphql.org/learn/)簡介，包括[ Best Practices](https://graphql.org/learn/best-practices/)。

### GraphQL查詢類型{#graphql-query-types}

使用GraphQL，您可以執行以下任一查詢：

* **單一項目**

* **[條目清單](https://graphql.org/learn/schema/#lists-and-non-null)**

## AEM GraphQL API {#aem-graphql-api}

對於[Adobe Experience作為雲端體驗，已實作標準GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)的自訂實作。

AEM GraphQL API實作以[GraphQL Java庫](https://graphql.org/code/#java)為基礎。

## 與AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}搭配使用的內容片段

[Content ](#content-fragments) Fragments可作為GraphQL的AEM查詢基礎，如下：

* 它們可讓您設計、建立、組織和發佈不受頁面限制的內容。
* [內容片段模型](#content-fragments-models)通過定義的資料類型提供所需的結構。
* 定義模型時可用的[片段參考](#fragment-references)可用於定義其他結構層。

![用於GraphQL的內容片](assets/cfm-nested-01.png "段用於GraphQL的內容片段")

### 內容片段 {#content-fragments}

內容片段:

* 包含結構化內容。

* 它們以[內容片段模型](#content-fragments-models)為基礎，該模型預先定義所產生片段的結構。

### 內容片段模型 {#content-fragments-models}

以下[內容片段模型](/help/assets/content-fragments/content-fragments-models.md):

* 提供GraphQL所需的資料類型和欄位。 它們可確保您的應用程式只要求可能的項目，並接收預期的項目。

* 您的模型中可使用資料類型&#x200B;**[片段參考](#fragment-references)**&#x200B;來參考其他內容片段，因此引入其他層級的結構。

### 片段參考{#fragment-references}

**[片段參考](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* 與GraphQL結合使用特別受到關注。

* 是定義內容片段模型時可使用的特定資料類型。

* 參照另一個片段，取決於特定的內容片段模型。

* 可讓您擷取結構化資料。

   * 當定義為&#x200B;**multifeed**&#x200B;時，素數片段可參考（擷取）多個子片段。

### JSON預覽{#json-preview}

若要協助您設計和開發內容片段模型，您可以預覽[JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)。

## 瞭解如何搭配AEM使用GraphQL —— 範例內容與查詢{#learn-graphql-with-aem-sample-content-queries}

請參閱[學習如何搭配AEM使用GraphQL —— 範例內容與查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md)，以取得使用AEM GraphQL API的簡介。