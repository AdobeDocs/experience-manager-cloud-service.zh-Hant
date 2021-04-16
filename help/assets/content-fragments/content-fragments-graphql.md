---
title: 使用內容片段與GraphQL進行無頭內容傳送
description: 瞭解如何搭配GraphQLAEM使用內容片段來傳送無頭內容。
feature: 內容片段
role: Business Practitioner
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
translation-type: tm+mt
source-git-commit: 1d0343dc7940566b88ad490bb8fb08a5ad4ff5c2
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# 使用內容片段與GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}進行無頭內容傳送

以Adobe Experience Manager(AEM)為Cloud Service，您可以搭配使用內容片段和AEMGraphQL API（以標準GraphQL為基礎的自訂實作），無條理地提供結構化內容，以便用於您的應用程式。 自訂單一API查詢的功能可讓您擷取並傳送您想要／需要轉譯的特定內容（作為對單一API查詢的回應）。

>[!NOTE]
>
>有關AEM Sites作為Cloud Service的無頭開AEM發的簡介，請參閱[無頭和](/help/implementing/developing/headless/introduction.md)。

>[!NOTE]
>
>GraphQL目前用於Adobe Experience Manager()的兩個（單獨）情AEM形中作為Cloud Service:
>
>* [AEM商務會透過GraphQL從商務平台取用資料](/help/commerce-cloud/integrating/magento.md)。
>* [內AEM容片段與AEMGraphQL API（以標準GraphQL為基礎的自訂實作）搭配運作，以提供結構化內容供您的應用程式使用](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## 無頭CMS {#headless-cms}

無頭內容管理系統(CMS)是：

* &quot;*無頭內容管理系統或無頭CMS是從頭構建的純後端內容管理系統(CMS)，它是內容儲存庫，可通過API訪問內容，以便在任何設備上顯示。*

   請參閱[Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system)。

在編寫內容片段時，這AEM表示：

* 您可以使用「內容片段」來製作並非主要用來直接發佈在格式化頁面(1:1)的內容。

* 內容片段的內容將依照內容片段模型以預先確定的方式建構。 如此可簡化應用程式的存取，進一步處理您的內容。

## GraphQL —— 概述{#graphql-overview}

GraphQL是：

* &quot;*...API的查詢語言，以及使用您現有資料來完成這些查詢的執行階段。*&quot;。

   請參閱[GraphQL.org](https://graphql.org)

[AEM GraphQL API](#aem-graphql-api)允許您對[內容片段](/help/assets/content-fragments/content-fragments.md)執行（複雜）查詢；每個查詢都根據特定的模型類型。 然後，您的應用程式就可以使用傳回的內容。

## AEM GraphQL API {#aem-graphql-api}

針對Adobe Experience as a Cloud Experience，我們開發了標準GraphQL API的自訂實作。 如需詳細資訊，請參AEM閱[ GraphQL API以搭配內容片段](/help/assets/content-fragments/graphql-api-content-fragments.md)使用。

GraphQL AEM API實現基於[GraphQL Java庫](https://graphql.org/code/#java)。

## 用於GraphQL API AEM {#content-fragments-use-with-aem-graphql-api}的內容片段

[內](#content-fragments) 容片段可作為GraphQL查詢的基礎，如AEM下：

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

## 學習將GraphQL與AEM-示例內容和查詢{#learn-graphql-with-aem-sample-content-queries}一起使用

有關使用GraphQL API的簡介，請參AEM閱[學習如何使用GraphQL with AEM - Sample Content and Queries](/help/assets/content-fragments/content-fragments-graphql-samples.md)。

## 教學課程——無頭和GraphQLAEM快速入門

正在尋找實作教學課程？ 請參閱[無頭和GraphQL&lt;a1/AEM>端對端教學課程，說明如何在無頭CMS情境中使用外部應用程式AEM的GraphQL API來建立和公開內容。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)
