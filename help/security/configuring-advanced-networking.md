---
title: 為 AEM as a Cloud Service 設定進階網路
description: 了解如何為 AEM as a Cloud Service 設定進階網路功能，例如 VPN 或彈性或專用輸出 IP 地址等
exl-id: 968cb7be-4ed5-47e5-8586-440710e4aaa9
source-git-commit: dde06fb7b678de8bf07aae54ee411aab7208ab2c
workflow-type: ht
source-wordcount: '3053'
ht-degree: 100%

---

# 為 AEM as a Cloud Service 設定進階網路 {#configuring-advanced-networking}

本文旨在向您介紹 AEM as a Cloud Service 中的不同進階網路功能，包括 VPN 的自助設定、非標準連接埠和專用輸出 IP 地址。

>[!INFO]
>
>您還可以在這個[位置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=en)找到一系列旨在向您逐步解釋每個進階網路選項的文章。

## 概觀 {#overview}

AEM as a Cloud Service 提供多種類型的進階網路功能，客戶可以使用 Cloud Manager API 進行設定。這些類別包括：

* [彈性的連接埠輸出](#flexible-port-egress) - 設定 AEM as a Cloud Service 以允許非標準連接埠的輸出流量
* [專用輸出 IP 地址](#dedicated-egress-IP-address) - 將 AEM as a Cloud Service 的對外流量設定為源自唯一的 IP
* [虛擬私人網路 (VPN)](#vpn) - 為擁有 VPN 技術的客戶在客戶的基礎結構和 AEM as a Cloud Service 之間提供安全流量

本文詳述了當中各個選項，包括如何設定它們。 作為一般設定策略，`/networkInfrastructures` API 端點會在程式層級叫用以宣告所要的進階網路類型，然後叫用每個環境的 `/advancedNetworking` 端點以啟用基礎結構並設定特定於環境的參數。請參考 Cloud Manager API 文件中的適當端點，了解各種正式語法以及範例請求和回應。

一個程式可以提供單一進階網路變體。 在決定使用彈性連接埠輸出或專用輸出 IP 位址時，如果不需要特定的 IP 位址，建議您選擇彈性連接埠輸出，因為 Adobe 可以最佳化彈性連接埠輸出流量的效能。

>[!INFO]
>
>進階網路不適用於沙箱程式。
>此外，環境必須升級到 AEM 版本 5958 或更高版本。

>[!NOTE]
>
>已經佈建舊版專用輸出技術而需要設定這些選項之一的客戶不應這麼做，否則網站連線能力可能會受波及。請聯絡 Adobe 支援以取得協助。

## 彈性連接埠輸出 {#flexible-port-egress}

此進階網路功能允許您設定 AEM as a Cloud Service 透過預設開啟的 HTTP (連接埠 80) 和 HTTPS (連接埠 443) 以外的連接埠輸出流量。

### 考量事項 {#flexible-port-egress-considerations}

如果您不需要 VPN 並且不需要專用輸出 IP 位址，則建議選擇彈性連接埠輸出，因為不依賴專用出口的流量可以達到更高的輸出量。

### 設定 {#configuring-flexible-port-egress-provision}

對每個程式會叫用一次 POST`/program/<programId>/networkInfrastructures` 端點，直接傳遞 `flexiblePortEgress` 的值 (`kind` 參數和區域)。 端點會以 `network_id` 及其他資訊回應，包括狀態。 完整的參數集和確切的語法，以及如哪些參數之後不能變更等重要資訊，[可以在 API 文件中參考。](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)

呼叫後，通常需要大約 15 分鐘的時間來佈建網路基礎結構。對 Cloud Manager 的[網路基礎結構 GET 端點](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure)的呼叫會顯示「就緒」狀態。

如果程式範圍的彈性連接埠輸出設定準備就緒，則必須對每個環境叫用 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端點，以在環境層級啟用網路以及選擇性地宣告任何連接埠轉送規則。參數可根據環境設定，以提供靈活性。

應透過指定目標主機集 (名稱或 IP，以及使用連接埠) 為 80/443 以外的任何目標連接埠宣告連接埠轉送規則，但前提是不使用 http 或 https 通訊協定：對於每個目標主機，客戶必須將預期的目標連接埠對應到 30000 到 30999 之間的連接埠。

API 應該在幾秒鐘內回應，指示更新狀態，大約 10 分鐘後，端點的 `GET` 方法應指出進階網路已啟用。

### 更新 {#updating-flexible-port-egress-provision}

程式層級設定可以透過叫用 `PUT /api/program/<program_id>/network/<network_id>` 端點進行更新，並且將在幾分鐘內生效。

>[!NOTE]
>
> 「kind」參數 (`flexiblePortEgress`、`dedicatedEgressIP` 或 `VPN`) 無法修改。請聯絡客戶支援以尋求協助，描述已經建立的內容和變更的原因。

可以透過再次叫用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端點來更新每個環境的連接埠轉送規則，確保包括完整的設定參數集，而不是子集。

### 停用彈性連接埠輸出 {#disabling-flexible-port-egress-provision}

為了&#x200B;**停用**&#x200B;來自特定環境的彈性連接埠輸出，請叫用 `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`。

如需關於 API 的詳細資訊，請參閱 [Cloud Manager API 文件](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)。

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

如果使用非標準 Java 網路程式庫，請使用上述屬性為所有流量設定 Proxy。

目標流經 `portForwards` 參數中宣告的連接埠的非 http/s 流量應該參照一個名為 `AEM_PROXY_HOST` 的屬性，以及對應的連接埠。 例如：

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

**Apache / Dispatcher 設定**

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

## 專用輸出 IP 位址 {#dedicated-egress-IP-address}

>[!NOTE]
>
>如果在 2021 年 9 月版本 (10/6/21) 之前已為您佈建專用輸出 IP，請參考[舊版專用輸出位址客戶](#legacy-dedicated-egress-address-customers)。

### 優點 {#benefits}

在與 SaaS 廠商 (如 CRM 廠商) 整合或在 AEM as a Cloud Service 之外有提供 IP 位址允許清單的其他整合時，這個專用的 IP 位址可以增強安全性。透過將專用的 IP 位址新增到允許清單，可確保只允許來自客戶的 AEM Cloud Service 的流量流入外部服務。這是在來自任何其他 IPS 允許的流量之外的補充。

如果沒有啟用專用 IP 位址功能，來自 AEM as a Cloud Service 的流量會流經與其他客戶共用的一組 IP。

### 設定 {#configuring-dedicated-egress-provision}

>[!INFO]
>
>專用輸出 IP 位址無法提供 Splunk 轉送功能。

設定專用輸出 IP 位址與[彈性連接埠輸出](#configuring-flexible-port-egress-provision)同出一轍。

主要區別在於流量一律從專用的、唯一的 IP 輸出。要尋找該 IP，請使用 DNS 解析器識別與 `p{PROGRAM_ID}.external.adobeaemcloud.com` 相關聯的 IP 位址。 該 IP 位址預期不會變更，但如果將來需要變更，將提供事先通知。

除了 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端點中的彈性連接埠輸出支援的路由規則之外，專用輸出 IP 位址還支援 `nonProxyHosts` 參數。這允許您宣告一組應該路由經過共用 IP 位址範圍而不是專用 IP 的主機，這可能很有用，因為經過共用 IPS 輸出的流量可能得到進一步最佳化。`nonProxyHost` URL 可能遵循 `example.com` 或`*.example.com` 的模式，其中僅在網域開頭支援萬用字元。

在決定使用彈性連接埠輸出或專用輸出 IP 位址時，如果不需要特定的 IP 位址，客戶應該選擇彈性連接埠輸出，因為 Adobe 可以最佳化彈性連接埠輸出流量的效能。

### 停用專用輸出 IP 位址 {#disabling-dedicated-egress-IP-address}

為了&#x200B;**停用**&#x200B;來自特定環境的專用輸出 IP 位址，請叫用 `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`。

如需關於 API 的詳細資訊，請參閱 [Cloud Manager API 文件](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)。

### 流量路由 {#dedcated-egress-ip-traffic-routing}

Http 或 https 流量將流經預先設定的 Proxy，前提是它們使用標準 Java 系統屬性進行 Proxy 設定。

目標流經`portForwards` 參數中宣告的連接埠的非 http/s 流量應該參照一個名為 `AEM_PROXY_HOST` 的屬性，以及對應的連接埠。 例如：

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
    <td>流經 http proxy 設定，預設針對使用標準 Java HTTP 用戶端程式庫的 http/s 流量所設定</td>
    <td>任何</td>
    <td>流經專用輸出 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http proxy 設定 (例如，如果從標準 Java HTTP 用戶端程式庫中明確移除，或者如果使用忽略標準 Proxy 設定的 Java 程式庫)</td>
    <td>80 或 443</td>
    <td>流經共用叢集 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http proxy 設定 (例如，如果從標準 Java HTTP 用戶端程式庫中明確移除，或者如果使用忽略標準 Proxy 設定的 Java 程式庫)</td>
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

## 功能使用情況 {#feature-usage}

功能與導致輸出流量的 Java 程式碼或程式庫相容，前提是它們使用標準 Java 系統屬性進行 Proxy 設定。實際上，這應該包括最常見的程式庫。

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

一些程式庫需要明確設定才能使用標準 Java 系統屬性進行 Proxy 設定。

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

相同的專用 IP 適用於客戶在其 Adobe 組織中的所有程式以及每個程式中的所有環境。它適用於作者和發佈服務。

### 偵錯考量 {#debugging-considerations}

為了驗證流量確實在預期的專用 IP 位址上傳出，請檢查目標服務中的記錄 (如果可用)。否則，呼叫偵錯服務可能會有幫助，例如 [https://ifconfig.me/IP](https://ifconfig.me/IP)，這將傳回呼叫的 IP 位址。

## 舊版專用輸出位址客戶 {#legacy-dedicated-egress-address-customers}

如果在 2021.09.30 之前已為您佈建專用輸出 IP，則您的專用輸出 IP 功能僅支援 HTTP 和 HTTPS 連接埠。
這包括 HTTP/1.1 和加密後的 HTTP/2。此外，一個專用輸出端點可以分別透過連接埠 80/443 上的 HTTP/HTTPS 與任何目標通訊。

## 虛擬私人網路 (VPN) {#vpn}

VPN 允許從著作、發佈或預覽連線到內部部署基礎結構或資料中心。例如，用於存取資料庫的方法。

它還允許連線到 SaaS 廠商，例如支援 VPN 的 CRM 廠商，或從公司網路連線到 AEM as a Cloud Service 著作、預覽或發佈。

支援大多數採用 IPSec 技術的 VPN 裝置。 請查閱[本頁](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable)的裝置清單，根據 **RouteBased 設定指示**&#x200B;欄中的資訊。按照表中所述設定裝置。

### 一般考量 {#general-vpn-considerations}

* 支援僅限於單一 VPN 連線
* Splunk 轉送功能無法透過 VPN 連線提供。

### 建立 {#vpn-creation}

對每個程式會叫用一次 POST `/program/<programId>/networkInfrastructures` 端點，傳遞設定資訊的承載，包括：`kind` 參數的值「vpn」、區域、位址空間 (CIDR 清單 - 請注意，這之後不能修改)、DNS 解析器 (用於解析客戶網路中的名稱) 和 VPN 連線資訊，例如閘道設定、共用 VPN 金鑰和 IP 安全性原則。端點會以 `network_id` 及其他資訊回應，包括狀態。 應參考 [API 文件](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)中完整的參數集和確切的語法。

呼叫後，通常需要 45 到 60 分鐘的時間來佈建網路基礎結構。可以呼叫 API 的 GET 方法傳回目前狀態，這最終會從 `creating` 轉成 `ready`。請參閱 API 文件以了解各種狀態。

如果程式範圍的 VPN 設定準備就緒，則必須對每個環境叫用 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端點，以在環境層級啟用網路以及宣告任何連接埠轉送規則。參數可根據環境設定，以提供靈活性。

請參閱 [API 文件](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration)以取得詳細資訊。

對於任何應透過 VPN 路由的非 http/s 協訊協定 TCP 流量，應透過指定目標主機集 (名稱或 IP，以及連接埠) 來宣告連接埠轉送規則。對於每個目標主機，客戶必須將預期的目標連接埠對應到 30000 到 30999 之間的連接埠，其中的值在程式的各個環境中必須是唯一的。客戶還可以在 `nonProxyHosts` 參數中列出一組 URL，這會針對應繞過 VPN 路由，但卻透過共用 IP 範圍的流量宣告 URL。它遵循 `example.com` 或 `*.example.com` 的模式，其中僅在網域開頭支援萬用字元。

API 應該在幾秒鐘內做出回應，表明 `updating` 的狀態，大約 10 分鐘後，呼叫 Cloud Manager 的環境 GET 端點將顯示 `ready` 的狀態，表示已套用對環境的更新。

請注意，即使沒有環境流量路由規則 (主機或旁路)，仍然必須用空白承載呼叫 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`。

### 更新 VPN {#updating-the-vpn}

程式層級 VPN 設定可以透過叫用 `PUT /api/program/<program_id>/network/<network_id>` 端點進行更新。

請注意，在初始 VPN 佈建後，無法變更位址空間。如果有必要，請聯絡客戶支援。此外，`kind` 參數 (`flexiblePortEgress`、`dedicatedEgressIP` 或 `VPN`) 無法修改。請聯絡客戶支援以尋求協助，描述已經建立的內容和變更的原因。

可以透過再次叫用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端點來更新每個環境的路由規則，確保包括完整的設定參數集，而不是子集。 套用環境更新通常需要 5-10 分鐘的時間。

### 停用 VPN {#disabling-the-vpn}

要為特定環境停用 VPN，請叫用 `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`。 [API 文件](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)中有更多詳細資料。

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
    <td>如果 IP 在 <i>VPN 閘道位址</i>空間範圍內，並透過 http proxy 設定 (預設針對使用標準 Java HTTP 用戶端程式庫的 http/s 流量所設定)</td>
    <td>任何</td>
    <td>流經 VPN</td>
    <td><code>10.0.0.1:443</code>它也可以是主機名稱。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果 IP 不在 <i>VPN 閘道位址</i>空間範圍內，並透過 http proxy 設定 (預設針對使用標準 Java HTTP 用戶端程式庫的 http/s 流量所設定)</td>
    <td>任何</td>
    <td>流經專用輸出 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http proxy 設定 (例如，如果從標準 Java HTTP 用戶端程式庫中明確移除，或者如果使用忽略標準 Proxy 設定的 Java 程式庫)
</td>
    <td>80 或 443</td>
    <td>流經共用叢集 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http proxy 設定 (例如，如果從標準 Java HTTP 用戶端程式庫中明確移除，或者如果使用忽略標準 Proxy 設定的 Java 程式庫)</td>
    <td>80 或 443 之外的連接埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http 或非 https</b></td>
    <td>如果 IP 在 <i>VPN 閘道位址空間</i>範圍內，並且用戶端連線到 <code>AEM_PROXY_HOST</code> 環境變數 (使用 <code>portOrig</code> 在 <code>portForwards</code>API 參數中宣告)</td>
    <td>任何</td>
    <td>流經 VPN</td>
    <td><code>10.0.0.1:3306</code>它也可以是主機名稱。</td>
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

### 供設定的實用網域{#vpn-useful-domains-for-configuration}

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
    <td>來自 VPN 的連線在 CDN 上會顯示為來自此 IP。 若是要只允許來自 VPN 的連線進入 AEM，請將 Cloud Manager 設定為僅允許此 IP 並封鎖其他所有一切。請參閱「限制輸入 VPN 連線」一節以取得詳細資料。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/A</td>
    <td>AEM 端 VPN 閘道的 IP。 客戶的網路工程團隊可以使用此項，僅允許從特定 IP 位址的 VPN 連線到他們的 VPN 閘道。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>來自 VPN 的 AEM 端到客戶端之流量的 IP。 這可以在客戶的設定中加入允許清單，以確保只能從 AEM 建立連線。</td>
    <td>如果客戶想要允許 VPN 存取 AEM，他們應該設定 CNAME DNS 項目，將他們的自訂網域和/或 <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 和/或 <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 對應至此。</td>
  </tr>
</tbody>
</table>

### 將 VPN 限制為輸入連線 {#restrict-vpn-to-ingress-connections}

如果您只想允許 VPN 存取 AEM，則可以在 Cloud Manager 中設定環境允許清單，如此只有由 `p{PROGRAM_ID}.external.adobeaemcloud.com` 定義的 IP 允許與環境交談。 就像 Cloud Manager 中任何其他基於 IP 的允許清單一樣，這也可以相同方式完成。

如果規則必須基於路徑，請在 Dispatcher 層級使用標準的 http 指令來拒絕或允許某些 IP。他們同時應該確保所要的路徑不可快取在 CDN 上，讓請求始終可到達來源。

**Httpd 設定範例**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 刪除程式的網路基礎結構 {#deleting-network-infrastructure}

要&#x200B;**刪除**&#x200B;程式的網路基礎結構，請叫用 `DELETE /program/{program ID}/networkinfrastructure/{networkinfrastructureID}`。

>[!NOTE]
>
> 如果所有環境都停用了進階網路，則刪除作業只會刪除基礎結構。

## 在進階網路類型之間轉換 {#transitioning-between-advanced-networking-types}

可以按照以下程序在進階網路類型之間移轉：

* 在所有環境中停用進階網路
* 刪除進階網路基礎結構
* 使用正確的值重新建立進階網路基礎結構
* 重新啟用環境層級進階網路

>[!WARNING]
>
> 此程序將導致進階網路服務在刪除和重新建立之間停機

如果停機導致顯著的業務衝擊，請聯絡客戶支援以尋求協助，描述已經建立的內容和變更的原因。
