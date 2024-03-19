---
title: 在CDN設定流量
description: 瞭解如何在設定檔案中宣告規則和篩選器，並使用Cloud Manager設定管道將它們部署到CDN，以設定CDN流量。
feature: Dispatcher
source-git-commit: 0a0c9aa68b192e8e2a612f50a58ba5f9057c862d
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 2%

---


# 在CDN設定流量 {#cdn-configuring-cloud}

>[!NOTE]
>此功能尚未正式推出。若要加入率先採用者計畫，請傳送電子郵件至 `aemcs-cdn-config-adopter@adobe.com` 並說明您的使用案例。

AEMas a Cloud Service提供可在以下位置設定的功能集合： [Adobe管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) 修改傳入要求或傳出回應之性質的圖層。 下列規則（在本頁中詳細說明）可宣告為達成下列行為：

* [要求轉換](#request-transformations)  — 修改傳入請求的各個方面，包括標題、路徑和引數。
* [回應轉換](#response-transformations)  — 修改回使用者端的標題（例如網頁瀏覽器）。
* [使用者端重新導向程式](#client-side-redirectors)  — 觸發瀏覽器重新導向。
* [來源選取器](#origin-selectors) - proxy到不同的來源後端。

CDN也可以設定流量篩選規則（包括WAF），這可控制CDN允許或拒絕的流量。 此功能已發行，您可以在 [包含WAF規則的流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) 頁面。

此外，如果CDN無法連絡其來源，您可以撰寫規則來參考自行託管的自訂錯誤頁面（然後呈現）。 如需詳細資訊，請參閱 [設定CDN錯誤頁面](/help/implementing/dispatcher/cdn-error-pages.md) 文章。

所有這些在原始檔控制的組態檔中宣告的規則，都是透過以下方式部署： [Cloud Manager的設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). 請注意，組態檔的累積大小不能超過100KB。

## 評估順序 {#order-of-evaluation}

在功能上，先前提到的各種功能會依下列順序評估：

![影像](/help/implementing/dispatcher/assets/order.png)

## 設定 {#initial-setup}

您必須先執行下列操作，才能在CDN設定流量：

* 首先，在Git專案的頂層資料夾中建立此資料夾和檔案結構：

```
config/
     cdn.yaml
```

* 其次， `cdn.yaml` 設定檔案應同時包含中繼資料和下列範例所述的規則。

## 要求轉換 {#request-transformations}

請求轉換規則可讓您修改傳入的請求。 規則支援根據各種相符條件（包括規則運算式）來設定、取消設定和變更路徑、查詢引數和標頭（包括Cookie）。 您也可以設定變數，以便稍後在評估序列中參照。

使用案例多種多樣，包括URL重寫以簡化應用程式或對映舊版URL。

如前所述，設定檔案有大小限制，因此具有較大需求的組織應在 `apache/dispatcher` 圖層。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:  
  experimental_requestTransformations:
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
 
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header
 
      - name: set-query-param-rule
        when:
          reqProperty: path
          equals: /set-query-param
        actions:
          - type: set
            queryParam: someParam
            value: someValue
 
      - name: unset-query-param-rule
        when:
          reqProperty: path
          equals: /unset-query-param
        actions:
          - type: unset
            queryParam: someParam
 
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
 
      - name: set-req-cookie-rule
        when:
          reqProperty: path
          equals: /set-req-cookie
        actions:
          - type: set
            reqCookie: someParam
            value: someValue
 
      - name: unset-req-cookie-rule
        when:
          reqProperty: path
          equals: /unset-req-cookie
        actions:
          - type: unset
            reqCookie: someParam
 
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some value
 
      - name: unset-variable-rule
        when:
          reqProperty: path
          equals: /unset-variable
        actions:
          - type: unset
            var: some_var_name
 
      - name: replace-segment
        when:
          reqProperty: path
          like: /replace-segment/*
        actions:
          - type: replace
            reqProperty: path
            match: /replace-segment/
            value: /segment-was-replaced/
 
      - name: replace-extension
        when:
          reqProperty: path
          like: /replace-extension/*.html
        actions:
          - type: replace
            reqProperty: path
            match: \.html
            value: ''
 
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
```

**動作**

下表說明可用的動作。

| 名稱 | 屬性 | 含義 |
|-----------|--------------------------|-------------|
| **設定** | reqHeader，值 | 將指定的標頭設定為給定的值。 |
|     | queryParam，值 | 將指定的查詢引數設定為指定值。 |
|     | reqCookie，值 | 將指定的Cookie設定為指定的值。 |
|     | 變數，值 | 將指定的變數設為指定值。 |
| **未設定** | reqHeader | 移除指定的標頭。 |
|         | queryParam | 移除指定的查詢引數。 |
|         | reqCookie | 移除指定的Cookie。 |
|         | 變數 | 移除指定的變數。 |
|         | queryParamMatch | 移除符合指定規則運算式的所有查詢引數。 |
| **replace** | reqProperty，符合，值 | 以新值取代部分請求屬性。 目前僅支援「path」屬性。 |

### 變數 {#variables}

您可以在請求轉換期間設定變數，稍後在評估序列中參考它們。 請參閱 [評估順序](#order-of-evaluation) 圖表以取得更多詳細資料。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:   
  experimental_requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value
 
  experimental_responseTransformations:
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

## 回應轉換 {#response-transformations}

回應轉換規則可讓您設定和取消設定CDN傳出回應的標頭。 另請參閱上述範例，以參考先前在請求轉換規則中設定的變數。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  experimental_responseTransformations:
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
 
      # Example: Multi-action on response header
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
```

**動作**

下表說明可用的動作。

| 名稱 | 屬性 | 含義 |
|-----------|--------------------------|-------------|
| **設定** | reqHeader，值 | 將指定的標頭設定為回應中的指定值。 |
| **未設定** | respHeader | 從回應中移除指定的標頭。 |

## 來源選取器 {#origin-selectors}

您可以利用AEM CDN將流量路由到不同的後端，包括非Adobe應用程式（可能依路徑或子網域為基礎）。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy-me* }
        action:
          type: selectOrigin
          originName: example-com
          # useCache: false
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
|-----------|--------------------------|-------------|
| **selectOrigin** | 來源名稱 | 其中一個已定義來源的名稱。 |
|     | useCache （選用，預設為true） | 標示是否將快取用於符合此規則的請求。 |

**來源**

與來源的連線僅限SSL且使用連線埠443。

| 屬性 | 含義 |
|------------------|--------------------------------------|
| **名稱** | 可由「action.originName」參考的名稱。 |
| **網域** | 用來連線至自訂後端的網域名稱。 它也用於SSL SNI和驗證。 |
| **ip** （選用，支援iv4和ipv6） | 若提供，可用來連線到後端而非「網域」。 仍會使用「網域」進行SSL SNI和驗證。 |
| **forwardHost** （選擇性，預設為false） | 若設為true，則會將使用者端請求的「Host」標頭傳送至後端，否則「domain」值將會傳送至「Host」標頭。 |
| **forwardCookie** （選擇性，預設為false） | 若設為true，則會將使用者端請求中的「Cookie」標頭傳遞至後端，否則會移除Cookie標頭。 |
| **forwardAuthorization** （選擇性，預設為false） | 如果設為true ，則會將使用者端請求中的&quot;Authorization&quot;標頭傳遞至後端，否則會移除Authorization標頭。 |
| **逾時** （選用，以秒為單位，預設為60） | CDN應等待後端伺服器傳遞HTTP回應本文第一個位元組的秒數。 此值也會用作後端伺服器的位元組逾時之間的值。 |

## 使用者端重新導向程式 {#client-side-redirectors}

對於301、302和類似的使用者端重新導向，您可以使用使用者端重新導向規則。 如果規則相符，CDN會以包含狀態代碼和訊息的狀態行回應（例如HTTP/1.1 301 Moved Permanently），以及位置標頭集。

允許使用固定值的絕對和相對位置。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_redirects:
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
