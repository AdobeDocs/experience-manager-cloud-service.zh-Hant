---
title: 為 AEM as a Cloud Service 設定進階網路
description: 了解如何為 AEM as a Cloud Service 設定進階網路功能，例如 VPN 或彈性或專用輸出 IP 地址等
exl-id: 968cb7be-4ed5-47e5-8586-440710e4aaa9
source-git-commit: 01b55f2ff06d3886724dbb2c25d0c109a5ab6aec
workflow-type: tm+mt
source-wordcount: '5142'
ht-degree: 94%

---


# 為 AEM as a Cloud Service 設定進階網路 {#configuring-advanced-networking}

本文旨在向您介紹 AEM as a Cloud Service 中的不同進階網路功能，包括 VPN 的自助設定和 API 佈建、非標準連接埠和專用輸出 IP 地址。

>[!TIP]
>
>除了本文件以之外，還有一系列教學課程專門引導您了解此[位置的每個進階網路選項。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)

## 概觀 {#overview}

AEM as a Cloud Service 提供以下進階網路選項：

* [彈性連接埠輸出](#flexible-port-egress) - 設定 AEM as a Cloud Service 以允許非標準連接埠的輸出流量。
* [專用輸出 IP 地址](#dedicated-egress-ip-address) - 將 AEM as a Cloud Service 的對外流量設定為源自唯一的 IP。
* [虛擬私人網路 (VPN)](#vpn) - 可在您的基礎結構和 AEM as a Cloud Service 之間提供安全流量 (如果您有 VPN)。

本文首先會詳細說明每個選項以及為什麼您可能會使用這些選項，然後會說明如何使用 Cloud Manager UI 和 API 來設定選項，最後會提供一些進階的使用案例。

>[!CAUTION]
>
>如果您已設定舊版專用輸出技術並希望設定這些進階網路選項之一， [請先聯絡 Adobe Client Care。](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home)
>
>嘗試使用舊版專用輸出技術設定進階網路時，可能會影響網站連線。

### 要求和限制 {#requirements}

設定進階網路功能時，有以下限制。

* 一個程式可以提供單一進階網路選項 (彈性連接埠輸出、專用輸出 IP 位址或 VPN)。
* 進階網路不適用於[沙箱程式。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
* 使用者必須擔任&#x200B;**管理員**&#x200B;角色，才能在您的程式中新增和設定網路基礎架構。
* 必須先建立生產環境，然後才能將網路基礎架構加入您的程式。
* 您的網路基礎設施必須與生產環境的主要區域位於相同區域內。
   * 如果您的生產環境有[額外的發佈區域，](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) 您可以建立鏡像每個額外區域的額外網路基礎架構。
   * 您建立的網路基礎架構數量不得超過生產環境中設定的最大區域數量。
   * 您可以定義與生產環境所用區域一樣多的網路基礎設施，但新基礎設施必須與先前建立的基礎設施類型相同。
   * 建立多個基礎架構時，您只能從尚未建立進階網路基礎架構的區域中做選擇。

### 設定和啟用進階網絡 {#configuring-enabling}

使用進階網路功能需要兩個步驟：

1. 進階網路選項的設定必須先在程式層級完成，無論是 [彈性連接埠輸出、](#flexible-port-egress) [專用輸出 IP 位址](#dedicated-egress-ip-address)或 [VPN](#vpn) 都一樣 。
1. 若要使用，進階網路選項必須 [已在環境層級啟用。](#enabling)

這兩個步驟都可以使用 Cloud Manager UI 或 Cloud Manager API 來完成。

* 使用 Cloud Manager UI 時，這表示要使用程式層級的精靈建立進階網路設定，然後編輯您希望啟用設定的每個環境。

* 當使用 Cloud Manager API 時，`/networkInfrastructures` API 端點會在程式層級呼叫以宣告所要的進階網路類型，然後呼叫每個環境的 `/advancedNetworking` 端點以啟用基礎結構並設定特定於環境的參數。

## 彈性連接埠輸出 {#flexible-port-egress}

此進階網路功能可讓您設定 AEM as a Cloud Service 以透過預設開啟的 HTTP (連接埠 80) 和 HTTPS (連接埠 443) 以外的連接埠輸出流量。

>[!TIP]
>
>在決定使用彈性連接埠輸出或專用輸出 IP 位址時，如果不需要特定的 IP 位址，建議您選擇彈性連接埠輸出，因為 Adobe 可以最佳化彈性連接埠輸出流量的效能。

>[!NOTE]
>
>建立後，彈性連接埠輸出基礎架構類型將無法編輯。變更設定值的唯一方法是刪除並重新建立。

### UI 設定 {#configuring-flexible-port-egress-provision-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)**」畫面中，選取程式。

1. 從「**程式概覽**」頁面，導覽至「**環境**」標籤，然後在左側面板選取「**網路基礎設施**」。

   ![新增網路基礎結構](assets/advanced-networking-ui-network-infrastructure.png)

1. 在啟動的「**新增網路基礎設施**」精靈中，選取「**彈性連接埠輸出**」，以及從「**區域**」下拉式選單選取應建立的區域，然後點選或按一下「**繼續**」。

   ![設定彈性連接埠輸出](assets/advanced-networking-ui-flexible-port-egress.png)

1. 「**確認**」標籤會總結您的選擇和後續步驟。點選或按一下「**儲存**」並建立內容結構。

   ![確認彈性連接埠輸出的設定](assets/advanced-networking-ui-flexible-port-egress-confirmation.png)

側面板中「**網路基礎設施**」標題下方會顯示一筆新記錄，其中包括基礎設施類型、狀態、區域以及已啟用該記錄的環境等詳細資訊。

![網路基礎架構下方的新輸入記錄](assets/advanced-networking-ui-flexible-port-egress-new-entry.png)

>[!NOTE]
>
>建立彈性連接埠輸出的基礎設施可能需要長達一個小時，建立後可以在環境層級進行設定。

### API 設定 {#configuring-flexible-port-egress-provision-api}

對每個程式會叫用一次 POST`/program/<programId>/networkInfrastructures` 端點，直接傳遞 `flexiblePortEgress` 的值 (`kind` 參數和區域)。端點會以 `network_id` 及其他資訊回應，包括狀態。

呼叫後，通常需要大約 15 分鐘的時間來佈建網路基礎結構。對 Cloud Manager 的[網路基礎結構 GET 端點](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure)的呼叫會顯示「**就緒**」狀態。

>[!TIP]
>
>完整的參數集和確切的語法，以及如哪些參數之後不能變更等重要資訊，[可以在 API 文件中參考。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

### 流量路由 {#flexible-port-egress-traffic-routing}

對於流向 80 或 443 以外連接埠的 http 或 https 流量，應使用以下主機和連接埠環境變數來設定 Proxy：

* 對於 HTTP：`AEM_PROXY_HOST` / `AEM_HTTP_PROXY_PORT ` (在 AEM 版本 &lt; 6094 中預設為 `proxy.tunnel:3128`)
* 對於 HTTPS：`AEM_PROXY_HOST` / `AEM_HTTPS_PROXY_PORT ` (在 AEM 版本 &lt; 6094 中預設為 `proxy.tunnel:3128`)

例如，以下是傳送請求至 `www.example.com:8443` 的範例程式碼：

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv().getOrDefault("AEM_PROXY_HOST", "proxy.tunnel");
int proxyPort = Integer.parseInt(System.getenv().getOrDefault("AEM_HTTPS_PROXY_PORT", "3128"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

如果使用非標準 Java 網路資料庫，請使用上述屬性為所有流量設定 Proxy。

目標流經 `portForwards` 參數中宣告的連接埠的非 http/s 流量應該參照一個名為 `AEM_PROXY_HOST` 的屬性，以及對應的連接埠。例如：

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

下表描述了流量路由：

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目標條件</th>
    <th>連接埠</th>
    <th>連線</th>
    <th>外部目標範例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http 或 https 通訊協定</b></td>
    <td>標準 http/s 流量</td>
    <td>80 或 443</td>
    <td>允許</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>流經使用以下環境變數和 Proxy 連接埠號碼設定的 http proxy 的非標準流量 (在 80 或 443 以外的其他連接埠上)。請勿在 Cloud Manager API 呼叫的 portForwards 參數中宣告目標連接埠：<br><ul>
     <li>AEM_PROXY_HOST (在 AEM 版本 &lt; 6094 中預設為 `proxy.tunnel`)</li>
     <li>AEM_HTTPS_PROXY_PORT (在 AEM 版本 &lt; 6094 中預設為連接埠 3128)</li>
    </ul>
    <td>80 或 443 之外的連接埠</td>
    <td>允許</td>
    <td>example.com:8443</td>
  </tr>
  <tr>
    <td></td>
    <td>不使用 http proxy 的非標準流量 (在連接埠 80 或 443 之外的其他連接埠上)</td>
    <td>80 或 443 之外的連接埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http 或非 https</b></td>
    <td>連接到 <code>AEM_PROXY_HOST</code> 環境變數 (使用 <code>portOrig</code> 在 <code>portForwards</code> API 參數中宣告) 的用戶端。</td>
    <td>任何</td>
    <td>允許</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>其他一切</td>
    <td>任何</td>
    <td>已封鎖</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

#### Apache / Dispatcher 設定 {#apache-dispatcher}

可以使用上述屬性設定 AEM Cloud Service Apache/Dispatcher 層的 `mod_proxy` 指令。

```
ProxyRemote "http://example.com:8080" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "http://example.com:8080"
ProxyPassReverse "/somepath" "http://example.com:8080"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## 專用輸出 IP 位址 {#dedicated-egress-ip-address}

在與 SaaS 廠商 (如 CRM 廠商) 整合或在 AEM as a Cloud Service 之外有提供 IP 位址允許清單的其他整合時，專用的 IP 位址可以增強安全性。透過將專用IP位址新增至允許清單，可確保只允許來自AEM Cloud Service的流量流入外部服務。 這是在來自任何其他 IPS 允許的流量之外的補充。

相同的專用 IP 適用於您的 Adobe 組織中所有程式以及您所用程式中的全部環境。它適用於編寫和發佈服務。

如果沒有啟用專用 IP 位址功能，來自 AEM as a Cloud Service 的流量會流經與其他 AEM as a Cloud Service 客戶共用的一組 IP。

設定專用輸出 IP 位址類似[彈性連接埠輸出。](#flexible-port-egress) 主要區別在於設定後，流量一律從專用的、唯一的 IP 輸出。要尋找該 IP，請使用 DNS 解析器識別與 `p{PROGRAM_ID}.external.adobeaemcloud.com` 相關聯的 IP 位址。該 IP 位址預期不會變更，但如果必須變更會事先通知。

>[!TIP]
>
>在決定使用彈性連接埠輸出或專用輸出 IP 位址時，如果不需要特定的 IP 位址，建議您選擇彈性連接埠輸出，因為 Adobe 可以最佳化彈性連接埠輸出流量的效能。

>[!NOTE]
>
>如果在 2021.09.30 之前 (即 2021 年 9 月版本之前) 已為您佈建專用輸出 IP，則您的專用輸出 IP 功能僅支援 HTTP 和 HTTPS 連接埠。
>
>這包括 HTTP/1.1 和加密後的 HTTP/2。此外，一個專用輸出端點可以分別透過連接埠 80/443 上的 HTTP/HTTPS 與任何目標通訊。

>[!NOTE]
>
>建立後，專用輸出 IP 位址基礎架構類型將無法編輯。變更設定值的唯一方法是刪除並重新建立。

>[!INFO]
>
>專用輸出 IP 位址無法提供 Splunk 轉送功能。

### UI 設定 {#configuring-dedicated-egress-provision-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)**」畫面中，選取程式。

1. 從「**程式概覽**」頁面，導覽至「**環境**」標籤，然後在左側面板選取「**網路基礎設施**」。

   ![新增網路基礎結構](assets/advanced-networking-ui-network-infrastructure.png)

1. 在啟動的「**新增網路基礎設施**」精靈中，選取「**專用輸入 IP 位址**」，以及從「**區域**」下拉式選單選取應建立的區域，然後點選或按一下「**繼續**」。

   ![設定專用輸出 IP 位址](assets/advanced-networking-ui-dedicated-egress.png)

1. 「**確認**」標籤會總結您的選擇和後續步驟。點選或按一下「**儲存**」並建立內容結構。

   ![確認彈性連接埠輸出的設定](assets/advanced-networking-ui-dedicated-egress-confirmation.png)

側面板中「**網路基礎設施**」標題下方會顯示一筆新記錄，其中包括基礎設施類型、狀態、區域以及已啟用該記錄的環境等詳細資訊。

![網路基礎架構下方的新輸入記錄](assets/advanced-networking-ui-flexible-port-egress-new-entry.png)

>[!NOTE]
>
>建立彈性連接埠輸出的基礎設施可能需要長達一個小時，建立後可以在環境層級進行設定。

### API 設定 {#configuring-dedicated-egress-provision-api}

對每個程式會叫用一次 POST`/program/<programId>/networkInfrastructures` 端點，直接傳遞 `dedicatedEgressIp` 的值 (`kind` 參數和區域)。端點會以 `network_id` 及其他資訊回應，包括狀態。

呼叫後，通常需要大約 15 分鐘的時間來佈建網路基礎結構。對 Cloud Manager 的[網路基礎結構 GET 端點](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure)的呼叫會顯示「**就緒**」狀態。

>[!TIP]
>
>完整的參數集和確切的語法，以及如哪些參數之後不能變更等重要資訊，[可以在 API 文件中參考。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

### 流量路由 {#dedicated-egress-ip-traffic-routing}

Http 或 https 流量將流經預先設定的 Proxy，前提是它們使用標準 Java 系統屬性進行 Proxy 設定。

目標流經`portForwards` 參數中宣告的連接埠的非 http/s 流量應該參照一個名為 `AEM_PROXY_HOST` 的屬性，以及對應的連接埠。例如：

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目標條件</th>
    <th>連接埠</th>
    <th>連線</th>
    <th>外部目標範例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http 或 https 通訊協定</b></td>
    <td>到 Azure 或 Adobe 服務的流量</td>
    <td>任何</td>
    <td>流經共用叢集 IP (不是專用的 IP)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>符合 <code>nonProxyHosts</code> 參數的主機</td>
    <td>80 或 443</td>
    <td>流經共用叢集 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>符合 <code>nonProxyHosts</code> 參數的主機</td>
    <td>80 或 443 之外的連接埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>流經 http proxy 設定，預設針對使用標準 Java HTTP 用戶端資料庫的 http/s 流量所設定</td>
    <td>任何</td>
    <td>流經專用輸出 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http proxy 設定 (例如，如果從標準 Java HTTP 用戶端資料庫中明確移除，或者如果使用忽略標準 Proxy 設定的 Java 資料庫)</td>
    <td>80 或 443</td>
    <td>流經共用叢集 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http proxy 設定 (例如，如果從標準 Java HTTP 用戶端資料庫中明確移除，或者如果使用忽略標準 Proxy 設定的 Java 資料庫)</td>
    <td>80 或 443 之外的連接埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http 或非 https</b></td>
    <td>連接到 <code>AEM_PROXY_HOST</code> 環境變數 (使用 <code>portOrig</code> 在 <code>portForwards</code> API 參數中宣告) 的用戶端</td>
    <td>任何</td>
    <td>流經專用輸出 IP</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>其他任何項目</td>
    <td></td>
    <td>已封鎖</td>
    <td></td>
  </tr>
</tbody>
</table>

### 功能使用情況 {#feature-usage}

功能與導致輸出流量的 Java 程式碼或資料庫相容，前提是它們使用標準 Java 系統屬性進行 Proxy 設定。實際上，這應該包括最常見的資料庫。

以下是程式碼範例：

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

一些資料庫需要明確設定才能使用標準 Java 系統屬性進行 Proxy 設定。

使用 Apache HttpClient 的範例，需要明確呼叫
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) 或使用 
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem())：

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();

  HttpClient httpClient = HttpClientBuilder.create().useSystemProperties().build();
  HttpGet request = new HttpGet(finalUrl.toURI());
  request.setHeader("Accept", "application/json");
  request.setHeader("X-API-KEY", apiKey);
  HttpResponse response = httpClient.execute(request);
  String result = EntityUtils.toString(response.getEntity());
}
```

### 偵錯考量 {#debugging-considerations}

若要驗證流量確實在預期的專用 IP 位址上傳出，請檢查目標服務中的記錄 (如果可用)。否則，呼叫偵錯服務可能會有幫助，例如 [https://ifconfig.me/IP](https://ifconfig.me/IP)，這將傳回呼叫的 IP 位址。

## 虛擬私人網路 (VPN) {#vpn}

VPN 允許從製作、發佈或預覽執行個體連線到內部部署基礎結構或資料中心。例如，這對於安全存取資料庫很有用。VPN 還允許連線到 SaaS 廠商，例如支援 VPN 的 CRM 廠商，或從公司網路連線到 AEM as a Cloud Service 製作、預覽或發佈執行個體。

支援大多數採用 IPSec 技術的 VPN 裝置。請查閱[本裝置清單內 **RouteBased 設定指示**&#x200B;欄中的資訊。](https://docs.microsoft.com/zh-tw/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable) 按照表中所述設定裝置。

>[!NOTE]
>
>請注意這些 VPN 基礎架構的限制：
>
>* 支援僅限於單一 VPN 連線
>* Splunk 轉送功能無法透過 VPN 連線提供。
>* DNS Resolver 必須列在閘道位址空間中才能解析私有主機名稱。

### UI 設定 {#configuring-vpn-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)**」畫面中，選取程式。

1. 從「**程式概覽**」頁面，導覽至「**環境**」標籤，然後在左側面板選取「**網路基礎設施**」。

   ![新增網路基礎結構](assets/advanced-networking-ui-network-infrastructure.png)

1. 在啟動的「**新增網路基礎設施**」精靈中，選取「**虛擬私人網路**」並提供必要的資訊，然後點選或按一下「**繼續**」。

   * **區域**  - 這是應建立基礎設施的區域。
   * **位址空間**  — 位址空間只能是您自己的空間中的一個/26 CIDR （64個IP位址）或更大的IP範圍。
      * 該值以後便無法變更。
   * **DNS 資訊** - 這是遠端 DNS 解析器的清單。
      * 輸入 DNS 伺服器位址後，按下`Enter`再新增另一個位址。
      * 在位址後面，點選或按一下 `X` 即可移除。
   * **共用金鑰** - 這是您的 VPN 預先共用金鑰。
      * 選取「**顯示共用金鑰**」，顯示金鑰以仔細檢查該值。

   ![設定 VPN](assets/advanced-networking-ui-vpn.png)

1. 在精靈的「**連線** 」標籤中，提供「**連接名稱**」以識別您的 VPN 連線，並點選或按一下「**新增連接**」。

   ![新增連線](assets/advanced-networking-ui-vpn-add-connection.png)

1. 在「**新增連接**」對話框中，定義您的 VPN 連線，然後點選或按一下「**儲存**」。

   * **連線名稱** - 這是您的 VPN 連線的說明性名稱；您在&#x200B;&#x200B;上一個步驟中提供了名稱，且您可以在此處更新。
   * **位址** - 這是 VPN 裝置的 IP 位址。
   * **位址空間** - 這些是透過 VPN 進行路由的 IP 位址範圍。
      * 輸入一個範圍後，按下`Enter`再新增另一個範圍。
      * 在一個範圍後面，點選或按一下 `X` 即可移除。
   * **IP 安全性原則** - 依需要調整預設值

   ![新增 VPN 連線](assets/advanced-networking-ui-vpn-adding-connection.png)

1. 對話框關閉，您會返回精靈的「**連線**」標籤。點選或按一下&#x200B;**繼續**。

   ![新增 VPN 連線](assets/advanced-networking-ui-vpn-connection-added.png)

1. 「**確認**」標籤會總結您的選擇和後續步驟。點選或按一下「**儲存**」並建立內容結構。

   ![確認彈性連接埠輸出的設定](assets/advanced-networking-ui-vpn-confirm.png)

側面板中「**網路基礎設施**」標題下方會顯示一筆新記錄，其中包括基礎設施類型、狀態、區域以及已啟用該記錄的環境等詳細資訊。

### API 設定 {#configuring-vpn-api}

每個方案一次，POST `/program/<programId>/networkInfrastructures` 叫用端點，傳遞設定資訊的承載，包括： **vpn** 針對 `kind` 引數、區域、位址空間（CIDR清單 — 請注意，這之後無法修改）、DNS解析器（用於解析網路中的名稱）以及VPN連線資訊，例如閘道設定、共用VPN金鑰以及IP安全性原則。 端點會以 `network_id` 及其他資訊回應，包括狀態。

呼叫後，通常需要 45 到 60 分鐘的時間來佈建網路基礎結構。可以呼叫 API 的 GET 方法傳回目前狀態，這最終會從 `creating` 轉成 `ready`。請參閱 API 文件以了解各種狀態。

>[!TIP]
>
>完整的參數集和確切的語法，以及如哪些參數之後不能變更等重要資訊，[可以在 API 文件中參考。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

### 流量路由 {#vpn-traffic-routing}

下表描述了流量路由。

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目標條件</th>
    <th>連接埠</th>
    <th>連線</th>
    <th>外部目標範例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http 或 https 通訊協定</b></td>
    <td>到 Azure 或 Adobe 服務的流量</td>
    <td>任何</td>
    <td>流經共用叢集 IP (不是專用的 IP)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>符合 <code>nonProxyHosts</code> 參數的主機</td>
    <td>80 或 443</td>
    <td>流經共用叢集 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>符合 <code>nonProxyHosts</code> 參數的主機</td>
    <td>80 或 443 之外的連接埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>如果 IP 在 <i>VPN 閘道位址</i>空間範圍內，並透過 http proxy 設定 (預設針對使用標準 Java HTTP 用戶端資料庫的 http/s 流量所設定)</td>
    <td>任何</td>
    <td>流經 VPN</td>
    <td><code>10.0.0.1:443</code><br>它也可以是主機名稱。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果 IP 不在 <i>VPN 閘道位址</i>空間範圍內，並透過 http proxy 設定 (預設針對使用標準 Java HTTP 用戶端資料庫的 http/s 流量所設定)</td>
    <td>任何</td>
    <td>流經專用輸出 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http proxy 設定 (例如，如果從標準 Java HTTP 用戶端資料庫中明確移除，或者如果使用忽略標準 Proxy 設定的 Java 資料庫)
</td>
    <td>80 或 443</td>
    <td>流經共用叢集 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http proxy 設定 (例如，如果從標準 Java HTTP 用戶端資料庫中明確移除，或者如果使用忽略標準 Proxy 設定的 Java 資料庫)</td>
    <td>80 或 443 之外的連接埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http 或非 https</b></td>
    <td>如果 IP 在 <i>VPN 閘道位址空間</i>範圍內，並且用戶端連線到 <code>AEM_PROXY_HOST</code> 環境變數 (使用 <code>portOrig</code> 在 <code>portForwards</code>API 參數中宣告)</td>
    <td>任何</td>
    <td>流經 VPN</td>
    <td><code>10.0.0.1:3306</code><br>它也可以是主機名稱。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果 IP 不在 <i>VPN 閘道位址空間</i>範圍內，並且用戶端連線到 <code>AEM_PROXY_HOST</code> 環境變數 (使用 <code>portOrig</code> 在 <code>portForwards</code>API 參數中宣告)</td>
    <td>任何</td>
    <td>流經專用輸出 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>其他任何項目</td>
    <td>任何</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
</tbody>
</table>

### 供設定的實用網域 {#vpn-useful-domains-for-configuration}

下圖提供了一組網域和相關聯的 IP 的視覺化表示，對設定和開發很有幫助。圖表下方的表格描述了這些網域和 IP。

![VPN 網域設定](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>網域模式</th>
    <th>輸出 (自 AEM) 含義</th>
    <th>輸入 (至 AEM) 含義</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>專用輸出 IP 位址，用於流向網際網路而不是流經私人網路的流量 </td>
    <td>來自 VPN 的連線在 CDN 上會顯示為來自此 IP。若是要只允許來自 VPN 的連線進入 AEM，請將 Cloud Manager 設定為僅允許此 IP 並封鎖其他所有一切。請參閱「限制輸入 VPN 連線」一節以取得詳細資料。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.{REGION}-gateway.external.adobeaemcloud.com</code></td>
    <td>不適用</td>
    <td>AEM 端 VPN 閘道的 IP。您的網路工程團隊可以使用此項來僅允許從特定IP位址到您的VPN閘道的VPN連線。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.{REGION}.inner.adobeaemcloud.net</code></td>
    <td>來自VPN的AEM端到您端的流量IP。 這可以在您的設定中加入允許清單，以確保只能從AEM建立連線。</td>
    <td>如果您想要允許VPN存取AEM，您應該設定CNAME DNS專案以對應您的自訂網域和/或 <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 和/或 <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 至此。</td>
  </tr>
</tbody>
</table>

### 將 VPN 限制為輸入連線 {#restrict-vpn-to-ingress-connections}

如果您只想允許 VPN 存取 AEM，則可以在 Cloud Manager 中設定環境允許清單，如此只有由 `p{PROGRAM_ID}.external.adobeaemcloud.com` 定義的 IP 允許與環境交談。就像 Cloud Manager 中任何其他基於 IP 的允許清單一樣，這也可以相同方式完成。

如果規則必須基於路徑，請在 Dispatcher 層級使用標準的 http 指令來拒絕或允許某些 IP。他們同時應該確保所要的路徑不可快取在 CDN 上，讓請求始終可到達來源。

#### Httpd 設定範例 {#httpd-example}

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 在「環境」中，啟用「進階網路設定」 {#enabling}

為程式設定好進階網路選項後，無論是[彈性連接埠輸出、](#flexible-port-egress) [專用輸出 IP 位址](#dedicated-egress-ip-address) 或 [VPN](#vpn)，為了要使用您必須在環境層級啟用。

當您為環境啟用進階網路設定時，您可以啟用選購的連接埠轉送和非代理主機。 參數可根據環境設定，以提供靈活性。

* **連接埠轉送** - 應為 80/443 以外的任何目標連接埠宣布連接埠轉送規則，但前提是不使用 http 或 https 協定。
   * 連線埠轉送規則是透過指定目標主機集（名稱或IP和連線埠）來定義。
   * 透過 http/https 使用連接埠 80/443 的用戶端連線仍然必須在其連線中使用 Proxy 設定，並將進階網路的屬性套用至該連線。
   * 對於每個目標主機，您必須將預期的目標連線埠對應到30000到30999之間的連線埠。
   * 連接埠轉送規則適用於所有進階網路類型。

* **非代理主機** - 非代理主機可讓您宣告一組應透過共用 IP 位址範圍 (而非專用 IP) 進行路由的主機。
   * 這可能很有用，因為可以進一步最佳化透過共享 IP 輸出的流量。
   * 非代理主機僅適用於專用輸出進階 IP 位址和 VPN 進階網路類型。

>[!NOTE]
>
>如果環境在&#x200B;**更新**&#x200B;狀態中，您無法為環境啟用進階網路設定。

### 啟用使用 UI {#enabling-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)**」畫面中，選取程式。

1. 從「**計劃概覽**」頁面，導覽至「**環境**」標籤，並選取您希望啟用進階網路設定的環境 (在左側面板的「**環境**」標題中)。 然後，選取所選環境的「**進階網路設定**」標籤，然後點選或按一下「**啟用網路基礎設施**」。

   ![選取環境以啟用進階網絡](assets/advanced-networking-ui-enable-environments.png)

1. 「**設定進階網路**」對話框開啟。

1. 在「**非代理主機**」標籤上，對於專用輸出 IP 位址和 VPN，您可以選擇性地定義一組主機，這些主機應透過共用 IPS 位址範圍進行路由 (而非專用的 IP)，方法是在「**非代理主機**」欄位中提供主機名，然後點選或按一下「**新增**」。

   * 該主機將會新增至標籤上的主機清單。
   * 重複此步驟以新增多個主機。
   * 點選或按一下該列右側的 X，即可移除主機。
   * 此標籤不適用於彈性連接埠輸出設定。

   ![新增非代理主機](assets/advanced-networking-ui-enable-non-proxy-hosts.png)

1. 在 **連線埠轉送** 索引標籤上，您可以選擇性地為80/443以外的任何目的地連線埠定義連線埠轉送規則（如果未使用HTTP或HTTPS）。 提供&#x200B;**名稱**、 **連接埠來源**&#x200B;和&#x200B;**連接埠目標**，然後點選或按一下「**新增**」。

   * 該規則將會新增至標籤上的規則清單中。
   * 重複此步驟以新增多個規則。
   * 點選或按一下該列右側的 X，即可移除規則。

   ![定義可選擇的連接埠轉送](assets/advanced-networking-ui-port-forwards.png)

1. 在對話框中，點選或按一下「**儲存**」，將設定套用至環境。

進階網路設定將套用於所選環境中。返回「**環境**」標籤，您可以查看套用於所選環境的設定詳細資訊及其狀態。

![已設定進階網路的環境](assets/advanced-networking-ui-configured-environment.png)

### 啟用使用 API {#enabling-api}

若要為環境啟用進階網路設定，必須為每個環境叫用 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端點。

API 應該在幾秒鐘內做出回應，表明 `updating` 的狀態，大約 10 分鐘後，呼叫 Cloud Manager 的環境 GET 端點將顯示 `ready` 的狀態，表示已套用對環境的更新。

可以透過叫用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端點來更新每個環境的連接埠轉送規則，並且要包括完整的設定參數集而非子集。

專用輸出 IP 位址和 VPN 進階網路類型支援 `nonProxyHosts` 參數。此參數可讓您聲明一組主機，這些主機應透過共用的 IPS 位址範圍 (而非專用的 IP) 進行路由。`nonProxyHost` URL 可能遵循 `example.com` 或`*.example.com` 的模式，其中僅在網域開頭支援萬用字元。

即使沒有環境流量路由規則 (主機或旁路)，仍然必須用空白承載呼叫 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`。

>[!TIP]
>
>完整的參數集和確切的語法，以及如哪些參數之後不能變更等重要資訊，[可以在 API 文件中參考。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

## 編輯並刪除環境中的進階網路設定 {#editing-deleting-environments}

 [為環境啟用進階網路設定後，](#enabling) 您可以更新這些設定的詳細資訊或將其刪除。

>[!NOTE]
>
>如果網路基礎設施在「**建立中**」、「**更新中**」或「**刪除中**」的狀態，您就無法編輯網路基礎設施。

### 使用 UI 進行編輯或刪除 {#editing-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)**」畫面中，選取程式。

1. 從「**計劃概覽**」頁面，導覽至「**環境**」標籤，並選取您希望啟用進階網路設定的環境 (在左側面板的「**環境**」標題中)。 然後，選取所選環境的「**進階網路設定**」標籤，然後點選或按一下省略號按鈕。

   ![在程式層級選取編輯或刪除進階網絡](assets/advanced-networking-ui-edit-delete.png)

1. 在省略號選單中，選取「**編輯**」或「**刪除**」。

   * 如果您選擇「**編輯**」，請按照上一節「[啟用使用者介面](#enabling-ui)」中所述的步驟更新資訊，然後點選或按一下「**儲存**」。
   * 如果您選擇「**刪除**」，請在「**刪除網路設定**」對話框中使用「**刪除**」來確認刪除，或使用「**取消**」來中止。

變更將反映在「**環境**」標籤上。

### 使用 API 進行編輯或刪除 {#editing-api}

若要刪除特定環境的進階網絡，請呼叫 `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`。

>[!TIP]
>
>完整的參數集和確切的語法，以及如哪些參數之後不能變更等重要資訊，[可以在 API 文件中參考。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

## 編輯和刪除程式的網路基礎結構 {#editing-deleting-program}

一旦為程式建立了網路基礎結構，就只能編輯有限的屬性。如果您不需要，您可以刪除整個程式的進階網路基礎架構。

>[!NOTE]
>
>請注意編輯和刪除網路基礎設施有以下這些限制：
>
>* 如果所有環境都停用了進階網路，則刪除作業只會刪除基礎結構。
>* 如果網路基礎設施在「**建立中**」、「**更新中**」或「**刪除中**」的狀態，您就無法編輯網路基礎設施。
>* 建立後，只能編輯 VPN 進階網路基礎架構類型，然後，只能編輯有限的欄位。
>* 基於安全理由，在編輯 VPN 進階網路基礎架構時，一定要隨時提供&#x200B;**共用金鑰**，即使您未編輯金鑰也一樣要提供。

### 使用 UI 進行編輯和刪除 {#delete-ui}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)**」畫面中，選取程式。

1. 從「**程式概覽**」頁面，導覽至「**環境**」標籤，然後在左側面板選取「**網路基礎設施**」標題。然後，點選或按一下要刪除的基礎架構旁的省略號按鈕。

   ![在程式層級選取編輯或刪除進階網絡](assets/advanced-networking-ui-delete-infrastructure.png)

1. 在省略號選單中，選取「**編輯**」或「**刪除**」。

1. 如果您選擇「**編輯**」，「**編輯網路基礎架構**」精靈會開啟。請依照建立基礎架構時說明的步驟，依需要進行編輯。

1. 如果您選擇「**刪除**」，請在「**刪除網路設定**」對話框中使用「**刪除**」來確認刪除，或使用「**取消**」來中止。

變更將反映在「**環境**」標籤上。

### 使用 API 進行編輯和刪除 {#delete-api}

要&#x200B;**刪除**&#x200B;程式的網路基礎結構，請叫用 `DELETE /program/{program ID}/networkinfrastructure/{networkinfrastructureID}`。

## 變更程式的進階網路基礎架構類型 {#changing-program}

一次只能為程式設定一種類型的進階網路基礎設施，即彈性連接埠輸出、專用輸出 IP 位址或 VPN。

如果您決定需要其他進階網路基礎架構類型，而不需要已設定的網路基礎架構類型，您必須刪除現有的網路基礎架構類型並建立新的網路基礎架構類型。請依照以下程序進行：

1. [在所有環境中刪除進階網路](#editing-deleting-environments)
1. [刪除進階網路基礎結構。](#editing-deleting-program)
1. 建立您現在需要的進階網路基礎架構類型， [彈性連接埠輸出、](#flexible-port-egress) [專用輸出 IP 位址](#dedicated-egress-ip-address)或[ VPN。](#vpn)
1. [在環境層級重新啟用進階網路。](#enabling)

>[!WARNING]
>
> 此程序將導致進階網路服務在刪除和重新建立之間停機
> 如果停機導致顯著的業務衝擊，請聯絡客戶支援以尋求協助，描述已經建立的內容和變更的原因。

## 額外發佈區域的進階網路設定 {#advanced-networking-configuration-for-additional-publish-regions}

將額外區域新增到已設定進階網路的環境時，來自和進階網路規則相符的額外發佈區域的流量會依預設路由通過主要區域。但是，如果主要區域變成無法使用，並且在額外區域中尚未啟用進階網路，則進階網路流量會下降。如果您想在其中一個區域發生中斷時將延遲最佳化並提高可用性，則有必要啟用額外發佈區域的進階網路。以下章節會說明兩種不同的案例。

>[!NOTE]
>
>所有區域都共用相同的[環境進階網路設定](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Environment-Advanced-Networking-Configuration)，因此無法根據流量輸出的區域將流量路由至不同的目標。

### 專用的輸出 IP 位址 {#additional-publish-regions-dedicated-egress}

#### 進階網路已在主要區域中啟用 {#already-enabled}

如果已在主要區域中啟用進階網路設定，請依照下列步驟進行：

1. 如果您已鎖定基礎結構，以便將專用的 AEM IP 位址加入允許清單，則建議暫時停用該基礎結構中的任何否決規則。如果不這樣做，有一小段時間您自己的基礎結構會拒絕來自新區域的 IP 位址的請求。如果您已經由完整網域名稱 (FQDN) 鎖定基礎結構 (例如 `p1234.external.adobeaemcloud.com`)，則沒有必要這麼做，因為所有 AEM 區域都會從相同的 FQDN 輸出進階網路流量
1. 根據進階網路文件中的說明，可透過對 Cloud Manager Create Network Infrastructure API 的 POST 呼叫為次要區域建立計畫範圍的網路基礎結構。承載的 JSON 設定相對於主要區域的唯一差異是區域屬性
1. 如果您的基礎結構必須由 IP 鎖定以允許 AEM 流量，請新增和 `p1234.external.adobeaemcloud.com` 相符的 IPS。每個區域都應該有一個。

#### 尚未在任何區域中設定進階網路 {#not-yet-configured}

此程序和先前的說明大部分類似。但是，如果尚未啟用進階網路的生產環境，則有機會先在中繼環境中啟用以測試該設定：

1. 透過對 [Cloud Manager Create Network Infrastructure API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Network-infrastructure/operation/createNetworkInfrastructure) 的 POST 呼叫建立所有區域的網路基礎結構。承載的 JSON 設定相對於主要區域的唯一差異是區域屬性
1. 若是中繼環境，可透過執行 `PUT api/program/{programId}/environment/{environmentId}/advancedNetworking` 以啟用和設定環境範圍的進階網路。如需詳細資訊，請參閱[這裡](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Environment-Advanced-Networking-Configuration/operation/enableEnvironmentAdvancedNetworkingConfiguration)的 API 文件。
1. 如有必要，可鎖定外部基礎結構，最好透過 FQDN (例如 `p1234.external.adobeaemcloud.com`)。不然可透過 IP 位址進行
1. 如果中繼環境按預期運作，請啟用並設定環境範圍的進階網路設定以進行生產。

#### VPN {#vpn-regions}

該程序和專用的輸出 IP 位址說明幾乎相同。唯一的差異是，除了區域屬性的設定和主要區域不同之外，可選擇將 `connections.gateway` 欄位設定為路由至由貴組織操作的不同 VPN 端點，地理位置也許會更接近新區域。
