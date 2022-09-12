---
title: 使用AEM無標題的反向連結篩選設定
description: Adobe Experience Manager的「反向連結篩選器」可啟用來自協力廠商主機的存取。 需要反向連結篩選器的OSGi設定，才能為無周邊應用程式啟用GraphQL端點的存取。
feature: GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# 反向連結篩選 {#referrer-filter}

Adobe Experience Manager的「反向連結篩選器」可啟用來自協力廠商主機的存取。 需要反向連結篩選器的OSGi設定，才能為無周邊應用程式啟用GraphQL端點的存取。

若要這麼做，請為反向連結篩選器新增適當的OSGi設定，以：

* 指定受信任的網站主機名；heer `allow.hosts` 或 `allow.hosts.regexp`,
* 授予此主機名稱的存取權。

檔案的名稱必須是 `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

例如，若要授予具有反向連結之請求的存取權 `my.domain` 您可以：

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
>* 確保未公開任何敏感資訊
>* 不使用通配符 [*] 語法；這既會停用對GraphQL端點的驗證存取，也會將其公開給全世界。


>[!CAUTION]
>
>所有GraphQL [綱要](#schema-generation) (衍生自已 **已啟用**)可透過GraphQL端點讀取。
>
>這意味著，您需要確保沒有敏感資料可用，因為這些資料可能會以這種方式洩露；例如，這包括可以在模型定義中顯示為欄位名稱的資訊。
