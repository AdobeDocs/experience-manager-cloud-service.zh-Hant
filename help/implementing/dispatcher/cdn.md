---
title: AEM as a Cloud Service 中的 CDN
description: 瞭解如何使用AEM管理的CDN以及如何將您自己的CDN指向AEM管理的CDN。
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
role: Admin
source-git-commit: 3a10a0b8c89581d97af1a3c69f1236382aa85db0
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 23%

---


# AEM as a Cloud Service 中的 CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM as Cloud Service 會隨附內建的 CDN。其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。"

AEM as Cloud Service 會隨附內建的 CDN。其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

AEM管理的CDN符合大部分客戶的效能與安全性需求。 對於發佈層級，客戶可以選擇從他們自己必須管理的 CDN 指向它。依不同個案可允許此情況，以滿足特定先決條件為基礎，包括但不限於客戶和他們的 CDN 供應商有一個難以放棄的舊版整合。

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## AEM管理的CDN  {#aem-managed-cdn}

請依照下列章節，使用Cloud Manager自助服務UI，使用AEM的現成可用CDN準備內容傳送：

1. [管理 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理客戶網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

根據預設，對於AEM管理的CDN設定，所有公用流量都可以在生產和非生產（開發和中繼）環境中前往發佈服務。 您可以透過Cloud Manager使用者介面限制特定環境的發佈服務流量（例如，依IP位址範圍限制分段）。

如需詳細資訊，請參閱[管理 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

>[!CAUTION]
>
>AEM受管理的CDN只會處理來自允許IP的請求。 如果您將自己的CDN指向AEM管理的CDN，則請確定CDN的IP包含在允許清單中。

### 設定 CDN 上的流量 {#cdn-configuring-cloud}

設定CDN流量和篩選器的規則可在設定檔案中宣告，並使用[Cloud Manager的設定管道部署至CDN。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)如需詳細資訊，請參閱[在CDN設定流量](/help/implementing/dispatcher/cdn-configuring-traffic.md)和[包含WAF規則的流量篩選器規則](/help/security/traffic-filter-rules-including-waf.md)。

### 設定CDN錯誤頁面 {#cdn-error-pages}

CDN錯誤頁面可設定為在罕見情況下無法連線到AEM時，覆寫提供給瀏覽器的預設無品牌頁面。 如需詳細資訊，請參閱[設定CDN錯誤頁面](/help/implementing/dispatcher/cdn-error-pages.md)。

## 客戶 CDN 會指向 AEM 管理的 CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客戶 CDN 會指向 AEM 管理的 CDN"
>abstract="AEM as Cloud Service 為客戶提供了使用其現有 CDN 的選項。對於發佈層級，客戶可以選擇從他們自己必須管理的 CDN 指向它。依不同個案可允許此情況，以滿足特定先決條件為基礎，包括但不限於客戶和他們的 CDN 供應商有一個難以放棄的舊版整合。"

如果客戶必須使用其現有的CDN，他們可以管理該CDN，並將其指向AEM管理的CDN，前提是滿足以下條件：

* 客戶必須擁有現有的CDN，且必須重新安裝CDN，如此將十分麻煩。
* 客戶必須管理該網站。
* 客戶必須能夠設定CDN以搭配AEM as a Cloud Service使用 — 請參閱下方呈現的設定指示。
* 客戶必須有隨時待命的工程CDN專家，以備出現相關問題時使用。
* 客戶在前往生產環境之前，必須先執行並成功通過負載測試。

設定指示：

1. 將您的CDN指向AdobeCDN的輸入作為其原始網域。 例如，`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 將SNI設為AdobeCDN的入口。
1. 將Host標頭設定為原始網域。 例如：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 使用網域名稱設定`X-Forwarded-Host`標頭，讓AEM可以判斷主機標頭。 例如：`X-Forwarded-Host:example.com`。
1. 設定`X-AEM-Edge-Key`。 應該使用Cloud Manager設定管線來設定值，如[本文章](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value)所述。

   * 需要，以便AdobeCDN可以驗證要求的來源，並將`X-Forwarded-*`標頭傳遞至AEM應用程式。 例如，`X-Forwarded-For`是用來判斷使用者端IP。 因此，受信任的呼叫者（即客戶管理的CDN）有責任確保`X-Forwarded-*`標頭的正確性（請參閱以下備註）。
   * 您可以選擇是否在`X-AEM-Edge-Key`不存在時封鎖對AdobeCDN輸入端的存取。 如果您需要直接存取AdobeCDN的入口（將被封鎖），請通知Adobe。

請參閱[範例CDN廠商組態](#sample-configurations)一節，以取得主要CDN廠商的組態範例。

在接受即時流量之前，您應該向Adobe的客戶支援驗證端對端流量路由是否正常運作。

設定`X-AEM-Edge-Key`後，您可以依照以下方式測試要求是否正確路由。

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
>使用您自己的CDN時，您不需要在Cloud Manager中安裝網域和憑證。 AdobeCDN中的路由是使用預設網域`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`完成的，該預設網域應在請求`Host`標頭中傳送。 以自訂網域名稱覆寫要求`Host`標頭可能會導致AdobeCDN不正確地路由要求。


>[!NOTE]
>
>管理自己CDN的客戶應確保傳送至AEM CDN的標頭的完整性。 例如，建議客戶清除所有`X-Forwarded-*`標頭，並將它們設定為已知和控制值。 例如，`X-Forwarded-For`應包含使用者端的IP位址，而`X-Forwarded-Host`應包含網站的主機。

>[!NOTE]
>
>沙箱計畫環境不支援客戶提供的CDN。

只有在發生快取遺失時，才需要客戶CDN和AEM CDN之間的額外躍點。 使用本文所述的快取最佳化策略，新增客戶CDN應該只會帶來可忽略的延遲。

發佈層級支援此客戶CDN設定，但製作層級前不支援。

### CDN廠商設定範例 {#sample-configurations}

以下提供數家領先CDN廠商的數個設定範例。

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

AEM管理的CDN會新增標頭至具有下列各項的每個要求：

* 國家/地區代碼： `x-aem-client-country`
* 大陸代碼： `x-aem-client-continent`

>[!NOTE]
>
>如果有客戶管理的CDN，這些標題會反映客戶CDN Proxy伺服器的位置，而非實際使用者端。 因此，對於客戶管理的CDN，地理位置標題應由客戶CDN管理。

國家/地區代碼的值是[此處](https://en.wikipedia.org/wiki/tw/ISO_3166-1)描述的Alpha-2代碼。

大陸代碼的值如下：

* AF非洲
* 南極洲
* 作為亞洲
* 歐盟歐洲
* NA北美洲
* OC大洋洲
* 南美洲南美洲

此資訊可能適合用於使用案例，例如根據請求來源（國家/地區）重新導向至不同的URL。 根據地理資訊來快取回應時，請使用Vary標頭。 例如，重新導向至特定國家/地區的登陸頁面應一律包含`Vary: x-aem-client-country`。 如有需要，您可以使用`Cache-Control: private`來防止快取。 另請參閱[快取](/help/implementing/dispatcher/caching.md#html-text)。
