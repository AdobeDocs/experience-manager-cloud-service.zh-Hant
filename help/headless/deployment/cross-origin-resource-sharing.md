---
title: AEM Headless 跨原始資源共用 (CORS) 設定
description: Adobe Experience Manager 跨原始資源共用 (CORS) 允許無周邊網頁應用程式對 AEM 進行用戶端呼叫。需要 CORS 設定才能存取 GraphQL 端點。
feature: GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
source-git-commit: 316680823fe4bc85e1f4359305047c0d1f517dc7
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 90%

---

# 跨原始資源共用 (CORS) 設定。

>[!CAUTION]
>
>如果 [Dispatcher中的快取已啟用](/help/headless/deployment/dispatcher-caching.md) 則不需要CORS篩選器，因此可忽略此區段。

>[!NOTE]
>
>如需 AEM 中 CORS 資源共用原則的詳細概述，請參閱[了解跨原始資源共用 (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors))。

若要存取 GraphQL 端點，必須設定 CORS 原則並新增至[透過 Cloud Manager 部署到 AEM](/help/implementing/cloud-manager/deploy-code.md) 的 AEM 專案。做法是為所需端點新增適當的 OSGi CORS 設定。可以建立多個 CORS 設定並將其部署到不同環境。[WKND 參考網站](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)有提供範例

CORS 設定必須指定一個受信任的網站來源 `alloworigin` 或 `alloworiginregexp`，其存取權必須授予。

設定檔案的名稱必須類似：`com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json`，其中 `appname` 為您的應用程式名稱。

例如，若要授予 GraphQL 端點 `/content/cq:graphql/wknd/endpoint` 和 `https://my.domain` 之持續性查詢端點的存取權，您可以使用：

```json
{
  "supportscredentials":false,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/cq:graphql/wknd/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

如果您為端點設定了虛名路徑，您也可以在 `allowedpaths` 中使用它。
