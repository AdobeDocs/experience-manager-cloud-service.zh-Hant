---
title: 設定流量篩選規則（使用WAF規則）
description: 使用流量篩選規則（搭配WAF規則）來篩選流量
source-git-commit: b1b184b63ab6cdeb8a4e0019c31a34db59438a3d
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 70%

---


# 設定流量篩選規則（使用WAF規則）以篩選流量 {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>此功能尚未正式推出。若要加入正在進行的早期採用者計劃，請寄送電子郵件至 **aemcs-waf-adopter@adobe.com**，郵件內容包括貴組織的名稱以及您對該功能感興趣的原因。

Adobe會嘗試減輕對客戶網站的攻擊，但主動篩選符合特定模式的流量以便讓惡意流量不會到達您的應用程式中，可能會很有用。 可能的方法包括：

* Apache 層模組，例如 `mod_security`
* 設定透過Cloud Manager的設定管道部署到CDN的流量篩選規則

本文會說明流量篩選規則方法。 這些規則大多會根據請求屬性和請求標頭（包括IP、路徑和使用者代理）來封鎖或允許請求。 這些規則可由所有AEMas a Cloud ServiceSites和Forms客戶設定。

授權WAF （Web應用程式防火牆）附加元件的客戶也可以設定稱為「WAF流量篩選規則」（簡稱WAF規則）的其他規則類別。 這些WAF規則會封鎖符合已知與惡意流量相關聯的各種模式的請求。 請聯絡您的Adobe客戶團隊，以取得授權這項即將推出的功能的詳細資訊。 請注意，早期採用者計劃期間不需要另外取得授權。

流量篩選器規則可以部署到生產（非沙箱）計畫中的所有雲端環境型別(RDE、dev、stage、prod)。

## 設定 {#setup}

1. 首先，請在 git 中建立以下檔案夾和檔案結構的最高層級檔案夾：

   ```
   config/
        cdn/
           cdn.yaml
   ```

