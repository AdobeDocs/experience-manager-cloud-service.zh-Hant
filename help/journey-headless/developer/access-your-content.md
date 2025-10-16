---
title: 如何透過 AEM Delivery API 存取您的內容
description: 在 AEM Headless 開發人員歷程的這一部分中，了解如何使用 GraphQL 查詢來存取您的內容片段內容。
exl-id: 1adecc69-5f92-4007-8a2a-65bf1e960645
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2ccca86a0e611b93c273e37abb6e0fd7870421d4
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 100%

---

# 如何透過 AEM Delivery API 存取您的內容 {#access-your-content}

在這個部分的 [AEM Headless 開發人員歷程](overview.md)中，您可以了解如何使用 GraphQL 查詢來存取您的內容片段內容並提供給您的應用程式 ( Headless 傳遞)。

## 目前進度 {#story-so-far}

在 AEM Headless 歷程的上一份文件「[如何建立內容模型](model-your-content.md)」中，您已了解在 AEM 中建立內容模型的基本知識，所以現在您應該了解如何建立內容結構模型，然後使用 AEM 內容片段模型和內容片段實現該結構。

* 認識內容模型相關的概念和術語。
* 了解為什麼 Headless 內容傳遞需要內容模型。
* 了解如何使用 AEM 內容片段模型實現此結構 (和使用內容片段製作內容)。
* 了解如何建立內容模型；基本範例的原則。

本文章以這些基本知識為基礎，以便您了解如何使用 AEM GraphQL API 在 AEM 存取您現有的 Headless 內容。

* **客群**：初學者
* **目標**：了解如何使用 GraphQL 查詢來存取內容片段的內容。
   * 介紹 GraphQL 和 AEM GraphQL API。
   * 深入了解 AEM GraphQL API 的詳細資訊。
   * 查看一些範例查詢以了解實務運作。

## 所以您想存取您的內容嗎？ {#so-youd-like-to-access-your-content}

所以...您已經取得所有這些內容，結構整齊 (在內容片段中)，正等待提供給您的新應用程式。問題是 - 如何到達那裡？

您需要的是可以找出特定內容為目標的方法，選擇您需要的內容並將其傳回到您的應用程式以進一步處理。

有了 Adobe Experience Manager (AEM) as a Cloud Service，您可以使用 AEM GraphQL API 有選擇地存取內容片段，以僅傳回需要的內容。這表示您可以實現 Headless 傳遞結構化的內容，以便在您的應用程式中使用。

>[!NOTE]
>
>AEM GraphQL API 是根據標準 GraphQL API 規格的自訂實作。

## GraphQL - 簡介 {#graphql-introduction}

GraphQL 是一種開放原始碼的規格，它提供：

* 查詢語言，使您能夠從結構化物件中選擇特定內容。
* 執行階段，使用您的結構化內容來完成這些查詢。

GraphQL 是強式類型 API。這表示&#x200B;*所有*&#x200B;內容必須按類型清楚結構和組織，以便 GraphQL *了解*&#x200B;要存取什麼以及如何存取。資料欄位在 GraphQL 結構描述中定義，其定義內容物件的結構。

然後，GraphQL 端點提供回應 GraphQL 查詢的路徑。

這一切表示您的應用程式可以準確、可靠和有效率地選擇它需要的內容，正是您搭配 AEM 使用時所需要的。

>[!NOTE]
>
>請參閱 *GraphQL*.org 和 *GraphQL*.com。

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL API 是根據標準 GraphQL API 規格的自訂版本，特別設定為允許您對內容片段執行 (複雜) 查詢。

使用內容片段，因為內容的結構是根據內容片段模型建立的。這滿足了 GraphQL 的基本要求。

* 內容片段模型由一個或多個欄位組成。
   * 每個欄位都是根據資料類型定義的。
* 內容片段模型用於產生對應的 AEM GraphQL 結構描述。

為了實際存取 GraphQL 以用於 AEM (和內容)，端點用於提供存取路徑。

然後，透過 AEM GraphQL API 傳回的內容可以供您的應用程式使用。

為了協助您直接輸入和測試查詢，標準 GraphiQL 介面的實作也可與 AEM GraphQL (這可與 AEM 一起安裝) 搭配使用。它提供語法醒目顯示、自動完成、自動建議等功能，以及歷史記錄和線上文件。

>[!NOTE]
>
>AEM GraphQL API 實作是以 GraphQL Java 程式庫為基礎。

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEM as a Cloud Service environment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM as a Cloud Service is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## 與 AEM GraphQL API 搭配使用的內容片段 {#content-fragments-use-with-aem-graphql-api}

內容片段可作為 AEM 結構描述和查詢之 GraphQL 的基礎，如下所示：

* 它們使您能夠設計、建立、策劃和發佈可以 Headless 方式傳遞之獨立於頁面的內容。
* 它們根據內容片段模型，該模型使用選擇的資料類型為產生的片段預先定義結構。
* 可以使用片段參考資料類型完成額外的結構層，在定義模型時可用。

