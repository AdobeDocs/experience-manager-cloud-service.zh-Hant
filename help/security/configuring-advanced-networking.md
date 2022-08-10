---
title: 配置高級網路AEM以as a Cloud Service
description: 瞭解如何配置高級網路功能，如VPN或靈活或專用的出口IP地址，以便AEMas a Cloud Service
exl-id: 968cb7be-4ed5-47e5-8586-440710e4aaa9
source-git-commit: b8a827e73d8eba9184be352d0aa4705dfb24b642
workflow-type: tm+mt
source-wordcount: '3016'
ht-degree: 1%

---

# 配置高級網路AEM以as a Cloud Service {#configuring-advanced-networking}

本文旨在向您介紹as a Cloud Service中的不同高級網路功能AEM，包括VPN的自助配置、非標準埠和專用出口IP地址。

>[!INFO]
>
>您還可以找到一系列文章，旨在指導您瞭解此處的每個高級網路選項 [位置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=en)。

## 概觀 {#overview}

AEMas a Cloud Service提供多種高級網路功能，客戶可使用Cloud Manager API進行配置。 這些包括：

* [靈活的埠出口](#flexible-port-egress)  — 配AEM置as a Cloud Service以允許非標準埠的出站通信
* [專用出口IP地址](#dedicated-egress-IP-address)  — 配置as a Cloud ServiceAEM之外的流量以源於唯一IP
* [虛擬專用網(VPN)](#vpn)  — 為具有VPN技術的客戶保AEM護客戶基礎架構和as a Cloud Service之間的通信

本文詳細介紹了這些選項中的每一個，包括如何配置這些選項。 作為一般配置策略， `/networkInfrastructures` 在程式級別調用API端點以聲明所需類型的高級網路，然後調用到 `/advancedNetworking` 用於每個環境的終結點，以啟用基礎架構並配置特定於環境的參數。 請參考Cloud Manager API文檔中每個正式語法的相應終結點以及示例請求和響應。

程式可以設定單個高級網路變體。 在決定靈活埠出口和專用出口IP地址時，建議在不需要特定IP地址時選擇靈活的埠出口，因為Adobe可以優化靈活埠出口通信的效能。

>[!INFO]
>
>沙盒程式不提供高級網路。
>此外，環境必須升級AEM到5958版或更高版本。

>[!NOTE]
>
>已配置了舊式專用出口技術的客戶，如果需要配置其中一個選項，則不應這樣做，否則站點連接可能會受到影響。 請與Adobe支援部門聯繫以獲得幫助。

## 靈活埠出口 {#flexible-port-egress}

此高級網路功能允許AEM您配置as a Cloud Service，以通過預設開啟的HTTP（埠80）和HTTPS（埠443）以外的埠傳輸通信。

### 注意事項 {#flexible-port-egress-considerations}

如果您不需要VPN並且不需要專用出口IP地址，則建議選擇靈活的埠出口，因為不依賴專用出口的通信可以獲得更高的吞吐量。

### 設定 {#configuring-flexible-port-egress-provision}

每個程式一次，POST `/program/<programId>/networkInfrastructures` 調用端點，僅傳遞 `flexiblePortEgress` 為 `kind` 參數和區域。 端點用 `network_id`，以及包括狀態在內的其他資訊。 API文檔中應引用全套參數和準確語法。

調用後，配置網路基礎架構通常需要大約15分鐘。 呼叫雲管理器 [網路基礎架構GET](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) 將顯示「ready」狀態。

如果程式範圍的靈活埠出口配置已就緒， `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 必鬚根據環境調用端點，以在環境級別啟用網路，並可選地聲明任何埠轉發規則。 可根據環境配置參數，以提供靈活性。

對於除80/443以外的任何目標埠，應聲明埠轉發規則，但僅當不使用http或https協定時，才應指定目標主機集（名稱或IP，並帶有埠）。 對於每個目標主機，客戶必須將目標埠映射到從30000到30999的埠。

API應在幾秒內作出響應，指示更新狀態，大約10分鐘後，終結點的 `GET` 方法應指示已啟用高級網路。

### 更新 {#updating-flexible-port-egress-provision}

可通過調用 `PUT /api/program/<program_id>/network/<network_id>` 將在幾分鐘內生效。

>[!NOTE]
>
> &quot;kind&quot;參數(`flexiblePortEgress`。 `dedicatedEgressIP` 或 `VPN`)。 聯繫客戶支援以獲得幫助，說明已建立的內容和更改的原因。

通過再次調用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端點，確保包括完整的配置參數集，而不是子集。

### 禁用靈活埠出口 {#disabling-flexible-port-egress-provision}

為了 **禁用** 從特定環境執行靈活埠出口，調用 `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`。

有關API的詳細資訊，請參見 [Cloud Manager API文檔](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)。

### 流量路由 {#flexible-port-egress-traffic-routing}

對於流向80或443以外埠的http或https通信，應使用以下主機和埠環境變數配置代理：

* 對於HTTP: `AEM_PROXY_HOST` / `AEM_HTTP_PROXY_PORT ` (預設為 `proxy.tunnel:3128` 在AEM版本&lt; 6094)
* 對於HTTPS: `AEM_PROXY_HOST` / `AEM_HTTPS_PROXY_PORT ` (預設為 `proxy.tunnel:3128` 在AEM版本&lt; 6094)

例如，此處是將請求發送到 `www.example.com:8443`:

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

如果使用非標準Java網路庫，請為所有通信配置使用上述屬性的代理。

通過在中聲明的埠進行目標的非http/s通信 `portForwards` 參數應引用名為 `AEM_PROXY_HOST`，以及映射的埠。 例如：

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

下表說明了流量路由：

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目標條件</th>
    <th>埠</th>
    <th>連線</th>
    <th>外部目標示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP或https協定</b></td>
    <td>標準http/s通信</td>
    <td>八十、四百四十三</td>
    <td>允許</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>通過使用以下環境變數和代理埠號配置的http代理的非標準通信量（在80或443以外的其他埠上）。 不要在Cloud Manager API調用的portForws參數中聲明目標埠：<br><ul>
     <li>AEM_PROXY_HOST(在版本&lt; 6094中預設為「proxy.tunnel」AEM)</li>
     <li>AEM_HTTPS_PROXY_PORT(在版本&lt; 6094中預設為端AEM口3128)</li>
    </ul>
    <td>80或443以外的埠</td>
    <td>允許</td>
    <td>example.com:8443</td>
  </tr>
  <tr>
    <td></td>
    <td>非標準通信量（在埠80或443之外的其他埠上）不使用http代理</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>客戶端連接到 <code>AEM_PROXY_HOST</code> 環境變數使用 <code>portOrig</code> 在 <code>portForwards</code> API參數。</td>
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

**Apache/Dispatcher配置**

AEM Cloud ServiceApache/Dispatcher層 `mod_proxy` 可以使用上述屬性配置指令。

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

## 專用出口IP地址 {#dedicated-egress-IP-address}

>[!NOTE]
>
>如果您在2021年9月版本(10/6/21)之前已配置了專用出口IP，請參閱 [舊式專用出口地址客戶](#legacy-dedicated-egress-address-customers)。

### 好處 {#benefits}

當與SaaS供應商（如CRM供應商）整合時，此專用IP地址可增強安全性，或在as a Cloud Service之外提供AEMIP地址允許清單的其他整合。 通過將專用IP地址添加到允許清單，它確保僅允許來自客戶的AEM Cloud Service的流量流入外部服務。 這是除了允許來自任何其他IP的通信外。

如果沒有啟用專用IP地址功能，則從AEMas a Cloud Service的IP中傳出的流量會通過與其他客戶共用的一組IP流。

### 設定 {#configuring-dedicated-egress-provision}

>[!INFO]
>
>Splunk轉發功能不能從專用的出口IP地址進行。

配置專用出口IP地址與 [柔性埠出口](#configuring-flexible-port-egress-provision)。

主要區別在於，通信總是會從專用、唯一的IP流出。 要查找該IP，請使用DNS解析程式標識與 `p{PROGRAM_ID}.external.adobeaemcloud.com`。 IP地址不會更改，但如果將來需要更改，將提供高級通知。

除了中靈活埠出口支援的路由規則外， `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端點，專用出口IP地址支援 `nonProxyHosts` 的下界。 這允許您聲明一組應通過共用IP地址範圍而不是專用IP路由的主機，這可能非常有用，因為通過共用IP的流量可能會進一步優化。 的 `nonProxyHost` URL可能遵循以下模式 `example.com` 或 `*.example.com`，其中只在域的開頭支援通配符。

在確定靈活的埠出口和專用的出口IP地址時，如果不需要特定的IP地址，客戶應選擇靈活的埠出口，因為Adobe可以優化靈活的埠出口通信的效能。

### 禁用專用出口IP地址 {#disabling-dedicated-egress-IP-address}

為了 **禁用** 特定環境的專用出口IP地址，調用 `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`。

有關API的詳細資訊，請參見 [Cloud Manager API文檔](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)。

### 流量路由 {#dedcated-egress-ip-traffic-routing}

Http或https通信將通過預配置的代理，前提是它們使用標準Java系統屬性進行代理配置。

通過在中聲明的埠進行目標的非http/s通信 `portForwards` 參數應引用名為 `AEM_PROXY_HOST`，以及映射的埠。 例如：

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目標條件</th>
    <th>埠</th>
    <th>連線</th>
    <th>外部目標示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP或https協定</b></td>
    <td>到Azure或Adobe服務的流量</td>
    <td>任何</td>
    <td>通過共用群集IP（而非專用IP）</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>與 <code>nonProxyHosts</code> 參數</td>
    <td>八十、四百四十三</td>
    <td>通過共用群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>與 <code>nonProxyHosts</code> 參數</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>通過http代理配置，預設使用標準Java HTTP客戶端庫為http/s通信配置</td>
    <td>任何</td>
    <td>通過專用出口IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果從標準Java HTTP客戶端庫中顯式刪除，或者使用忽略標準代理配置的Java庫）</td>
    <td>八十、四百四十三</td>
    <td>通過共用群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果從標準Java HTTP客戶端庫中顯式刪除，或者使用忽略標準代理配置的Java庫）</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>客戶端連接到 <code>AEM_PROXY_HOST</code> env變數使用 <code>portOrig</code> 在 <code>portForwards</code> API參數</td>
    <td>任何</td>
    <td>通過專用出口IP</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>其他任何</td>
    <td></td>
    <td>已封鎖</td>
    <td></td>
  </tr>
</tbody>
</table>

## 功能使用 {#feature-usage}

該功能與導致出站通信的Java代碼或庫相容，前提是它們使用標準Java系統屬性進行代理配置。 在實踐中，這應包括最常見的圖書館。

下面是代碼示例：

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

某些庫需要顯式配置才能使用標準Java系統屬性進行代理配置。

使用Apache HttpClient的示例，需要顯式調用
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) 或
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem()):

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

同一專用IP適用於客戶Adobe組織中的所有計畫以及每個計畫中的所有環境。 它適用於作者和發佈服務。

### 調試注意事項 {#debugging-considerations}

為了驗證通信確實在預期的專用IP地址上傳出，請檢查目標服務中的日誌（如果可用）。 否則，呼叫調試服務(例如 [https://ifconfig.me/IP](https://ifconfig.me/IP)，將返回呼叫IP地址。

## 舊式專用出口地址客戶 {#legacy-dedicated-egress-address-customers}

如果您在2021.09.30之前已使用專用出口IP進行配置，則專用出口IP功能僅支援HTTP和HTTPS埠。
這包括加密時的HTTP/1.1和HTTP/2。

## 虛擬專用網(VPN) {#vpn}

VPN允許通過作者、發佈或預覽連接到內部基礎架構或資料中心。 例如，用於訪問資料庫的方法。

它還允許連接到SaaS供應商，如支援VPN的CRM供應商，或從公司網路連接到AEMas a Cloud Service作者、預覽或發佈。

大多數採用IPSec技術的VPN設備都受支援。 請查閱位於的設備清單 [此頁](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable)，根據 **基於路由的配置說明** 的雙曲餘切值。 按照表中所述配置設備。

### 一般注意事項 {#general-vpn-considerations}

* 僅支援單個VPN連接
* VPN連接上不能使用Splunk轉發功能。

### 建立 {#vpn-creation}

每個程式一次，POST `/program/<programId>/networkInfrastructures` 調用端點，傳遞配置資訊的負載，包括：「vpn」的值 `kind` 參數、區域、地址空間（CIDR清單 — 請注意，以後無法修改）、DNS解析器（用於解析客戶網路中的名稱）和VPN連接資訊（如網關配置、共用VPN密鑰和IP安全策略）。 端點用 `network_id`，以及包括狀態在內的其他資訊。 在中應引用完整的參數集和精確語法 [API文檔](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)。

一旦調用，配置網路基礎架構通常需要45到60分鐘。 可以調用API的GET方法以返回當前狀態，該狀態將最終從 `creating` 至 `ready`。 請查閱API文檔以瞭解所有狀態。

如果程式範圍的VPN配置已就緒， `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 必鬚根據環境調用端點，以在環境級別啟用網路並聲明任何埠轉發規則。 可根據環境配置參數，以提供靈活性。

查看 [API文檔](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) 的子菜單。

對於應通過VPN路由的任何非http/s協定TCP通信，應聲明埠轉發規則，方法是指定目標主機集（名稱或IP，並帶有埠）。 對於每個目標主機，客戶必須將目標埠映射到從30000到30999的埠，在該埠中，值必須在程式中的各個環境中是唯一的。 客戶還可以在 `nonProxyHosts` 參數，它聲明流量應繞過VPN路由的URL，而是通過共用IP範圍。 它遵循 `example.com` 或 `*.example.com`，其中只在域的開頭支援通配符。

API應在幾秒內響應，表示 `updating` 大約10分鐘後，調用Cloud Manager的環境GET終結點時，將顯示 `ready`，表示已應用對環境的更新。

請注意，即使沒有環境通信路由規則（主機或旁路）, `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 必須仍然被調用，只要負載為空。

### 更新VPN {#updating-the-vpn}

通過調用 `PUT /api/program/<program_id>/network/<network_id>` 端點。

請注意，初始VPN設定後，地址空間不能更改。 如有必要，請與客戶支援聯繫。 另外， `kind` 參數(`flexiblePortEgress`。 `dedicatedEgressIP` 或 `VPN`)。 聯繫客戶支援以獲得幫助，說明已建立的內容和更改的原因。

通過再次調用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端點，確保包括完整的配置參數集，而不是子集。 應用環境更新通常需要5到10分鐘。

### 禁用VPN {#disabling-the-vpn}

要為特定環境禁用VPN，請調用 `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`。 中的詳細資訊 [API文檔](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)。

### 流量路由 {#vpn-traffic-routing}

下表介紹了流量路由。

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目標條件</th>
    <th>埠</th>
    <th>連線</th>
    <th>外部目標示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP或https協定</b></td>
    <td>到Azure或Adobe服務的流量</td>
    <td>任何</td>
    <td>通過共用群集IP（而非專用IP）</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>與 <code>nonProxyHosts</code> 參數</td>
    <td>八十、四百四十三</td>
    <td>通過共用群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>與 <code>nonProxyHosts</code> 參數</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP在 <i>VPN網關地址</i> 空間範圍，並通過http代理配置（預設使用標準Java HTTP客戶端庫為http/s通信配置）</td>
    <td>任何</td>
    <td>通過VPN</td>
    <td><code>10.0.0.1:443</code>它也可以是主機名。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP不掉入 <i>VPN網關地址空間</i> 範圍，並通過http代理配置（預設使用標準Java HTTP Client庫為http/s通信配置）</td>
    <td>任何</td>
    <td>通過專用出口IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果從標準Java HTTP客戶端庫中顯式刪除，或者使用忽略標準代理配置的Java庫）
</td>
    <td>八十、四百四十三</td>
    <td>通過共用群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果從標準Java HTTP客戶端庫中顯式刪除，或者使用忽略標準代理配置的Java庫）</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>如果IP在 <i>VPN網關地址空間</i> 範圍和客戶端連接到 <code>AEM_PROXY_HOST</code> env變數使用 <code>portOrig</code> 在 <code>portForwards</code> API參數</td>
    <td>任何</td>
    <td>通過VPN</td>
    <td><code>10.0.0.1:3306</code>它也可以是主機名。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP不掉入 <i>VPN網關地址空間</i> 範圍和客戶端連接 <code>AEM_PROXY_HOST</code> env變數使用 <code>portOrig</code> 在 <code>portForwards</code> API參數</td>
    <td>任何</td>
    <td>通過專用出口IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>其他任何</td>
    <td>任何</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
</tbody>
</table>

### 配置的有用域{#vpn-useful-domains-for-configuration}

下圖提供了一組域和關聯IP的可視表示，這些IP對配置和開發非常有用。 下圖的下表進一步說明了這些域和IP。

![VPN域配置](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>域模式</th>
    <th>出口(從AEM)含義</th>
    <th>入口(到AEM)含義</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>專用出口IP地址，用於通過Internet而不是專用網路傳輸流量 </td>
    <td>來自VPN的連接將顯示在CDN上，即來自此IP。 要僅允許從VPN連接進入，AEM請配置雲管理器，以僅允許此IP並阻止其他所有內容。 有關詳細資訊，請參閱「限制VPN連接入口」部分。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/A</td>
    <td>VPN網關的IP位AEM於一側。 客戶的網路工程團隊可以使用此功能僅允許從特定IP地址到其VPN網關的VPN連接。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>從VPN側到客AEM戶側的通信的IP。 這可以在客戶配置中列出，以確保只能從中建立連AEM接。</td>
    <td>如果客戶希望允許VPN訪問，AEM他們應配置CNAME DNS條目以映射其自定義域和/或 <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 和/或 <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 這個。</td>
  </tr>
</tbody>
</table>

### 將VPN限制為入口連接 {#restrict-vpn-to-ingress-connections}

如果您只允許VPN訪問，AEM則可以在雲管理器中配置環境允許清單，以便僅通過 `p{PROGRAM_ID}.external.adobeaemcloud.com` 才能與環境溝通。 這可以與雲管理器中任何其他基於IP的允許清單的方式相同。

如果規則必須基於路徑，請在調度程式級別使用標準http指令拒絕或允許某些IP。 它們應確保在CDN上也不可快取所需路徑，以便請求始終到達原點。

**Httpd配置示例**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 刪除程式的網路基礎架構 {#deleting-network-infrastructure}

至 **刪除** 程式的網路基礎架構，調用 `DELETE /program/{program ID}/networkinfrastructure/{networkinfrastructureID}`。

>[!NOTE]
>
> 僅當所有環境都禁用其高級網路時，「刪除」將刪除基礎結構。

## 在高級網路類型之間轉換 {#transitioning-between-advanced-networking-types}

可以通過以下步驟在高級網路類型之間遷移：

* 在所有環境中禁用高級網路
* 刪除高級網路基礎架構
* 使用正確的值重新建立高級網路資訊
* 啟用環境級高級網路

>[!WARNING]
>
> 此過程將導致刪除和重新建立之間的高級網路服務停機

如果停機會對業務產生重大影響，請聯繫客戶支援以獲得幫助，介紹已建立的內容和更改的原因。
