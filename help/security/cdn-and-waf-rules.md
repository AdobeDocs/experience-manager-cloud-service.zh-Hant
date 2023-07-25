---
title: 設定CDN和WAF規則以篩選流量
description: 使用CDN和Web應用程式防火牆規則來篩選惡意流量
source-git-commit: 579f2842a72c7da1c9d24772bdae354a943de40c
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---


# 設定CDN和WAF規則以篩選流量 {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>此功能尚未正式推出。若要加入進行中的早期採用者計畫，請傳送電子郵件至 **aemcs-waf-adopter@adobe.com**，包括貴組織的名稱以及有關您對功能感興趣的內容。

Adobe會嘗試減輕對客戶網站的攻擊，但主動篩選符合特定模式的請求以便惡意流量不會到達您的應用程式可能會有幫助。 可能的方法包括：

* Apache層模組，例如 `mod_security`
* 設定透過Cloud Manager的設定管道部署到CDN的規則。

本文會介紹後一種方法，該方法提供兩種規則：

1. **CDN規則**：根據請求屬性和請求標頭（包括IP、路徑和使用者代理）封鎖或允許請求。 這些規則可由所有AEMas a Cloud Service客戶設定
1. **WAF** （Web應用程式防火牆）規則：封鎖符合已知與惡意流量相關聯的各種模式的請求。 這些規則可由授權WAF附加元件的客戶設定；請聯絡您的Adobe客戶團隊以取得詳細資料。 請注意，在早期採用者計畫期間不需要額外的授權。

這些規則可部署至開發、測試和生產雲端環境型別，以用於生產（非沙箱）計畫。 未來將提供RDE環境支援。

## 設定 {#setup}

1. 首先，在Git中建立下列資料夾和檔案結構頂層資料夾：

   ```
   config/
        cdn/
           cdn.yaml
           _config.yaml
   ```

1. `_config.yaml` 說明有關設定的部分中繼資料。 「kind」引數應設為「CDN」，而版本應設為結構描述版本，目前為「1」。 請參閱下列程式碼片段：

   ```
   kind: "CDN"
   version: "1"
   ```

   <!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. `cdn.yaml` 應該包含CDN規則和WAF規則的清單，如下節所述
