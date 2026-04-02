---
title: 網路連線測試
description: 使用Cloud Manager中的網路連線測試來驗證進階網路和VPN設定，然後再在環境中啟用網路。
feature: Security
role: Admin
source-git-commit: b29b3a980a0bc1c619fb23c52acda79fae9bf945
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 2%

---


# 網路連線測試 {#network-connectivity-test}

**網路連線測試**&#x200B;是一種Cloud Manager診斷工具，可讓您在環境中啟用進階網路之前，以及在上線之前，先驗證進階網路和VPN設定。 使用它來驗證AEM必須連線的主機與連線埠（包括內部或私用端點）是否可透過進階網路將使用的相同連線路徑連線。

測試從屬於您程式的「進階網路」設定的&#x200B;**輸出Proxy基礎結構**&#x200B;執行，而不是從「作者」或「發佈」Pod執行。 它會使用與進階網路作用中時AEM所使用的相同輸出網路路徑。 該設計對&#x200B;**VPN**&#x200B;情境特別有用：您可在上線之前確認私人或內部部署系統的DNS解析、網路路由、防火牆規則和服務可用性。

如需布建VPN、專用輸出IP或彈性連線埠輸出的背景，請參閱[為AEM as a Cloud Service設定進階網路](/help/security/configuring-advanced-networking.md)。

>[!IMPORTANT]
>
>成功的連線測試證明「進階網路」的網路路徑可以到達您的目標。 您的應用程式程式碼仍必須設定為視需要使用進階網路Proxy （例如，與Proxy相關的環境變數和連線埠轉送）。 如果程式碼繞過Proxy，即使測試通過，您也可能看不到來自預期輸出路徑的流量。

## 何時使用此工具 {#when-to-use}

* 在&#x200B;**之後，在**&#x200B;程式&#x200B;**層級和**&#x200B;之前&#x200B;**或在**&#x200B;環境&#x200B;**上啟用它時，建立進階網路**。
* 驗證&#x200B;**VPN**&#x200B;與您操作的私人或內部部署系統（例如內部主機名稱或私人IP位址）的連線。
* 當服務未如預期回應時，縮小防火牆或路由問題的DNS問題範圍。

>[!NOTE]
>
>此工具適用於使用進階網路（VPN、專用輸出IP或彈性連線埠輸出）的程式。 它不是沒有進階網路的標準AEM連線能力的一般用途測試。

## 先決條件 {#prerequisites}

* Cloud Manager計畫。
* 已為程式建立進階網路基礎結構（請參閱[設定進階網路](/help/security/configuring-advanced-networking.md)）。

## 如何執行測試 {#how-to-run-a-test}

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登入Cloud Manager並開啟您的組織和程式。
1. 開啟程式的&#x200B;**環境**&#x200B;索引標籤。 在左側邊欄中，選取&#x200B;**網路基礎結構**。

1. 在&#x200B;**網路基礎結構**&#x200B;頁面上，在資料表中找出您的基礎結構。 請選取資料列以開啟測試體驗，或開啟資料列動作功能表（![水準省略符號資料列動作功能表的Adobe頻譜小圖示](assets/ellipsis.svg)），然後選擇&#x200B;**測試**。

   ![Cloud Manager程式環境區域，包含用來啟動網路連線測試的網路基礎結構表格、基礎結構列和列動作功能表](assets/network-connectivity-test-cloud-manager-open-test-from-infrastructure-list.png)

1. **網路測試**&#x200B;對話方塊開啟。 輸入&#x200B;**主機**&#x200B;和&#x200B;**連線埠**，選取&#x200B;**測試**，然後在結果區域中檢閱DNS解析、連線埠開啟、HTTP連線能力及連線能力。 選擇性動作（例如&#x200B;**複製到剪貼簿**&#x200B;和最近的測試歷史記錄）會出現在對話方塊中。 請參閱[瞭解結果](#understanding-results)，瞭解如何解譯每個區段。

   ![Cloud Manager網路連線測試對話方塊，包含主機和連線埠欄位、測試動作，以及DNS解析、連線埠開啟、HTTP連線及連線能力的結果](assets/network-connectivity-test-cloud-manager-results-dialog.png)

### 輸入欄位 {#input-fields}

| 欄位 | 說明 | 範例 |
| --- | --- | --- |
| **主機** | AEM應到達之服務的主機名稱或IP位址。 | `internal-api.example.com`、`10.0.1.50` |
| **連線埠** | 目標主機上的TCP連線埠(1-65535)。 通用值可能會出現在捷徑清單中（例如，80、443、587、22）。 | `443` |

### 步驟 {#test-steps}