1. `cdn.yaml` 應該包含中繼資料，以及流量篩選器規則和WAF規則的清單。

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
         ...
   ```

「kind」參數應設定為「CDN」，版本則應設定為綱要版本，目前是「1」。請參閱下面的範例。


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. 若要設定WAF規則，則必須在Cloud Manager中啟用WAF，如以下針對新方案和現有方案方案方案方案所述。 請注意，必須為 WAF 購買單獨的授權。

   1. 若要對新計畫設定 WAF，請勾選「**WAF-DDOS 防護**」核取方塊 (在&#x200B;**安全性**&#x200B;索引標籤中)，如下所示。繼續依照「[新增生產計劃](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)」中說明的步驟進行，以建立您的計畫

   1. 若要對現有計畫設定 WAF，請選取「**編輯計畫**」選項 (依照「[編輯計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)」文件中說明的步驟進行)。接著，在精靈的「**安全性**」索引標籤中，您隨時都可以取消勾選或勾選 WAF-DDOS 選項

1. 若為 RDE 以外的環境類型，則請執行 Cloud Manager 設定管道，可以依如下所述進行設定。

   1. 在 Cloud Manager 首頁的管道卡中，選取「**新增生產管道**」或者「**新增非生產管道**」，即可啟動新增管道精靈
   1. 在設定索引標籤中選取「**部署管道**」

      ![選取部署管道選項](/help/security/assets/deployment.png)

   1. 為您的管道命名並選取部署觸發器，然後選取「**繼續**」
   1. 在「**原始程式碼**」索引標籤中，選取「**目標性部署**」，然後選取「**設定**」

      ![選取目標部署](/help/security/assets/target-deployment.png)

   1. 根據需要選取存放庫和分支。如果選取環境中存在設定管道，則此選項會停用。

      ![設定管道概觀](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      > 使用者必須以部署管理員身分登入，才能設定或執行這些管道。
      > 此外，每個環境只能設定和執行一個設定管道。

   1. 選取&#x200B;**儲存**。您的新管道即會顯示在管道卡中，並可在您就緒後執行。
   1. 對於RDE，將使用命令列，但目前不支援RDE。

## 流量篩選器規則語法 {#rules-syntax}

您可以設定 `traffic filter rules` 以比對IP、使用者代理、請求標題、主機名稱、地理和url等模式。

授權WAF產品的客戶也可設定流量篩選規則的特殊類別，稱為 `WAF traffic filter rules` 參照一或多個WAF旗標的（簡稱WAF規則），這些旗標會列在它自己的以下區段中。

以下是流量篩選規則集的範例，其中也包含WAF規則。

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

cdn.yaml檔案中流量篩選規則的格式如下所述。 請參閱稍後章節中的一些範例。


| **屬性** | **大多數流量篩選規則** | **WAF流量篩選規則** | **類型** | **預設值** | **說明** |
|---|---|---|---|---|---|
| 名稱 | X | X | `string` | - | 規則名稱 (64 個字元的長度，只能包含英數字元和 -) |
| 時間 | X | X | `Condition` | - | 基本結構是：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>請參閱下面的條件結構語法，其中會說明 getter、述詞以及結合多個條件的方式。 |
| 動作 | X | X | `Action` | 記錄 | log、allow、block、log或action物件預設為log |
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
| cookie | `string` | 傳回具有指定名稱的 Cookie |

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

### 動作結構 {#action-structure}

指定者 `action` 欄位，可以是指定動作型別（允許、區塊、記錄）的字串，並假設所有其他選項的預設值，或是定義規則型別的物件，透過 `type` 必填欄位，以及適用於該型別的其他選項。

**動作型別**

動作會根據其在下表中的型別來排定優先順序，此排序方式反映動作的執行順序：

| **名稱** | **允許的屬性** | **含義** |
|---|---|---|
| **允許** | `wafFlags` (可選) | 如果wafFlags不存在，將停止進一步的規則處理並繼續提供回應。 如果wafFlags存在，它會停用指定的WAF保護並繼續進一步的規則處理。 |
| **區塊** | `status, wafFlags` （選擇性且互斥） | 如果wafFlags不存在，會傳回HTTP錯誤，略過所有其他屬性，錯誤碼會由status屬性定義或預設為406。 如果wafFlags存在，它會啟用指定的WAF保護並繼續進一步的規則處理。 |
| **記錄** | `wafFlags` (可選) | 會記錄規則已觸發的事實，否則不會影響處理。 wafFlags無效 |

### WAF旗標清單 {#waf-flags-list}

此 `wafFlag` 屬性可能包含下列專案：

| **旗標ID** | **標幟名稱** | **說明** |
|---|---|---|
| SQLI | SQL 注入 | SQL 注入指試圖透過執行任意資料庫查詢以取得對應用程式的存取權或獲取特權資訊。 |
| BACKDOOR | 後門 | 後門訊號指試圖決定系統是否存在常見後門檔案的要求。 |
| CMDEXE | 命令執行 | 命令執行指試圖透過由使用者輸入的任意系統命令獲取控制或毀損目標系統。 |
| XSS | 跨網站指令碼 | 跨網站指令碼指試圖透過惡意 JavaScript 程式碼劫持使用者的帳戶或 Web 瀏覽工作階段。 |
| 周遊 | 目錄周遊 | 目錄周遊指試圖瀏覽整個系統中的特權檔案，期望能獲取敏感資訊。 |
| USERAGENT | 攻擊工具 | 攻擊工具指使用自動化軟體識別安全漏洞或試圖惡意探索發現的漏洞。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻擊會試圖惡意探索出現在 2.16.0 之前的 Log4J 版本中的 [Log4Shell 漏洞](https://en.wikipedia.org/wiki/Log4Shell) |
| AWS SSRF | AWS-SSRF | 伺服器端請求偽造 (SSRF) 是一種要求，會試圖傳送由 Web 應用程式發出的要求到目標內部系統。AWS SSRF 攻擊會利用 SSRF 獲取 Amazon Web Services (AWS) 金鑰並獲取對 S3 貯體及其資料的存取權。 |
| BHH | 錯誤跳躍標頭 | 錯誤跳躍標頭指透過格式錯誤的傳輸編碼 (TE) 或內容長度 (CL) 標頭或格式正確的 TE 和 CL 標頭進行的 HTTP 走私嘗試 |
| ABNORMALPATH | 異常路徑 | 異常路徑指原始路徑和標準化路徑不同 (例如：`/foo/./bar` 會標準化為 `/foo/bar`) |
| 已壓縮 | 偵測到壓縮 | POST 要求內文被壓縮，並且無法檢查。例如，若指定「Content-Encoding: gzip」要求標頭，並且 POST 內文並非純文字。 |
| DOUBLEENCODING | 雙重編碼 | 雙重編碼會檢查雙重編碼 html 字元的規避技術 |
| FORCEFULBROWSING | 強制瀏覽 | 強制瀏覽指試圖存取管理頁面時失敗 |
| NOTUTF8 | 無效的編碼 | 無效的編碼可能會導致伺服器將要求中的惡意字元翻譯為回應，進而導致拒絕服務或 XSS |
| JSON-ERROR | JSON 編碼錯誤 | 指定為在「Content-Type」要求標頭中包含 JSON 但包含 JSON 剖析錯誤的 POST、PUT 或 PATCH 要求內文。這經常和程式設計錯誤或自動化亦或惡意要求有關。 |
| MALFORMED-DATA | 要求內文中格式錯誤的資料 | 根據「Content-Type」要求標頭，格式錯誤的 POST、PUT 或 PATCH 要求內文。例如，如果指定了「Content-Type: application/x-www-form-urlencoded」要求標頭並包含 json 的 POST 內文。這經常是程式設計錯誤、自動化或惡意要求。需要代理程式 3.2 或更高版本。 |
| SANS | 惡意的 IP 流量 | 已被報告為參與了惡意活動的 [SANS 網際網路風暴中心](https://isc.sans.edu/) IP 位址清單 |
| SIGSCI-IP | 網路效應 | 由 SignalSciences 標記的 IP：每當決策引擎因惡意訊號而標記 IP 時，即會將 IP 傳播給所有客戶。接著會記錄來自這些 IP 位址的後續要求 (其中會包含標幟持續時間中的任何其他訊號)。 |
| NO-CONTENT-TYPE | 缺少「Content-Type」要求標頭 | 沒有「Content-Type」要求標頭的 POST、PUT 或 PATCH 要求。在此案例中，預設情況下應用程式伺服器應假設「Content-Type: text/plain; charset=us-ascii」。許多自動化和惡意要求可能會缺少「內容類型」。 |
| NOUA | 沒有使用者代理程式 | 許多自動化和惡意要求會使用偽造的使用者代理程式或缺少使用者代理程式，這使得難以識別發出要求的裝置類型。 |
| TORNODE | Tor 流量 | Tor 是可隱藏使用者身份的軟體。Tor 流量激增可能表示有攻擊者試圖掩飾其位置。 |
| DATACENTER | 資料中心流量 | 資料中心流量指源自於已識別主機提供者的非自然流量。這種類型的流量通常和真正的一般使用者無關。 |
| NULLBYTE | 空位元 | 空位元通常不會出現在要求中，因為這表示該要求的格式錯誤且可能是惡意的。 |
| IMPOSTOR | SearchBot 冒充者 | 搜尋機器人冒充者指冒充 Google 或 Bing 搜尋機器人的人，但並不合法。請注意，這本身不仰賴回應，但必須先在雲端中解析，因此不應用於預規則中。 |
| PRIVATEFILE | 私人檔案 | 私人檔案通常在本質上屬於機密性，例如 Apache `.htaccess` 檔案或可能洩漏敏感資訊的設定檔案 |
| SCANNER | 掃描程式 | 可識別熱門的掃描服務和工具 |
| RESPONSESPLIT | HTTP 回應拆分 | 會識別何時將 CRLF 字元作為輸入提交給應用程式，以將標頭注入 HTTP 回應 |
| XML-ERROR | XML 編碼錯誤 | 指定為在「Content-Type」要求標頭中包含 XML 但包含 XML 剖析錯誤的 POST、PUT 或 PATCH 要求內文。這經常和程式設計錯誤或自動化亦或惡意要求有關。 |

## 考量事項 {#considerations}

* 建立兩個衝突規則時，允許規則總是優先於封鎖規則。例如，如果您建立一條封鎖特定路徑的規則，又建立一條允許特定 IP 位址的規則，則來自遭封鎖路徑上的該 IP 位址的要求會受到允許。

* 如果規則相符並遭封鎖，CDN 會以 `406` 傳回代碼回應。

* 組態檔不應包含秘密，因為任何有權存取Git存放庫的人都能讀取。

## 規則範例 {#examples}

下面是一些規則範例。如需進一步探討速率限制的範例，請參閱[「速率限制」一節](#rules-with-rate-limits)。

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
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
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

此規則會封鎖對路徑 /block-me 的要求，並封鎖和 SQLI 或 XSS 模式相符的每個要求：

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

**範例 4**

此規則會封鎖對OFAC國家/地區的存取權：

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
        action: block
```

