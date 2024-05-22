---
title: Edge Side包含
description: Adobe Managed CDN現在支援Edge Side Include (ESI)，這是邊緣層級動態網頁內容組合的標籤語言。
feature: Dispatcher
source-git-commit: 8f9173e45dd802ecced21531dfa161890e4a8af1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 1%

---

# Edge Side包含 {#edge-side-includes}

>[!NOTE]
>此功能尚未正式推出。若要加入率先採用者計畫，請傳送電子郵件至 `aemcs-cdn-config-adopter@adobe.com` 並說明您的使用案例。

內容傳送速度受益於積極快取頁面，透過設定快取標頭為高存留時間(TTL)值來達成。 當頁面包含需要經常重新整理或可能完全無法快取的動態內容時，這可能會很具挑戰性。 幸運的是，有些策略可以使用高TTL快取包含HTML的頁面，將較動態內容片段的擷取延遲到稍後，透過使用者端Javascript或CDN擷取。 後一種方法是稱為Edge Side Include (ESI)的標準，AEM發佈功能呈現的網站支援此標準。 此HTML包含ESI標籤，指示CDN將頁面的服務遞延給瀏覽器，直到其評估這些標籤為止，並從來源擷取其他較動態（較低TTL）的內容（如果TTL尚未過期，則稱為CDN快取）。

Edge Side Include的某些使用案例可能很有用：

* 顯示一般使用者的名稱或一般使用者特有的其他資訊。
* 顯示最近資訊的清單，例如新聞文章或股價。

## ESI語法 {#esi-syntax}

如果上層頁面，ESI語法如下 `/content/page.html` 包含程式碼片段 `content/snippets/mysnippet.html`.

```
<html>
  <head>
      <title>My Site</title>
  </head>
  <body>
    <div id="content">
      <esi:include src="/content/snippets/mysnippet.html" />
    </div>
  </body>
</html>
```

請參閱 [ESI規格](https://www.w3.org/TR/esi-lang/) 以取得詳細資訊。

### 考量事項 {#esi-syntax-considerations}

* 支援下列ESI標籤：包含、註解、移除。
* ESI標籤會依序在CDN中處理，而非同時處理，因此具有低TTL的頁面上的許多ESI標籤可能會為一般使用者的體驗增加延遲。
* ESI：包含處理的最大深度為5。
* ESI：包含處理片段的總數上限為256。


## Apache設定 {#esi-apache}

如果您的頁面具有ESI標籤，您應在Apache設定中宣告以下屬性：

```
<LocationMatch "/parent-pages/*content/page.html">
   # disable dispatcher compression
   SetEnv no-gzip 1
   # enable esi processing 
   Header set x-aem-esi "on"
   # enable edgeCDN compression
   Header set x-aem-compress "on"

   # typically the main page is cached at the CDN
   Header always set Cache-Control "max-age=300"
 </LocationMatch>


<LocationMatch "/content/snippets/mysnippet.html">
  SetEnv no-gzip 1

  # typically the included page is either set to a lower TTL than the parent page, or not cached at all, as these 2 commented declarations show, respectively:
  #Header always set Cache-Control "no-cache"
  #Header always set Cache-Control "max-age=50"
 </LocationMatch> 
```

設定的屬性有下列行為：

| 屬性 | 行為 |
|-----------|--------------------------|
| **no-gzip** | 如果設為1，HTML頁面會從Apache傳輸至未壓縮的CDN。 這是ESI的必要步驟，因為內容必須未壓縮地傳送至CDN，這樣CDN才能檢視及評估ESI標籤。<br/><br/>上層頁面和包含的程式碼片段都應將no-gzip設為1。<br/><br/>根據請求的，此設定會覆寫Apache原本可能使用的任何壓縮設定 `Accept-Encoding` 值。 |
| **x-aem-esi** | 如果設為「開啟」，CDN將會評估上層HTML頁面的ESI標籤。  預設不會設定標頭。 |
| **x-aem-compress** | 若設為「開啟」，CDN會將內容從CDN壓縮至瀏覽器。 由於從Apache傳輸上層頁面到CDN必須解壓縮，ESI才能運作(`no-gzip` 設為1)，這樣可以減少延遲。<br/><br/>若此標頭未設定，當CDN從未壓縮的來源擷取內容時，也會將內容未壓縮提供給使用者端。 因此，如果符合下列條件，則必須設定此標題 `no-gzip` 設為1 （ESI的必要專案），並且需要提供從CDN壓縮至瀏覽器的內容。 |

## Sling動態包含 {#esi-sdi}

雖然不需要， [Sling動態包含](https://sling.apache.org/documentation/bundles/dynamic-includes.html) (SDI)可用來產生在CDN上解譯的ESI片段。
