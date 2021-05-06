---
title: 如何透過傳送API存取您AEM的內容
description: 在「無頭開發人AEM員歷程」的這部分，瞭解如何使用GraphQL查詢來存取您的內容片段內容。
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 861ef15a0060d51fd32e2d056871d1679f77a21e
workflow-type: tm+mt
source-wordcount: '1931'
ht-degree: 0%

---

# 如何透過傳送APIAEM存取您的內容{#access-your-content}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[AEM Headless Developer Journey（無頭開發人員歷程）的這部分，您可以學習如何使用GraphQL查詢來存取您的內容片段。](overview.md)

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，您學習了內容建模的基本知識[](model-your-content.md)，因此您現在應瞭解如何建立內容結構模型，然後使用內容片段模型和內容片段來實AEM現該結構：

* 識別與內容模型相關的概念和術語。
* 瞭解為何需要建立內容模型才能傳送無頭內容。
* 瞭解如何使用內容片段模型AEM（以及使用內容片段製作內容）來實現此結構。
* 瞭解如何建立內容模型；基本樣本的原則。

本文以這些基礎為基礎，讓您瞭解如何使用GraphQL API存取您AEM現有的AEM無頭內容。

* **觀眾**:初學者
* **目標**:瞭解如何使用GraphQL查詢存取內容片段AEM的內容：
   * 介紹GraphQL和AEMGraphQL API。
   * 深入瞭解GraphQL AEM API的詳細資訊。
   * 檢視一些範例查詢，瞭解實際運作的方式。

## 所以您想要存取您的內容？{#so-youd-like-to-access-your-content}

所以……您擁有這些內容，結構精巧（在「內容片段」中），而且只要等待新應用程式的提供。 問題是，如何實現？

您需要的是定位特定內容、選擇所需內容並將它傳回應用程式，以便進一步處理。

以Adobe Experience Manager(AEM)為Cloud Service，您可以使用GraphQL API，選擇性地存取您的內容片段，以AEM僅傳回所需的內容。 這表示您可以實現無頭傳送結構化內容，以便用於您的應用程式。

>[!NOTE]
>
>GraphQL AEM API是根據標準GraphQL API規格而自訂的實作。

## GraphQL —— 簡介{#graphql-introduction}

GraphQL是開放原始碼規範，它提供：

* 查詢語言，可讓您從結構化物件中選擇特定內容。
* 執行階段，以便對結構化內容執行這些查詢。

GraphQL是&#x200B;*強*&#x200B;類型化API。 這表示&#x200B;*所有*&#x200B;內容必須依類型清楚地結構化和組織，以便GraphQL *瞭解*&#x200B;要訪問的內容和訪問方式。 資料欄位在GraphQL結構中定義，定義內容對象的結構。

然後，GraphQL端點提供響應GraphQL查詢的路徑。

所有這些都表示您的應用程式可以精確、可靠且有效率地選取所需的內容——只是搭配使用時所需的內AEM容。

>[!NOTE]
>
>請參閱&#x200B;*GraphQL*.org和&#x200B;*GraphQL*.com。

## AEM和GraphQL {#aem-graphql}

GraphQL用於中的各種位AEM置；例如：

* 內容片段
   * 已針對此使用案例（無頭傳送至您的應用程式）開發自訂API。
      * 這是GraphQL AEM API。
* 商務
   * AEM商務透過GraphQL從商務平台取用資料。
   * GraphQL整合了各AEM種第三方商務解決方案，與CIF核心元件提供的擴充勾點搭配使用。
      * 這不會使用AEMGraphQL API。

>[!NOTE]
>
>「無頭歷程」的這個步驟僅與GraphQL APIAEM和內容片段有關。

## AEM GraphQL API {#aem-graphql-api}

GraphQL AEM API是以標準GraphQL API規格為基礎的自訂版本，特別設定為允許您對內容片段執行（複雜）查詢。

