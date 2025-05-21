---
title: 透過 OpenAPI 傳遞 AEM 內容片段
description: 瞭解如何使用OpenAPI進行tAEM內容片段傳送
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 7f7ed3adcbd01f688f48f3ba4a0c25293b8b1551
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 4%

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

AEM也隨附使用中CDN快取失效機制。 這代表每當內容更新或發佈時，對應的JSON OpenAPI回應都會透過對Fastly的軟清除請求自動失效。 這可讓您在到達實際CDN快取存留期(`s-maxage`)之前，檢視JSON輸出中反映的變更。
