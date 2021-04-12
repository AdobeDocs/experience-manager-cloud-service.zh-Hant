---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
translation-type: tm+mt
source-git-commit: 753d023e1b2c5b76ed5c402c002046cc2c5c1de4
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 7%

---

# AEM as a Cloud Service 中的 CDN {#cdn}

因AEM為Cloud Service隨附內建CDN。 其主要用途，就是透過從瀏覽器附近的邊緣 CDN 節點傳遞可快取的內容，以便減少延遲的情形。它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

受管AEM理的CDN將滿足大部分客戶的效能與安全性需求。 對於發佈層，客戶可選擇從自己的CDN指向它，而他們需要管理CDN。 這將根據符合特定先決條件（包括但不限於與其CDN廠商舊有整合且難以放棄的客戶）而逐個允許。

## AEM受管理的CDN {#aem-managed-cdn}

請依照下列章節，使用Cloud Manager自助服務UI，使用現成可用的CDNAEM準備內容傳送：

1. [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

依預設，對於AEM受管理的CDN設定，所有公開流量都可以進入發佈服務，適用於製作和非製作（開發和舞台）環境。 如果您希望限制特定環境的發佈服務流量（例如，限制IP位址範圍的轉移），您可以透過Cloud Manager UI以自助方式進行。

請參閱[管理IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)以瞭解更多資訊。

>[!CAUTION]
>
>只有允許的IP要求才會由受管AEM理的CDN提供。 如果您將自己的CDN指向受AEM管理的CDN，請確定您的CDN的IP已包含在allowlist中。

## 客戶CDN指向AEM受管理的CDN {#point-to-point-CDN}

如果客戶必須使用其現有的CDN，則可以管理它並將它指向受AEM管理的CDN，前提是滿足以下條件：

* 客戶必須有現有的CDN，而且要取代的工作量很大。
* 客戶必須加以管理。
* 客戶必須能夠設定CDN以搭配使用AEM為Cloud Service-請參閱下列設定指示。
* 客戶必須有工程CDN專家隨時待命，以備相關問題出現時使用。
* 客戶必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 使用域名設定`X-Forwarded-Host`標頭。 例如：`X-Forwarded-Host: example.com`。
1. 使用原始網域(即AEMCDN的入口)設定主機標題。 例如：`Host: publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 將SNI報頭髮送到源。 與主機標題一樣， SNI標題必須是源域。
1. 設定`X-Edge-Key`或`X-AEM-Edge-Key`（如果您的CDN刪除`X-Edge-*`）。值應來自Adobe。
   * 這是必要的，以便AdobeCDN可驗證請求來源，並將`X-Forwarded-*`標題傳遞至應用程AEM式。 例如，`X-Forwarded-Host`用於確AEM定主機標題，`X-Forwarded-For`用於確定客戶機IP。 因此，它成為受信任呼叫者（即客戶管理的CDN）的責任，以確保`X-Forwarded-*`標題的正確性（請參閱下方的附註）。
   * 或者，當`X-Edge-Key`不存在時，可以封鎖對AdobeCDN入口的存取。 如果您需要直接存取AdobeCDN的入口（待封鎖），請通知Adobe。

在接受即時流量之前，您應向Adobe的客戶支援驗證端對端流量路由是否正常運作。

>[!NOTE]
>
>管理其CDN的客戶應確保傳送至CDN的標題的完整AEM性。 例如，建議客戶清除所有`X-Forwarded-*`標題，並將其設為已知和控制值。 例如，`X-Forwarded-For`應包含客戶端的IP地址，而`X-Forwarded-Host`應包含站點的主機。

雖然從客戶CDN到受管理CDN的跳數可能會很有效，但由於額外的跳數，可能會AEM造成小的效能點擊。

請注意，此客戶CDN設定支援發佈層，但不支援在作者層之前。

## 地理位置標題{#geo-headers}

受管AEM理的CDN會透過下列項目將標題新增至每個請求：

* 國家代碼：`x-aem-client-country`
* 大陸代碼：`x-aem-client-continent`

國家代碼的值是[此處](https://en.wikipedia.org/wiki/ISO_3166-1)所述的Alpha-2代碼。

大陸代碼的值為：

* AF非洲
* 南極洲
* AS Asia
* 歐盟
* 北美洲
* 大洋洲OC
* SA南美洲

這些資訊對於使用案例可能很有用，例如根據請求的來源（國家）重新導向至不同的URL。 請使用「變更」標題來快取依地理資訊的回應。 例如，重新導向至特定國家／地區著陸頁面時，應一律包含`Vary: x-aem-client-country`。 如有需要，您可以使用`Cache-Control: private`來防止快取。 另請參見[Caching](/help/implementing/dispatcher/caching.md#html-text)。
