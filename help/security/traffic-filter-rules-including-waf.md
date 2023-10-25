---
title: 包含WAF規則的流量篩選規則
description: 設定流量篩選規則，包括Web應用程式防火牆(WAF)規則
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 221f6df73fe660c6f8dbf79affdccdd081ad3906
workflow-type: tm+mt
source-wordcount: '4210'
ht-degree: 43%

---


# 包含WAF規則的流量篩選規則 {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>
>此功能尚未正式推出。若要加入正在進行的早期採用者計劃，請寄送電子郵件至 **aemcs-waf-adopter@adobe.com**，郵件內容包括貴組織的名稱以及您對該功能感興趣的原因。

流量篩選規則可以用來在CDN層封鎖或允許請求，這可能在以下情況下有用：

* 在新網站上線之前，限制內部公司流量存取特定網域
* 建立速率限制，以減少受體積DDoS攻擊的影響
* 防止已知為惡意的IP位址鎖定您的頁面

這些流量篩選規則中的部分規則可供所有AEMas a Cloud ServiceSites和Forms客戶使用。 他們主要在要求屬性和要求標題上操作，包括IP、主機名稱、路徑和使用者代理。

流量篩選規則的子類別需要增強式安全性授權或WAF-DDoS保護安全性授權。 這些強大的規則稱為WAF （Web應用程式防火牆）流量篩選規則（簡稱WAF規則），可存取 [WAF旗標](#waf-flags-list) 本文稍後會說明。 Sites和Forms客戶可聯絡其Adobe帳戶團隊，以取得關於授權此進階功能的詳細資訊。

流量篩選器規則可以透過Cloud Manager設定管道部署到生產（非沙箱）計畫中的開發、暫存和生產環境型別。 未來將提供RDE支援。

## 本文的組織方式 {#how-organized}

本文分為下列小節：

* **流量保護概觀：** 瞭解如何保護您免受惡意流量的侵擾。
* **設定規則的建議程式：** 閱讀保護網站的高階方法。
* **設定：** 瞭解如何設定、設定和部署流量篩選器規則，包括進階WAF規則。
* **規則語法：** 閱讀中有關流量篩選規則宣告方式的資訊 `cdn.yaml` 組態檔。 這包括所有Sites和Forms客戶可用的流量篩選規則，以及授權該功能的使用者的WAF規則子類別。
* **規則範例：** 請參閱宣告規則的範例，以幫助您順利上路。
* **費率限制規則：** 瞭解如何使用速率限制規則來保護您的網站免受高流量攻擊。
* **CDN記錄：** 檢視哪些宣告的規則和WAF標幟符合您的流量。
* **控制面板工具：** 分析您的CDN記錄檔，以提出新的流量篩選規則。
* **教學課程：** 關於功能的實用知識，包括如何使用儀表板工具來宣告正確的規則。
<!-- About the tutorial: sets the context for a linked tutorial, which gives you practical knowledge about the feature, including how to use dashboard tooling to declare the right rules. -->

## 流量保護概觀 {#traffic-protection-overview}

在目前的數位環境中，惡意流量是持續存在的威脅。 我們瞭解風險的嚴重性，並提供數種方法來保護客戶應用程式並在發生攻擊時減少攻擊。

在邊緣，AdobeManaged CDN會吸收網路層（第3層和第4層）的DDoS攻擊，包括泛洪和反射/放大攻擊。

根據預設，Adobe會採取措施來防止由於突發的意外高流量超過特定臨界值而導致效能降低。 萬一DDoS攻擊影響網站可用性，Adobe的作業團隊會收到警報，並採取步驟進行緩解。

客戶可透過在內容傳送流程的各個層級設定規則，採取主動措施來減少應用程式層級攻擊（第7層）。

例如，在Apache層，客戶可以設定 [dispatcher模組](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) 或 [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) 以限制對特定內容的存取。

正如本文所述，流量篩選規則可以使用Cloud Manager的配置管道部署到CDN。 除了流量請求型流量篩選規則（根據IP位址、路徑和標題等屬性）之外，客戶也可以授權功能強大的流量篩選規則子類別（稱為WAF規則）。

## 建議的程式 {#suggested-process}

以下是建議用於制定正確流量篩選規則的高階端對端流程：

1. 設定非生產及生產設定管道，如 [設定](#setup) 區段。
1. 已授權WAF流量篩選規則子類別的客戶應在Cloud Manager中啟用它們。
1. 閱讀並試用本教學課程，以具體瞭解如何使用流量篩選規則，包括WAF規則（如果已授權）。 本教學課程會逐步引導您部署規則至開發環境、模擬惡意流量、下載 [CDN記錄](#cdn-logs)，並在中分析它們 [儀表板工具](#dashboard-tooling).
1. 將建議的初始規則複製到 `cdn.yaml` 並將設定以記錄模式部署到生產環境。
1. 收集部分流量後，使用分析結果 [儀表板工具](#dashboard-tooling) 以檢視是否有任何相符專案。 尋找誤判，並進行任何必要的調整，最終在區塊模式中啟用預設規則。
1. 根據CDN記錄的分析新增自訂規則，先在開發環境中使用模擬流量進行測試，然後以記錄模式部署到中繼和生產環境，最後以封鎖模式。
1. 持續監控流量，隨著威脅環境的變化而變更規則。

## 設定 {#setup}

1. 首先，在Git中的專案最上層資料夾中建立下列資料夾和檔案結構：

   ```
   config/
        cdn.yaml
   ```

1. `cdn.yaml` 應包含中繼資料以及流量篩選規則和 WAF 規則的清單。

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
       # Block simple path
       - name: block-path
         when:
           allOf:
             - reqProperty: tier
               matches: "author|publish"
             - reqProperty: path
               equals: '/block/me'
         action: block
   ```

此 `kind` 引數應設為 `CDN` 而版本應設為結構描述版本，目前為 `1`. 請進一步參閱下方範例。


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. 若要設定 WAF 規則，必須在 Cloud Manager 中啟用 WAF (如下所述)，對於新的和現有的計劃案例都適用。請注意，必須為 WAF 購買單獨的授權。

   1. 若要在新程式上設定WAF，請核取 **WAF-DDOS保護** 核取方塊 **安全性** 標籤設定時機 [新增生產計畫。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. 若要在現有程式上設定WAF， [編輯您的程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) 並在 **安全性** 標籤取消核取或核取 **WAF-DDOS** 選項。

1. 對於RDE以外的環境型別，在Cloud Manager中建立目標部署設定管道。

   * [請參閱此檔案以瞭解生產管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [請參閱本檔案以瞭解非生產管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

若為 RDE，會使用命令列，但目前不支援 RDE。

## 流量篩選規則語法 {#rules-syntax}

您可以將 `traffic filter rules` 設定為符合 IPS、使用者代理、要求標頭、主機名稱、地理位置和 URL 等模式。

授權增強式安全性或WAF-DDoS保護安全性產品的客戶也可以設定特殊類別的流量篩選規則，稱為 `WAF traffic filter rules` 參照一或多個（簡稱WAF規則）的 [WAF旗標](#waf-flags-list).

以下是一組流量篩選規則的範例，其中也包括 WAF 規則。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

中的流量篩選器規則格式 `cdn.yaml` 檔案如下所述。 檢視部分 [其他範例](#examples) 在稍後的章節中，以及在其他章節中 [費率限制規則](#rate-limit-rules).


| **屬性** | **大部分流量篩選規則** | **WAF 流量篩選規則** | **類型** | **預設值** | **說明** |
|---|---|---|---|---|---|
| 名稱 | X | X | `string` | - | 規則名稱 (64 個字元的長度，只能包含英數字元和 -) |
| 時間 | X | X | `Condition` | - | 基本結構是：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[請參閱下面的條件結構語法，其中會說明 getter、述詞以及結合多個條件的方式。](#condition-structure) |
| 動作 | X | X | `Action` | 記錄 | log、allow、block、log 或 action 物件，預設為 log |
| rateLimit | X |   | `RateLimit` | 未定義 | 速率限制設定。若未定義，則停用速率限制。<br><br>以下會有一個單獨的章節說明 rateLimit 語法以及範例。 |

### 條件結構 {#condition-structure}

條件可以是一個簡單的條件，也可以是一個條件群組。

**簡單條件**

簡單條件由 getter 和述詞組成。

```
{ <getter>: <value>, <predicate>: <value> }
```

**群組條件**

條件群組由多個簡單和/或群組條件組成。

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **屬性** | **類型** | **含義** |
|---|---|---|
| **allOf** | `array[Condition]` | **和** 作業。如果所有列出的條件都傳回 true，則為 true |
| **anyOf** | `array[Condition]` | **或** 作業。如果任何列出的條件都傳回 true，則為 true |

**Getter**

| **屬性** | **類型** | **說明** |
|---|---|---|
| reqProperty | `string` | 要求屬性。<br><br>以下其中之一：`path`、`queryString`、`method`、`tier`、`domain`、`clientIp`、`clientCountry`<br><br>網域屬性是要求的主機標頭的小寫變換。對於字串比較很有用，因此不會因區分大小寫而錯過相符的情況。<br><br>`clientCountry` 會使用顯示在 [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) 的字母代碼 |
| reqHeader | `string` | 傳回具有指定名稱的要求標頭 |
| queryParam | `string` | 傳回具有指定名稱的查詢參數 |
| reqCookie | `string` | 傳回具有指定名稱的 Cookie |
| postParam | `string` | 從本文傳回具有指定名稱的引數。 只有當內文為內容型別時才有作用 `application/x-www-form-urlencoded` |

**述詞**

| **屬性** | **類型** | **含義** |
|---|---|---|
| **等於** | `string` | 如果 getter 結果等於所提供的值，則為 true |
| **doesNotEqual** | `string` | 如果 getter 結果不等於所提供的值，則為 true |
| **like** | `string` | 如果 getter 結果和所提供的模式相符，則為 true |
| **notLike** | `string` | 如果 getter 結果和所提供的模式不相符，則為 true |
| **matches** | `string` | 如果 getter 結果和所提供的 regex 相符，則為 true |
| **doesNotMatch** | `string` | 如果 getter 結果和所提供的 regex 不相符，則為 true |
| **in** | `array[string]` | 如果所提供的清單包含 getter 結果，則為 true |
| **notIn** | `array[string]` | 如果所提供的清單不包含 getter 結果，則為 true |
| **存在** | `boolean` | 若設為true且屬性存在或設為false且屬性不存在時為true |

### 動作結構 {#action-structure}

由 `action` 欄位指定，可以是字串，此字串會指定動作類型 (允許、封鎖、記錄) 並假設所有其他選項使用預設值，也可以是物件，在其中規則類型是透過 `type` 必要欄位所定義以及適用該類型的其他選項。

**動作類型**

動作根據下表中的類型排定優先順序，以反映動作的執行順序：

| **名稱** | **允許的屬性** | **含義** |
|---|---|---|
| **允許** | `wafFlags` (可選) | 如果沒有 wafFlags，則停止進一步處理規則並繼續提供回應。如果有 wafFlags，它將停用指定的 WAF 保護並繼續進一步處理規則。 |
| **封鎖** | `status, wafFlags` (可選且互斥) | 如果沒有 wafFlags，則繞過所有其他屬性傳回 HTTP 錯誤，錯誤代碼由狀態屬性定義或預設為 406。如果有 wafFlags，它將啟用指定的 WAF 保護並繼續進一步處理規則。 |
| **記錄** | `wafFlags` (可選) | 記錄規則已觸發的事實，否則不影響處理作業。wafFlags 沒有影響 |

### WAF 標幟清單 {#waf-flags-list}

此 `wafFlags` 屬性可用於可授權的WAF流量篩選規則，可參考下列內容：

| **標幟 ID** | **標幟名稱** | **說明** |
|---|---|---|
| SQLI | SQL 注入 | SQL 注入指試圖透過執行任意資料庫查詢以取得對應用程式的存取權或獲取特權資訊。 |
| BACKDOOR | 後門 | 後門訊號指試圖決定系統是否存在常見後門檔案的要求。 |
| CMDEXE | 命令執行 | 命令執行指試圖透過由使用者輸入的任意系統命令獲取控制或毀損目標系統。 |
| XSS | 跨網站指令碼 | 跨網站指令碼指試圖透過惡意 JavaScript 程式碼劫持使用者的帳戶或 Web 瀏覽工作階段。 |
| 周遊 | 目錄周遊 | 目錄周遊指試圖瀏覽整個系統中的特權檔案，期望能獲取敏感資訊。 |
| USERAGENT | 攻擊工具 | 攻擊工具指使用自動化軟體識別安全漏洞或試圖惡意探索發現的漏洞。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻擊會試圖惡意探索出現在 2.16.0 之前的 Log4J 版本中的 [Log4Shell 漏洞](https://en.wikipedia.org/wiki/Log4Shell) |
| BHH | 錯誤跳躍標頭 | 錯誤跳躍標頭指透過格式錯誤的傳輸編碼 (TE) 或內容長度 (CL) 標頭或格式正確的 TE 和 CL 標頭進行的 HTTP 走私嘗試 |
| ABNORMALPATH | 異常路徑 | 異常路徑指原始路徑和標準化路徑不同 (例如：`/foo/./bar` 會標準化為 `/foo/bar`) |
| DOUBLEENCODING | 雙重編碼 | 雙重編碼會檢查雙重編碼 html 字元的規避技術 |
| NOTUTF8 | 無效的編碼 | 無效的編碼可能會導致伺服器將要求中的惡意字元翻譯為回應，進而導致拒絕服務或 XSS |
| JSON-ERROR | JSON 編碼錯誤 | 指定為在「Content-Type」要求標頭中包含 JSON 但包含 JSON 剖析錯誤的 POST、PUT 或 PATCH 要求內文。這經常和程式設計錯誤或自動化亦或惡意要求有關。 |
| MALFORMED-DATA | 要求內文中格式錯誤的資料 | 根據「Content-Type」要求標頭，格式錯誤的 POST、PUT 或 PATCH 要求內文。例如，如果指定了「Content-Type: application/x-www-form-urlencoded」要求標頭並包含 json 的 POST 內文。這經常是程式設計錯誤、自動化或惡意要求。需要代理程式 3.2 或更高版本。 |
| SANS | 惡意的 IP 流量 | 已被報告為參與了惡意活動的 [SANS 網際網路風暴中心](https://isc.sans.edu/) IP 位址清單 |
| SIGSCI-IP | 網路效應 | 由 SignalSciences 標記的 IP：每當決策引擎因惡意訊號而標記 IP 時，即會將 IP 傳播給所有客戶。接著會記錄來自這些 IP 位址的後續要求 (其中會包含標幟持續時間中的任何其他訊號)。 |
| NO-CONTENT-TYPE | 缺少「Content-Type」要求標頭 | 沒有「Content-Type」要求標頭的 POST、PUT 或 PATCH 要求。在此案例中，預設情況下應用程式伺服器應假設「Content-Type: text/plain; charset=us-ascii」。許多自動化和惡意要求可能會缺少「內容類型」。 |
| NOUA | 沒有使用者代理程式 | 許多自動化和惡意要求會使用偽造的使用者代理程式或缺少使用者代理程式，這使得難以識別發出要求的裝置類型。 |
| TORNODE | Tor 流量 | Tor 是可隱藏使用者身份的軟體。Tor 流量激增可能表示有攻擊者試圖掩飾其位置。 |
| NULLBYTE | 空位元 | 空位元通常不會出現在要求中，因為這表示該要求的格式錯誤且可能是惡意的。 |
| PRIVATEFILE | 私人檔案 | 私人檔案通常在本質上屬於機密性，例如 Apache `.htaccess` 檔案或可能洩漏敏感資訊的設定檔案 |
| SCANNER | 掃描程式 | 可識別熱門的掃描服務和工具 |
| RESPONSESPLIT | HTTP 回應拆分 | 會識別何時將 CRLF 字元作為輸入提交給應用程式，以將標頭注入 HTTP 回應 |
| XML-ERROR | XML 編碼錯誤 | 指定為在「Content-Type」要求標頭中包含 XML 但包含 XML 剖析錯誤的 POST、PUT 或 PATCH 要求內文。這經常和程式設計錯誤或自動化亦或惡意要求有關。 |

## 考量事項 {#considerations}

* 建立兩個衝突規則時，允許規則總是優先於封鎖規則。例如，如果您建立一條封鎖特定路徑的規則，又建立一條允許特定 IP 位址的規則，則來自遭封鎖路徑上的該 IP 位址的要求會受到允許。

* 如果規則相符並遭封鎖，CDN 會以 `406` 傳回代碼回應。

* 設定檔不應包含密碼，因為任何有權存取 git 存放庫的人都可以讀取。

## 規則範例 {#examples}

下面是一些規則範例。請參閱 [速率限制區段](#rules-with-rate-limits) 向下展開以取得費率限制規則的範例。

**範例 1**

此規則會封鎖來自 IP 192.168.1.1 的要求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**範例 2**

此規則會使用包含 Chrome 的使用者代理程式封鎖發佈的路徑 `/helloworld` 上的要求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
        when:
          allOf:
          - { reqProperty: path, equals: /helloworld }
          - { reqProperty: tier, equals: publish }
          - { reqHeader: user-agent, matches: '.*Chrome.*'  }
        action:
          type: block
```

**範例 3**

此規則會封鎖包含查詢參數 `foo` 的要求，但會允許來自 IP 192.168.1.1 的每個要求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when: { queryParam: url-param, equals: foo }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**範例 4**

此規則會封鎖路徑請求 `/block-me`，並封鎖符合「 」的每個請求 `SQLI` 或 `XSS` 模式。 此範例包含WAF流量篩選規則，此規則會參考 `SQLI` 和 `XSS` [WAF旗標](#waf-flags-list)，則需要個別的授權。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**範例 5**

此規則會封鎖對 OFAC 國家的存取：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: block-ofac-countries
        when:
          allOf:
            - reqProperty: tier
              matches: "author|publish"
            - reqProperty: clientCountry
              in:
                - SY
                - BY
                - MM
                - KP
                - IQ
                - CD
                - SD
                - IR
                - LR
                - ZW
                - CU
                - CI
        action: block
```

## 費率限制規則 {#rate-limits-rules}

若相符程度經過一段時間後超過特定速率，則有時也需要只封鎖和某種規則相符的流量。設定 `rateLimit` 屬性的值會限制那些和規則條件相符的要求的速率。

速率限制規則不能參考WAF旗標。 所有Sites和Forms客戶皆可使用。

### rateLimit 結構 {#ratelimit-structure}

| **屬性** | **類型** | **預設** | **含義** |
|---|---|---|---|
| 限制 | 10 到 10000 之間的整數 | 必要 | 每秒觸發規則之要求的要求速率（每CDN POP）。 |
| 視窗 | 整數列舉：1、10 或 60 | 10 | 計算要求速率的取樣期間 (秒數). |
| 懲罰 | 60 到 3600 之間的整數 | 300 (5 分鐘) | 封鎖相符要求時間的秒數 (四捨五入到最接近的分鐘). |
| groupBy | array[Getter] | 無 | 速率限制器計數器將由一組要求屬性 (例如 clientIp) 彙總。 |

### 範例 {#ratelimiting-examples}

**範例 1**

在過去60秒內，若使用者端超過每秒100個要求（每個CDN POP），此規則會封鎖5百萬使用者端：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**範例 2**

封鎖路徑/critical/resource上在過去60秒內超過每秒100個要求（每個CDN POP）時的60個要求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when: { reqProperty: path, equals: /critical/resource }
        action:
          type: block
        rateLimit: { limit: 100, window: 60, penalty: 60 }
```

## CDN 記錄 {#cdn-logs}

AEM as a Cloud Service 會提供對 CDN 記錄的存取權，這對於包括快取命中率最佳化以及設定 CDN 和 WAF 規則等使用案例都非常有幫助。選取作者或發佈服務時，CDN 記錄會顯示在 Cloud Manager **下載記錄**&#x200B;對話框中。

請注意，CDN記錄可能會延遲最多5分鐘。

此 `rules` 屬性會說明哪些流量篩選器規則符合，其模式如下：

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例如：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

這些規則的行為方式如下：

* 任何相符規則的客戶宣告規則名稱將列在matches屬性中。
* action屬性詳細說明規則是否具有封鎖、允許或記錄的效果。
* 如果授權並啟用WAF，則waf屬性將列出偵測到的任何waf規則（例如SQLI；請注意，這與客戶宣告的名稱無關），無論組態中是否列出了waf規則。
* 如果沒有客戶宣告的規則符合且沒有waf規則符合，規則屬性屬性將為空白。

一般而言，相符的規則會顯示在對 CDN 發出的所有要求的記錄條目中，無論是 CDN 命中、通過還是未命中。但是，會顯示 WAF 規則的記錄條目僅限於發送給被視為 CDN 未命中或通過但不被視為 CDN 命中的 CDN 要求。

以下範例顯示一個範例 `cdn.yaml` 和兩個CDN記錄專案：


```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS ]
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/block-me",
"method": "GET",
"res_ctype": "",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=path-rule,action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

### 記錄格式 {#cdn-log-format}

以下是 CDN 記錄中使用的欄位名稱清單以及簡要說明。

| **欄位名稱** | **說明** |
|---|---|
| *timestamp* | TLS 終止後要求開始的時間. |
| *ttfb* | *首位元組時間 (Time To First Byte)* 的縮寫。發出要求開始到回應內文開始串流的時間之間的時間間隔。 |
| *cli_ip* | 用戶端 IP 位址。 |
| *cli_country* | 雙字母 [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) 用戶端國家/地區的 alpha-2 國家/地區代碼。 |
| *rid* | 用於唯一識別要求的要求標頭的值。 |
| *req_ua* | 負責發出特定 HTTP 要求的使用者代理程式。 |
| *主機* | 發送要求的目標機構。 |
| *url* | 包括查詢參數的完整路徑。 |
| *方法* | 用戶端傳送的 HTTP 方法，例如「GET」或「POST」。 |
| *res_ctype* | 此內容類型用於指明資源的原始媒體類型。 |
| *cache* | 快取的狀態。可能的值包括 HIT、MISS 或 PASS |
| *狀態* | 作為整數值的 HTTP 狀態代碼。 |
| *res_age* | 回應已經 (在所有的節點) 快取的時間量 (以秒為單位)。 |
| *pop* | CDN 快取伺服器的資料中心。 |
| *rules* | 任何符合的規則其名稱。<br><br>還會指出該相符程度是否導致封鎖。<br><br>例如，「`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`」<br><br>如果沒有相符的規則，則為空白。 |

## 控制面板工具 {#dashboard-tooling}

Adobe提供一種機制，可將控制面板工具下載到您的電腦上，以擷取透過Cloud Manager下載的CDN記錄。 透過此工具，您可以分析流量以協助建立適當的流量篩選規則來宣告，包括WAF規則。

控制面板工具可直接從 [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Github存放庫。

[請參閱教學課程](#tutorial) 以取得如何使用儀表板工具的具體指示。

## 教學課程 {#tutorial}

Adobe提供一種機制，可將控制面板工具下載到您的電腦上，以擷取透過Cloud Manager下載的CDN記錄。 透過此工具，您可以分析流量以協助建立適當的流量篩選規則來宣告，包括WAF規則。 本節首先會提供一些熟悉開發環境中儀表板工具的指示，然後是有關如何利用該知識在生產環境中建立規則的指南。

控制面板工具可直接從 [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) GitHub存放庫。


### 熟悉儀表板工具 {#dashboard-getting-familiar}

1. 建立與開發環境關聯的Cloud Manager非生產設定管道。 首先選取 **部署管道** 選項。 然後選取 **目標部署**，設定、您的存放庫、 Git分支，並將程式碼位置設為/config。

   ![新增非生產管道選取部署](/help/security/assets/waf-select-pipeline1.png)

   ![新增非生產管道選取目標](/help/security/assets/waf-select-pipeline2.png)

[如需有關設定非生產管道的詳細資訊，請參閱此檔案。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. 在您的工作區中，建立根層級的資料夾設定並新增名為的檔案 `cdn.yaml`，您可在此宣告簡單規則，並以記錄模式設定，而非以封鎖模式設定。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: log
```

1. 提交並推送您的變更，並使用設定管道部署您的設定。

   ![執行設定管道](/help/security/assets/waf-run-pipeline.png)

1. 在部署您的設定後，嘗試存取 `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` 使用您的網頁瀏覽器或搭配以下的curl指令。 系統應顯示404錯誤頁面，因為該頁面不存在。

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. 從Cloud Manager下載CDN記錄並驗證規則是否如預期相符，且具有符合規則名稱的規則屬性：

   ```
   "rules": "match=log-rule-example"
   ```

   ![選取下載記錄](/help/security/assets/waf-download-logs1.png)

   ![下載記錄檔](/help/security/assets/waf-download-logs2.png)

1. 使用儀表板工具載入Docker影像，並按照README擷取CDN記錄。 如下列熒幕擷取畫面所示，選取正確的時段、正確的環境和正確的篩選器。

   ![從儀表板選取時間](/help/security/assets/dashboard-select-time.png)

   ![從儀表板選取環境](/help/security/assets/dashboard-select-env.png)

1. 套用正確的篩選器後，您應該就能看到儀表板載入預期的資料。 在下方熒幕擷圖中，規則記錄規則範例在過去2小時內已由Ireland的同一IP使用網頁瀏覽器和curl觸發3次。

   ![檢視開發儀表板資料](/help/security/assets/dashboard-see-data-logmode.png)
   ![檢視開發儀表板資料Widget](/help/security/assets/dashboard-see-data-logmode2.png)

1. 現在變更cdn.yaml以將規則置於封鎖模式，以確保頁面如預期般遭到封鎖。 然後像之前一樣認可、推送並觸發設定管道。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: block
```

1. 在部署您的設定後，嘗試存取 `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` 使用您的網頁瀏覽器或搭配以下的curl指令。 系統應該會顯示406錯誤頁面，指出已封鎖要求。

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. 請再次在Cloud Manager中下載您的CDN記錄檔（注意：新請求可能需要5分鐘的時間才會公開在您的CDN記錄檔中），然後像先前一樣在儀表板工具中匯入這些請求。 完成後，請重新整理您的儀表板。 如底下熒幕擷圖所示，請求 `/log/me` 已被我們的規則封鎖。

   ![檢視生產儀表板資料](/help/security/assets/dashboard-see-data-blockmode.png)
   ![檢視生產儀表板資料](/help/security/assets/dashboard-see-data-blockmode2.png)

1. 如果您已啟用WAF流量篩選器（此功能為GA後，這將需要額外的授權），請在記錄模式下以WAF流量篩選器規則重複此動作，然後部署規則。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: log-waf-flags
        when:
          reqProperty: tier
          matches: "author|publish"
        action:
          type: log
          wafFlags:
              - SANS
              - SIGSCI-IP
              - TORNODE
              - NOUA
              - SCANNER
              - USERAGENT
              - PRIVATEFILE
              - ABNORMALPATH
              - TRAVERSAL
              - NULLBYTE
              - BACKDOOR
              - LOG4J-JNDI
              - SQLI
              - XSS
              - CODEINJECTION
              - CMDEXE
              - NO-CONTENT-TYPE
              - UTF8
```

1. 使用工具，例如 [nikto](https://github.com/sullo/nikto/tree/master) 以產生相符請求。 以下命令會在1分鐘內傳送約550個惡意請求。

   ```
   ./nikto.pl -useragent "MyAgent (Demo/1.0)" -D V -Tuning 9 -ssl -h https://publish-pXXXXX-eYYYYY.adobeaemcloud.com
   ```

1. 從Cloud Manager下載CDN記錄（請記住，這些記錄最多可能需要5分鐘才會顯示）並驗證是否同時顯示相符的已宣告規則和WAF標幟。

   如您所見，WAF已將Nikto產生的數個請求標籤為惡意請求。 我們可以看到Nikto嘗試利用CMDEXE、SQLI和NULLBYTE漏洞。 如果您現在將動作從記錄變更為封鎖，並使用Nikto重新觸發掃描，則先前已標幟的所有要求這次都會遭到封鎖。

   ![檢視WAF資料](/help/security/assets/dashboard-see-data-waf.png)


   請注意，只要要求符合任何WAF標幟，這些WAF標幟就會出現，即使它們不是已宣告規則的一部分亦然；如此一來，您就始終會知道潛在的新惡意流量，因為您尚未宣告符合的規則。 例如：

   ```
   "rules": "match=log-waf-flags,waf=SQLI,action=blocked"
   ```

1. 在記錄模式下，使用使用速率限制的規則重複此步驟。 一如既往，認可、推送並觸發設定管道以套用您的設定。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: limit-requests-client-ip
        when:
          reqProperty: tier
          matches: "author|publish"
        rateLimit:
          limit: 10
          window: 1
          penalty: 60
          groupBy:
            - reqProperty: clientIp
        action: log
```

1. 使用工具，例如 [韋蓋塔](https://github.com/tsenart/vegeta) 以產生流量。

   ```
   echo "GET https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com" | vegeta attack -duration=5s | tee results.bin | vegeta report
   ```

1. 執行工具後，您可以下載CDN記錄並在控制面板中擷取記錄，以確認已觸發速率限制器規則

   ![檢視WAF資料](/help/security/assets/waf-dashboard-ratelimiter-1.png)

   ![檢視WAF資料](/help/security/assets/waf-dashboard-ratelimiter-2.png)

   如您所見，規則 **limit-requests-client-ip** 已觸發。

   現在您已熟悉流量篩選規則的運作方式，您可以移至生產環境。

### 將規則部署至生產環境 {#dashboard-prod-env}

請務必先在記錄模式中宣告規則，以驗證沒有誤判，這表示會錯誤封鎖的合法流量。

1. 建立與您的生產環境相關聯的生產設定管道。

1. 將下列建議的規則複製到您的cdn.yaml。 您可能希望根據網站即時流量的獨特特性來修改規則。 認可、推播並觸發您的設定管道。 確定規則處於記錄模式。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds 100 req/sec on a time window of 1sec
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 100
        window: 1
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
    - name: block-ofac-countries
      when:
        allOf:
          - { reqProperty: tier, equals: publish }
          - reqProperty: clientCountry
            in:
              - SY
              - BY
              - MM
              - KP
              - IQ
              - CD
              - SD
              - IR
              - LR
              - ZW
              - CU
              - CI
      action: log
    # Enable recommended WAF protections (only works if WAF is enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        matches: "author|publish"
      action:
        type: log
        wafFlags:
          - SANS
          - SIGSCI-IP
          - TORNODE
          - NOUA
          - SCANNER
          - USERAGENT
          - PRIVATEFILE
          - ABNORMALPATH
          - TRAVERSAL
          - NULLBYTE
          - BACKDOOR
          - LOG4J-JNDI
          - SQLI
          - XSS
          - CODEINJECTION
          - CMDEXE
          - NO-CONTENT-TYPE
          - UTF8
    # Disable protection against CMDEXE on /bin
    - name: allow-cdmexe-on-root-bin
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            matches: "^/bin/.*"
      action:
        type: log
        wafFlags:
          - CMDEXE
```

1. 新增任何其他規則以封鎖您可能知道的惡意流量。 例如，某些攻擊您網站的IP。

1. 幾分鐘、幾小時或幾天後（視您網站的流量而定），從Cloud Manager下載CDN記錄並使用儀表板分析它們。

1. 以下是一些考量事項：
   1. 流量比對宣告規則會出現在圖表和請求記錄中，以便您輕鬆檢查是否觸發了宣告規則。
   1. 流量符合WAF旗標會顯示在圖表和請求記錄中，即使您未將其記錄在規則中也是如此。 如此一來，您就能隨時掌握潛在的新惡意流量，並視需要建立新規則。 檢視未反映在宣告規則中的WAF標幟，並考慮宣告它們。
   1. 如需比對規則，請檢查請求記錄檔中是否有誤判，並檢視您是否可從規則中篩選出這些誤判。 例如，可能只有某些路徑是誤判。

1. 設定適當的規則以封鎖模式，並考慮新增其他規則。 當您進一步分析並帶來更多流量時，部分規則可能仍會維持在記錄模式。

1. 重新部署設定。

1. 反複分析、經常分析控制面板。

