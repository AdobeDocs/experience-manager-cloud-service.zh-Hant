---
title: 常見案例的CDN設定片段
description: 適用於Adobe管理的CDN和客戶管理的CDN設定的可供複製的YAML模式，包括邊緣驗證、重新導向、快取變化、流量整形和速率限制。
feature: Dispatcher
role: Admin
source-git-commit: ab43facbd4c34c92878e303acf2fef9cc127e28a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# 常見案例的CDN設定片段 {#cdn-configuration-snippets}

本文針對AEM as a Cloud Service收集實用的`cdn.yaml`模式。 將它們與[CDN流量規則](/help/implementing/dispatcher/cdn-configuring-traffic.md)、[客戶管理的CDN認證](/help/implementing/dispatcher/cdn-credentials-authentication.md)以及[包含WAF](/help/security/traffic-filter-rules-including-waf.md)的流量篩選規則的功能檔案搭配使用。 使用Cloud Manager [設定管道](/help/operations/config-pipeline.md)部署程式碼片段。

>[!NOTE]
>
>將主機名稱、路徑、IP範圍、金鑰和臨界值取代為符合您程式的值。 升級變更之前，請先在非生產環境中測試變更。

## 客戶管理的CDN {#customer-managed-cdn}

### 僅針對某些網域設定Edge金鑰驗證 {#edge-auth-selected-hosts}

問題：在[客戶管理的CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn)上，您必須對某些客戶主機名稱強制執行驗證，而其他可觸及發佈的主機名稱則應該保持可用而不需使用該標題（例如在轉出期間或當您的CDN後面只有一個品牌網域時）。

解決方案：只有當第一個來自`X-Forwarded-Host`的主機名稱等於您的目標主機名稱（例如`example.com`）時，才需要`X-AEM-Edge-Key`驗證。 規則會使用`forwardedDomain`要求屬性來執行該相符專案，並對您的邊緣驗證者執行`authenticate`動作。 取代程式的主機名稱、驗證器名稱和金鑰預留位置。

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: forwardedDomain, equals: "example.com" }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

### 設定非來自VPN IP之請求的Edge金鑰驗證 {#edge-auth-trusted-ips}

問題：設定BYOCDN的邊緣金鑰驗證，但僅允許針對VPN IP直接存取發佈網域

解決方案：只有當使用者端IP不在VPN IP清單中時，才需要X-AEM-Edge-Key驗證

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: clientIp, notIn: ["10.0.0.1", "11.0.0.0/24", "<other VPN IPs>"] }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

## 重新導向 {#redirects}

### 從APEX網域重新導向至www {#apex-to-www}

```yaml
kind: "CDN"
version: "1"
data:
 redirects:
   rules:
     - name: non-www-to-www-redirect
       when:
         reqProperty: domain
         doesNotMatch: '^www\.'
       action:
         type: redirect
         status: 301
         location:
           join:
             format: 'https://www.%s%s'
             args:
               - reqProperty: domain
               - reqProperty: url
```

### 修改快取索引鍵 {#cache-key}

CDN不會公開個別的「快取金鑰」欄位。 由於URL參與快取，您可以透過變更URL來分割快取專案，例如透過[請求轉換](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)新增查詢引數。

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: set-request-different-cache-curl
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqHeader: user-agent
              matches: curl
        actions:
          - type: set
            queryParam: cache
            value: 'curl'
```

### 重新導向至標準化路徑 {#trailing-slash}

當瀏覽器在發佈時要求尾端斜線（例如從`https://www.example.com/path/`到`https://www.example.com/path`）時，傳送永久重新導向。

```yaml
kind: "CDN"
version: "1"
data:
  redirects:
    rules:
      - name: remove-trailing-slash
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: www.example.com
            - reqProperty: originalPath
              matches: ^/(.+)/$
        action:
          type: redirect
          status: 301
          location:
            reqProperty: originalPath
            transform:
              - op: replace
                match: ^/(.+)/$
                replacement: https://www.example.com/\1
```

### 從JSON Cookie擷取資訊 {#json-cookie}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when: { reqProperty: tier, equals: publish }
        actions:
        - type: set
          reqHeader: x-mycookie-info
          value:
            reqCookie: mycookie
            transform: 
            - 'base64decode'
            - { op: 'replace', match: '"info":\s*"([^"]*)"', replacement: '\1'} 
```

## 跨來源設定 {#cross-origin}

### 從CDN處理OPTIONS請求 {#options-from-cdn}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when:
          allOf: 
            - { reqProperty: path, like: /mypathi*  }
            - { reqProperty: method, equals: "OPTIONS" }
            - { reqHeader: Origin, equals: "https://example.com" }
        actions:
          - type: respond
            status: 200
            reason: "OK"
            headers:
              content-type: 'text/plain'
              access-control-allow-origin: { reqHeader: Origin }
              access-control-allow-methods: "*"
              access-control-allow-headers: "*"
```

## 流量篩選器 {#traffic-filters}

### 速率限制ASN {#rate-limit-asn}

問題：每個IP的速率限制可能會遺漏分散式阻斷服務(DDoS)模式：每個位址都會維持在臨界值以下，所以合法和濫用的流量在IP層看起來都類似。

解決方案：依自治系統名稱(`clientAsName`)計算要求，讓限制器彙總共用相同網路名稱的主機。 程式碼片段會將`clientAsName`寫入每個要求的記錄檔屬性，然後套用比率限制至以該值分組的作者和發佈。 許多使用者可以共用一個ASN （例如大型ISP或公司VPN出口），因此請仔細調整限制並監控CDN記錄以找出誤報。

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: client_as_name
            value:
              reqProperty: clientAsName
  trafficFilters:
    rules:
    - name: limit-requests-client-as-name
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        count: all
        groupBy:
          - reqProperty: clientAsName
      action: block
```