1. 輸入&#x200B;**主機**&#x200B;和&#x200B;**連線埠**。
1. 選取&#x200B;**測試**。 結果通常會在幾秒內顯示。
1. 選用：使用&#x200B;**複製到剪貼簿**&#x200B;來擷取完整的JSON結果（適用於支援案例）。
1. 可能會列出最近的測試以快速重新執行。

## 瞭解結果 {#understanding-results}

此工具會報告多個維度。 它們一起說明目標是否可以從進階網路連線，以及HTTP感知檢查的行為方式。

### DNS 解析 {#dns-resolution}

| 結果 | 含義 |
| --- | --- |
| `ips: ["10.0.1.50"]` | DNS解析成功。 主機名稱會使用與您的進階網路組態關聯的解析器解析為列出的IP位址。 |
| `error: "DNS resolution error: ..."` | DNS解析失敗。 設定的DNS伺服器無法解析主機名稱（名稱錯誤、無法連線解析器、記錄遺失及類似原因）。 |

>[!NOTE]
>
>如果您輸入&#x200B;**數值IP**&#x200B;而不是主機名稱，則會略過該值的DNS解析，並直接使用IP。

### 連接埠開啟 {#port-open}

| 結果 | 含義 |
| --- | --- |
| `Yes` / true | TCP連線成功 — 連線埠已開啟並接受連線。 |
| `No` / false | 連線埠已關閉、被防火牆篩選或主機無法連線。 |

### HTTP 連線 {#http-connectivity}

已在&#x200B;**每個連線埠**&#x200B;上嘗試HTTP/HTTPS要求。 工具一律會先嘗試&#x200B;**HTTPS**，然後回溯為&#x200B;**HTTP**。 如果兩者皆不運作，則結果會對應至簡短、可讀的&#x200B;**錯誤**&#x200B;訊息（請參閱下表）。

**成功輸出**

| 輸出 | 含義 |
| --- | --- |
| `protocol: "https"`、`status_code: 200`、`reason: "200 OK"` | HTTPS連線成功。 |
| `protocol: "http"`、`status_code: 301`、`reason: "301 Moved Permanently"` | HTTP連線成功；服務正在重新導向（通常是HTTPS）。 這是正常現象。 |

**已分類的錯誤輸出**

| 錯誤 | 注意 | 含義 |
| --- | --- | --- |
| `"Not an HTTP/HTTPS service"` | `"The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."` | 連線埠已開啟，但服務不會說HTTP。 資料庫、SFTP、自訂TCP和類似服務都會發生這種情況。 |
| `"Connection refused"` | `"The port is not accepting connections. Verify the service is running and listening on this port."` | 這個連線埠沒有正在接聽的專案。 |
| `"Connection timed out"` | `"The connection timed out. Check firewall rules and network routing."` | 防火牆或路由問題導致連線無法進行。 |
| `"No IPs resolved for host"` | — | dns解析失敗；無法測試HTTP。 |

>[!NOTE]
>
>來自目標服務的任何HTTP狀態代碼（例如，`200`、`301`、`302`、`403`、`404`或`500`）都是連線的&#x200B;**成功訊號**，這表示&#x200B;**網路路徑**&#x200B;有效。 狀態代碼反映服務本身的回應，而非整體網路健康狀態。 對於非HTTP服務，工具會指出&#x200B;**不是HTTP/HTTPS服務**；使用&#x200B;**連線埠開啟**&#x200B;和&#x200B;**可連線性**&#x200B;作為這些服務的可靠指標。

### 可觸及性 {#reachability}

| 結果 | 含義 |
| --- | --- |
| **可連線** | 目標主機和連線埠可從進階網路基礎架構連線。 網路設定正確。 |
| **無法連線：無法存取連線埠** | DNS解析成功，但TCP到連線埠沒有成功。 這通常是防火牆或路由問題。 |
| **無法連線： DNS解析失敗** | 無法使用您的設定解析主機名稱。 這表示DNS設定有問題。 |

### 多個DNS解析器 {#multiple-dns-resolvers}

如果您的進階網路基礎結構定義&#x200B;**多個DNS解析器**：

* 當&#x200B;**所有解析器傳回相同結果**&#x200B;時，您會看到標示為&#x200B;**的**&#x200B;單一合併`default`結果。
* 當解析程式傳回&#x200B;**個不同的結果**&#x200B;時，每個解析程式的結果會分別顯示&#x200B;**個** （標示為`resolver_1`、`resolver_2`等）、**和解析程式IP**，所以您可以檢視哪個DNS伺服器造成不一致。

## 疑難排解 {#troubleshooting}

