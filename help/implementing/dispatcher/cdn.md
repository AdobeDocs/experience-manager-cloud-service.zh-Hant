---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 612082f22895af596247f69c4d57222376d7b519
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 7%

---

# AEM as a Cloud Service 中的 CDN {#cdn}


>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM asCloud Service隨附內建的CDN。 主要用途是透過從瀏覽器附近邊緣的CDN節點傳送可快取的內容，以減少延遲。 它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。"

AEM asCloud Service隨附內建的CDN。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

AEM管理的CDN將可滿足大部分客戶的效能和安全性需求。 對於發佈層級，客戶可選擇從自己需要管理的CDN指向該層級。 我們將根據符合特定必要條件（包括但不限於與其CDN廠商進行舊版整合且難以放棄的客戶），逐個允許這項操作。

## AEM Managed CDN  {#aem-managed-cdn}

請依照下節所述，使用Cloud Manager自助服務UI，透過現成可用的AEM CDN來準備內容傳遞：

1. [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

依預設，針對AEM管理的CDN設定，針對生產及非生產（開發及預備）環境，所有公用流量皆可進入發佈服務。 如果您想要針對特定環境限制發佈服務的流量（例如，限制預備的IP位址範圍），您可以透過Cloud Manager UI以自助方式執行此作業。

請參閱 [管理IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) 了解更多。

>[!CAUTION]
>
>AEM管理的CDN只會處理來自允許IP的請求。 如果您將自己的CDN指向AEM管理的CDN，請確定CDN的IP包含在允許清單中。

## 客戶CDN指向AEM Managed CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客戶CDN指向AEM Managed CDN"
>abstract="AEM as Cloud Service可讓客戶選擇使用其現有的CDN。 對於發佈層級，客戶可選擇從自己需要管理的CDN指向該層級。 我們將根據符合特定必要條件（包括但不限於與其CDN廠商進行舊版整合且難以放棄的客戶），逐個允許這項操作。"

如果客戶必須使用其現有的CDN，他們可以管理CDN並將其指向AEM管理的CDN，但須符合下列條件：

* 客戶必須擁有現有的CDN，而更換這些CDN的工作量會很大。
* 客戶必須管理它。
* 客戶必須能將CDN設定為可與AEMas a Cloud Service搭配使用 — 請參閱下方的設定指示。
* 若發生相關問題，客戶必須有工程CDN專家隨時待命。
* 客戶必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 將您的CDN指向AdobeCDN的入口作為其來源網域。 例如， `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. SNI還必須設定為AdobeCDN的入口
1. 將Host標題設為來源網域。 例如： `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. 設定 `X-Forwarded-Host` 包含網域名稱的標題，以便AEM可判斷主機標題。 例如： `X-Forwarded-Host:example.com`.
1. 設定 `X-AEM-Edge-Key`. 值應來自Adobe。
   * 這是必要的，讓AdobeCDN可以驗證請求來源並傳遞 `X-Forwarded-*` 標題至AEM應用程式。 例如，`X-Forwarded-For` 用於確定客戶端IP。 因此，它成為受信任呼叫者（即客戶管理的CDN）的責任，以確保 `X-Forwarded-*` 標題（請參閱下方附註）。
   * 此外，當AdobeCDN的入口被封鎖時， `X-AEM-Edge-Key` 不存在。 如果您需要直接存取AdobeCDN的入口（待封鎖），請通知Adobe。

在接受即時流量之前，您應向Adobe的客戶支援驗證端對端流量路由是否正常運作。

取得 `X-AEM-Edge-Key`，您可以依照下列方式來測試要求是否正確路由：

```
https: //publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H 'X-Forwarded-Host: example.com' -H 'X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>'
```

請注意，使用您自己的CDN時，不需要在Cloud Manager中安裝網域和憑證。 AdobeCDN中的路由將使用預設網域完成 `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.

>[!NOTE]
>
>管理自己CDN的客戶應確保傳送至AEM CDN的標題完整無缺。 例如，建議客戶清除所有 `X-Forwarded-*` 標題，並將其設為已知和控制的值。 例如， `X-Forwarded-For` 應包含用戶端的IP位址，而 `X-Forwarded-Host` 應包含網站的主機。

>[!NOTE]
>
>沙箱方案環境不支援客戶提供的CDN。

由於額外的躍點，可能會導致效能點擊較小，但從客戶CDN到AEM管理CDN的躍點可能會很有效。

請注意，此客戶CDN設定支援發佈層級，但不支援在製作層級之前。

## 地理位置標題 {#geo-headers}

AEM管理的CDN會透過下列方式將標題新增至每個請求：

* 國家/地區代碼： `x-aem-client-country`
* 大陸代碼： `x-aem-client-continent`

國家/地區代碼的值是描述的Alpha-2代碼 [此處](https://en.wikipedia.org/wiki/ISO_3166-1).

大陸代碼的值為：

* AF非洲
* 南極洲
* AS亞洲
* 歐盟
* 北美
* 大洋洲奧克
* SA南美洲

此資訊在使用案例中可能會很實用，例如根據要求的來源（國家）重新導向至不同的url。 請使用Vary標題，快取根據地理資訊的回應。 例如，重新導向至特定國家/地區登陸頁面應一律包含 `Vary: x-aem-client-country`. 如有需要，您可以使用 `Cache-Control: private` 以防止快取。 另請參閱 [快取](/help/implementing/dispatcher/caching.md#html-text).