### 內容片段模型 {#content-fragments-models}

這些內容片段模型：

* **啟用**&#x200B;後，用於產生結構描述。
* 提供 GraphQL 所需的資料類型和欄位。它們確保您的應用程式只要求可能的內容並接收預期的內容。
* **片段參考**&#x200B;資料類型可在您的模型中用來參考另一個內容片段，從而引入額外的結構層。

### 片段參考 {#fragment-references}

**片段參考**&#x200B;和&#x200B;**片段參考 UUID**：

* 為在定義內容片段模型時可用的特定資料類型。
* 可參考另一個片段，取決於特定的內容片段模型。
* 可讓您建立並接著擷取結構化資料。

   * 當定義為 **multifeed** 時，主片段可以參考 (擷取) 多個子片段。

## 實際使用 AEM GraphQL API {#actually-using-aem-graphiql}

### 初始設定 {#initial-setup}

在開始對您的內容進行查詢之前，您需要：

* 啟用您的端點
   * 使用「工具 > 一般 > GraphQL」
   * [啟用 GraphQL 端點](/help/headless/graphql-api/graphql-endpoint.md)
      * 這也會啟用 GraphiQL IDE。

### 範例結構 {#sample-structure}

若要實際在查詢中使用 AEM GraphQL API，我們可以使用兩個非常基本的內容片段模型結構：

* 公司
   * 名稱 - 文字
   * CEO (人員) - 片段參考
   * 員工 (人員) - 片段參考
* 人員
   * 名稱 - 文字
   * 名字 - 文字

如您所見，CEO 和員工欄位參考了人員片段。

以下情況會使用片段模型：

* 在內容片段編輯器建立內容時
* 產生您將查詢的 GraphQL 結構描述

### 在哪裡測試您的查詢 {#where-to-test-your-queries}

可以在 GraphiQL 介面輸入查詢。您可以從以下任一方式存取查詢編輯器：

* **工具** > **一般** > **GraphQL 查詢編輯器**
* 直接；例如 `http://localhost:4502/aem/graphiql.html`

![GraphiQL 介面](assets/graphiql-interface.png "GraphiQL 介面")

### 查詢快速入門 {#getting-Started-with-queries}

一個簡單的查詢是傳回「公司」結構描述中所有項目的名稱。您在這裡要求所有公司名稱的清單：

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

一個稍微複雜的查詢是選擇所有名稱不是「Jobs」的人員。這將篩選出所有名稱沒有 Jobs 的人員。這是使用 EQUALS_NOT 運算子完成 (還有更多)：

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

您還可以建構更複雜的查詢。例如，查詢至少有一名員工名稱為「Smith」的所有公司。此查詢說明了對任何名稱為「Smith」的人員的篩選，從跨巢狀片段傳回資訊：

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

如需使用 AEM GraphQL API 的完整詳細資訊，以及設定必要的元素，您可以參考：

* 了解如何將 GraphQL 與 AEM 搭配使用
* 範例內容片段結構
* 了解搭配使用 GraphQL 與 AEM - 範例內容和查詢

## 下一步 {#whats-next}

現在您已經了解如何使用 AEM GraphQL API 存取和查詢 Headless 內容，您現在可以[了解如何使用 REST API 存取和更新內容片段的內容](update-your-content.md)。

## 其他資源 {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [GraphQL.org](https://graphql.org)
   * [結構描述](https://graphql.org/learn/schema/)
   * [變數](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java 程式庫](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [了解如何將 GraphQL 與 AEM 搭配使用](/help/headless/graphql-api/content-fragments.md)
   * [啟用 GraphQL 端點](/help/headless/graphql-api/graphql-endpoint.md)
   * [安裝 AEM GraphiQL 介面](/help/headless/graphql-api/graphiql-ide.md)
* [範例內容片段結構](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)
* [了解搭配使用 GraphQL 與 AEM - 範例內容和查詢](/help/headless/graphql-api/sample-queries.md)
   * [範例查詢 - 單一特定城市片段](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)
   * [中繼資料的範例查詢 - 列出 GB 獎項的中繼資料](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)
   * [範例查詢 - 所有具有名稱變化的城市](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)
* [在設定瀏覽器中啟用內容片段功能](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)
* [使用內容片段](/help/sites-cloud/administering/content-fragments/overview.md)
   * [內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
   * [JSON 輸出](/help/assets/content-fragments/content-fragments-json-preview.md)
* [了解跨原始資源共用 (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=zh-Hant#understand-cross-origin-resource-sharing-(cors))
* [GraphQL 持續性查詢 - 在 Dispatcher 中啟用快取](/help/headless/deployment/dispatcher-caching.md)
* [為伺服器端 API 產生存取權杖](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [AEM Headless 快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=zh-Hant) - 此為簡短的教學影片系列，概觀如何使用 AEM 的 Headless 功能，包括內容模型和 GraphQL。
