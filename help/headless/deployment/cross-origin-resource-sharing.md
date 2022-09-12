---
title: 使用AEM無頭式進行跨原始資源共用(CORS)設定
description: Adobe Experience Manager的跨原始資源共用(CORS)可讓無頭式Web應用程式對AEM進行用戶端呼叫。 需要CORS配置才能啟用對GraphQL端點的訪問。
feature: GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 跨原始資源共用(CORS)設定

>[!NOTE]
>
>如需AEM中CORS資源共用原則的詳細概述，請參閱 [了解跨原始資源共用(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

若要存取GraphQL端點，必須設定CORS原則，並新增至AEM專案，即 [透過Cloud Manager部署至AEM](/help/implementing/cloud-manager/deploy-code.md). 若要這麼做，請為所需端點新增適當的OSGi CORS設定檔案。 可建立多個CORS設定並部署至不同環境。 如需範例，請參閱 [WKND參考站點](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

CORS設定必須指定受信任的網站來源 `alloworigin` 或 `alloworiginregexp` 必須授予其存取權。

設定檔案的名稱必須如下： `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` where `appname` 會反映應用程式的名稱。

例如，要授予對GraphQL端點的訪問權 `/content/cq:graphql/wknd/endpoint` 和持續查詢端點 `https://my.domain` 您可以使用：

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

如果您已設定端點的虛名路徑，也可以在 `allowedpaths`.
