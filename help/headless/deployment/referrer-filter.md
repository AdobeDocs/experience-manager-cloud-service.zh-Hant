---
title: AEM Headless 查閱者篩選器設定
description: Adobe Experience Manager 的查閱者篩選器允許第三方主機存取。需要查閱者篩選器的 OSGi 設定，無周邊應用程式才能存取 GraphQL 端點。
feature: GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
source-git-commit: 076cafe3d096fd7f4c808f1b2553a9ba6b6c1833
workflow-type: ht
source-wordcount: '277'
ht-degree: 100%

---

# 查閱者篩選器 {#referrer-filter}

Adobe Experience Manager 的查閱者篩選器允許第三方主機存取。

需要查閱者篩選器的 OSGi 設定，無周邊應用程式才能透過 HTTP POST 存取 GraphQL 端點。使用透過 HTTP GET 存取 AEM 的 AEM Headless 持續性查詢時，不需要查閱者篩選器設定。

>[!WARNING]
> AEM 的查閱者篩選器不是 OSGi 設定工廠，這表示一次只有一個設定在 AEM 服務上作用。盡可能避免新增自訂查閱者篩選器設定，因為這會覆寫 AEM 的原生設定，並可能破壞產品功能。

這可透過為查閱者篩選器新增適當的 OSGi 設定來完成，這會：

* 指定受信任網站的主機名稱；`allow.hosts` 或 `allow.hosts.regexp`，
* 授予此主機名稱的存取權。

檔案名稱必須是 `org.apache.sling.security.impl.ReferrerFilter.cfg.json`。

例如，要授予使用查閱者 `my.domain` 之要求的存取權，您可以：

```xml
{
    "allow.empty": false,
    "allow.hosts": [
      "my.domain"
    ],
    "allow.hosts.regexp": [
      ""
    ],
    "filter.methods": [
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp": [
      ""
    ]
}
```

>[!CAUTION]
>
>客戶有責任：
>
>* 僅將存取權授予受信任網域
>* 確保敏感資訊沒有公開
>* 不要使用萬用字元 [*] 語法；這將停用對 GraphQL 端點的已驗證存取，並將其公開給整個世界。


>[!CAUTION]
>
>所有 GraphQL [結構描述](#schema-generation) (衍生自&#x200B;**已啟用**&#x200B;的內容片段模型) 都可透過 GraphQL 端點讀取。
>
>這表示您必須確保沒有敏感資料，因為它可能會以這種方式洩露；例如，這包括可以在模型定義中做為欄位名稱出現的資訊。
