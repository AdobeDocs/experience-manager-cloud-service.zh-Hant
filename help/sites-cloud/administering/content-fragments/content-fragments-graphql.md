---
title: 透過GraphQL使用內容片段進行無頭式內容傳送
description: 了解透過GraphQL實現AEM無頭式CMS的基本概念，將內容片段用於無頭式內容傳送。
feature: Content Fragments, GraphQL API
role: User
exl-id: ef48f737-a5b3-4913-9f37-6b9f681bc048
source-git-commit: 6204830f30c28daba3ff87ba60acd0150847b523
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 2%

---

# 透過GraphQL使用內容片段進行無頭式內容傳送 {#headless-content-delivery-using-content-fragments-with-graphQL}

透過內容片段和GraphQL API，您可以使用Adobe Experience Manager(AEM)as a Cloud Service作為無頭式內容管理系統(CMS)。

這是使用內容片段與AEM GraphQL API(以標準GraphQL為基礎的自訂實作)來無條理地提供結構化內容，以便在您的應用程式中使用而達成。 自訂單一API查詢的功能可讓您擷取並傳送您要/需要呈現的特定內容（作為單一API查詢的回應）。

>[!NOTE]
>
>另請參閱:
>
>* [什麼是Headless?](/help/headless/what-is-headless.md) 了解無頭概念和術語的簡介。
>
>* [無頭式與AEM](/help/headless/introduction.md) 以了解AEM Sitesas a Cloud Service的無頭開發。


>[!NOTE]
>
>GraphQL目前用於Adobe Experience Manager(AEM)的兩個（個別）案例as a Cloud Service:
>
>* [AEM商務會透過GraphQL取用來自商務平台的資料](/help/commerce-cloud/integrating/magento.md).
>* [AEM內容片段可與AEM GraphQL API(以標準GraphQL為基礎的自訂實作)搭配使用，提供結構化內容以供您的應用程式使用](/help/headless/graphql-api/content-fragments.md).


## 無頭式CMS {#headless-cms}

無頭式內容管理系統(CMS)是僅限於後端的內容管理系統，設計並明確建置為內容存放庫，可透過API存取內容，以便顯示在任何裝置上。

就在AEM中編寫內容片段而言，這表示：

* 您可以使用內容片段來製作主要不打算直接在格式化頁面上(1:1)發的內容。

* 內容片段的內容將根據內容片段模型以預先決定的方式建構。 這可簡化應用程式的存取，進而處理您的內容。

## GraphQL — 概觀 {#graphql-overview}

GraphQL是：

* &quot;*...API的查詢語言，以及使用您現有資料完成這些查詢的執行階段。*」。

   請參閱 [GraphQL.org](https://graphql.org)

此 [AEM GraphQL API](#aem-graphql-api) 可讓您對 [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md);每個查詢都根據特定模型類型。 之後，您的應用程式就可以使用傳回的內容。

## AEM GraphQL API {#aem-graphql-api}

針對Adobe Experience as a Cloud Experience，已開發標準GraphQL API的自訂實作。 請參閱 [AEM GraphQL API以搭配內容片段使用](/help/headless/graphql-api/content-fragments.md) 以取得詳細資訊。

AEM GraphQL API實作以 [GraphQL Java程式庫](https://graphql.org/code/#java).

## 要與AEM GraphQL API搭配使用的內容片段 {#content-fragments-use-with-aem-graphql-api}

[內容片段](#content-fragments) 可作為GraphQL查詢的基礎，如下：

* 它們可讓您設計、建立、組織和發佈不受頁面影響的內容。
* 此 [內容片段模型](#content-fragments-models) 通過定義的資料類型提供所需的結構。
* 此 [片段參考](#fragment-references)，可在定義模型時使用，以定義其他結構層。

![與GraphQL搭配使用的內容片段](assets/cfm-nested-01.png "與GraphQL搭配使用的內容片段")

### 內容片段 {#content-fragments}

內容片段:

* 包含結構化內容。

* 它們以 [內容片段模型](#content-fragments-models)，會預先定義產生片段的結構。

### 內容片段模型 {#content-fragments-models}

這些 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md):

* 用於產生 [結構](https://graphql.org/learn/schema/)一次 **已啟用**.

* 提供GraphQL所需的資料類型和欄位。 它們可確保您的應用程式只要求可能的項目，並接收預期的項目。

* 資料類型 **[片段參考](#fragment-references)** 可用於模型中以參考其他內容片段，因此引入其他層級的結構。

### 片段參考 {#fragment-references}

此 **[片段參考](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* 與GraphQL有特別的興趣。

* 是定義內容片段模型時可使用的特定資料類型。

* 參考另一個片段，取決於特定內容片段模型。

* 可讓您擷取結構化資料。

   * 定義為 **多重摘要**，則主要片段可參考（擷取）多個子片段。

### JSON 預覽 {#json-preview}

若要協助設計和開發內容片段模型，您可以預覽 [JSON輸出](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md).

## 了解透過 AEM 使用 GraphQL - 範例內容和查詢 {#learn-graphql-with-aem-sample-content-queries}

請參閱 [學習如何搭配AEM使用GraphQL — 範例內容與查詢](/help/headless/graphql-api/sample-queries.md) AEM GraphQL API的使用簡介。

## 教學課程 — AEM Headless和GraphQL快速入門

尋找實作教學課程？ 結帳 [AEM Headless和GraphQL快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) 端對端教學課程，說明如何在無頭CMS情境中，使用AEM GraphQL API建置和公開內容，並供外部應用程式使用。
