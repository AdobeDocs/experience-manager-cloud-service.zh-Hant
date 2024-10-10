---
title: AEM Headless 查閱者篩選器設定
description: Adobe Experience Manager 的查閱者篩選器允許第三方主機存取。需要查閱者篩選器的 OSGi 設定， Headless 應用程式才能存取 GraphQL 端點。
feature: Headless, GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
solution: Experience Manager
role: Admin, Developer
source-git-commit: 3096436f8057833419249d51cb6c15e6c28e9e13
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 55%

---

# 查閱者篩選器 {#referrer-filter}

Adobe Experience Manager 的查閱者篩選器允許第三方主機存取。

需要查閱者篩選器的 OSGi 設定， Headless 應用程式才能透過 HTTP POST 存取 GraphQL 端點。使用透過 HTTP GET 存取 AEM 的 AEM Headless 持續性查詢時，不需要查閱者篩選器設定。

>[!WARNING]
> AEM 的查閱者篩選器不是 OSGi 設定工廠，這表示一次只有一個設定在 AEM 服務上作用。盡可能避免新增自訂查閱者篩選器設定，因為這會覆寫 AEM 的原生設定，並可能破壞產品功能。

這可透過為查閱者篩選器新增適當的 OSGi 設定來完成，這會：

* 指定受信任網站的主機名稱；`allow.hosts` 或 `allow.hosts.regexp`，
* 授予此主機名稱的存取權。

檔案名稱必須是 `org.apache.sling.security.impl.ReferrerFilter.cfg.json`。

## 設定範例 {#example-configuration}

例如，要授予使用查閱者 `my.domain` 之要求的存取權，您可以：

>[!CAUTION]
>
>這是可能會覆寫標準設定的基本範例。 您必須確保產品更新一律會套用至任何自訂。

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

## 資料安全性 {#data-security}

>[!CAUTION]
>
>您有責任完全處理下列各點。

為確保您的資料安全無虞，您必須確保：

* 存取許可權僅&#x200B;**僅**&#x200B;授與信任的網域

* **未使用**&#x200B;中的萬用字元[`*`]語法；這既會停用對GraphQL端點的已驗證存取權，也會將其公開給整個世界

* 敏感資訊為&#x200B;**永不公開**；不直接也不間接：

   * 例如，所有[GraphQL結構描述](/help/headless/graphql-api/content-fragments.md#schema-generation)都是：

      * 衍生自&#x200B;**已啟用**&#x200B;的內容片段模型

     **和**

      * 可透過GraphQL端點讀取

     這表示在模型定義中以欄位名稱顯示的資訊可以變為可用。

您必須確保任何方法都無法取得敏感資料，因此必須仔細考慮這些詳細資訊。
