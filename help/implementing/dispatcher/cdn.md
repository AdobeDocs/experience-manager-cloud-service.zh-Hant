---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 15%

---

# AEM as a Cloud Service 中的 CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM as Cloud Service 會隨附內建的 CDN。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。"

AEM as Cloud Service 會隨附內建的 CDN。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

AEM管理的CDN可滿足大部分客戶的效能和安全需求。 對於發佈層級，客戶可選擇從自己必須管理的CDN指向該層級。 您可根據符合特定必要條件，逐個允許此情境，包括但不限於與其CDN廠商進行舊版整合且難以放棄的客戶。

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## AEM管理的CDN  {#aem-managed-cdn}

請依照下節所述，使用Cloud Manager自助服務UI，透過現成可用的AEM CDN來準備內容傳遞：

1. [管理 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理客戶網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

依預設，針對AEM管理的CDN設定，針對生產與非生產（開發與預備）環境，所有公用流量皆可進入發佈服務。 您可以透過Cloud Manager使用者介面，針對特定環境限制發佈服務的流量（例如，限制預備的IP位址範圍）。

如需了解更多，請參閱[管理 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

>[!CAUTION]
>
>AEM管理的CDN只會提供允許IP的請求。 如果您將自己的CDN指向AEM管理的CDN，請確定CDN的IP包含在允許清單中。

## 客戶CDN指向AEM管理的CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客戶 CDN 會指向 AEM 管理的 CDN"
>abstract="AEM as Cloud Service 為客戶提供了使用其現有 CDN 的選項。對於發佈層級，客戶可選擇從自己必須管理的CDN指向該層級。 您可根據符合特定必要條件，逐個允許此情境，包括但不限於與其CDN廠商進行舊版整合且難以放棄的客戶。"

如果客戶必須使用其現有的CDN，他們可以管理CDN並將其指向AEM管理的CDN，但須符合下列條件：

* 客戶必須擁有現有的CDN，而更換這些CDN的工作量會很大。
* 客戶必須管理它。
* 客戶必須能將CDN設定為可與AEMas a Cloud Service搭配使用 — 請參閱下方的設定指示。
* 客戶必須有工程CDN專家隨時待命，以防發生相關問題。
* 客戶必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 將您的CDN指向AdobeCDN的入口作為其來源網域。 例如， `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. 將SNI設定為AdobeCDN的入口。
1. 將Host標題設為來源網域。 例如：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 設定 `X-Forwarded-Host` 包含網域名稱的標題，以便AEM可判斷主機標題。 例如：`X-Forwarded-Host:example.com`。
1. 設定 `X-AEM-Edge-Key`. 值應來自Adobe。

   * 需要，讓AdobeCDN驗證請求來源並傳遞 `X-Forwarded-*` 標題至AEM應用程式。 例如，`X-Forwarded-For` 用於確定客戶端IP。 因此，它成為受信任呼叫者（即客戶管理的CDN）的責任，以確保 `X-Forwarded-*` 標題（請參閱下方附註）。
   * 此外，當AdobeCDN的入口被封鎖時， `X-AEM-Edge-Key` 不存在。 如果您需要直接存取AdobeCDN的入口（待封鎖），請通知Adobe。

請參閱 [CDN廠商設定範例](#sample-configurations) 主要CDN廠商的設定範例小節。

在接受即時流量之前，您應向Adobe的客戶支援驗證端對端流量路由是否正常運作。

取得 `X-AEM-Edge-Key`，您可以依照下列方式測試要求是否正確路由。

在Linux®中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

在Windows中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>使用您自己的CDN時，您不需要在Cloud Manager中安裝網域和憑證。 AdobeCDN中的路由是使用預設網域完成 `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` 應在請求中傳送 `Host` 頁首。 覆寫請求 `Host` 具有自訂網域名稱的標題，可能會導致AdobeCDN錯誤地路由請求。


>[!NOTE]
>
>管理自己CDN的客戶應確保傳送至AEM CDN的標題完整無缺。 例如，建議客戶清除所有 `X-Forwarded-*` 標題，並將其設為已知和控制的值。 例如， `X-Forwarded-For` 應包含用戶端的IP位址，而 `X-Forwarded-Host` 應包含網站的主機。

>[!NOTE]
>
>沙箱方案環境不支援客戶提供的CDN。

只有在快取遺失時，才需要客戶CDN與AEM CDN之間的額外躍點。 若使用本文所述的快取最佳化策略，新增客戶CDN應該只會造成可忽略的延遲。

發佈層級支援此客戶CDN設定，但製作層級不支援。

### CDN廠商設定範例 {#sample-configurations}

以下是數家主要CDN廠商的數個設定範例。

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Cloudflare**

![Cloudflare1](assets/cloudflare1.png "Cloudflare")
![Cloudflare2](assets/cloudflare2.png "Cloudflare")

## 地理位置標題 {#geo-headers}

AEM管理的CDN會透過下列方式將標題新增至每個請求：

* 國家/地區代碼： `x-aem-client-country`
* 大陸代碼： `x-aem-client-continent`

>[!NOTE]
>
>如果有客戶管理的CDN，這些標題會反映客戶CDN代理伺服器的位置，而非實際用戶端。 因此，若是由客戶管理的CDN，地理位置標題應由客戶CDN管理。

國家/地區代碼的值是描述的Alpha-2代碼 [此處](https://en.wikipedia.org/wiki/ISO_3166-1).

大陸代碼的值為：

* AF非洲
* 南極洲
* AS亞洲
* 歐盟
* 北美
* 大洋洲奧克
* SA南美洲

此資訊在使用案例中可能會很實用，例如根據要求的來源（國家）重新導向至不同的url。 請使用Vary標題，根據地理資訊快取回應。 例如，重新導向至特定國家/地區登陸頁面應一律包含 `Vary: x-aem-client-country`. 如有需要，您可以使用 `Cache-Control: private` 以防止快取。 另請參閱 [快取](/help/implementing/dispatcher/caching.md#html-text).
