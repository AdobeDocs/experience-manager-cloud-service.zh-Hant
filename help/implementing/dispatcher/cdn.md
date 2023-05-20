---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 25%

---

# AEM as a Cloud Service 中的 CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM as Cloud Service 會隨附內建的 CDN。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。"

AEM as Cloud Service 會隨附內建的 CDN。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

托AEM管CDN滿足大多數客戶的效能和安全要求。 對於發佈層級，客戶可以選擇從他們自己必須管理的 CDN 指向它。依不同個案可允許此情況，以滿足特定先決條件為基礎，包括但不限於客戶和他們的 CDN 供應商有一個難以放棄的舊版整合。

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## 托AEM管CDN  {#aem-managed-cdn}

按照以下各節，使用Cloud Manager自助服務UI，通過使用現成CDNAEM準備內容交付：

1. [管理 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理客戶網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制通信**

預設情況下，AEM對於受管理的CDN設定，所有公共通信都可以進入發佈服務，無論是生產環境還是非生產環境（開發和階段）。 您可以通過Cloud Manager用戶介面限制給定環境的發佈服務的流量（例如，通過IP地址範圍限制轉移）。

如需了解更多，請參閱[管理 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

>[!CAUTION]
>
>只有來自允許IP的請求由托管CDNAEM提供。 如果將您自己的CDN指向受AEM管理的CDN，則請確保CDN的IP包含在允許清單中。

## 客戶CDN指向AEM托管CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客戶 CDN 會指向 AEM 管理的 CDN"
>abstract="AEM as Cloud Service 為客戶提供了使用其現有 CDN 的選項。對於發佈層級，客戶可以選擇從他們自己必須管理的 CDN 指向它。依不同個案可允許此情況，以滿足特定先決條件為基礎，包括但不限於客戶和他們的 CDN 供應商有一個難以放棄的舊版整合。"

如果客戶必須使用其現有CDN，他們可以管理它並將其指向受AEM管理的CDN，但滿足以下條件：

* 客戶必須擁有一個需要更換的現有CDN。
* 客戶必須管理它。
* 客戶必須能夠配置CDN以使用AEMas a Cloud Service — 請參閱下面提供的配置說明。
* 客戶必須有工程CDN專家，在出現與案例相關的問題時隨時待命。
* 客戶必須執行並成功傳遞負載test，然後才能開始生產。

配置說明：

1. 將您的CDN指向AdobeCDN的入口作為其源域。 比如說， `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 將SNI設定為AdobeCDN的入口。
1. 將主機頭設定為源域。 例如：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 設定 `X-Forwarded-Host` 包含域名的標頭，AEM以便確定主機標頭。 例如：`X-Forwarded-Host:example.com`。
1. 設定 `X-AEM-Edge-Key`. 值應來自Adobe。

   * 需要AdobeCDN驗證請求源並傳遞 `X-Forwarded-*` 到應用程式AEM的標題。 比如說，`X-Forwarded-For` 用於確定客戶端IP。 因此，它成為可信呼叫者（即客戶管理的CDN）的責任，以確保CDN的正確性 `X-Forwarded-*` 標題（請參閱下面的注釋）。
   * 可選地，當AdobeCDN的入口被阻止時 `X-AEM-Edge-Key` 不存在。 如果需要直接訪問AdobeCDN的入口（要阻止），請通知Adobe。

查看 [示例CDN供應商配置](#sample-configurations) 部分，以瞭解主要CDN供應商的配置示例。

在接受即時通信之前，您應該向Adobe的客戶支援驗證端到端通信路由是否正常運行。

獲取 `X-AEM-Edge-Key`，您可以test請求已正確路由，如下所示。

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
>使用您自己的CDN時，無需在雲管理器中安裝域和證書。 AdobeCDN中的路由是使用預設域完成的 `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` 應在請求中發送 `Host` 標題。 覆蓋請求 `Host` 具有自定義域名的標頭可能會導致AdobeCDN錯誤地路由請求。


>[!NOTE]
>
>管理自己的CDN的客戶應確保發送到AEMCDN的報頭的完整性。 例如，建議客戶清除所有 `X-Forwarded-*` 並將其設定為已知值和受控值。 比如說， `X-Forwarded-For` 應包含客戶端的IP地址，而 `X-Forwarded-Host` 應包含站點的主機。

>[!NOTE]
>
>沙盒程式環境不支援客戶提供的CDN。

只有在快取未命中時，才需要AEM客戶CDN和CDN之間的額外躍點。 通過使用本文描述的快取優化策略，增加一個客戶CDN只會引入可忽略的延遲。

發佈層支援此客戶CDN配置，但不在作者層之前。

### 示例CDN供應商配置 {#sample-configurations}

下面是幾個主要CDN供應商的幾個配置示例。

**Akamai**

![阿卡邁1](assets/akamai1.png "阿卡邁")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon雲前**

![雲前1](assets/cloudfront1.png "Amazon雲前")
![CloudFront2](assets/cloudfront2.png "Amazon雲前")

**雲閃**

![雲閃1](assets/cloudflare1.png "雲閃")
![Cloudflare2](assets/cloudflare2.png "雲閃")

## 地理位置標題 {#geo-headers}

托AEM管的CDN將報頭添加到每個請求中：

* 國家/地區代碼： `x-aem-client-country`
* 大陸代碼： `x-aem-client-continent`

>[!NOTE]
>
>如果存在客戶管理的CDN，則這些報頭反映客戶CDN代理伺服器的位置，而不是實際的客戶端。 因此，對於客戶管理的CDN，地理位置報頭應該由客戶CDN管理。

國家代碼的值是說明的Alpha-2代碼 [這裡](https://en.wikipedia.org/wiki/ISO_3166-1)。

洲代碼的值為：

* 非洲足球會
* 南極洲
* 亞洲
* 歐盟
* 北美
* 大洋洲奧克會
* 南美

此資訊對於使用情況可能非常有用，例如根據請求的來源（國家）重定向到不同的url。 使用「變化」標頭快取取決於地理資訊的響應。 例如，重定向到特定國家/地區登錄頁時應始終包含 `Vary: x-aem-client-country`。 如果需要，您可以 `Cache-Control: private` 來阻止快取。 另請參閱 [快取](/help/implementing/dispatcher/caching.md#html-text)。
