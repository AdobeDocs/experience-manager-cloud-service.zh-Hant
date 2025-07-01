---
title: 透過 OpenAPI 傳遞 AEM 內容片段
description: 瞭解如何使用OpenAPI進行tAEM內容片段傳送
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 28d0d6bdfd9e6f1c1483bed7c5e65df340e8b559
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---


# 透過 OpenAPI 傳遞 AEM 內容片段 {#aem-content-fragment-delivery-with-openapi}

在Adobe Experience Manager (AEM) as a Cloud Service中，用於內容片段傳送的AEM OpenAPI：

* 是一種OpenAPI，針對以JSON格式即時傳送AEM內容片段而最佳化
* 提供現代CDN整合，讓作用中內容失效
* 專注於內容傳送（效能、擴充性、CDN整合、最佳化的JSON控制和輸出）
* 包括將JSON水合為參考片段和資產的能力

此API：

* 是AEM Assets HTTP API中[內容片段支援的後續專案](/help/assets/content-fragments/assets-api-content-fragments.md)

* 補充[內容片段和內容片段模型OpenAPI](/help/headless/content-fragment-openapis.md)，讓您管理內容片段和內容片段模型(CRUD)

* 是[AEM GraphQL API的HTTP REST替代方案，用於內容片段](/help/headless/graphql-api/content-fragments.md)

如需完整檔案，請參閱[使用OpenAPI的AEM內容片段傳送](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/)。

>[!NOTE]
>
>請參閱[結構化內容傳遞與管理的AEM API](/help/headless/apis-headless-and-content-fragments.md)，以取得各種可用API的概觀，以及所涉及概念的比較。

>[!IMPORTANT]
>
>若要在AEM as a Cloud Service上使用OpenAPI啟用內容片段傳送，請確保尚未啟用，然後提交標題為「**使用OpenAPI啟用內容片段傳送**」的Adobe支援票證，並指定：
>
>* Cloud Service程式和環境ID
>* 您要使用內容片段傳送OpenAPI解決的使用案例詳細資訊
>* Adobe應回應並隨時通知有關請求和專案的所有聯絡人的詳細資訊（如有需要）

## 快取 {#caching}

AEM與AEM CDN Fastly整合。 這表示會在Fastly層級快取發佈層級上提供的JSON回應。

接著，系統會根據預先定義的快取標題，快取回應（無法設定）：

* 回應會在瀏覽器/使用者端快取中快取5分鐘
   * `max-age`=`300`
* 回應會在CDN快取中快取1小時
   * `s-maxage`=`3600`
* 重新驗證新請求時，可為過時內容提供最多1小時的服務
   * `stale-while-revalidate`=`3600`
* 過時內容可錯誤提供長達1天的服務
   * `stale-on-error`=`86400`

使用OpenAPI的內容片段傳送支援作用中CDN快取失效。 這代表每當內容更新或發佈時，對應的JSON OpenAPI回應都會透過對Fastly的軟清除請求自動失效。 這可讓您在到達實際CDN快取存留期(`s-maxage`)之前，檢視JSON輸出中反映的變更。

## 可用性 {#availability}

預覽和發佈層級提供OpenAPI的內容片段傳送。 OpenAPI會傳送JSON格式的內容片段，以供預覽和即時傳送。

若要使用OpenAPI預覽內容片段傳送，可以：

* 發佈到預覽
* 啟用存取以使用IP允許清單預覽
* 取得預覽URL

## CORS {#cors}

[CORS允許的原始項](/help/headless/deployment/cross-origin-resource-sharing.md)定義可以呼叫API的原始項。

此API不會考慮在Dispatcher設定端定義(特別是為GraphQL定義)的CORS允許來源。

## API速率限制 {#api-rate-limits}

API允許新請求的速率每秒最多200個請求（每個環境）。

一旦超過此限制，API就會開始傳送429錯誤。 這些錯誤必須由任何使用者端應用程式處理，且失敗的請求會在指數輪詢重試後重試。

<!-- 
## Limitations {#limitations}
-->