內容片段是使用的，因為內容是根據內容片段模型來建構的。 這滿足了GraphQL的基本要求。

* 內容片段模型由一或多個欄位組成。
   * 每個欄位都根據資料類型定義。
* 內容片段模型用於生成相應的AEMGraphQL模式。

要實際訪問GraphQLAEM（和內容），使用端點提供訪問路徑。

然後，您的應用程AEM式可透過GraphQL API傳回的內容。

>[!NOTE]
>
>GraphQL AEM API實施基於GraphQL Java庫。

### 作者和發佈環境的使用案例{#use-cases-author-publish-environments}

GraphQL API的使AEM用案例取決於作為Cloud Service環境AEM的類型：

* 發佈環境；用於：
   * 查詢JS應用程式的內容（標準使用案例）

* 作者環境；用於：
   * 查詢內容以「用於內容管理」:
      * GraphQL AEM in as aCloud Service當前是只讀API。
      * REST API可用於CR(u)D操作。

## 用於GraphQL API AEM {#content-fragments-use-with-aem-graphql-api}的內容片段

內容片段可用作GraphQL的架構和查詢AEM基礎，如下：

* 它們可讓您設計、建立、組織和發佈不受頁面限制的內容。
* 它們以內容片段模型為基礎，內容片段模型透過定義的資料類型預先定義產生片段的結構。
* 使用「片段參考」(Fragment Reference)資料類型（定義模型時可用）可實現其他結構層。

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

* 可讓您建立並擷取結構化資料。

   * 當定義為&#x200B;**multifeed**&#x200B;時，素數片段可參考（擷取）多個子片段。

### JSON預覽{#json-preview}

若要協助您設計和開發內容片段模型，您可以在內容片段編輯器中預覽JSON輸出。

## 從內容片段{#graphql-schema-generation-content-fragments}生成GraphQL模式

GraphQL是強式型別的API，這表示內容必須依類型清楚地結構化和組織。 GraphQL規範提供了一系列准則，說明如何建立強穩的API，以詢問特定例項的內容。 為此，客戶端需要獲取方案，該方案包含查詢所需的所有類型。

對於內容片段，GraphQL結構（結構和類型）基於&#x200B;**Enabled**&#x200B;內容片段模型及其資料類型。

>[!CAUTION]
>
>所有GraphQL結構（衍生自&#x200B;**Enabled**&#x200B;的內容片段模型）都可通過GraphQL端點讀取。
>
>這表示您需要確保沒有敏感內容可用，以確保沒有敏感資料通過GraphQL端點公開；例如，這包括在模型定義中可能顯示為欄位名稱的資訊。

例如，如果用戶建立了名為`Article`的內容片段模型，AEM則生成類型為`ArticleModel`的對象`article`。 此類型中的欄位對應於模型中定義的欄位和資料類型。

1. 內容片段模型：

   ![用於GraphQL的內容片](assets/graphqlapi-cfmodel.png "段模型用於GraphQL")