以下案例會將您在工具中可能看到的與縮小原因的步驟配對。 如需說明相同情況的完整&#x200B;**複製到剪貼簿** JSON，請參閱[輸出範例](#example-outputs)。

### DNS解析失敗 {#dns-failed}

#### 輸出

主機名稱未使用您的進階網路DNS設定來解析，因此工具無法測試連線埠。 在結果檢視中，**DNS解析**&#x200B;顯示錯誤字串，且&#x200B;**可連線性**&#x200B;報告DNS失敗：

```
DNS Resolution: error: "DNS resolution error: ..."
Reachability: "Unreachable: DNS resolution failed"
```

#### 建議

1. **驗證主機名稱是否正確** — 檢查錯字與您是否使用預期的&#x200B;**DNS區域** （錯誤的區域是常見的錯誤）。
1. 請確定&#x200B;**您的DNS解析器** （在網路基礎結構中設定的解析器）可從進階網路CIDR範圍&#x200B;**（工具和AEM用於傳出檢查的相同位址空間）連線**。 如果您依賴私人DNS，這些伺服器必須可以透過VPN通道或路由公開給進階網路的網路位址空間連線。
1. **確認您設定的DNS伺服器可以解析主機名稱** — Advanced Networking僅使用&#x200B;**僅**&#x200B;網路基礎結構設定中定義的解析器，**不**&#x200B;公用DNS （例如`8.8.8.8`）。 如果您的內部DNS沒有該主機名稱的記錄，則解析會失敗。
1. **對於VPN設定：**&#x200B;確認DNS伺服器IP位址位於VPN位址空間內（建立通道的遠端網路CIDR）。 無法從「進階網路」連線到未透過VPN通道路由之子網路上的解析器。

### DNS可以運作，但無法存取連線埠 {#dns-ok-port-blocked}

#### 輸出

此工具可以解析主機，但是連線埠的TCP無法成功。 摘要通常如下所示：

```
DNS Resolution: ips: ["10.0.1.50"]
Port Open: No
Reachability: "Unreachable: Port not accessible"
```

#### 建議

1. **檢閱目標服務上的防火牆和允許清單規則** — 必須允許來自進階網路基礎結構CIDR範圍的傳入流量（以及AEM使用的輸出IP位址）。 如果您使用VPN，請根據您的設計需要包含遠端網路CIDR。
1. **確認服務正在執行**，且&#x200B;**正在聆聽您輸入測試的主機與連線埠**。
1. **對於VPN設定：**&#x200B;確認通道已啟動、路由到達目標子網路，且目標位址位於透過VPN傳送的遠端網路位址空間。
1. 在您的基礎結構上，檢閱&#x200B;**網路安全性群組(NSG)、安全性規則或同等的專案**，這些專案可能會封鎖進階網路與目標之間的連線埠。
1. **確認連線埠號碼** — 確定處理序確實在聆聽您正在測試的連線埠。

### 測試顯示可連線，但AEM未連線 {#reachable-but-aem-fails}

#### 輸出

連線檢查本身成功。 簡短的摘要通常如下所示：

```
Port Open: Yes
Reachability: "Reachable"
```

這個結果表示從進階網路到您測試的主機與連線埠的路徑是開放的。 不保證AEM應用程式流量會使用該路徑：當您的程式碼執行時，服務記錄檔可能不會顯示來自您預期輸出IP的請求。

#### 建議

1. **應用程式程式碼必須設定為使用Proxy**。 連線測試證實網路路徑有效，但AEM必須明確透過&#x200B;**進階網路Proxy**&#x200B;路由要求（例如，透過&#x200B;**`AEM_PROXY_HOST`**&#x200B;環境變數）。 如果程式碼在沒有Proxy的情況下直接連線，流量不會流經進階網路基礎結構。
1. **檢閱HTTP使用者端中的Proxy設定** - HTTP使用者端應使用相同的Proxy設定（`AEM_PROXY_HOST`和適用的連線埠轉送）。
1. **在**&#x200B;環境&#x200B;**層級驗證進階網路的連線埠轉送設定**：在`portForwards`中，每個專案都必須將&#x200B;**`portOrig`**&#x200B;對應到右側&#x200B;**`portDest`**&#x200B;目標主機&#x200B;**上的**。 **`portOrig`**&#x200B;是您的AEM應用程式程式碼透過Proxy開啟輸出連線時，所連線至&#x200B;**的**&#x200B;連線埠。 **`portDest`**&#x200B;是遠端處理序正在接聽的目標服務&#x200B;**上的**&#x200B;實際連線埠。 **目標主機**&#x200B;是轉送中所使用的服務&#x200B;**的**&#x200B;主機名稱或位址。 這三者都必須符合寫入應用程式以連線的方式。
1. **檢查`nonProxyHosts`**。 如果目標主機列於該處，則要求略過該主機的Proxy **，且不會遵循您驗證的進階網路路徑。**