## 具有速率限制的規則 {#rules-with-rate-limits}

若相符程度經過一段時間後超過特定速率，則有時也需要只封鎖和某種規則相符的流量。設定 `rateLimit` 屬性的值會限制那些和規則條件相符的要求的速率。

### rateLimit 結構 {#ratelimit-structure}

| **屬性** | **類型** | **預設** | **含義** |
|---|---|---|---|
| 限制 | 10 到 10000 之間的整數 | 必要 | 觸發規則的要求速率 (以每秒要求數為單位). |
| 視窗 | 整數列舉：1、10 或 60 | 10 | 計算要求速率的取樣期間 (秒數). |
| 懲罰 | 60 到 3600 之間的整數 | 300 (5 分鐘) | 封鎖相符要求時間的秒數 (四捨五入到最接近的分鐘). |
| groupBy | 陣列[Getter] | 無 | 速率限制器計數器將依一組請求屬性（例如clientIp）彙總。 |

### 範例 {#ratelimiting-examples}

**範例 1**

在過去60秒內，當使用者端超過每秒100個請求時，此規則會封鎖5m的使用者端：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**範例 2**

封鎖路徑/critical/resource上在過去60秒內超過100個要求/秒時的60個要求：

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

## CDN 紀錄 {#cdn-logs}

