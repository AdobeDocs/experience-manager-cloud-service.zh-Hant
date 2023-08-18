---
title: 使用AEM Headless的Dispatcher端點設定
description: Dispatcher 是 Adobe Experience Manager 發佈環境前面的快取和安全層。多個設定用於向 Headless 應用程式開啟 GraphQL 端點。
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: 316680823fe4bc85e1f4359305047c0d1f517dc7
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 94%

---


# Dispatcher — 使用AEM Headless進行端點設定

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 是 Adobe Experience Manager 發佈環境前面的快取和安全層。依預設，內含多個設定用於向 Headless 應用程式開啟 GraphQL 端點。

>[!NOTE]
>
>如需 Dispatcher 的詳細文件，請參閱 [Dispatcher 指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)。

作為 AEM 專案的一部分，Dispatcher 模組包含在內，模組中有 Dispatcher 設定。從 [AEM 專案原型](https://github.com/adobe/aem-project-archetype)新產生的專案會自動包含可啟用 GraphQL 端點的[篩選器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter)。

## GraphQL 端點

作為預設篩選器的一部分，[GraphQL 端點](/help/headless/graphql-api/graphql-endpoint.md)是使用以下規則開啟：

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

`*` 萬用字元在 AEM 執行個體上開啟多個端點。使用 GraphQL 端點的查詢透過 `POST` 進行，回應&#x200B;**不會**&#x200B;被快取。

## GraphQL 持續性查詢

對持續性查詢的要求是針對不同的端點發出的。作為預設篩選器設定的一部分，[持續性查詢](/help/headless/graphql-api/persisted-queries.md) 的 URL 是使用以下規則開啟：

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

可以使用 `GET` 要求持續性查詢，在 Dispatcher 和 CDN 層級快取回應。更多快取和快取失效的詳細資訊，請參閱[此處](/help/implementing/dispatcher/caching.md)。
