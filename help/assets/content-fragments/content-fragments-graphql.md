---
title: 使用內容片段與GraphQL進行無頭內容傳送
description: 瞭解如何將Adobe Experience Manager(AEM)中的內容片段當做雲端服務與GraphQL搭配使用，以進行無頭內容傳送。
translation-type: tm+mt
source-git-commit: 54b377c6d98398fd5066dc4a3337a3877b9e3ed7
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---


# 使用內容片段與GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}進行無頭內容傳送

以Adobe Experience Manager(AEM)為雲端服務，您可以搭配使用內容片段和AEM GraphQL API（以標準GraphQL為基礎的自訂實作），來提供結構化內容，以便用於您的應用程式。 自訂單一API查詢的功能可讓您擷取並傳送您想要／需要轉譯的特定內容（作為對單一API查詢的回應）。

>[!NOTE]
>
>如需AEM Sites的雲端服務無頭開發簡介，請參閱[無頭和AEM](/help/implementing/developing/headless/introduction.md)。

## 無頭CMS {#headless-cms}

無頭內容管理系統(CMS)是：

* &quot;*無頭內容管理系統或無頭CMS是從頭構建的純後端內容管理系統(CMS)，它是內容儲存庫，可通過API訪問內容，以便在任何設備上顯示。*

   請參閱[Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system)。

就在AEM中製作內容片段而言，這表示：

* 您可以使用「內容片段」來製作並非主要用來直接發佈在格式化頁面(1:1)的內容。

* 內容片段的內容將依照內容片段模型以預先確定的方式建構。 如此可簡化應用程式的存取，進一步處理您的內容。

## GraphQL —— 概述{#graphql-overview}

GraphQL是：

* &quot;*...API的查詢語言，以及使用您現有資料來完成這些查詢的執行階段。*&quot;。

   請參閱[GraphQL.org](https://graphql.org)

[AEM GraphQL API](#aem-graphql-api)可讓您對[內容片段](/help/assets/content-fragments/content-fragments.md)執行（複雜）查詢；每個查詢都根據特定的模型類型。 然後，您的應用程式就可以使用傳回的內容。

## AEM GraphQL API {#aem-graphql-api}

針對Adobe Experience as a Cloud Experience，我們開發了標準GraphQL API的自訂實作。 如需詳細資訊，請參閱[AEM GraphQL API以搭配內容片段](/help/assets/content-fragments/graphql-api-content-fragments.md)使用。

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

* 用於生成[方案](https://graphql.org/learn/schema/)，一次&#x200B;**啟用**。

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

## 教學課程- AEM Headless和GraphQL快速入門

正在尋找實作教學課程？ 請參閱[AEM無頭和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端對端教學課程，說明如何在無頭CMS案例中，使用AEM的GraphQL API建立和公開內容，並由外部應用程式使用。