AEM as a Cloud Service 會提供對 CDN 紀錄的存取權，這對於包括快取命中率最佳化以及設定 CDN 和 WAF 規則等使用案例都非常有幫助。選取作者或發佈服務時，CDN 紀錄會顯示在 Cloud Manager **下載紀錄**&#x200B;對話框中。

「規則」屬性說明哪些流量篩選器規則相符，其模式如下：

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例如：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

規則的行為方式如下：

* 任何相符規則的客戶宣告規則名稱都會列在matches屬性中。
* action屬性詳細說明規則是否具有封鎖、允許或記錄的效果。
* 如果WAF已授權並啟用，則waf屬性會列出偵測到的任何waf規則（例如SQLI；請注意，這與客戶宣告的名稱無關），無論組態中是否列出了waf規則。
* 如果沒有相符的客戶宣告規則以及沒有相符的waf規則，則rules屬性屬性將為空白。

一般而言，無論是否為CDN點選、通過或錯過，對CDN的所有請求都會在記錄專案中顯示相符的規則。 但是，會顯示 WAF 規則的紀錄條目僅限於發送給被視為 CDN 未命中或通過但不被視為 CDN 命中的 CDN 要求。

以下範例顯示一個cdn.yaml範例和兩個CDN記錄專案：


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

### 紀錄格式 {#cdn-log-format}

以下是 CDN 紀錄中使用的欄位名稱清單以及簡要說明。

| **欄位名稱** | **說明** |
|---|---|
| *timestamp* | TLS 終止後要求開始的時間. |
| *ttfb* | *首位元組時間 (Time To First Byte)* 的縮寫。 發出要求開始到回應內文開始串流的時間之間的時間間隔。 |
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
| *rules* | 任何相符規則的名稱。<br><br>還會指出該相符程度是否導致封鎖。<br><br>例如，「`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`」<br><br>如果沒有相符的規則，則為空白。 |
