---
title: Dynamic Media中Open API的快取管理
description: Dynamic Media中Open API的快取管理
role: User
source-git-commit: 89f21f96a741acbd6458c3777227548fbc89e525
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Dynamic Media中Open API的快取管理 {#cache-management-dynamic-media-open-apis}

有效的快取管理對於提供高效能、可擴充且最新的數位資產至關重要。 在具有Open API的Dynamic Media中，快取管理會定義如何在傳遞管道的各個層級儲存、重新整理和傳遞內容。 資產傳送回應會在多個層級進行快取，以確保最佳效能和快速內容傳送。

使用Open API的Dynamic Media中長時間的快取包含[CDN層快取](#cdn-layer-caching)和[外部快取控制（BYOCDN和瀏覽器快取）](#byocdn-browser-caching)。

## CDN層快取 {#cdn-layer-caching}

資產傳遞回應會在[Adobe Managed CDN](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn#aem-managed-cdn)快取很長一段時間，以最大化效能並將原始端的負載降至最低。 此快取完全由Adobe管理，以確保為一般使用者提供一致的高品質體驗。 快取期間是特意針對效能最佳化，使用者無法加以自訂，以維持所有客戶的可靠性和有效內容傳遞。

所有傳送URL都會在邊緣(Fastly)快取很長一段時間，以確保最佳效能。 快取的傳送物件包括靜態轉譯、影片、原始影像二進位檔和動態轉換影像，例如透過URL引數產生的已調整大小或重新格式化的資產。<!--The CDN is designed to serve these assets directly from the cache without revalidating them, unless an explicit purge is performed.-->

## 外部快取控制（BYOCDN和瀏覽器快取） {#byocdn-browser-caching}

針對下游快取層，資產傳遞回應包含預設`Cache-Control`為`max-age`10分鐘&#x200B;**的**&#x200B;標頭。 這適用於自訂&#x200B;*自攜CDN (BYOCDN)設定*、*一般使用者瀏覽器*&#x200B;和任何&#x200B;*中繼快取代理*，以確保在整個傳遞路徑中擁有一致的快取控制。

### 自訂快取控制標題 {#customizing-cache-control-headers}

增加快取存留時間值超過預設設定，會增加提供過時內容的可能性，這可能會延遲一般使用者體驗中內容更新的可見度。 如果您需要修改特定使用案例的快取控制行為，可以設定自訂CDN規則以調整回應標頭。 這可讓您根據需求設定不同的快取持續時間。 請參閱回應標頭的[AEM自訂CDN規則](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic)。

```
responseTransformations:
    rules:
      - name: cache-asset-delivery
        when:
          allOf:
            - reqProperty: path
              like: '/adobe/assets/urn:aaid:aem:*'
            - reqProperty: tier
              equals: delivery
        actions:
          - type: set
            respHeader: Cache-Control
            value: max-age=300
```

如需有關快取管理的其他協助或問題，請連絡[Adobe支援](https://helpx.adobe.com/in/contact.html)。

## 使用中的快取失效 {#active-cache-invalidation}

每當更新、刪除或修改資產（任何中繼資料變更）時，具有Open API的Dynamic Media都會自動讓Adobe Managed CDN上的每個關聯傳送URL失效。 這適用於使用虛名ID或別名的URL，以及包含轉換引數（例如寬度、格式或品質）的任何URL。 此事件導向式失效可確保您的使用者一律會收到您資產的最新版本，無需手動干預。

### 手動清除快取 {#manual-cache-purging}

當需要手動清除快取內容時，您可以使用AEM的快取失效功能來清除。 有關如何清除特定快取URL的詳細說明，請參閱[AEM CDN快取失效](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-cache-purge#single-purge)。

## 常見問題{#faq-cache-management}

+++**快取管理如何影響現有的整合？**

資產URL保持不變，而從Adobe Managed CDN傳送至瀏覽器（和其他下游中介機構）的快取控制標題使用[`stale-while-revalidate directive`](https://web.dev/articles/stale-while-revalidate#whats_it_mean)繼續保持10分鐘不變，確保下游系統繼續以最佳方式運用其快取。

+++

+++**什麼會觸發快取清除？**

更新、修改、封存或刪除資產時，快取清除會自動觸發。

<!--The cache purge triggers automatically in the following circumstances:
 
 - when an asset is updated, modified, or archived.
 - when an asset reaches `ready_for_delivery` state after approval.-->

+++

<!--
+++ **How long does it take for the cache to refresh after updating an asset?**

Any time the asset changes, the cache refreshes usually in *less than 60 seconds*.

+++

<!--
+++ **What happens if the cache purge system fails?**
The following mechanisms can be followed:
 
 - **Automatic retries:** 3 retry attempts with exponential backoff
 - **Monitoring:** Sev-2 alert fires if staleness exceeds 10 minutes
 - **Natural expiry:** Even without purge, cache expires after 10 hours maximum
 - **Manual override:** Engineers can manually purge via CLI tool

+++
-->

+++ **長效快取支援哪些資產型別？**

具有事件導向作用中快取失效的持續快取適用於具有Open API的Dynamic Media中的所有資產型別，無論資產型別或格式為何。

+++

+++ **我可以選擇退出存放庫的長期快取嗎？**

您可以聯絡[Adobe支援](https://helpx.adobe.com/in/contact.html)，說明理由，Adobe將與您聯絡以進行討論。

+++


>[!MORELIKETHIS]
>
>- [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
>- [虛名URL](/help/assets/vanity-urls.md)
