---
title: 具有無頭的跨源資源共用(CORS)配AEM置
description: Adobe Experience Manager的跨源資源共用(CORS)允許無頭Web應用程式進行客戶端呼AEM叫。 需要CORS配置才能訪問GraphQL終結點。
feature: GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 跨源資源共用(CORS)配置

>[!NOTE]
>
>有關CORS資源共用策略的詳細概述，請參AEM見 [瞭解跨源資源共用(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors))。

要訪問GraphQL終結點，必須配置CORS策略並將其添加AEM到 [通過雲管AEM理器部署到](/help/implementing/cloud-manager/deploy-code.md)。 這是通過為所需端點添加適當的OSGi CORS配置檔案來完成的。 可以建立多個CORS配置並將其部署到不同的環境。 例如， [WKND參考站點](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

CORS配置必須指定受信任的網站源 `alloworigin` 或 `alloworiginregexp` 必須授予其訪問權限。

配置檔案必須命名為： `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` 何處 `appname` 反映應用程式的名稱。

例如，授予對GraphQL終結點的訪問權限 `/content/cq:graphql/wknd/endpoint` 和永續查詢終結點 `https://my.domain` 您可以使用：

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

如果已為端點配置虛榮路徑，也可以在 `allowedpaths`。
