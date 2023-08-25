---
title: 設定 CDN 和 WAF 規則以篩選流量
description: 使用 CDN 和 Web 應用程式防火牆規則篩選惡意流量
source-git-commit: 0f1ee0ec5fc2d084a6dfdc65d15a8497c23f11a2
workflow-type: tm+mt
source-wordcount: '2391'
ht-degree: 97%

---


# 設定 CDN 和 WAF 規則以篩選流量 {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>此功能尚未正式推出。若要加入正在進行的早期採用者計劃，請寄送電子郵件至 **aemcs-waf-adopter@adobe.com**，郵件內容包括貴組織的名稱以及您對該功能感興趣的原因。

Adobe 試圖減輕針對客戶網站發動的攻擊，但主動篩選和特定模式相符的要求可能有助於阻擋惡意流量，使其無法接觸您的應用程式。可能的方法包括：

* Apache 層模組，例如 `mod_security`
* 透過 Cloud Manager 的設定管道設定部署到 CDN 的規則。

本文會說明後面一種方法，這會提供兩種類別的規則：

1. **CDN 規則**：會根據要求屬性和要求標頭封鎖或允許要求，包括 IP、路徑和使用者代理程式。所有 AEM as a Cloud Service 客戶都可以設定這類規則
1. **WAF** (Web 應用程式防火牆) 規則：會封鎖和惡意流量相關的各種已知模式相符的要求。這些規則可由取得 WAF 外掛程式授權的客戶進行設定；如需詳細資料，請和您的 Adob&#x200B;&#x200B;e 帳戶團隊聯絡。請注意，早期採用者計劃期間不需要另外取得授權。

可將這些規則部署到開發、中繼和生產的雲端環境類型，適用於生產 (非沙箱) 計畫。未來將提供對 RDE 環境的支援。

## 設定 {#setup}

1. 首先，請在 git 中建立以下檔案夾和檔案結構的最高層級檔案夾：

   ```
   config/
        cdn/
           cdn.yaml
           _config.yaml
   ```

1. `_config.yaml` 會說明一些有關設定的中繼資料。「kind」參數應設定為「CDN」，版本則應設定為綱要版本，目前是「1」。請參閱以下片段：

   ```
   kind: "CDN"
   version: "1"
   ```

   <!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. `cdn.yaml` 應包括 CDN 規則和 WAF 規則的清單，如以下章節所述