### HTTP顯示錯誤，但連線埠已開啟 {#http-error-port-open}

#### 輸出

TCP成功，但HTTP/HTTPS探查仍報告失敗。 摘要通常如下所示：

```
Port Open: Yes
HTTP Connectivity: error: "Connection error: ..." or "Both HTTPS and HTTP failed. ..."
Reachability: "Reachable"
```

#### 建議

1. **服務可能不使用HTTP或HTTPS**，例如，原始TCP、gRPC或其他通訊協定。 當`Port open: Yes`和`Reachability: Reachable`仍確認網路路徑運作時，HTTP探查可能會失敗。 使用這些欄位作為非HTTP服務的信任來源。
1. **調查TLS和憑證組態**。 如果HTTPS失敗但HTTP成功（有時以例如`HTTPS failed, HTTP succeeded`的附註表示），服務可能有憑證問題，或可能只在該連線埠上提供HTTP。

### 請求逾時 {#timeout}

#### 輸出

```json
{ "error": "Request timeout" }
```

#### 建議

1. **允許服務回應時間** — 檢查使用5秒的逾時。 回應速度較慢的目標，即使在其他情況下運作良好，也會逾時。
1. **考慮網路延遲**。 在VPN連線上，高延遲或不健康的通道可能會使往返超過限制；請檢閱通道狀態和路由。
1. **再次執行測試**。 單次網路故障可能會產生不會發生的逾時。

## 範例輸出 {#example-outputs}

### 成功的HTTPS測試（例如連線埠443上的內部API） {#example-output-successful-https}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "protocol": "https",
        "status_code": 200,
        "reason": "200 OK"
      },
      "reachability": "Reachable"
    }
  ]
}
```

### 成功的非HTTP服務測試（例如連線埠5432上的資料庫） {#example-output-successful-non-http}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "error": "Not an HTTP/HTTPS service",
        "note": "The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."
      },
      "reachability": "Reachable"
    }
  ]
}
```

>[!NOTE]
>
>非HTTP服務應該會發生HTTP錯誤。 **連線埠開啟： true**&#x200B;和&#x200B;**可連線：可連線**&#x200B;確認網路路徑正常運作。

### DNS解析失敗 {#example-output-dns-resolution-failure}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "error": "DNS resolution error: dial udp 10.0.0.2:53: i/o timeout"
      },
      "port_open": false,
      "http_connectivity": {
        "error": "DNS resolution failed"
      },
      "reachability": "Unreachable: DNS resolution failed"
    }
  ]
}
```

### 無法存取連線埠（防火牆/服務關閉） {#example-output-port-not-accessible}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": false,
      "http_connectivity": {
        "error": "Connection error: dial tcp 10.0.1.50:443: i/o timeout"
      },
      "reachability": "Unreachable: Port not accessible"
    }
  ]
}
```

## 重要注意事項 {#important-notes}

### 此測試沒有執行的動作 {#what-this-test-does-not-do}

* 測試不會從AEM作者或發佈Pod內部執行。 它從&#x200B;**輸出Proxy基礎結構**&#x200B;執行。 這樣會驗證網路層，而不是程式碼中的應用程式層級Proxy設定。
* 它不會驗證您的AEM應用程式的Proxy設定。 即使結果為`Reachable`，仍必須將AEM程式碼設定為使用Proxy。
* 它本身不會驗證環境層級的連線埠轉送設定。 它會測試來自基礎結構路徑的原始連線。
* 它不會傳送自訂裝載。 HTTP測試發出基本`GET`要求給`/`。

### 回應時間 {#response-time}

* **一般：**&#x200B;大約2到3秒。
* **最大值：**&#x200B;大約五秒逾時。
* **所有DNS解析器**&#x200B;和連線檢查並行執行。

### HTTP與非HTTP服務 {#http-vs-non-http-services}

工具會在每個連線埠上嘗試HTTP/HTTPS連線。 對於非HTTP服務（例如，連線埠5432上的PostgreSQL、3306上的MySQL、22上的SFTP、6379上的Redis），HTTP檢查可能會失敗，並出現連線錯誤 — 這是預期情況。 依賴`Port open`和`Reachability`確認這些服務的連線能力。

## 相關資訊 {#related-information}

* [設定 AEM as a Cloud Service 的進階網路](/help/security/configuring-advanced-networking.md)
* [Experience League上的進階網路教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/networking/advanced-networking)
