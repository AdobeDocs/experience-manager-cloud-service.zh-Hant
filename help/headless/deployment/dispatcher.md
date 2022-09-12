---
title: 使用AEM Headless進行Dispatcher設定
description: Dispatcher是Adobe Experience Manager Publish環境前面的快取和安全層。 有幾種配置用於向無周邊應用程式開啟GraphQL端點。
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---

# 使用AEM Headless進行Dispatcher設定

此 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 是Adobe Experience Manager Publish環境前面的快取和安全層。 預設會包含數個設定，以向無周邊應用程式開啟GraphQL端點。

>[!NOTE]
>
>如需Dispatcher的詳細檔案，請參閱 [Dispatcher指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)

作為AEM專案的一部分，會包含Dispatcher模組，其中包含Dispatcher的設定。 從 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 自動包含 [篩選器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) 啟用GraphQL端點。

## GraphQL端點

作為預設篩選的一部分， [GraphQL端點](/help/headless/graphql-api/graphql-endpoint.md) 會使用下列規則開啟：

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

此 `*` 萬用字元會開啟AEM例項上的多個端點。 使用GraphQL端點進行查詢時，將使用 `POST` 而回應 **not** 快取。

## GraphQL持續查詢

對不同端點提出持續查詢請求。 作為預設篩選設定的一部分， [持續查詢](/help/headless/graphql-api/persisted-queries.md) 會使用下列規則開啟：

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

可使用 `GET`，借此在Dispatcher和CDN層級快取回應。 有關快取和快取失效的詳細資訊，請查閱 [此處](/help/implementing/dispatcher/caching.md).
