---
title: 流量篩選規則包括 WAF 規則
description: 設定流量篩選規則，包括 Web 應用程式防火牆 (WAF) 規則。
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
feature: Security
role: Admin
source-git-commit: c54f77a7e0a034bab5eeddcfe231973575bf13f4
workflow-type: tm+mt
source-wordcount: '4582'
ht-degree: 82%

---


# 流量篩選規則包括 WAF 規則 {#traffic-filter-rules-including-waf-rules}

流量篩選規則可用於封鎖或允許 CDN 層的要求，這在以下情境中可能很有用：

* 在新網站上線之前，限制特定網域存取公司內部流量
* 建立速率限制，以減少受到容量 DoS 攻擊的影響
* 防止已知的惡意 IP 位址目標定位您的頁面

這些流量篩選規則中有許多適用於所有AEM as a Cloud Service Sites和Forms客戶。 這些規則稱為&#x200B;*標準流量篩選規則*，主要在要求屬性和要求標題（包括IP、主機名稱、路徑和使用者代理程式）上運作。 標準流量篩選規則包含用來防止流量尖峰的速率限制規則。

流量篩選規則的子類別需要增強的安全性授權或 WAF-DDoS 保護授權。這些強大的規則稱為WAF （Web應用程式防火牆）流量篩選規則(或簡稱&#x200B;*WAF規則*)，可存取本文稍後所述的[WAF旗標](#waf-flags-list)。

流量篩選器規則可以透過 Cloud Manager 設定管道，部署至開發、中繼和生產環境類型。可以使用命令列工具將設定檔案部署至快速開發環境 (RDE) 中。

[按照教學課程進行操作](#tutorial)，快速建立此功能的具體專業知識。

>[!NOTE]
>如需其他有關在內容傳遞網路設定流量的選項，包括編輯請求/回應、宣告重新導向和代理到非 AEM 來源，請參閱[在內容傳遞網路上設定流量](/help/implementing/dispatcher/cdn-configuring-traffic.md)文章。


## 本文的結構方式 {#how-organized}

本文章分為以下幾個章節：

* **流量保護概觀：**&#x200B;了解如何保護您以避免受惡意流量的傷害。
* **設定規則的建議流程：**&#x200B;閱讀關於保護網站的高級方法。
* **設定：**&#x200B;了解如何設定、配置和部署流量篩選規則，包括進階的 WAF 規則。
* **規則語法：**&#x200B;閱讀有關如何在 `cdn.yaml` 設定檔案宣告流量篩選規則。此包括可供所有 Sites 和 Forms 客戶使用的流量篩選規則，以及針對那些授權該功能者所提供的 WAF 規則子類別。
* **規則範例：**&#x200B;查看已宣告的規則範例以協助您進行。
* **速率限制規則：**&#x200B;了解如何使用速率限制規則保護您的網站避免受到大量的攻擊。
* **流量篩選規則警報**：設定警報，以便在觸發規則時收到通知。
* **來源流量尖峰預設警報**：來源出現暗示可能發生 DDoS 攻擊的流量尖峰時收到通知。
* **CDN 日誌：**&#x200B;查看哪些宣告的規則和 WAF 標幟與您的流量相符。
* **儀表板工具：**&#x200B;分析您的 CDN 日誌以提出新的流量篩選規則。
* **推薦的入門規則：**&#x200B;一組可以開始使用的入門規則。
* **教學課程：**&#x200B;有關該功能的實用知識，包括如何使用儀表板工具宣告正確的規則。

## 流量保護概觀 {#traffic-protection-overview}

在目前的數位環境中，惡意流量是一種揮之不去的威脅。Adobe 了解風險的嚴重性，並提供多種方法保護客戶應用程式，以及在發生時減輕攻擊。

在邊緣，Adobe 管理的內容傳遞網路會吸收網路層上的 DoS 攻擊 (第 3 層和第 4 層)，包括洪水攻擊和反射/放大攻擊。

預設情況下，Adobe 會採取措施來防止因超出特定臨界值的意外突發高流量所導致的效能降低。如果有影響網站可用性的 DoS 攻擊，Adobe 的營運團隊會收到警報並採取減輕影響的步驟。

客戶可以透過在不同層的內容傳遞流程設定規則，以採取主動式措施減輕應用程式層攻擊 (第 7 層)。

例如，在 Apache 層，客戶可以設定 [Dispatcher 模組](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-access-to-content-filter)或 [ModSecurity](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection) 以限制對特定內容的存取。

如本文所述，使用 Cloud Manager 的[設定管道](/help/operations/config-pipeline.md)可以將流量篩選規則部署到 Adobe 管理的內容傳遞網路。除了&#x200B;*基於IP位址、路徑和標題等屬性的標準流量篩選規則*，或基於設定速率限制的規則之外，客戶還可以授權稱為&#x200B;*WAF規則*&#x200B;的強大流量篩選規則子類別。

## 建議的流程 {#suggested-process}

以下是制定正確流量篩選規則的高階建議端到端流程：

1. 設定非生產和生產設定管道，如[設定](#setup)章節的敘述。
1. 已授權&#x200B;*WAF流量篩選器規則*&#x200B;的客戶應在Cloud Manager中啟用這些規則。
1. 閱讀並嘗試本教學課程，以具體了解如何使用流量篩選規則，包括 WAF 規則 (若已獲得授權)。本教學課程將引導您將規則部署到開發環境、模擬惡意流量、下載 [CDN 日誌](#cdn-logs)，以及在[儀表板工具](#dashboard-tooling)中進行分析。
1. 將建議的入門規則複製到`cdn.yaml`，並將設定部署至生產環境，並將部分規則部署至記錄模式。
1. 在收集一些流量之後，使用[儀表板工具](#dashboard-tooling)分析結果，以了解是否有任何符合的項目。找出誤判，並進行任何必要的調整，最終在區塊模式中啟用所有入門規則。
1. 如有必要，請根據CDN記錄的分析，新增自訂規則，先在開發環境中使用模擬流量進行測試，然後以記錄模式部署到中繼和生產環境，然後是封鎖模式。
1. 持續監控流量，隨著威脅態勢的發展來變更規則。

## 設定 {#setup}

1. 使用一組流量篩選規則(包括WAF規則)建立檔案`cdn.yaml`。 例如：

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

   請參閱[「使用設定管道」](/help/operations/config-pipeline.md#common-syntax)，取得 `data` 節點上方屬性的描述。`kind` 屬性值應設定為 *CDN*，版本應設定為 `1`。


1. 如果 WAF 規則已獲得授權，您應該在 Cloud Manager 中啟用該功能，如下針對新方案案例和現有方案案例所述。

   1. 若要對新方案設定 WAF，在[新增生產方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)時，請在「**安全性**」標籤中勾選「**WAF-DDOS 防護**」核取方塊。

   1. 若要在現有方案上設定 WAF，[編輯您的方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)並在「**安全性**」標籤隨時取消勾選或勾選「**WAF-DDOS**」選項。

1. 在Cloud Manager中建立設定管道，如[設定管道文章](/help/operations/config-pipeline.md#managing-in-cloud-manager)所述。 管道將參考頂層 `config` 資料夾，並將 `cdn.yaml` 檔案放在下方的某個位置，請參閱「[使用設定管道](/help/operations/config-pipeline.md#folder-structure)」。

## 流量篩選規則語法 {#rules-syntax}

您可以將&#x200B;*流量篩選規則*&#x200B;設定為符合 IPS、使用者代理、要求標頭、主機名稱、地理位置和 URL 等模式。

授權增強式安全性或WAF-DDoS Protection Security產品的客戶，也可以設定一種特殊類別的流量篩選器規則，稱為&#x200B;*WAF流量篩選器規則* (或簡稱&#x200B;*WAF規則*)，其會參考一或多個[WAF旗標](#waf-flags-list)。

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
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

`cdn.yaml` 檔案中流量篩選規則的格式如下所述。請參閱後面章節的一些[其他範例](#examples)，和關於[速率限制規則](#rate-limit-rules)的獨立章節。


| **屬性** | **大部分流量篩選規則** | **WAF 流量篩選規則** | **類型** | **預設值** | **說明** |
|---|---|---|---|---|---|
| 名稱 | X | X | `string` | - | 規則名稱 (64 個字元的長度，只能包含英數字元和 -) |
| 時間 | X | X | `Condition` | - | 基本結構是：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[請參閱下面的條件結構語法，其中會說明 getter、述詞以及結合多個條件的方式。](#condition-structure) |
| 動作 | X | X | `Action` | 記錄 | 記錄、允許、封鎖或動作物件。預設為記錄 |
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
| reqProperty | `string` | 要求屬性。<br><br>之一：<br><ul><li>`path`：傳回不包含查詢參數的 URL 完整路徑。(使用未轉義變體的 `pathRaw`)</li><li>`url`：傳回含查詢參數的完整 URL。(使用未轉義變體的 `urlRaw`)</li><li>`queryString`：傳回 URL 的查詢部分</li><li>`method`：傳回要求中所使用的 HTTP 方法。</li><li>`tier`：傳回 `author`、`preview` 或 `publish` 其中之一。</li><li>`domain`：傳回小寫的網域屬性 (如 `Host` 標頭的定義)</li><li>`clientIp`：傳回用戶端 IP 位址。</li><li>`forwardedDomain`：傳回`X-Forwarded-Host` 標頭內定義的第一個小寫網域</li><li>`forwardedIp`：傳回 `X-Forwarded-For` 標頭中的第一個 IP 位址。</li><li>`clientRegion`：傳回國家/地區細分代碼，指出客戶所在的區域，如 [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) 所述。</li><li>`clientCountry`：傳回兩個字母的代碼 ([區域指示符](https://en.wikipedia.org/wiki/Regional_indicator_symbol))，可識別客戶位於哪個國家/地區。</li><li>`clientContinent`：傳回兩個字母的代碼 (AF、AN、AS、EU、NA、OC、SA)，可識別客戶位於哪個洲。</li><li>`clientAsNumber`：傳回與用戶端 IP 相關的[自治系統](https://en.wikipedia.org/wiki/Autonomous_system_(網際網路))編號。</li><li>`clientAsName`：傳回與自治系統編號相關的名稱。</li></ul> |
| reqHeader | `string` | 傳回具有指定名稱的要求標頭 |
| queryParam | `string` | 傳回具有指定名稱的查詢參數 |
| reqCookie | `string` | 傳回具有指定名稱的 Cookie |
| postParam | `string` | 從要求內文傳回具有指定名稱的 Post 參數。只有當內文為內容類型 `application/x-www-form-urlencoded` 時才有效 |

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
| **存在** | `boolean` | 設定為 true 且屬性存在，或設為 false 且屬性不存在時為 true |

**附註**

* 要求屬性 `clientIp` 只能與以下述詞一起使用：`equals`、`doesNotEqual`、`in`、`notIn`。`clientIp` 也可以比對 IP 範圍 (在使用 `in` 和 `notIn` 述詞時)。以下範例將實施一項條件，以評估用戶端 IP 是否在 192.168.0.0/24 的 IP 範圍內 (即從 192.168.0.0 到 192.168.0.255)：

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* Adobe 建議使用 [regex101](https://regex101.com/)，以及在搭配規則運算式時使用 [Fastly Fiddle](https://fiddle.fastly.dev/)。您也可以從 [fastly 文件 - Fastly VCL 中的規則運算式](https://www.fastly.com/documentation/reference/vcl/regex/#best-practices-and-common-mistakes)，了解 Fastly 如何處理規則運算式的詳細資訊。


### 動作結構 {#action-structure}

一個`action`可以是指定動作 (允許、封鎖或記錄) 的字串，也可以是由動作類型 (允許、封鎖或記錄) 以及 wafFlags 和/或狀態等選項組成的物件。

**動作類型**

動作根據下表中的類型排定優先順序，以反映動作的執行順序：

| **名稱** | **允許的屬性** | **含義** |
|---|---|---|
| **允許** | `wafFlags` (可選)，`alert` (可選) | 如果沒有 wafFlags，則停止進一步處理規則並繼續提供回應。如果有 wafFlags，這將停用指定的 WAF 保護並繼續進一步處理規則。<br>如果已指定要發送警報，則當規則在 5 分鐘內觸發 10 次時，系統將發送行動中心通知。一旦觸發特定規則的警報，直到第二天 (UTC) 它才會再次觸發。 |
| **封鎖** | `status, wafFlags` (可選且互斥)，`alert` (可選) | 如果沒有 wafFlags，則繞過所有其他屬性來傳回 HTTP 錯誤，錯誤代碼由狀態屬性定義或預設為 406。如果有 wafFlags，這將啟用指定的 WAF 保護並繼續進一步處理規則。<br>如果已指定要發送警報，則當規則在 5 分鐘內觸發 10 次時，系統將發送行動中心通知。一旦觸發特定規則的警報，直到第二天 (UTC) 它才會再次觸發。 |
| **記錄** | `wafFlags` (可選)，`alert` (可選) | 記錄規則已觸發的事實，否則不影響處理作業。wafFlags 沒有影響。<br>如果已指定要發送警報，則當規則在 5 分鐘內觸發 10 次時，系統將發送行動中心通知。一旦觸發特定規則的警報，直到第二天 (UTC) 它才會再次觸發。 |

### WAF 標幟清單 {#waf-flags-list}

在可授權 WAF 流量篩選規則中可以使用的 `wafFlags` 屬性，可以參考以下內容：

#### 惡意流量

| **標幟 ID** | **標幟名稱** | **說明** |
|---|---|---|
| 攻擊 | 攻擊 | 與惡意流量（SQLI、CMDEXE、XSS等）相關的標幟彙總。 請參閱[建議的WAF規則一節](#recommended-waf-starter-rules)，瞭解如何有效使用此標幟。 |
| ATTACK-FROM-BAD-IP | 來自惡意 IP 的攻擊 | 類似於ATTACK旗標，但使用`BAD-IP`旗標進行「邏輯與」標示，因此如果要求符合ATTACK和BAD-IP，則會標示要求。 請參閱[建議的WAF規則一節](#recommended-waf-starter-rules)，瞭解如何有效使用此標幟。 |
| SQLI | SQL 注入 | SQL 注入指試圖透過執行任意資料庫查詢以取得對應用程式的存取權或獲取特權資訊。 |
| BACKDOOR | 後門 | 後門訊號指試圖決定系統是否存在常見後門檔案的要求。 |
| CMDEXE | 命令執行 | 命令執行指試圖透過由使用者輸入的任意系統命令獲取控制或毀損目標系統。 |
| CMDEXE-NO-BIN | 命令執行 (除`/bin/`以外) | 由於 AEM 架構，提供同 `CMDEXE` 等級的保護，但停用 `/bin` 的誤報。 |
| XSS | 跨網站指令碼 | 跨網站指令碼指試圖透過惡意 JavaScript 程式碼劫持使用者的帳戶或 Web 瀏覽工作階段。 |
| 周遊 | 目錄周遊 | 目錄周遊指試圖瀏覽整個系統中的特權檔案，期望能獲取敏感資訊。 |
| USERAGENT | 攻擊工具 | 攻擊工具指使用自動化軟體識別安全漏洞或試圖惡意探索發現的漏洞。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻擊會試圖惡意探索出現在 2.16.0 之前的 Log4J 版本中的 [Log4Shell 漏洞](https://zh.wikipedia.org/wiki/tw/Log4Shell) |
| CVE | CVE | 可識別 CVE 的旗標。一律與 `CVE-<CVE Number>` 旗標結合使用。請聯絡 Adobe 以深入了解 Adobe 能保護您免受哪些 CVE 侵害。 |

#### 可疑流量

| **標幟 ID** | **標幟名稱** | **說明** |
|---|---|---|
| ABNORMALPATH | 異常路徑 | 異常路徑指原始路徑和標準化路徑不同 (例如：`/foo/./bar` 會標準化為 `/foo/bar`) |
| 惡意-IP | 惡意 IP | 識別來自已知為惡意的IP位址的請求，因為包含在資料集（例如`SANS`和`TORNODE`）中，或根據WAF先前偵測到的惡意行為 |
| BHH | 錯誤跳躍標頭 | 錯誤跳躍標頭指透過格式錯誤的傳輸編碼 (TE) 或內容長度 (CL) 標頭或格式正確的 TE 和 CL 標頭進行的 HTTP 走私嘗試 |
| CODEINJECTION | 程式碼注入 | 程式碼注入是指試圖透過由使用者輸入的任意應用程式碼命令獲取控制或毀損目標系統。 |
| 已壓縮 | 偵測到壓縮 | POST 要求內文被壓縮，並且無法檢查。例如，如果指定了 `Content-Encoding: gzip` 請求標頭，且 POST 內文並非純文字。 |
| RESPONSESPLIT | HTTP 回應拆分 | 會識別何時將 CRLF 字元作為輸入提交給應用程式，以將標頭注入 HTTP 回應 |
| NOTUTF8 | 無效的編碼 | 無效的編碼可能會導致伺服器將要求中的惡意字元翻譯為回應，進而導致拒絕服務或 XSS |
| MALFORMED-DATA | 要求內文中格式錯誤的資料 | 根據「Content-Type」要求標頭，格式錯誤的 POST、PUT 或 PATCH 要求內文。例如，如果指定了「Content-Type: application/x-www-form-urlencoded」要求標頭並包含 json 的 POST 內文。這經常是程式設計錯誤、自動化或惡意要求。需要代理程式 3.2 或更高版本。 |
| SANS | 惡意的 IP 流量 | [SANS 網際網路風暴中心](https://isc.sans.edu/)進行惡意活動的被舉報 IP 位址清單 |
| NO-CONTENT-TYPE | 缺少「Content-Type」要求標頭 | 沒有「Content-Type」要求標頭的 POST、PUT 或 PATCH 要求。在此案例中，預設情況下應用程式伺服器應假設「Content-Type: text/plain; charset=us-ascii」。許多自動化和惡意要求可能會缺少「內容類型」。 |
| NOUA | 沒有使用者代理程式 | 指示請求不包含「使用者代理」標頭或未設定的標頭值。 |
| NULLBYTE | 空位元 | 空位元通常不會出現在要求中，因為這表示該要求的格式錯誤且可能是惡意的。 |
| OOB-DOMAIN | 頻外網域 | 頻外網域通常用於滲透測試期間，以識別出允許網路存取的漏洞所在。 |
| PRIVATEFILE | 私人檔案 | 私人檔案在本質上屬於機密性，例如 Apache `.htaccess` 檔案或可能洩漏敏感資訊的設定檔案 |
| SCANNER | 掃描程式 | 可識別熱門的掃描服務和工具 |

#### 雜項流量

| **標幟 ID** | **標幟名稱** | **說明** |
|---|---|---|
| DATACENTER | 資料中心 | 將請求識別為來自已知的主機提供者。這種類型的流量通常和真正的一般使用者無關。 |
| DOUBLEENCODING | 雙重編碼 | 雙重編碼會檢查雙重編碼 html 字元的規避技術 |
| JSON-ERROR | JSON 編碼錯誤 | 指定為在「Content-Type」要求標頭中包含 JSON 但包含 JSON 剖析錯誤的 POST、PUT 或 PATCH 要求內文。這經常和程式設計錯誤或自動化亦或惡意要求有關。 |
| TORNODE | Tor 流量 | Tor 是可隱藏使用者身份的軟體。Tor 流量激增可能表示有攻擊者試圖掩飾其位置。 |
| XML-ERROR | XML 編碼錯誤 | 指定為在「Content-Type」要求標頭中包含 XML 但包含 XML 剖析錯誤的 POST、PUT 或 PATCH 要求內文。這經常和程式設計錯誤或自動化亦或惡意要求有關。 |

## 考量事項 {#considerations}

* 建立兩個衝突規則時，允許的規則總是優先於封鎖規則。例如，如果您建立一條封鎖特定路徑的規則，又建立一條允許特定 IP 位址的規則，則來自遭封鎖路徑上的該 IP 位址的要求會受到允許。

* 如果規則相符並遭封鎖，CDN 會以 `406` 傳回代碼回應。

* 設定檔不應包含密碼，因為任何有權存取 git 存放庫的人都可以讀取。

* 在 Cloud Manager 中定義的 IP 允許清單優先於流量篩選規則。

* WAF 規則的符合項目只會出現在 CDN 未命中和通過的 CDN 記錄中，而非點擊的記錄中。

## 規則範例 {#examples}

下面是一些規則範例。如需進一步探討速率限制規則的範例，請參閱[「速率限制」一節](#rate-limit-rules)。

**範例 1**

此規則會封鎖來自 **IP192.168.1.1** 的請求：

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

此規則會封鎖含有查詢參數 `foo` 的發佈請求，但會允許來自 IP 192.168.1.1 的每項請求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when:
          allOf:
            - { queryParam: url-param, equals: foo }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**範例 4**

此規則會封鎖發佈時對路徑 `/block-me` 的要求，並封鎖和 `SQLI` 或 `XSS` 模式相符的每個要求。此範例包含 WAF 流量篩選規則，其參考了 `SQLI` 和 `XSS`[WAF 標幟](#waf-flags-list)，因此需要單獨的授權。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
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

## 速率限制規則

有時，如果流量超過傳入要求的特定速率 (基於特定條件)，則需要封鎖流量。設定 `rateLimit` 屬性的值會限制那些和規則條件相符的要求的速率。

速率限制規則不能參考 WAF 標幟。它們提供給所有網站和表單客戶使用。

速率限制是根據 CDN POP 計算的。例如，假設蒙特婁、邁阿密和都柏林的 POP 流量分別為每秒 80、90 和 120 個請求。並且，速率限制規則設定在以 100 為限。在這種情況下，只有到都柏林的流量會受到速率限制。

速率限制是根據到達邊緣的流量、到達來源的流量或錯誤數量進行評估。

### rateLimit 結構 {#ratelimit-structure}

| **屬性** | **類型** | **預設** | **含義** |
|---|---|---|---|
| 限制 | 10 到 10000 之間的整數 | 必要 | 觸發規則的要求速率是以每秒要求數為單位 (per CDN POP)。 |
| 視窗 | 整數列舉：1、10 或 60 | 10 | 計算要求速率的取樣期間 (秒數)。計數器的準確性取決於時間範圍的大小 (範圍愈大，準確度愈高)。例如，1 秒時間範圍的準確度預計為 50%，60 秒時間範圍的準確度預計為 90%。 |
| 懲罰 | 60 到 3600 之間的整數 | 300 (5 分鐘) | 封鎖相符要求時間的秒數 (四捨五入到最接近的分鐘)。 |
| 計數 | 所有、擷取、錯誤 | 全部 | 根據邊緣流量 (全部)、來源流量 (擷取) 或錯誤數量 (錯誤) 進行評估。 |
| groupBy | array[Getter] | 無 | 速率限制器計數器將由一組要求屬性 (例如 clientIp) 彙總。 |

### 範例 {#ratelimiting-examples}

**範例 1**

當在過去 10 秒內超過平均 60 個要求/秒時 (per CDN POP)，此規則將封鎖用戶端 5 毫秒：

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
        count: all
        groupBy:
          - reqProperty: clientIp
      action: block
```

**範例 2**

當在 10 秒時間內每秒對來源平均發出超過 100 個要求 (每個 CDN POP)，系統就會封鎖在 path /critical/resource 上的要求達 60 秒：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when:
          allOf:
            - { reqProperty: path, equals: /critical/resource }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
        rateLimit: { limit: 100, window: 10, penalty: 60, count: fetches }
```

## CVE 規則 {#cve-rules}

如果 WAF 已獲得授權，Adobe 就會自動套用封鎖規則來防範許多已知的 CVE (常見漏洞和暴露)，而新的 CVE 可能會在發現後立即新增。客戶不應也不需自行設定 CVE 規則。

如果流量請求符合 CVE，就會顯示在對應的內容傳遞網路記錄項目中。

如果對特定 CVE 有疑問或您的組織想要停用特定 CVE 規則，請聯絡 Adobe 支援。

## 流量篩選規則警報 {#traffic-filter-rules-alerts}

規則可設定為在 5 分鐘時間內觸發十次時發送行動中心通知。當出現某些流量模式時，此類規則會向您發送警報，以便您採取任何必要的措施。一旦觸發特定規則的警報，直到第二天 (UTC) 它才會再次觸發。

了解更多關於[行動中心](/help/operations/actions-center.md)，包括如何設定接收電子郵件所需的通知設定檔。

![行動中心通知](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


警報屬性可以套用到所有動作類型 (允許、封鎖、記錄) 的動作節點。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
          alert: true
```

## 來源流量尖峰預設警報 {#traffic-spike-at-origin-alert}

有大量流量傳送到來源，且其中來自相同 IP 位址的請求臨界值相當高，因而暗示可能發生 DDoS 攻擊時，將傳送[行動中心](/help/operations/actions-center.md)電子郵件通知。

如果達到此臨界值，Adobe 將阻止來自該 IP 位址的流量，但建議採取其他措施來保護您的來源，包括設定速率限制流量篩選規則，以便在臨界值較低時阻擋流量尖峰。請參閱[「使用流量篩選器規則封鎖 DoS 和 DDoS 攻擊」教學課程](#tutorial-blocking-DDoS-with-rules)以瞭解引導式逐步說明。

此警報預設為啟用，但可以將 *defaultTrafficAlerts* 屬性設定為 False 來加以停用。一旦觸發特定規則的警報，直到第二天 (UTC) 它才會再次觸發。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
   defaultTrafficAlerts: false
```

## CDN 記錄 {#cdn-logs}

AEM as a Cloud Service 會提供對 CDN 記錄的存取權，這對於包括快取命中率最佳化以及設定流量篩選規則等使用案例都非常有幫助。選取作者或發佈服務時，CDN 記錄會顯示在 Cloud Manager **下載記錄**&#x200B;對話框中。

CDN 記錄可能會延遲最多五分鐘。

`rules` 屬性描述要符合哪些流量篩選規則，並具有以下模式：

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例如：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

這些規則的行為方式如下：

* 任何符合規則的客戶宣告規則名稱會列於 `match` 屬性中。
*  `action` 屬性會確定規則是阻止、允許或記錄。
* 如果 WAF 已取得授權並啟用， `waf` 屬性會列出所有偵測到的 WAF 標幟 (例如 SQLI)。無論 WAF 標幟是否列在任何規則中，都是如此。這是提供深入分析要宣告的潛在新規則。
* 如果沒有客戶宣告的規則相符且沒有 WAF 規則相符，則 `rules` 屬性為空。

如前所述，WAF 規則的符合項目只會出現在 CDN 未命中和通過的 CDN 記錄中，而非點擊的記錄中。

以下範例顯示了一個範例 `cdn.yaml` 和兩個 CDN 記錄條目：


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
| *timestamp* | TLS 終止後要求開始的時間。 |
| *ttfb* | *首位元組時間 (Time To First Byte)* 的縮寫。發出要求開始到回應內文開始串流的時間之間的時間間隔。 |
| *cli_ip* | 用戶端 IP 位址。 |
| *cli_country* | 雙字母 [ISO 3166-1](https://zh.wikipedia.org/wiki/tw/ISO_3166-1) 用戶端國家/地區的 alpha-2 國家/地區代碼。 |
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

## 儀表板工具 {#dashboard-tooling}

Adobe 提供了將儀表板工具下載到您電腦上的機制，以擷取透過 Cloud Manager 下載的 CDN 日誌。使用此工具，您可以分析流量，以協助制定要宣告的適當流量篩選規則，包括 WAF 規則。

儀表板工具可以直接從 [AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling) GitHub 存放庫原地複製。

[教學課程](#tutorial)可提供如何使用儀表板工具的具體說明。

## 建議的入門者規則 {#recommended-starter-rules}

Adobe建議從下方的流量篩選規則開始，然後隨著時間推移逐漸改良。 *標準規則*&#x200B;可與Sites或Forms授權搭配使用，而&#x200B;*WAF規則*&#x200B;需要增強式安全性或WAF-DDoS保護授權。

### 建議的標準規則 {#recommended-nonwaf-starter-rules}

從下列規則開始：

1. 速率限制（記錄模式）：
   * 記錄來自指定IP的流量超過速率限制。 在驗證未收到任何警報後，將變更為封鎖模式；如果收到警報，則表示限制值太低。
2. 特定國家/地區（區塊模式）：
   * 封鎖來自特定國家/地區的流量（根據您的業務需求修改國家/地區代碼）

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds an average of 100 req/sec to origin on a time window of 10sec
    - name: limit-origin-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 100
        window: 10
        count: fetches
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    #  Block client for 5m when it exceeds an average of 500 req/sec on a time window of 10sec
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 500
        window: 10
        count: all
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
      alert: true
    # Block requests coming from OFAC countries
    - name: ofac-countries
      when:
        allOf:
          - { reqProperty: tier, in: ["author", "publish"] }
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

### 建議的WAF規則 {#recommended-waf-starter-rules}

將下列規則新增至您現有的設定：

1. ATTACK-FROM-BAD-IP旗標（封鎖模式）：
   * 立即封鎖同時符合可疑模式(包括[WAF旗標清單](#waf-flags-list)中的數個)且源自已知為惡意的IP位址的流量。
   * ATTACK-FROM-BAD-IP旗標本身就同時符合兩個條件（模式比對和已知的惡意IP），將誤判的風險降到最低。 因此，您可以安全地立即在封鎖模式中套用此規則。
2. 攻擊旗標（記錄模式）：
   * 一開始會記錄（而不是封鎖）符合可疑模式，但並非源自已知惡意IP位址的流量。 這種記錄而非封鎖的謹慎方法有助於避免無意中封鎖合法流量（誤報）。
   * 部署此規則後，請仔細分析CDN記錄，確認未正確標幟合法請求。 一旦您確定沒有合法的流量受到影響，請切換到封鎖模式。

>[!NOTE]
> 我們的經驗顯示，與ATTACK旗標相關的誤判並不多見。 因此，即使IP位址未知為惡意，立即封鎖所有可疑流量並隨後使用CDN記錄分析來識別和引入合法流量的允許規則可能是一種實用的策略。 每個組織都應評估自己的風險承受能力，權衡加強保護的好處，以及無意中封鎖合法請求的風險。
>

```
    # blocks likely attack traffic, which also comes from suspected IPs
    - name: attacks-from-bad-ips-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: block
        wafFlags:
          - ATTACK-FROM-BAD-IP
    # log likely attack traffic, and later switch to block mode if false positives aren't observed
    - name: attacks-from-any-ips-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - ATTACK
```

### 舊版建議WAF規則 {#previous-waf-starter-rules}

2025年7月之前，Adobe建議使用下列的WAF規則，這些規則在抵禦惡意流量方面仍然有效且有效。 請參閱教學課程，以瞭解移轉至新建議規則的相關考量事項。

<details>
  <summary>展開以檢視舊版建議的WAF規則。</summary>

```
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - TRAVERSAL
          - CMDEXE-NO-BIN
          - XSS
          - LOG4J-JNDI
          - BACKDOOR
          - USERAGENT
          - SQLI
          - SANS
          - TORNODE
          - NOUA
          - SCANNER
          - PRIVATEFILE
          - NULLBYTE
```
</details>

## 教學課程 {#tutorial}

完成[一系列教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview)，以取得有關流量篩選器規則(包括WAF規則)的實用知識及經驗。

教學課程包括：

* 標準和WAF流量篩選規則概觀
* 設定建議的標準和WAF流量篩選規則以封鎖攻擊，包括拒絕服務(DoS)和其他威脅
* 使用Cloud Manager設定管道部署規則
* 使用工具模擬惡意流量來測試規則
* 使用記錄分析工具分析結果
* 最佳實務




