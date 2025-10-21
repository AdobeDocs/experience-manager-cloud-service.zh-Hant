---
title: 設定 CDN 上的流量
description: 瞭解如何在設定檔案中宣告規則和篩選器，並使用Cloud Manager設定管道將它們部署到CDN，以設定CDN流量。
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: a8c313c3b1324e4195c2aeb70a5a56e4ef66fcf3
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---


# 設定 CDN 上的流量 {#cdn-configuring-cloud}

AEM as a Cloud Service提供可在[Adobe管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)層設定的功能集合，可修改傳入要求或傳出回應的性質。 下列規則（在本頁中詳細說明）可宣告為達成下列行為：

* [要求轉換](#request-transformations) — 修改傳入要求的方面，包括標頭、路徑和引數。
* [回應轉換](#response-transformations) — 修改回使用者端的標題（例如網頁瀏覽器）。
* [伺服器端重新導向](#server-side-redirectors) — 觸發瀏覽器重新導向。
* [來源選取器](#origin-selectors) — 代理至不同的來源後端。

在CDN也可以設定的是流量篩選規則(包括WAF)，其可控制CDN允許或拒絕的流量。 此功能已發行，您可以在[流量篩選器規則(包括WAF規則)](/help/security/traffic-filter-rules-including-waf.md)頁面中瞭解更多相關資訊。

此外，如果CDN無法連絡其來源，您可以撰寫規則來參考自行託管的自訂錯誤頁面（然後呈現）。 閱讀[設定CDN錯誤頁面](/help/implementing/dispatcher/cdn-error-pages.md)文章以進一步瞭解此專案。

所有這些在原始檔控制的設定檔案中宣告的規則，都是使用Cloud Manager [設定管道](/help/operations/config-pipeline.md)來部署。 請注意，設定檔案的累積大小（包括流量篩選規則）不得超過100KB。

## 評估順序 {#order-of-evaluation}

在功能上，先前提到的各種功能會依下列順序評估：

![評估順序](/help/implementing/dispatcher/assets/order.png)

## 設定 {#initial-setup}

您必須先執行下列操作，才能在CDN設定流量：

1. 建立名為`cdn.yaml`或類似的檔案，參考以下各節中的各種組態程式碼片段。

   所有程式碼片段都有這些通用屬性，在[設定管道](/help/operations/config-pipeline.md#common-syntax)中加以說明。 `kind`屬性值應該是&#x200B;*CDN*，且`version`屬性應該設定為&#x200B;*1*。

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   ```

1. 將檔案放置在名為&#x200B;*config*&#x200B;或類似名稱的頂層資料夾之下，如[設定管道](/help/operations/config-pipeline.md#folder-structure)所述。

1. 在Cloud Manager中建立設定管道，如[設定管道](/help/operations/config-pipeline.md#managing-in-cloud-manager)中所述。

1. 部署設定。

## 規則語法 {#configuration-syntax}

以下各節中的規則型別會共用相同語法。

規則由名稱、條件「when子句」和動作參考。

「when」子句會根據包括網域、路徑、查詢字串、標頭和Cookie在內的屬性，決定是否評估規則。 各規則型別的語法相同；如需詳細資訊，請參閱「流量篩選規則」文章中的[條件結構區段](/help/security/traffic-filter-rules-including-waf.md#condition-structure)。

動作節點的詳細資訊因規則型別而異，以下各節將概述這些詳細資訊。

在設定規則中，您可以參考定義為環境變數的密碼（請參閱[設定密碼](/help/implementing/dispatcher/cdn-credentials-authentication.md)）。

## 要求轉換 {#request-transformations}

請求轉換規則可讓您修改傳入的請求。 規則支援根據各種相符條件（包括規則運算式）來設定、取消設定和變更路徑、查詢引數和標頭（包括Cookie）。 您也可以設定變數，以便稍後在評估序列中參照。

使用案例多種多樣，包括URL重寫以簡化應用程式或對映舊版URL。

如前所述，組態檔有大小限制，因此需求較大的組織應在`apache/dispatcher`層定義規則。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  requestTransformations:
    removeMarketingParams: true
    rules:
      - name: set-header-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: some value
      - name: set-header-with-reqproperty-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: {reqProperty: path}
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header
      - name: unset-matching-query-params-rule
        when:
          reqProperty: path
          equals: /unset-matching-query-params
        actions:
          - type: unset
            queryParamMatch: ^removeMe_.*$
      - name: unset-all-query-params-except-exact-two-rule
        when:
          reqProperty: path
          equals: /unset-all-query-params-except-exact-two
        actions:
          - type: unset
            queryParamMatch: ^(?!leaveMe$|leaveMeToo$).*$
      - name: multi-action
        when:
          reqProperty: path
          like: /multi-action
        actions:
          - type: set
            reqHeader: x-header1
            value: body set by transformation rule
          - type: set
            reqHeader: x-header2
            value: '201'
      - name: replace-html
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: \.html$
            replacement: ""
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: forwarded_host
            value:
              reqHeader: x-forwarded-host
```

**動作**

下表說明可用的動作。

| 名稱 | 屬性 | 含義 |
|-----------|--------------------------|-------------|
| **設定** | reqProperty，值 | 設定指定的請求引數（只支援「path」屬性） |
|     | reqHeader，值 | 將指定的要求標頭設定為指定的值。 |
|     | queryParam，值 | 將指定的查詢引數設定為指定值。 |
|     | reqCookie，值 | 將指定的要求Cookie設定為指定的值。 |
|     | logProperty，值 | 將指定的CDN記錄屬性設定為指定的值。 |
|     | 變數，值 | 將指定的變數設為指定值。 |
| **取消設定** | reqProperty | 移除指定的請求引數（只支援「path」屬性） |
|     | reqHeader，值 | 移除指定的請求標頭。 |
|     | queryParam，值 | 移除指定的查詢引數。 |
|     | reqCookie，值 | 移除指定的Cookie。 |
|     | logProperty，值 | 移除指定的CDN記錄屬性。 |
|     | 變數 | 移除指定的變數。 |
|     | queryParamMatch | 移除符合指定規則運算式的所有查詢引數。 |
|     | queryParamDoesNotMatch | 移除不符合指定規則運算式的所有查詢引數。 |
| **轉換** | op:replace， （reqProperty或reqHeader、queryParam或reqCookie或var），符合，取代 | 以新值取代部分請求引數（僅支援「path」屬性）、請求標頭、查詢引數、Cookie或變數。 |
|              | op:tolower， （reqProperty或reqHeader、queryParam或reqCookie或var） | 將請求引數（僅支援「path」屬性）、請求標頭、查詢引數、Cookie或變數設定為小寫值。 |

取代動作支援擷取群組，如下所示：

```
      - name: extract-country-code-from-path
        when:
          reqProperty: path
          matches: ^/([a-zA-Z]{2})(/.*|$)
        actions:
          - type: set
            var: country-code
            value:
              reqProperty: path
          - type: transform
            var: country-code
            op: replace
            match: ^/([a-zA-Z]{2})(/.*|$)
            replacement: \1
      - name: replace-jpg-with-jpeg
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: (.*)(\.jpg)$
            replacement: "\1\.jpeg"
```

動作可以鏈結在一起。 例如：

```
actions:
    - type: transform
      reqProperty: path
      op: replace
      match: \.html$
      replacement: ""
    - type: transform
      reqProperty: path
      op: tolower
```

### 變數 {#variables}

您可以在請求轉換期間設定變數，稍後在評估序列中參考它們。 如需詳細資訊，請參閱[評估順序](#order-of-evaluation)圖表。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value

  responseTransformations:
    rules:
      - name: set-response-header-while-variable
        when:
          var: some_var_name
          equals: some_value
        actions:
          - type: set
            respHeader: x-some-header
            value: some header value
```

### 記錄屬性 {#logproperty}

您可以使用請求和回應轉換，在CDN記錄中新增您自己的記錄屬性。

設定範例：

```
requestTransformations:
  rules:
    - name: log-on-request
      when: "*"
      actions:
        - type: set
          logProperty: forwarded_host
          value:
            reqHeader: x-forwarded-host
responseTransformations:
  rules:
    - name: log-on-response
      when: '*'
      actions:
        - type: set
          logProperty: cache_control
          value:
            respHeader: cache-control
```

記錄範例：

```
{
"timestamp": "2025-03-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "",
"forwarded_host": "example.com",
"cache_control": "max-age=300"
}
```

## 回應轉換 {#response-transformations}

回應轉換規則可讓您設定和取消設定CDN傳出回應的標題、Cookie和狀態。 另請參閱上述範例，以參考先前在請求轉換規則中設定的變數。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  responseTransformations:
    rules:
      - name: set-response-header-rule
        when:
          reqProperty: path
          like: /set-response-header
        actions:
          - type: set
            value: value-set-by-resp-rule
            respHeader: x-resp-header
      - name: unset-response-header-rule
        when:
          reqProperty: path
          like: /unset-response-header
        actions:
          - type: unset
            respHeader: x-header1
      - name: multi-action-response-header-rule
        when:
          reqProperty: path
          like: /multi-action-response-header
        actions:
          - type: set
            respHeader: x-resp-header-1
            value: value-set-by-resp-rule-1
          - type: set
            respHeader: x-resp-header-2
            value: value-set-by-resp-rule-2
      - name: status-code-rule
        when:
          reqProperty: path
          like: status-code
        actions:
          - type: set
            respProperty: status
            value: '410'
      - name: set-response-cookie-with-attributes-as-object
        when: '*'
        actions:
          - type: set
            respCookie: first-name
            value: first-value
            attributes:
              expires: '2025-08-29T10:00:00'
              domain: example.com
              path: /some-path
              secure: true
              httpOnly: true
              extension: ANYTHING
      - name: unset-response-cookie
        when: '*'
        actions:
          - type: unset
            respCookie: third-name
```

**動作**

下表說明可用的動作。

| 名稱 | 屬性 | 含義 |
|-----------|--------------------------|-------------|
| **設定** | respProperty，值 | 設定回應屬性。 僅支援「status」屬性以設定狀態代碼。 |
|     | respHeader，值 | 將指定的回應標頭設定為給定的值。 |
|     | respCookie，屬性（到期、網域、路徑、安全、httpOnly、副檔名）、值 | 將具有特定屬性的指定請求Cookie設定為給定值。 |
|     | logProperty，值 | 將指定的CDN記錄屬性設定為指定的值。 |
|     | 變數，值 | 將指定的變數設為指定值。 |
| **取消設定** | respHeader | 從回應中移除指定的標頭。 |
|     | respCookie，值 | 移除指定的Cookie。 |
|     | logProperty，值 | 移除指定的CDN記錄屬性。 |
|     | 變數 | 移除指定的變數。 |

## 來源選取器 {#origin-selectors}

您可以運用AEM CDN將流量路由至不同的後端，包括非Adobe應用程式（可能依路徑或子網域為基礎）。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy* }
        action:
          type: selectOrigin
          originName: example-com
          # skipCache: true
          # headers:
          #   Authorization: ${{AUTH_TOKEN}}
    origins:
      - name: example-com
        domain: www.example.com
        # ip: '1.1.1.1'
        # forwardHost: true
        # forwardCookie: true
        # forwardAuthorization: true
        # timeout: 20
```

**動作**

可用動作如下表所述。

| 名稱 | 屬性 | 含義 |
|---------------------|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **selectOrigin** | 來源名稱 | 其中一個已定義來源的名稱。 |
|                     | skipCache （選用，預設為false） | 標示是否將快取用於符合此規則的請求。 預設會根據回應快取標題（例如Cache-Control或Expires）快取回應 |
|                     | 標頭（選擇性，預設為`{}`） | 包含其他HTTP標題的機碼值組，將於規則觸發時傳送至選取的後端。 鍵值與標頭名稱相對應，而值則與標頭值相對應 |
| **selectAemOrigin** | 來源名稱 | 其中一個預先定義AEM來源的名稱（支援的值： `static`）。 |
|                     | skipCache （選用，預設為false） | 標示是否將快取用於符合此規則的請求。 預設會根據回應快取標題（例如Cache-Control或Expires）快取回應 |
|                     | 標頭（選擇性，預設為`{}`） | 包含其他HTTP標題的機碼值組，將於規則觸發時傳送至選取的後端。 鍵值與標頭名稱相對應，而值則與標頭值相對應 |

**來源**

與來源的連線僅限SSL且使用連線埠443。

| 屬性 | 含義 |
|------------------|--------------------------------------|
| **名稱** | 可由「action.originName」參考的名稱。 |
| **網域** | 用來連線至自訂後端的網域名稱。 它也用於SSL SNI和驗證。 |
| **ip** （選擇性，支援的iv4和ipv6） | 若提供，可用來連線到後端而非「網域」。 仍會使用「網域」進行SSL SNI和驗證。 |
| **forwardHost** （選擇性，預設為false） | 若設為true，則會將使用者端請求的「Host」標頭傳送至後端，否則「domain」值將會傳送至「Host」標頭。 |
| **forwardCookie** （選擇性，預設為false） | 若設為true，則會將使用者端請求中的「Cookie」標頭傳遞至後端，否則會移除Cookie標頭。 |
| **forwardAuthorization** （選擇性，預設為false） | 如果設為true ，則會將使用者端請求中的&quot;Authorization&quot;標頭傳遞至後端，否則會移除Authorization標頭。 |
| **逾時** （選擇性，以秒為單位，預設為60） | CDN應等待後端伺服器傳遞HTTP回應本文第一個位元組的秒數。 此值也會用作後端伺服器的位元組逾時之間的值。 |

### 將自訂網域代理至AEM靜態層 {#proxy-custom-domain-static}

來源選取器可用來將AEM發佈流量路由到使用[前端管道](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)部署的AEM靜態內容。 使用案例包括在與頁面相同的網域(例如example.com/static)上或在明確不同的網域(例如static.example.com)上提供靜態資源。

以下是可實現此目標的原點選取器規則的範例：

```
kind: CDN
version: '1'
metadata:
  envTypes: ["dev"]
data:
  originSelectors:
    rules:
      - name: select-aem-static-origin
        when:
          reqProperty: domain
          equals: static.example.com
        action:
          type: selectAemOrigin
          originName: static
```

### 代理至Edge Delivery Services {#proxying-to-edge-delivery}

在某些情況下，來源選擇器應該用於透過AEM Publish將流量路由到AEM Edge Delivery Services：

* 部分內容是由AEM Publish管理的網域所傳送，而其他來自相同網域的內容是由Edge Delivery Services所傳送。
* Edge Delivery Services傳送的內容可受益於透過設定管道部署的規則，包括流量篩選器規則或請求/回應轉換。
* Edge Delivery設定管道可讓您定義如`trafficFilters`、`originSelectors`和`redirects`等規則，以設定Adobe管理的CDN設定。<!-- https://wiki.corp.adobe.com/pages/editpage.action?pageId=3610084282 -->

以下是可實現此目標的原點選取器規則的範例：

```
kind: CDN
version: '1'
metadata:
  envTypes: ["dev"]
data:
  originSelectors:
    rules:
      - name: select-edge-delivery-services-origin
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: <Production Host>
            - reqProperty: path
              matches: "^(/scripts/.*|/styles/.*|/fonts/.*|/blocks/.*|/icons/.*|.*/media_.*|/favicon.ico)"
        action:
          type: selectOrigin
          originName: aem-live
    origins:
      - name: aem-live
        domain: main--repo--owner.aem.live
```

>[!NOTE]
>
>因為已使用Adobe Managed CDN，請依照Edge Delivery Services **安裝程式推送失效檔案**，確定在[Managed](https://www.aem.live/docs/byo-dns#setup-push-invalidation)模式中設定推送失效。


## 伺服器端重新導向 {#server-side-redirectors}

對於301、302和類似的使用者端重新導向，您可以使用使用者端重新導向規則。 如果規則相符，CDN會以包含狀態代碼和訊息的狀態行回應（例如HTTP/1.1 301 Moved Permanently），以及位置標頭集。

允許使用固定值的絕對和相對位置。

請注意，設定檔案的累積大小（包括流量篩選規則）不得超過100KB。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  redirects:
    rules:
      - name: redirect-absolute
        when: { reqProperty: path, equals: "/page.html" }
        action:
          type: redirect
          status: 301
          location: https://example.com/page
      - name: redirect-relative
        when: { reqProperty: path, equals: "/anotherpage.html" }
        action:
          type: redirect
          location: /anotherpage
```

| 名稱 | 屬性 | 含義 |
|-----------|--------------------------|-------------|
| **重新導向** | 位置 | 「Location」標頭的值。 |
|     | 狀態（選擇性，預設為301） | 重新導向訊息中使用的HTTP狀態，預設為301，允許值為： 301、302、303、307、308。 |

重新導向的位置可以是字串常值(例如https://www.example.com/page)，或是由以下語法選擇性轉換的屬性（例如path）所產生：

```
redirects:
  rules:
    - name: country-code-redirect
      when: { reqProperty: path, like: "/" }
      action:
        type: redirect
        location:
          reqProperty: clientCountry
          transform:
            - op: replace
              match: '^(.*)$'
              replacement: 'https://www.example.com/\1/home'
            - op: tolower
    - name: www-redirect
      when: { reqProperty: domain, equals: "example.com" }
      action:
        type: redirect
        location:
          reqProperty: url
          transform:
            - op: replace
              match: '^/(.*)$'
              replacement: 'https://www.example.com/\1'
```
