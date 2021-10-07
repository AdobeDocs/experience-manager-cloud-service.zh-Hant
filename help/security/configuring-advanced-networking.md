---
title: 配置AEMas a Cloud Service的高級網路
description: 了解如何配置高級網路功能，如VPN或專用的輸出IP地址，以便AEMas a Cloud Service
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '2797'
ht-degree: 1%

---


# 配置AEMas a Cloud Service的高級網路 {#configuring-advanced-networking}

>[!INFO]
>
>進階網路功能是2021.9.0版的一部分，將於10月中旬為客戶啟用。

AEM as a Cloud Service提供數種進階網路功能，可由使用Cloud Manager API的客戶進行設定。 這些包括：

* [靈活的埠輸出](#flexible-port-egress)  — 配置AEMas a Cloud Service，以允許非標準埠的出站流量
* [專用輸出IP位址](#dedicated-egress-IP-address)  — 將流量從AEMas a Cloud Service配置為源自唯一IP
* [虛擬專用網路](#vpn)  — 為擁有VPN技術的客戶，確保客戶基礎架構與AEMas a Cloud Service之間的安全流量

本文詳細說明每個選項，包括如何設定。 作為一般配置策略，在程式級別調用`/networkInfrastructures` API端點以聲明所需的高級網路類型，然後為每個環境調用`/advancedNetworking`端點以啟用基礎架構並配置特定於環境的參數。 請參考Cloud Manager API檔案中各正式語法的適當端點，以及範例要求和回應。

當在靈活的埠輸出和專用的輸出IP地址之間進行決定時，如果不需要特定的IP地址，建議您選擇靈活的埠輸出，因為Adobe可以優化靈活的埠輸出通信的效能。

>[!INFO]
>
>沙箱方案無法使用進階網路。

>[!NOTE]
>
>已布建舊版專用出口技術的客戶若需要配置其中一個選項，則不應如此，否則網站連線可能會受到影響。 請聯絡Adobe支援以取得協助。

## 靈活的埠輸出 {#flexible-port-egress}

此進階網路功能可讓您設定AEM as a Cloud Service，以透過HTTP（埠80）和HTTPS（埠443）以外的預設開啟的埠輸出流量。

### 考量事項 {#flexible-port-egress-considerations}

如果您不需要VPN並且不需要專用的輸出IP地址，則建議選擇靈活的埠輸出，因為不依賴專用輸出的通信可以實現更高的吞吐量。

### 設定 {#configuring-flexible-port-egress-provision}

一旦每個程式調用POST`/program/<programId>/networkInfrastructures`端點，只需為`kind`參數和區域傳遞`flexiblePortEgress`值。 端點會以`network_id`回應，以及包含狀態的其他資訊。 API檔案中應參考完整的參數集和確切語法。

呼叫後，配置網路基礎架構通常需要約15分鐘。 呼叫Cloud Manager的[environment GET端點](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getEnvironment)時，會顯示狀態為「ready」。

如果程式範圍的靈活埠輸出配置已就緒，則必須為每個環境調用`PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`端點，以啟用環境級別的網路並聲明任何埠轉發規則。 參數可依環境設定，以提供彈性。

應通過指定目標主機集（名稱或IP，以及埠），為80/443以外的任何埠聲明埠轉發規則。 對於每個目標主機，客戶必須將目標埠映射到30000到30999的埠。

API應在幾秒內回應，指出更新狀態，大約10分鐘後，端點的`GET`方法應指出已啟用進階網路。

### 更新 {#updating-flexible-port-egress-provision}

調用`PUT /api/program/<program_id>/network/<network_id>`端點可以更新程式級配置，並在幾分鐘內生效。

>[!NOTE]
>
> 無法修改&quot;kind&quot;參數（`flexiblePortEgress`、`dedicatedEgressIP`或`VPN`）。 請聯絡客戶支援以取得協助，說明已建立的項目和變更的原因。

可通過再次調用`PUT /program/{programId}/environment/{environmentId}/advancedNetworking`端點來更新每個環境埠轉發規則，確保包含完整的配置參數集，而不是子集。

### 刪除或禁用靈活埠輸出 {#deleting-disabling-flexible-port-egress-provision}

為了&#x200B;**刪除**&#x200B;網路基礎架構，請提交客戶支援票證，說明已建立的內容以及需要刪除的原因。

為了從特定環境中&#x200B;**禁用**&#x200B;靈活埠輸出，請調用`DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`。

如需詳細資訊，請參閱[Cloud Manager API檔案](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)。

### 流量路由 {#flexible-port-egress-traffic-routing}

透過連接埠80或443前往目的地的HTTP或https流量，會透過預先設定的Proxy（假設使用標準Java網路程式庫）。 對於通過其他埠的http或https流量，應使用下列屬性來配置代理。

* `AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST`
* `AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT`

例如，以下是傳送要求至`www.example.com:8443`的范常式式碼：

```java
HttpsHost target = new HttpsHost("example.com", 8443, "https");
 
HttpHost proxy = new HttpHost(System.getenv("AEM_HTTPS_PROXY_HOST"),
                              Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT")),
                              "https");
 
RequestConfig config = RequestConfig.custom().setProxy(proxy).build();
 
HttpGet request = new HttpGet("/");
request.setConfig(config);
CloseableHttpResponse response = httpclient.execute(target, request);
```

如果使用非標準Java網路庫，請針對所有流量使用上述屬性來配置Proxy。

透過`portForwards`參數中宣告之埠而具有目的地的非http/s流量應參考名為`AEM_PROXY_HOST`的屬性以及對應的埠。 例如：

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

下表介紹了流量路由：

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目的地條件</th>
    <th>埠</th>
    <th>連線</th>
    <th>範例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http或https通訊協定</b></td>
    <td>標準http/s流量</td>
    <td>80或443</td>
    <td>允許</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>使用以下環境變數配置的http proxy的非標準流量（位於80或443以外的其他埠）:<br><ul>
     <li>AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST</li>
     <li>AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT</li>
    </ul>
    <td>80或443以外的埠</td>
    <td>允許</td>
  </tr>
  <tr>
    <td></td>
    <td>非標準流量（在埠80或443以外的其他埠上）不使用http proxy</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>用戶端使用在<code>portForwards</code> API參數中宣告的<code>portOrig</code>連線至<code>AEM_PROXY_HOST</code>環境變數。</td>
    <td>任何</td>
    <td>允許</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>其他所有項目</td>
    <td>任何</td>
    <td>已封鎖</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Apache / Dispatcher設定**

可使用上述屬性來設定AEM Cloud Service Apache/Dispatcher層級的`mod_proxy`指令。

```
ProxyRemote "http://example.com" "http://${AEM_HTTP_PROXY_HOST}:${AEM_HTTP_PROXY_PORT}"
ProxyPass "/somepath" "http://example.com"
ProxyPassReverse "/somepath" "http://example.com"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_HTTPS_PROXY_HOST}:${AEM_HTTPS_PROXY_PORT}"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## 專用輸出IP地址 {#dedicated-egress-IP-address}

>[!NOTE]
>
>如果您在2021年9月版本(10/6/21)之前已布建專用的輸出IP，請參考[舊版專用輸出地址客戶](#legacy-dedicated-egress-address-customers)。

### 優點 {#benefits}

此專用IP位址可在與SaaS廠商（如CRM廠商）整合，或AEMas a Cloud Service以外的其他整合（提供允許的IP位址清單）時，增強安全性。 將專用IP位址新增至允許清單，可確保只有來自客戶AEM Cloud Service的流量才可流入外部服務。 這是除了允許來自任何其他IP的流量以外。

若未啟用專用IP位址功能，來自AEMas a Cloud Service的流量會透過與其他客戶共用的一組IP來流動。

### 設定 {#configuring-dedicated-egress-provision}

>[!INFO]
>
>無法從專用的輸出IP地址使用Splunk轉發功能。

配置專用輸出IP地址與[靈活埠輸出](#configuring-flexible-port-egress-provision)相同。

主要差異在於，流量一律會從專屬的唯一IP傳出。 若要尋找該IP，請使用DNS解析器來識別與`p{PROGRAM_ID}.external.adobeaemcloud.com`相關聯的IP位址。 IP位址預期不會變更，但若日後需要變更，將會提供進階通知。

除了`PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`端點中靈活埠輸出支援的路由規則外，專用的輸出IP地址還支援`nonProxyHosts`參數。 這可讓您宣告一組主機，這些主機應通過共用IP地址範圍而不是專用IP路由，這可能很有用，因為通過共用IP的流量分配可能會進一步優化。 `nonProxyHost` URL可能遵循`example.com`或`*.example.com`的模式，其中通配符僅在域開頭時才受支援。

在決定靈活的埠輸出與專用的輸出IP地址時，如果不需要特定的IP地址，客戶應選擇靈活的埠輸出，因為Adobe可以優化靈活的埠輸出通信的效能。

### 流量路由 {#dedcated-egress-ip-traffic-routing}

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目的地條件</th>
    <th>埠</th>
    <th>連線</th>
    <th>範例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http或https通訊協定</b></td>
    <td>Azure或Adobe服務的流量</td>
    <td>任何</td>
    <td>通過共用群集IP（非專用IP）</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>與<code>nonProxyHosts</code>參數匹配的主機</td>
    <td>80或443</td>
    <td>通過共用群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>與<code>nonProxyHosts</code>參數匹配的主機</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>透過http代理設定，預設使用標準Java HTTP用戶端程式庫來設定http/s流量</td>
    <td>任何</td>
    <td>通過專用的輸出IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果從標準Java HTTP客戶端庫中顯式刪除，或使用忽略標準代理配置的Java庫）</td>
    <td>80或443</td>
    <td>通過共用群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果從標準Java HTTP客戶端庫中顯式刪除，或使用忽略標準代理配置的Java庫）</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>用戶端使用在<code>portForwards</code> API參數中宣告的<code>portOrig</code>連線至<code>AEM_PROXY_HOST</code> env變數</td>
    <td>任何</td>
    <td>通過專用的輸出IP</td>
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

## 舊版專屬出口地址客戶 {#legacy-dedicated-egress-address-customers}

如果您在2021.09.30之前已布建專用的輸出IP，則您的專用輸出IP功能將如下所述運作。

### 功能使用 {#feature-usage}

若Java系統屬性用於Proxy設定，則此功能與會產生傳出流量的Java程式碼或程式庫相容。 實際上，這應包含最常見的程式庫。

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

有些程式庫需要明確的設定，才能將標準Java系統屬性用於Proxy設定。

使用Apache HttpClient的範例，此範例需要明確呼叫
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html)或使用
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

同一專用IP會套用至其Adobe組織中的所有客戶方案，以及每個客戶方案中的所有環境。 它適用於製作和發佈服務。

僅支援HTTP和HTTPS埠。 加密時包括HTTP/1.1和HTTP/2。

### 除錯考量事項 {#debugging-considerations}

若要驗證流量是否確實在預期的專用IP位址上傳出，請檢查目的地服務的記錄（若有）。 否則，呼叫[https://ifconfig.me/IP](https://ifconfig.me/IP)等偵錯服務可能會很有用，這會傳回呼叫IP位址。

## 虛擬專用網(VPN) {#vpn}

VPN允許從作者、發佈或預覽連接到內部部署的基礎架構或資料中心。 例如，用於訪問資料庫的方法。

它還允許連接到SaaS供應商，例如支援VPN的CRM供應商，或從公司網路連接到AEMas a Cloud Service作者、預覽或發佈。

支援大多數採用IPSec技術的VPN設備。 根據&#x200B;**RouteBased配置說明**&#x200B;列中的資訊，在[此頁](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable)上查看設備清單。 如表所述配置設備。

### 一般考量 {#general-vpn-considerations}

* 僅支援單個VPN連接
* Splunk轉發功能無法通過VPN連接實現。

### 建立 {#vpn-creation}

一旦每個程式調用POST`/program/<programId>/networkInfrastructures`端點，並傳遞配置資訊的有效負載，包括：`kind`參數、區域、地址空間（CIDR清單 — 請注意以後不能修改）、DNS解析器（用於解析客戶網路中的名稱）和VPN連接資訊（如網關配置、共用VPN密鑰和IP安全策略）的「vpn」值。 端點會以`network_id`回應，以及包含狀態的其他資訊。 [API檔案](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)中應參考完整的參數集和確切語法。

呼叫後，配置網路基礎架構通常需要45到60分鐘。 可呼叫API的GET方法以傳回目前狀態，最終從`creating`反轉至`ready`。 請參閱API檔案，了解所有狀態。

如果程式範圍的VPN配置已就緒，則必須為每個環境調用`PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`端點，以啟用環境級別的網路並聲明任何埠轉發規則。 參數可依環境設定，以提供彈性。

如需詳細資訊，請參閱[ API檔案](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration)。

應為應通過VPN路由的任何非http/s協定TCP通信聲明埠轉發規則，方法是指定目標主機集（名稱或IP，以及埠）。 對於每個目標主機，客戶必須將目標埠映射到從30000到30999的埠，其中的值必須在程式中的各個環境中是唯一的。 客戶也可以在`nonProxyHosts`參數中列出一組url，該參數聲明流量應繞過VPN路由，而是通過共用IP範圍。 它會遵循`example.com`或`*.example.com`的模式，其中只有域開頭才支援通配符。

API應在幾秒後回應，指出狀態`updating` ，大約10分鐘後，對Cloud Manager的環境GET端點的呼叫會顯示狀態`ready`，指出已套用環境更新。

請注意，即使沒有環境流量路由規則（主機或旁路），仍必須呼叫`PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`，只要有空的裝載。

### 更新VPN {#updating-the-vpn}

調用`PUT /api/program/<program_id>/network/<network_id>`端點可以更新程式級VPN配置。

請注意，在初始VPN配置後，地址空間無法更改。 如有必要，請聯絡客戶支援。 此外，無法修改`kind`參數（`flexiblePortEgress`、`dedicatedEgressIP`或`VPN`）。 請聯絡客戶支援以取得協助，說明已建立的項目和變更的原因。

可通過再次調用`PUT /program/{programId}/environment/{environmentId}/advancedNetworking`端點來更新每個環境的路由規則，確保包含完整的配置參數集，而不是子集。 環境更新通常需要5-10分鐘才能套用。

### 刪除或禁用VPN {#deleting-or-disabling-the-vpn}

要刪除網路基礎架構，請提交客戶支援票證，說明已建立的內容以及需要刪除的原因。

要禁用特定環境的VPN，請調用`DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`。 [API檔案](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)中的更多詳細資料。

### 流量路由 {#vpn-traffic-routing}

下表說明流量路由。

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目的地條件</th>
    <th>埠</th>
    <th>連線</th>
    <th>範例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http或https通訊協定</b></td>
    <td>Azure或Adobe服務的流量</td>
    <td>任何</td>
    <td>通過共用群集IP（非專用IP）</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>與<code>nonProxyHosts</code>參數匹配的主機</td>
    <td>80或443</td>
    <td>通過共用群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>與<code>nonProxyHosts</code>參數匹配的主機</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP落在<i>VPN網關地址</i>空間範圍中，並通過http代理配置（預設配置用於使用標準Java HTTP客戶端庫的http/s通信）</td>
    <td>任何</td>
    <td>通過VPN</td>
    <td><code>10.0.0.1:443</code>也可以是主機名稱。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP未落在<i>VPN網關地址空間</i>範圍內，並通過http代理配置（預設配置為使用標準Java HTTP客戶端庫的http/s通信）</td>
    <td>任何</td>
    <td>通過專用的輸出IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果從標準Java HTTP客戶端庫中顯式刪除，或使用忽略標準代理配置的Java庫）
</td>
    <td>80或443</td>
    <td>通過共用群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果從標準Java HTTP客戶端庫中顯式刪除，或使用忽略標準代理配置的Java庫）</td>
    <td>80或443以外的埠</td>
    <td>已封鎖</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>如果IP落在<i>VPN網關地址空間</i>範圍中，並且客戶端使用在<code>portForwards</code> API參數中聲明的<code>portOrig</code>連接到<code>AEM_PROXY_HOST</code>環境變數</td>
    <td>任何</td>
    <td>通過VPN</td>
    <td><code>10.0.0.1:3306</code>也可以是主機名稱。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP不落在<i>VPN網關地址空間</i>範圍中，且用戶端使用<code>portForwards</code> API參數中宣告的<code>portOrig</code>連線至<code>AEM_PROXY_HOST</code> env變數</td>
    <td>任何</td>
    <td>通過專用的輸出IP</td>
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

### 配置的有用域{#vpn-useful-domains-for-configuration}

下圖以視覺化方式呈現一組對設定和開發相當實用的網域和相關IP。 下圖的表格進一步說明了這些網域和IP。

![VPN域配置](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>域模式</th>
    <th>輸出(來自AEM)表示</th>
    <th>入口(至AEM)表示</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>專用的輸出IP地址，用於通往Internet的流量，而不是通過專用網路 </td>
    <td>來自VPN的連線會在CDN顯示為來自此IP。 若要僅允許從VPN進入AEM的連線，請設定Cloud Manager僅允許此IP並封鎖其他所有項目。 有關詳細資訊，請參閱「限制VPN連接入口」部分。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/A</td>
    <td>AEM端的VPN網關IP。 客戶的網路工程團隊可以使用此功能，僅允許從特定IP地址到其VPN網關的VPN連接。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>從VPN的AEM端到客戶端的流量IP。 這可允許列在客戶的設定中，以確保只能從AEM進行連線。</td>
    <td>如果客戶只想允許VPN存取AEM，則應將CNAME DNS項目設定為將<code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code>和/或<code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code>對應至此項目。</td>
  </tr>
</tbody>
</table>

### 將VPN限制為入口連接 {#restrict-vpn-to-ingress-connections}

如果您只想允許VPN存取AEM，可在Cloud Manager中設定環境允許清單，以便僅允許`p{PROGRAM_ID}.external.adobeaemcloud.com`定義的IP與環境通訊。 這可以與Cloud Manager中其他任何IP型允許清單的方式相同。

如果規則必須以路徑為基礎，請在Dispatcher層級使用標準http指示，以拒絕或允許特定IP。 他們應該能確保CDN也無法快取所需的路徑，以便讓請求一律傳至來源。

**Httpd配置示例**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 在高級網路類型之間轉換 {#transitioning-between-advanced-networking-types}

由於無法修改`kind`參數，請聯繫客戶支援以尋求幫助，說明已建立的內容和更改的原因。