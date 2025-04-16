---
title: 使用OpenAPI的AEM內容片段傳送
description: 瞭解如何使用OpenAPI進行tAEM內容片段傳送
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 使用OpenAPI的AEM內容片段傳送 {#aem-content-fragment-delivery-with-openapi}

>[!IMPORTANT]
>
>此API可透過早期採用者計畫取得。
>
>若要檢視狀態，以及如果您有興趣要如何套用，請檢視[發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

在Adobe Experience Manager (AEM) as a Cloud Service中，用於內容片段傳送的AEM OpenAPI：

* 是[AEM Edge Delivery Services](/help/edge/overview.md)上的HTTP REST API，旨在從JSON格式的內容片段傳送結構化內容
* 提供現代CDN整合，讓作用中內容失效
* 專注於內容傳送（效能、擴充性、CDN整合、最佳化的JSON控制和輸出）
* 包括將JSON水合為參考片段和資產的能力

此API：

* 是AEM Assets HTTP API中[內容片段支援的後續專案](/help/assets/content-fragments/assets-api-content-fragments.md)

* 補充[內容片段和內容片段模型OpenAPI](/help/headless/content-fragment-openapis.md)，讓您管理內容片段和內容片段模型(CRUD)

* 是[AEM GraphQL API的HTTP REST替代方案，用於內容片段](/help/headless/graphql-api/content-fragments.md)

如需完整檔案，請參閱[AEM Sites API結構描述 — 內容片段傳送API (2024.07-experimental)](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/delivery/)。

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
