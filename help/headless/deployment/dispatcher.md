---
title: AEM Headless 的 Dispatcher 設定
description: Dispatcher 是 Adobe Experience Manager 發佈環境前面的快取和安全層。多個設定用於向無周邊應用程式開啟 GraphQL 端點。
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 55%

---

# AEM Headless 的 Dispatcher 設定

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 是 Adobe Experience Manager 發佈環境前面的快取和安全層。依預設，內含多個設定用於向無周邊應用程式開啟 GraphQL 端點。

>[!NOTE]
>
>如需Dispatcher的詳細檔案，請參閱 [Dispatcher指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant).

AEM專案中包含Dispatcher模組，其中包含了Dispatcher的設定。 新產生的專案 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 自動包含 [篩選器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) 會啟用GraphQL端點。

## GraphQL端點

作為預設篩選器的一部分，[GraphQL 端點](/help/headless/graphql-api/graphql-endpoint.md)是使用以下規則開啟：

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

`*` 萬用字元在 AEM 執行個體上開啟多個端點。使用GraphQL端點進行查詢的方法有： `POST` 而回應是 **not** 已快取。

## GraphQL 持續性查詢

針對不同端點提出持續查詢的請求。 在預設篩選設定中， [持久查詢](/help/headless/graphql-api/persisted-queries.md) 開啟時遵循下列規則：

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

可以使用請求持久查詢 `GET`，方法是在Dispatcher和CDN層級快取回應。 更多快取和快取失效的詳細資訊，請參閱[此處](/help/implementing/dispatcher/caching.md)。
