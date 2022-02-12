---
title: 具有無頭的調度AEM程式配置
description: Dispatcher是Adobe Experience Manager發佈環境前的快取和安全層。 幾種配置用於向無頭應用程式開啟GraphQL端點。
feature: Dispatcher, GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# 具有無頭的調度AEM程式配置

的 [調度程式](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 是Adobe Experience Manager發佈環境前的快取和安全層。 預設情況下，包含若干配置，以向無頭應用程式開啟GraphQL端點。

>[!NOTE]
>
>有關Dispatcher的詳細文檔，請參見 [《 Dispatcher指南》](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)

作為項目的一AEM部分，包括一個包含調度程式配置的調度程式模組。 從 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 自動包含 [篩選](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) 啟用GraphQL端點。

## GraphQL端點

作為預設篩選器的一部分， [GraphQL端點](/help/headless/graphql-api/graphql-endpoint.md) 將使用以下規則開啟：

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

的 `*` 通配符可開啟實例上的多個AEM端點。 將使用GraphQL終結點進行查詢 `POST` 而回應會 **不** 被快取。

## GraphQL永續查詢

對永續查詢的請求針對不同的端點。 作為預設篩選器配置的一部分， [永續查詢](/help/headless/graphql-api/persisted-queries.md) 將使用以下規則開啟：

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

可使用 `GET`，從而在Dispatcher和CDN級別快取響應。 可以找到有關快取和快取無效的詳細資訊 [這裡](/help/implementing/dispatcher/caching.md)。
