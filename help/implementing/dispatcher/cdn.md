---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: cebeabc56ad3f55bae4ca5d51c7a630480b40577
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AEM as a Cloud Service 中的 CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="因AEM為Cloud Service隨內置CDN一起提供。 其主要目的是通過從位於邊緣的CDN節點處在瀏覽器附近提供可快取內容來減少延遲。 它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。"

因AEM為Cloud Service隨內置CDN一起提供。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

托管AEMCDN將滿足大多數客戶的效能和安全要求。 對於發佈層，客戶可以選擇從自己的CDN指向它，他們需要管理它。 這將基於滿足某些先決條件（包括但不限於與其CDN供應商進行舊式整合的客戶很難放棄）而按個例允許。

另外，請參閱以下視頻 [雲5 AEM CDN第1部分](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) 和 [雲5 AEM CDN第2部分](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) 有關as a Cloud Service中CDN的其AEM他資訊。

## 托AEM管CDN  {#aem-managed-cdn}

按照以下各節，使用Cloud Manager自助服務UI，通過使用現成CDNAEM準備內容交付：

1. [管理SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自定義域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制通信**

預設情況下，對AEM於托管CDN設定，所有公共通信都可以進入發佈服務，無論是生產環境還是非生產環境（開發和階段）。 如果希望將流量限制到給定環境的發佈服務（例如，按IP地址範圍限制轉移），可以通過Cloud Manager UI以自助方式執行此操作。

請參閱 [管理IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) 來瞭解更多資訊。

>[!CAUTION]
>
>只有允許的IP的請求才會由托管AEMCDN提供。 如果將您自己的CDN指AEM向托管CDN，則確保CDN的IP包含在允許清單中。

## 客戶CDN指向托AEM管CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客戶CDN指向托AEM管CDN"
>abstract="因AEM為Cloud Service為客戶提供了使用其現有CDN的選項。 對於發佈層，客戶可以選擇從自己的CDN指向它，他們需要管理它。 這將基於滿足某些先決條件（包括但不限於與其CDN供應商進行舊式整合的客戶很難放棄）而按個例允許。"

如果客戶必須使用其現有CDN，他們可以管理它並將其指向受AEM管CDN，但滿足以下條件：

* 客戶必須擁有一個需要更換的現有CDN。
* 客戶必須管理它。
* 客戶必須能夠配置CDN以使用AEMas a Cloud Service — 請參閱下面提供的配置說明。
* 客戶必須有工程CDN專家隨時待命，以防出現相關問題。
* 客戶必須執行並成功傳遞負載test，然後才能開始生產。

>[!NOTE]
>
>AdobeCDN不是可選的。 客戶自帶CDN必須將其指向托AEM管CDN。

配置說明：

1. 將您的CDN指向AdobeCDN的入口作為其源域。 比如說， `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 還必須將SNI設定為AdobeCDN的入口。
1. 將主機頭設定為源域。 例如： `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 設定 `X-Forwarded-Host` 包含域名的標頭，AEM以便確定主機標頭。 例如： `X-Forwarded-Host:example.com`。
1. 設定 `X-AEM-Edge-Key`. 值應來自Adobe。

   * 這是必需的，以便AdobeCDN可以驗證請求源並傳遞 `X-Forwarded-*` 到應用程式AEM的標題。 比如說，`X-Forwarded-For` 用於確定客戶端IP。 因此，它成為可信呼叫者（即客戶管理的CDN）的責任，以確保CDN的正確性 `X-Forwarded-*` 標題（請參閱下面的注釋）。
   * 可選地，當AdobeCDN的入口被阻止時 `X-AEM-Edge-Key` 不存在。 如果您需要直接訪問AdobeCDN的入口（要阻止），請通知Adobe。

在接受即時通信之前，您應該向Adobe的客戶支援驗證端到端通信路由是否正常運行。

獲取 `X-AEM-Edge-Key`，您可以test請求已正確路由，如下所示：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H 'X-Forwarded-Host: example.com' -H 'X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>'
```

請注意，使用您自己的CDN時，無需在雲管理器中安裝域和證書。 AdobeCDN中的路由將使用預設域完成 `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。

>[!NOTE]
>
>管理自己的CDN的客戶應確保發送到AEMCDN的報頭的完整性。 例如，建議客戶清除所有 `X-Forwarded-*` 並將其設定為已知值和受控值。 比如說， `X-Forwarded-For` 應包含客戶端的IP地址，而 `X-Forwarded-Host` 應包含站點的主機。

>[!NOTE]
>
>沙盒程式環境不支援客戶提供的CDN。

由於額外的躍點，可能會對效能造成很小的影響，儘管從客戶CDN到受管AEM理CDN的躍點可能會很高效。

請注意，發佈層支援此客戶CDN配置，但不在作者層前。

## 地理位置標題 {#geo-headers}

托AEM管CDN將報頭添加到每個請求，具有：

* 國家/地區代碼： `x-aem-client-country`
* 大陸代碼： `x-aem-client-continent`

國家代碼的值是說明的Alpha-2代碼 [這裡](https://en.wikipedia.org/wiki/ISO_3166-1)。

洲代碼的值為：

* 非洲足球會
* 南極洲
* 亞洲
* 歐盟
* 北美
* 大洋洲奧克會
* 南美

此資訊對於使用情況可能非常有用，例如根據請求的來源（國家）重定向到不同的url。 使用「變化」標頭快取與地理資訊相關的響應。 例如，重定向到特定國家/地區登錄頁時應始終包含 `Vary: x-aem-client-country`。 如果需要，您可以 `Cache-Control: private` 來阻止快取。 另請參閱 [快取](/help/implementing/dispatcher/caching.md#html-text)。