1. 對應的GraphQL模式（從GraphiQL自動文檔輸出）:
   ![基於內容片段模型的GraphQL](assets/graphqlapi-cfm-schema.png "模式基於內容片段模型的GraphQL模式")

   這表示產生的類型`ArticleModel`包含數個[欄位](#fields)。

   * 其中3個由用戶控制：`author`、`main`和`referencearticle`。

   * 其他欄位則會自動加入，AEM並代表提供特定內容片段相關資訊的實用方法；在此範例中，`_path`、`_metadata`、`_variations`。 這些[幫助欄位](#helper-fields)標有前面的`_`，以區分用戶定義的內容和自動生成的內容。

1. 當使用者根據文章模型建立內容片段後，就可透過GraphQL進行詢問。 如需範例，請參閱Sample Queries.md#graphql-sample-querys)(根據與GraphQL搭配使用的範例內容片段結構。

在GraphQL中，AEM模式是靈活的。 這表示每次建立、更新或刪除內容片段模型時都會自動產生此片段。 更新內容片段模型時，也會重新整理資料結構快取。

Sites GraphQL服務會監聽（在背景）對內容片段模型所做的任何修改。 檢測到更新時，只會重新生成模式的該部分。 此最佳化可節省時間並提供穩定性。

例如，如果：

1. 安裝包含`Content-Fragment-Model-1`和`Content-Fragment-Model-2`的軟體包：

   1. 將生成`Model-1`和`Model-2`的GraphQL類型。

1. 然後修改`Content-Fragment-Model-2`:

   1. 只有`Model-2` GraphQL類型會更新。

   1. 而`Model-1`則保持不變。

>[!NOTE]
>
>請務必注意，以防您透過REST api或其他方式對內容片段模型進行大量更新。

模式通過與GraphQL查詢相同的端點服務，客戶端處理以`GQLschema`副檔名調用模式的事實。 例如，對`/content/cq:graphql/global/endpoint.GQLschema`執行簡單的`GET`請求將導致輸出具有Content-type的架構：`text/x-graphql-schema;charset=iso-8859-1`。

### 方案生成——未發佈的模型{#schema-generation-unpublished-models}

當內容片段巢狀化時，可能會發佈父項內容片段模型，但參考的模型則不會。

>[!NOTE]
>
>UI可AEM防止此情況發生，但若以程式設計方式發佈，或使用內容封裝，則可能會發生此情況。

發生此情況AEM時，會為父內容片段模型產生&#x200B;*不完整*&#x200B;架構。 這表示從架構中移除與未發佈模型相關的片段參考。

## 圖AEM形QL端點{#aem-graphql-endpoints}

<!--
need details/examples
-->

端點是用於訪問GraphQL的路AEM徑。 您（或您的應用程式）可以使用此路徑：

* 訪問GraphQL模式，
* 發送您的GraphQL查詢，
* 接收響應（對您的GraphQL查詢）。

AEM允許：

* 全域端點——可供所有網站使用。
* 租用戶端點——您可以設定的，特定於指定的網站／專案。

## 權限 {#permissions}

權限是存取「資產」所需的權限。

## GraphiQLAEM介面{#aem-graphiql-interface}

為幫助您直接輸入和測試查詢，GraphQL介面的標準實現可與GraphQLAEM一起使用。 這可與一起安裝AEM。

它提供語法反白顯示、自動完成、自動建議等功能，以及歷史記錄和線上檔案。

![GraphiQL接](assets/graphiql-interface.png "口GraphiQL介面")

## 使AEM用GraphQL API {#using-aem-graphiql}

有關使用GraphQL API的詳AEM細資訊，以及配置必要的元素，您可以參考：

* 學習搭配使用GraphQL AEM
* 範例內容片段結構
* 學習如何搭配使用GraphQL AEM —— 範例內容與查詢

## 下一個{#whats-next}

現在，您已學會如何使用AEMGraphQL API存取和查詢無頭內容，您現在可以[瞭解如何使用REST API存取和更新內容片段](/help/implementing/developing/headless-journey/update-your-content.md)的內容。

## 其他資源 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [結構描述](https://graphql.org/learn/schema/)
   * [變數](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java庫](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [學習搭配使用GraphQL AEM](/help/assets/content-fragments/graphql-api-content-fragments.md)
* [範例內容片段結構](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [學習如何搭配使用GraphQL AEM —— 範例內容與查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [範例查詢——單一特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [中繼資料的範例查詢——列出標題為GB的獎項中繼資料](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [範例查詢——具有命名變異的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [在配置瀏覽器中啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)
* [瞭解跨原始資源共用(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [產生伺服器端API的存取Token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [開始使用無AEM頭](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) -一個短片教學課程系列，提供使用無頭功AEM能的概觀，包括內容建模和GraphQL。