1. 若要和 WAF 規則相符，必須在 Cloud Manager 中啟用 WAF (如下所述)，對於新的和現有的計劃案例都適用。請注意，必須為 WAF 購買單獨的授權。

   1. 若要對新計畫設定 WAF，請勾選「**WAF-DDOS 防護**」核取方塊 (在&#x200B;**安全性**&#x200B;索引標籤中)，如下所示。繼續依照「[新增生產計劃](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)」中說明的步驟進行，以建立您的計畫

   1. 若要對現有計畫設定 WAF，請選取「**編輯計畫**」選項 (依照「[編輯計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)」文件中說明的步驟進行)。接著，在精靈的「**安全性**」索引標籤中，您隨時都可以取消勾選或勾選 WAF-DDOS 選項

1. 若為 RDE 以外的環境類型，則請執行 Cloud Manager 設定管道，可以依如下所述進行設定。

   1. 在 Cloud Manager 首頁的管道卡中，選取「**新增生產管道**」或者「**新增非生產管道**」，即可啟動新增管道精靈
   1. 在設定索引標籤中選取「**部署管道**」

      ![選取部署管道選項](/help/security/assets/deployment.png)

   1. 為您的管道命名並選取部署觸發器，然後選取「**繼續**」
   1. 在「**原始程式碼**」索引標籤中，選取「**目標性部署**」，然後選取「**設定**」

      ![選取目標性部署](/help/security/assets/target-deployment.png)

   1. 根據需要選取存放庫和分支。如果選取環境中存在設定管道，則此選項會停用。

      ![設定管道概觀](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      >您對每個環境只能設定並執行一個設定管道。

   1. 選取&#x200B;**儲存**。您的新管道即會顯示在管道卡中，並可在您就緒後執行。
   1. 若為 RDE，會使用命令列，但目前不支援 RDE。

## 規則語法 {#rules-syntax}

下面會說明規則的格式，後續章節中則會提供一些範例。

| **屬性** | **CDN 規則** | **WAF 規則** | **類型** | **預設值** | **說明** |
|---|---|---|---|---|---|
| 名稱 | X | X | `string` | - | 規則名稱 (64 個字元的長度，只能包含英數字元和 -) |
| 時間 | X | X | `Condition` | - | 基本結構是：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>請參閱下面的條件結構語法，其中會說明 getter、述詞以及結合多個條件的方式。 |
| 動作 | X | X | `Enum` | 紀錄 (CDN 規則) | 若為 CDN 規則：允許、封鎖、記錄。預設為記錄。<br><br>若為 WAF 規則：`enableWafRules`、`disableWafRules`、紀錄。無預設值。 |
| rateLimit | X |   | `RateLimit` | 未定義 | 速率限制設定。若未定義，則停用速率限制。<br><br>以下會有一個單獨的章節說明 rateLimit 語法以及範例。 |
| wafRules |   | X | `array[Enum]` | - | 應啟用或停用的 WAF 規則清單。<br><br>範例包括 SQLI 和 XSS。 請參閱下面的 waf 規則清單以取得完整清單。 |

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

| **屬性** | **類型** | **說明** |
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

| **屬性** | **類型** | **說明** |
|---|---|---|
| **等於** | `string` | 如果 getter 結果等於所提供的值，則為 true |
| **doesNotEqual** | `string` | 如果 getter 結果不等於所提供的值，則為 true |
| **like** | `string` | 如果 getter 結果和所提供的模式相符，則為 true |
| **notLike** | `string` | 如果 getter 結果和所提供的模式不相符，則為 true |
| **matches** | `string` | 如果 getter 結果和所提供的 regex 相符，則為 true |
| **doesNotMatch** | `string` | 如果 getter 結果和所提供的 regex 不相符，則為 true |
| **in** | `array[string]` | 如果所提供的清單包含 getter 結果，則為 true |
| **notIn** | `array[string]` | 如果所提供的清單不包含 getter 結果，則為 true |

**wafRules List**

`wafRules` 屬性可能包括下列規則：

| **規則 ID** | **規則名稱** | **說明** |
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

## 範例 {#examples}

下面是一些規則範例。如需進一步探討速率限制的範例，請參閱[「速率限制」一節](#rules-with-rate-limits)。

**範例 1**

此規則會封鎖來自 IP 192.168.1.1 的要求：

```
data:
  rules:
    - name: "block-request-from-ip"
      when: { reqProperty: clientIp, equals: "192.168.1.1" }
      action: block
```

**範例 2**

此規則會使用包含 Chrome 的使用者代理程式封鎖發佈的路徑 `/helloworld` 上的要求：

```
data:
  rules:
    - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
      when:
        allOf:
          - { reqProperty: path, equals: /helloworld }
          - { reqProperty: tier, equals: publish }
          - { reqHeader: user-agent, matches: '.*Chrome.*'  }
      action: block
```

**範例 3**

此規則會封鎖包含查詢參數 `foo` 的要求，但會允許來自 IP 192.168.1.1 的每個要求：

```
data:
  rules:
    - name: "block-request-that-contains-query-parameter-foo"
      when: { queryParam: url-param, equals: foo }
      action: block
    - name: "allow-all-requests-from-ip"
      when: { reqProperty: clientIp, equals: 192.168.1.1 }
      action: allow
```

**範例 4**

此規則會封鎖對路徑 /block-me 的要求，並封鎖和 SQLI 或 XSS 模式相符的每個要求：

```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

## 具有速率限制的規則 {#rules-with-rate-limits}

若相符程度經過一段時間後超過特定速率，則有時也需要只封鎖和某種規則相符的流量。設定 `rateLimit` 屬性的值會限制那些和規則條件相符的要求的速率。

### rateLimit 結構 {#ratelimit-structure}

| **屬性** | **類型** | **預設值** | **說明** |
|---|---|---|---|
| 限制 | 10 到 10000 之間的整數 | 必要 | 觸發規則的要求速率 (以每秒要求數為單位) |
| 視窗 | 整數列舉：1、10 或 60 | 10 | 計算要求速率的取樣期間 (秒數) |
| 懲罰 | 60 到 3600 之間的整數 | 300 (5 分鐘) | 封鎖相符要求時間的秒數 (四捨五入到最接近的分鐘) |

### 範例 {#ratelimiting-examples}

範例1：當請求速率在最近60秒內超過每秒100個請求時，封鎖 `/critical/resource` 60秒

```
- name: rate-limit-example
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit: { limit: 100, window: 60, penalty: 60 }
```

範例 2：當 10 秒內要求速率超過每秒 10 個要求時，即封鎖資源 300 秒：

```
- name: rate-limit-using-defaults
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit:
    limit: 10
```

## CDN 紀錄 {#cdn-logs}

AEM as a Cloud Service 會提供對 CDN 紀錄的存取權，這對於包括快取命中率最佳化以及設定 CDN 和 WAF 規則等使用案例都非常有幫助。選取作者或發佈服務時，CDN 紀錄會顯示在 Cloud Manager **下載紀錄**&#x200B;對話框中。

如果要求和規則相符，則規則的名稱會顯示在規則屬性中，即使動作為「允許」，而因此不會封鎖流量。

相符的 CDN 規則會顯示在對 CDN 發出的所有要求的紀錄條目中，無論是 CDN 命中、通過還是未命中。但是，會顯示 WAF 規則的紀錄條目僅限於發送給被視為 CDN 未命中或通過但不被視為 CDN 命中的 CDN 要求。

以下範例會說明 `cdn.yaml` 範例以及兩個 CDN 紀錄條目，由於要求分別和 CDN 規則以及 WAF 規則相符而遭到封鎖，因此規則屬性中有非空白值。


```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
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
"rules": "cdn=path-rule;waf=;action=blocked"
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
"rules": "cdn=;waf=SQLI;action=blocked"
}
```

### 紀錄格式 {#cdn-log-format}

以下是 CDN 紀錄中使用的欄位名稱清單以及簡要說明。

| **欄位名稱** | **說明** |
|---|---|
| *timestamp* | TLS 終止後要求開始的時間 |
| *ttfb* | *首位元組時間 (Time To First Byte)* 的縮寫。 發出要求開始到回應內文開始串流的時間之間的時間間隔。 |
| *cli_ip* | 用戶端 IP 位址。 |
| *cli_country* | 雙字母 [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) 使用者端國家/地區的alpha-2國家/地區代碼。 |
| *rid* | 用於唯一識別要求的要求標頭的值。 |
| *req_ua* | 負責發出特定 HTTP 要求的使用者代理程式。 |
| *主機* | 發送要求的目標機構。 |
| *url* | 包括查詢參數的完整路徑。 |
| *方法* | 用戶端傳送的 HTTP 方法，例如「GET」或「POST」。 |
| *res_ctype* | 此內容類型會用於表示資源的原始媒體類型. |
| *cache* | 快取的狀態。可能的值包括 HIT、MISS 或 PASS |
| *狀態* | 作為整數值的 HTTP 狀態代碼。 |
| *res_age* | 回應已快取的時間（秒） （在所有節點中）。 |
| *pop* | CDN 快取伺服器的資料中心。 |
| *rules* | 任何相符規則的名稱，適用於 CDN 規則和 WAF 規則。<br><br>相符的 CDN 規則會顯示在對 CDN 發出的所有要求的紀錄條目中，無論是 CDN 命中、通過還是未命中。<br><br>還會指出該相符程度是否導致封鎖。<br><br>例如，「`cdn=;waf=SQLI;action=blocked`」<br><br>如果沒有相符的規則，則為空白。 |
