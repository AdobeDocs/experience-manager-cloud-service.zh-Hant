---
title: AEM as a Cloud Service 中的 CDN
description: 瞭解如何使用AEM管理的CDN，以及如何將您自己的CDN指向AEM管理的CDN。
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
role: Admin
source-git-commit: 62af306bbf645c4d70d0f07f95aa90e4d53e20f8
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 10%

---


# AEM as a Cloud Service 中的 CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM as Cloud Service 會隨附內建的 CDN。其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。"

AEM as a Cloud Service隨附整合式CDN，旨在從接近使用者瀏覽器的邊緣節點提供可快取的內容，以降低延遲時間。 這個完全受管理的CDN已針對AEM應用程式效能最佳化。

AEM管理的CDN符合大部分客戶的效能與安全性需求。 對於發佈層級，客戶可以選擇透過他們自己的CDN路由流量，他們必須管理此CDN。 此選項依具體情況而定，尤其是當客戶與難以取代的CDN提供者已有舊版整合時。

想要發佈至Edge Delivery Services階層的客戶，可利用Adobe的受管理CDN。 檢視[Adobe Managed CDN](#aem-managed-cdn)。<!-- CQDOC-21758, 5b -->


<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## Adobe Managed CDN {#aem-managed-cdn}

<!-- CQDOC-21758, 5a -->

若要透過AEM的自助UI使用Cloud Manager的內建CDN準備內容傳送，您可以利用Adobe的受管理CDN功能。 此功能可讓您處理自助式CDN管理，包括設定和安裝SSL憑證，例如DV （網域驗證）或EV/OV （延伸/組織驗證）憑證。 如需這些方法的詳細資訊，請參閱下列內容：

* [Cloud Manager中的Edge Delivery Services](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)
* [自訂網域名稱簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
* [SSL 憑證簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)
* [設定CDN](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)

**限制流量**

根據預設，對於AEM管理的CDN設定，所有公用流量都可進入發佈服務，無論是生產環境還是非生產（開發和中繼）環境。 您可以透過Cloud Manager使用者介面限制特定環境的發佈服務流量（例如，依IP位址範圍限制分段）。

如需詳細資訊，請參閱[管理 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

>[!CAUTION]
>
>AEM的Managed CDN只會提供來自允許IP的請求。 如果您將自己的CDN指向AEM管理的CDN，則請確定CDN的IP包含在IP允許清單中。

### 在CDN設定流量 {#cdn-configuring-cloud}

您可以透過多種方式設定CDN的流量，包括：

* 使用[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)封鎖惡意流量(包括選擇性授權的高階WAF規則)
* 修改[要求與回應](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)的性質
* 套用301/302 [使用者端重新導向](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)
* 宣告[原始選取器](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)將要求反向Proxy至非AEM後端

使用Git中的YAML檔案來設定這些功能。 而且，請使用Cloud Manager [設定管道](/help/implementing/dispatcher/cdn-configuring-traffic.md)來部署它們。

### 設定CDN錯誤頁面 {#cdn-error-pages}

您可以設定CDN錯誤頁面來取代預設的非品牌頁面。 在極少數無法使用AEM的情況下，會顯示此自訂頁面。 如需詳細資訊，請參閱[設定CDN錯誤頁面](/help/implementing/dispatcher/cdn-error-pages.md)。

### 清除CDN上的快取內容 {#purge-cdn}

使用 HTTP Cache-Control 標頭設定 TTL 是平衡內容傳遞效能和內容新鮮度的有效方法。不過，在必須立即提供更新內容的情況下，直接清除CDN快取可能會有助益。

閱讀有關[設定清除API Token](/help/implementing/dispatcher/cdn-credentials-authentication.md/#purge-API-token)和[清除快取的CDN內容](/help/implementing/dispatcher/cdn-cache-purge.md)的資訊。

### CDN的基本驗證 {#basic-auth}

對於輕度驗證使用案例，包括商務利害關係人審查內容，顯示需要使用者名稱和密碼的基本驗證對話方塊以保護內容。 [了解更多](/help/implementing/dispatcher/cdn-credentials-authentication.md)。

## 客戶管理的內容傳遞網路會指向 AEM 管理的內容傳遞網路 {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客戶CDN （或Proxy）指向AEM Managed CDN"
>abstract="AEM as Cloud Service 為客戶提供了使用其現有 CDN 的選項。對於發佈層級，客戶可以選擇從他們自己必須管理的 CDN 指向它。依不同個案可允許此情況，以滿足特定先決條件為基礎，包括但不限於客戶和他們的 CDN 供應商有一個難以放棄的舊版整合。"

如果客戶必須使用其現有的CDN (或任何型別的反向Proxy，例如負載平衡器或WAF)，他們可以管理它並將其指向AEM管理的CDN，前提是滿足以下條件：

* 客戶必須擁有現有的CDN，且必須重新安裝CDN，如此將十分麻煩。
* 客戶必須管理它。
* 客戶必須能夠設定CDN以搭配AEM as a Cloud Service使用 — 請參閱下方呈現的設定指示。
* 客戶必須有隨時待命的工程CDN專家，以備出現相關問題時使用。
* 客戶在前往生產環境之前，必須先執行並成功通過負載測試。

設定指示：

1. 將您的CDN指向Adobe CDN的輸入作為其原始網域。 例如，`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 將SNI設為Adobe CDN的入口。
1. 將Host標頭設定為原始網域。 例如：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 使用網域名稱設定`X-Forwarded-Host`標頭，讓AEM可以判斷主機標頭。 例如：`X-Forwarded-Host:example.com`。
1. 設定`X-AEM-Edge-Key`。 應該使用Cloud Manager設定管道來設定值，如[本文章](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)所述。

   * 需要，以便Adobe CDN可以驗證要求的來源，並將`X-Forwarded-*`標頭傳遞至AEM應用程式。 例如，`X-Forwarded-For`是用來判斷使用者端IP。 因此，受信任的呼叫者（即客戶管理的CDN）有責任確保`X-Forwarded-*`標頭的正確性（請參閱以下附註）。
   * 您可以選擇是否在`X-AEM-Edge-Key`不存在時封鎖對Adobe CDN輸入端的存取。 如果您需要直接存取Adobe CDN的入口（將被封鎖），請通知Adobe。

請參閱[範例CDN廠商組態](#sample-configurations)一節，以取得主要CDN廠商的組態範例。

在接受即時流量之前，您應向Adobe的客戶支援驗證端對端流量路由是否正常運作。

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
>使用您自己的CDN時，您不需要在Cloud Manager中安裝網域和憑證。 Adobe CDN中的路由是使用預設網域`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`完成的，應該以要求`Host`標頭傳送。 使用自訂網域名稱覆寫請求`Host`標頭可能會透過Adobe CDN將請求錯誤路由或導致421錯誤。

>[!NOTE]
>
>管理自己CDN的客戶應確保傳送至AEM CDN的標頭的完整性。 例如，建議客戶清除所有`X-Forwarded-*`標頭，並將它們設定為已知和控制值。 例如，`X-Forwarded-For`應包含使用者端的IP位址，而`X-Forwarded-Host`應包含網站的主機。

>[!NOTE]
>
>沙箱計畫環境不支援客戶提供的CDN。

只有在發生快取遺失時，才需要客戶CDN和AEM CDN之間的額外躍點。 使用本文所述的快取最佳化策略，新增客戶CDN應該只會帶來可忽略的延遲。

發佈層級支援此客戶CDN設定，但製作層級前不支援。

### 偵錯設定

若要偵錯BYOCDN設定，請使用值為`edge=true`的`x-aem-debug`標頭。 例如：

在Linux®中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -v -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>" -H "x-aem-debug: edge=true"
```

在Windows中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -v --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>" --header "x-aem-debug: edge=true"
```

此程式反映`x-aem-debug`回應標頭中要求使用的特定屬性。 例如：

```
x-aem-debug: byocdn=true,edge=true,edge-auth=edge-auth,edge-key=edgeKey1,X-AEM-Edge-Key=set,host=publish-p87058-e257304-cmstg.adobeaemcloud.com,x-forwarded-host=wknd.site,adobe_unlocked_byocdn=true
```

此程式可驗證詳細資訊，例如主機值、邊緣驗證設定和x-forwarded-host標頭值。 它也會識別是否已設定邊緣金鑰，以及比對項存在時使用哪個金鑰。

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

### 常見錯誤 {#common-errors}

提供的設定範例顯示所需的基本設定。 但是，客戶設定可能有其他影響規則，這些規則會移除、編輯或重新排列AEM as a Cloud Service提供流量所需的標頭。 以下是在設定客戶管理的CDN以指向AEM as a Cloud Service時發生的常見錯誤。

**重新導向至發佈服務端點**

當請求收到403禁止的回應時，表示請求缺少某些必要的標頭。 發生此情況的常見原因是CDN同時管理Apex和`www`網域流量，但未為`www`網域新增正確的標頭。 可透過檢查您的AEM as a Cloud Service CDN記錄並驗證所需的請求標頭來測試此問題。

**錯誤421錯誤導向重新導向**

訊息為`Requested host does not match any Subject Alternative Names (SANs) on TLS certificate`的421錯誤指出HTTP `Host`不符合憑證上列出的任何主機。 此問題通常表示`Host`或SNI設定錯誤。 確定`Host`以及SNI設定都指向publish-p&lt;PROGRAM_ID>-e.adobeaemcloud.com主機。

**太多重新導向回圈**

當頁面收到「太多重新導向」回圈時，系統會在CDN新增一些要求標題，以符合強制傳回本身的重新導向。 例如：

* 建立CDN規則以比對Apex網域或www網域，並僅新增Apex網域的X-Forwarded-Host標頭。
* Apex網域的請求符合此CDN規則，這會將Apex網域新增為X-Forwarded-Host標頭。
* 要求會傳送到來源，其中重新導向明確符合Apex網域的主機標頭(例如^example.com)。
* 會觸發重寫規則，將Apex網域的請求重寫為包含www子網域的https。
* 該重新導向會傳送至客戶的邊緣，而重新觸發CDN規則時，會針對Apex網域（而非www子網域）重新新增X-Forwarded-Host標頭。 接著，程式會重新開始，直到要求失敗為止。

若要解決此問題，請評估您的SSL重新導向策略、CDN規則、重新導向及重寫規則組合。

## 地理位置標題 {#geo-headers}

AEM管理的CDN會透過以下方式將標頭新增至每個請求：

* 國家/地區代碼： `x-aem-client-country`
* 大陸代碼： `x-aem-client-continent`

>[!NOTE]
>
>如果有客戶管理的CDN，這些標題會反映客戶的CDN Proxy伺服器的位置，而非實際使用者端。 客戶使用客戶管理的CDN時，應透過自己的CDN管理地理位置標題。

國家/地區代碼的值是[ISO 3166-1](https://zh.wikipedia.org/wiki/tw/ISO_3166-1)中描述的Alpha-2代碼。

大陸代碼的值如下：

* AF非洲
* 南極洲
* 作為亞洲
* 歐盟歐洲
* NA北美洲
* OC大洋洲
* 南美洲南美洲

根據請求的來源國家/地區，此資訊對於重新導向至不同的URL非常有用。 根據地理資訊來快取回應時，請使用Vary標頭。 例如，重新導向至特定國家/地區的登陸頁面應一律包含`Vary: x-aem-client-country`。 如有需要，您可以使用`Cache-Control: private`來防止快取。 另請參閱[快取](/help/implementing/dispatcher/caching.md#html-text)。