1. 為了符合WAF規則，必須在Cloud Manager中啟用WAF，如以下針對新方案和現有方案方案方案方案所述。 請注意，必須為WAF購買單獨的授權。

   1. 若要在新程式上設定WAF，請核取 **WAF-DDOS保護** 核取方塊 **安全性** 標籤，如下所示。 請依照中所述的步驟繼續操作 [新增生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 以建立您的程式

   1. 若要在現有程式上設定WAF，請選取 **編輯計畫** 選項，請依照以下說明的步驟操作： [編輯程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) 說明檔案。 然後，在 **安全性** 標籤中，您可以隨時取消核取或核取WAF-DDOS選項

1. 對於RDE以外的環境型別，執行Cloud Manager設定管道，可依照以下所述進行設定。

   1. 從Cloud Manager首頁的管道卡中，選擇 **新增生產管道** 或 **新增非生產管道** 啟動新增管道精靈
   1. 選取 **部署管道** 在設定索引標籤中

      ![選取部署管道選項](/help/security/assets/deployment.png)

   1. 為管道命名，並選取部署觸發程式，然後選取 **繼續**
   1. 在 **原始碼** 索引標籤，選取 **目標部署**，然後選取 **設定**

      ![選取目標部署](/help/security/assets/target-deployment.png)

   1. 視需要選取存放庫和分支。 如果所選環境存在設定管道，則此選擇為停用。

      ![設定管道概觀](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      >每個環境只能設定和執行一個設定管道。

   1. 選取&#x200B;**儲存**。您的新管道將顯示在管道卡中，並可在您準備就緒時執行。
   1. 對於RDE，將使用命令列，但目前不支援RDE。

## 規則語法 {#rules-syntax}

規則的格式如下所述，後面是後續章節中的一些範例。

| **屬性** | **CDN規則** | **WAF規則** | **類型** | **預設值** | **說明** |
|---|---|---|---|---|---|
| 名稱 | X | X | `string` | - | 規則名稱（64個字元長，只能包含英數字元和 — ） |
| 時間 | X | X | `Condition` | - | 基本結構為：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>請參閱以下的條件結構語法，其中說明了getter、述詞以及如何組合多個條件。 |
| 動作 | X | X | `Enum` | 記錄（CDN規則） | 對於CDN規則：允許、封鎖、記錄。 預設為log。<br><br>對於WAF規則： `enableWafRules`， `disableWafRules`，記錄。 無預設值。 |
| rateLimit | X |   | `RateLimit` | 未定義 | 速率限制設定。 如果未定義，則會停用速率限制。<br><br>下面有更詳細的個別章節說明rateLimit語法以及範例。 |
| wafRules |   | X | `array[Enum]` | - | 應啟用或停用的WAF規則清單。<br><br>範例包括SQLI和XSS。 如需完整清單，請參閱下方的waf規則清單。 |

### 條件結構 {#condition-structure}

條件可以是簡單的條件或一組條件。

**簡單條件**

簡單條件由getter和述片語成。

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
| **allOf** | `array[Condition]` | **和** 作業。 如果所有列出的條件都傳回true，則為true |
| **anyOf** | `array[Condition]` | **或** 作業。 如果任何列出的條件傳回true，則為true |

**Getter**

| **屬性** | **類型** | **說明** |
|---|---|---|
| reqProperty | `string` | 要求屬性。<br><br>下列其中一項： `path` ， `queryString`， `method`， `tier`， `domain`， `clientIp`， `clientCountry`<br><br>domain屬性是請求主機標頭的小寫轉換。 此變數對於字串比較很有用，因此相符專案不會因區分大小寫而遺失。<br><br>此 `clientCountry` 使用以下位置顯示的兩個字母代碼： [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) |
| reqHeader | `string` | 傳回具有指定名稱的請求標頭 |
| queryParam | `string` | 傳回具有指定名稱的查詢引數 |
| Cookie | `string` | 傳回具有指定名稱的Cookie |

**述詞**

| **屬性** | **類型** | **說明** |
|---|---|---|
| **等於** | `string` | 如果getter結果等於提供的值則為true |
| **doesNotEqual** | `string` | 如果getter結果不等於提供的值則為true |
| **讚** | `string` | 如果getter結果符合提供的模式，則為true |
| **notLike** | `string` | 如果getter結果不符合提供的模式，則為true |
| **matches** | `string` | 如果getter結果符合提供的regex，則為true |
| **doesNotMatch** | `string` | 如果getter結果不符合提供的regex，則為true |
| **中的** | `array[string]` | 如果提供的清單包含getter結果，則為true |
| **notIn** | `array[string]` | 如果提供的清單不包含getter結果，則為true |

**wafRules清單**

此 `wafRules` 屬性可能包含下列規則：

| **規則ID** | **規則名稱** | **說明** |
|---|---|---|
| SQLI | SQL插入 | SQL插入是嘗試透過執行任意的資料庫查詢來存取應用程式或取得授權的資訊。 |
| 後門 | 後門 | 後門訊號是嘗試判斷系統上是否存在通用後門檔案的要求。 |
| CMDEXE | 命令執行 | 命令執行是指透過使用者輸入的任何系統命令，嘗試取得控制或破壞目標系統。 |
| XSS | 跨網站指令碼 | 跨網站指令碼是指嘗試透過惡意JavaScript程式碼劫持使用者帳戶或網頁瀏覽工作階段。 |
| 周遊 | 目錄周遊 | Directory Traversal是嘗試在整個系統中瀏覽特殊許可權資料夾，以取得敏感資訊。 |
| USERAGENT | 攻擊工具 | Attack Tooling是使用自動化軟體來識別安全性弱點，或嘗試利用發現的弱點。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI攻擊嘗試利用 [Log4Shell漏洞](https://en.wikipedia.org/wiki/Log4Shell) 存在於2.16.0之前的Log4J版本中 |
| AWS SSRF | AWS-SSRF | Server Side Request Forgery (SSRF)是嘗試將Web應用程式提出的要求傳送至目標內部系統的要求。 AWS SSRF攻擊會使用SSRF來取得Amazon Web Services (AWS)金鑰，以及存取S3儲存貯體及其資料。 |
| BHH | 錯誤的躍點標頭 | 錯誤的Hop標頭表示透過格式錯誤的Transfer-Encoding (TE)或Content-Length (CL)標頭，或是格式正確的TE和CL標頭進行HTTP走私企圖 |
| 異常路徑 | 異常路徑 | 「異常路徑」表示原始路徑與標準化路徑不同(例如， `/foo/./bar` 已標準化為 `/foo/bar`) |
| 已壓縮 | 偵測到壓縮 | POST要求內文已壓縮，無法檢查。 例如，若指定「Content-Encoding： gzip」請求標頭，且POST內文不是純文字。 |
| DOUBLE編碼 | 雙重編碼 | 雙重編碼檢查雙重編碼html字元的規避技術 |
| FORCEFULBROWSING | 強制瀏覽 | 強制瀏覽是指存取管理頁面的嘗試失敗 |
| NOTUTF8 | 無效的編碼 | 無效的編碼會導致伺服器將請求中的惡意字元轉譯為回應，造成拒絕服務或XSS |
| JSON-ERROR | JSON編碼錯誤 | 指定為在「Content-Type」要求標頭中包含JSON，但包含JSON剖析錯誤的POST、PUT或PATCH要求內文。 這通常與程式設計錯誤、自動化或惡意請求有關。 |
| 格式錯誤的資料 | 請求內文中的資料格式錯誤 | 根據「Content-Type」請求標頭的格式錯誤的POST、PUT或PATCH請求內文。 例如，若指定「Content-Type： application/x-www-form-urlencoded」請求標頭且包含jsonPOST內文。 這通常是程式設計錯誤，或是自動化或惡意要求。 需要代理程式3.2或更新版本。 |
| SANS | 惡意IP流量 | [SANS網際網路風暴中心](https://isc.sans.edu/) 已回報參與惡意活動的IP位址清單 |
| SIGSCI-IP | 網路效果 | 由SignalSciences標幟的IP：每當決策引擎因惡意訊號而標幟該IP時，該IP會傳播給所有客戶。 接著會記錄來自這些IP位址的後續請求，這些位址包含標籤持續期間的任何其他訊號 |
| no-CONTENT-TYPE | 缺少「Content-Type」請求標頭 | 沒有「Content-Type」請求標頭的POST、PUT或PATCH請求。 在此情況下，應用程式伺服器預設應該假設「Content-Type： text/plain； charset=us-ascii」。 許多自動化和惡意請求可能遺失「內容型別」。 |
| 努阿 | 無使用者代理程式 | 許多自動化和惡意請求會使用虛假或遺失的使用者代理程式，使得識別發出請求的裝置型別變得困難。 |
| TORNODE | Tor流量 | Tor是隱藏使用者身分的軟體。 Tor流量尖峰可能表示攻擊者嘗試遮罩其位置。 |
| 資料中心 | 資料中心流量 | 資料中心流量是指源自已識別託管提供者的非自然流量。 這類流量通常不會與真正的一般使用者建立關聯。 |
| NULLBYTE | 空位元組 | Null位元組通常不會出現在請求中，並會指出請求格式錯誤且可能是惡意的。 |
| IMPOSTOR | SearchBot冒名者 | 搜尋機器人冒名者是假扮成Google或Bing搜尋機器人，但不合法的人。 請注意，這並非取決於回應本身，但必須先在雲端中解析，因此不應在預先規則中使用。 |
| PRIVATEFILE | 私人檔案 | 私人檔案通常屬於機密性質，例如Apache `.htaccess` 檔案或可能洩露敏感資訊的設定檔案 |
| 掃描器 | 掃描器 | 識別熱門的掃描服務和工具 |
| RESPONSESPLIT | HTTP回應分割 | 識別何時將CRLF字元提交為應用程式的輸入，以將標頭插入HTTP回應 |
| XML錯誤 | XML編碼錯誤 | POST、PUT或PATCH要求內文，指定為包含「Content-Type」要求標頭中的XML，但包含XML剖析錯誤。 這通常與程式設計錯誤、自動化或惡意請求有關。 |

## 考量事項 {#considerations}

* 建立兩個相衝突的規則時，允許規則將一律優先於區塊規則。 例如，如果您建立規則來封鎖特定路徑，並建立規則來允許一個特定IP位址，則將允許來自封鎖路徑上的該IP位址的請求。

* 如果規則符合併遭到封鎖，CDN會以回應 `406` 傳回碼。

## 範例 {#examples}

以下是一些規則範例。 請參閱 [速率限制區段](#rules-with-rate-limits) 再往下檢視速率限制範例。

**範例 1**

此規則會封鎖來自IP 192.168.1.1的請求：

```
data:
  rules:
    - name: "block-request-from-ip"
      when: { reqProperty: clientIp, equals: "192.168.1.1" }
      action: block
```

**範例 2**

此規則會封鎖路徑上的請求 `/helloworld` 以包含Chrome的使用者代理程式發佈時：

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

**範例3**

此規則會封鎖包含查詢引數的請求 `foo`，但允許來自IP 192.168.1.1的每個請求：

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

**範例4**

此規則會封鎖對/block-me路徑的要求，並封鎖符合SQLI或XSS模式的每個要求：

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

有時候，只有當符合專案在一段時間內超過特定速率時，才希望封鎖符合規則的流量。 設定值 `rateLimit` 屬性會限制符合規則條件的要求速率。

### rateLimit結構 {#ratelimit-structure}

| **屬性** | **類型** | **預設值** | **說明** |
|---|---|---|---|
| 限制 | 10到10000的整數 | 必填 | 每秒觸發規則之要求的要求速率 |
| 視窗 | 整數列舉： 1、10或60 | 10 | 計算請求速率的取樣視窗（以秒為單位） |
| 懲罰 | 從60到3600的整數 | 300 （5分鐘） | 已封鎖相符要求的期間（以秒為單位）（四捨五入至最接近的分鐘） |

### 範例 {#ratelimiting-examples}

範例 1：當請求速率在最近60秒內超過每秒100個請求時，封鎖 `/critical/resource` 60秒

```
- name: rate-limit-example
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit: { limit: 100, window: 60, penalty: 60 }
```

範例2：當要求速率在10秒內超過每秒10個要求時，請將資源封鎖300秒：

```
- name: rate-limit-using-defaults
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit:
    limit: 10
```

## CDN記錄 {#cdn-logs}

AEMas a Cloud Service提供對CDN記錄的存取權，這些記錄可用於使用案例，包括快取命中率最佳化以及設定CDN和WAF規則。 CDN記錄會顯示在Cloud Manager中 **下載記錄檔** 對話方塊，在選取Author或Publish服務時。

如果請求符合規則，則規則的名稱會顯示在rules屬性中，即使動作為「allow」亦然，因此不會封鎖流量。

對CDN的所有請求都會在記錄專案中顯示相符的CDN規則，無論是否為CDN點選、通過或錯過。 不過，WAF規則只會在對CDN的請求中出現，這些請求會視為CDN未命中或通過，而不是CDN點選。

以下範例顯示一個範例 `cdn.yaml` 和兩個CDN記錄專案，且規則屬性中具有非空白值，因為分別符合CDN規則和WAF規則的封鎖請求。


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
"cip": "147.160.230.112",
"rid": "974e67f6",
"host": "example.com",
"url": "/block-me",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=path-rule;waf=;action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=;waf=SQLI;action=blocked"
}
```

### 記錄格式 {#cdn-log-format}

以下是CDN記錄中使用的欄位名稱清單，以及簡短說明。

| **欄位名稱** | **說明** |
|---|---|
| *timestamp* | TLS終止後，要求開始的時間 |
| *ttfb* | 縮寫 *到第一個位元組的時間*. 要求開始的時間間隔，一直到回應主體開始串流處理之前的點。 |
| *cip* | 使用者端IP位址。 |
| *rid* | 用來唯一識別請求的請求標頭值。 |
| *主機* | 預期用於此要求的許可權。 |
| *url* | 完整路徑，包括查詢引數。 |
| *req_mthd* | 使用者端傳送的HTTP方法，例如&quot;GET&quot;或&quot;POST&quot;。 |
| *res_type* | 用於表示資源的原始媒體型別的Content-Type |
| *cache* | 快取的狀態。 可能的值包括「點選」、「未命中」或「通過」 |
| *res_status* | 整數值形式的HTTP狀態碼。 |
| *res_bsize* | 在回應中傳送給使用者端的內文位元組。 |
| *伺服器* | CDN快取伺服器的資料中心。 |
| *多項規則* | CDN規則和waf規則的任何相符規則名稱。<br><br>對CDN的所有請求都會在記錄專案中顯示相符的CDN規則，無論是否為CDN點選、通過或錯過。<br><br>也會指出相符是否導致區塊。 <br><br>例如，「`cdn=;waf=SQLI;action=blocked`&quot;<br><br>如果沒有相符的規則，則為空白。 |
