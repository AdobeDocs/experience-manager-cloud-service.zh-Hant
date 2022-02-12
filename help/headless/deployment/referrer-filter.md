---
title: 帶無頭的引用過濾器AEM配置
description: Adobe Experience Manager的引用過濾器允許從第三方主機訪問。 需要為引用過濾器配置OSGi配置，以便能夠訪問無頭應用程式的GraphQL終結點。
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# 引用篩選器 {#referrer-filter}

Adobe Experience Manager的引用過濾器允許從第三方主機訪問。 需要為引用過濾器配置OSGi配置，以便能夠訪問無頭應用程式的GraphQL終結點。

為此，請為引用過濾器添加適當的OSGi配置：

* 指定受信任的網站主機名；或 `allow.hosts` 或 `allow.hosts.regexp`。
* 授予對此主機名的訪問權限。

檔案的名稱必須為 `org.apache.sling.security.impl.ReferrerFilter.cfg.json`。

例如，向引用者授予對請求的訪問權限 `my.domain` 您可以：

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>客戶仍有責任：
>
>* 僅授予受信任域的訪問權限
>* 確保沒有洩露任何敏感資訊
>* 不使用通配符 [*] 語法；這既會禁用對GraphQL端點的經過身份驗證的訪問，又會將其向全世界公開。


>[!CAUTION]
>
>所有GraphQL [模式](#schema-generation) (源於已 **已啟用**)可通過GraphQL終結點讀取。
>
>這意味著您需要確保沒有敏感資料可用，因為敏感資料可能會以這種方式洩露；例如，這包括在模型定義中可以作為欄位名稱顯示的資訊。
