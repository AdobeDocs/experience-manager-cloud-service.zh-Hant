---
title: AEM as a Cloud Service的記錄轉送
description: 瞭解如何在AEM as a Cloud Service中將記錄轉送給記錄廠商
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 9c258e2906c37ee9b91d2faa78f7dfdaa5956dc2
workflow-type: tm+mt
source-wordcount: '1985'
ht-degree: 1%

---

# 記錄轉送 {#log-forwarding}

>[!NOTE]
>
>記錄轉送現在以自助方式設定，有別於傳統方法(需要提交Adobe支援票證)。 如果您的記錄轉送是由Adobe所設定，請參閱[移轉](#legacy-migration)區段。

擁有記錄廠商授權或託管記錄產品的客戶可以將AEM記錄(包括Apache/Dispatcher)和CDN記錄轉送至相關聯的記錄目的地。 AEM as a Cloud Service支援下列記錄目的地：

* Azure Blob儲存體
* Datadog
* Elasticsearch或OpenSearch
* HTTPS
* Splunk

記錄轉送是透過在Git中宣告設定以自助方式設定，並可透過Cloud Manager設定管道部署至開發、中繼和生產環境型別。 可使用命令列工具將設定檔案部署到快速開發環境(RDE)。

AEM和Apache/Dispatcher記錄檔可選擇透過AEM的進階網路基礎結構路由，例如專用輸出IP。

請注意，與傳送至記錄目的地的記錄檔相關聯的網路頻寬，會視為您組織網路I/O使用量的一部分。

## 本文的結構方式 {#how-organized}

本文章的編排方式如下：

* 設定 — 適用於所有記錄目的地
* 傳輸與進階網路 — 在建立記錄組態之前，應考慮網路設定
* 記錄目的地設定 — 每個目的地的格式稍有不同
* 記錄專案格式 — 記錄專案格式的相關資訊
* 從舊版記錄轉送移轉 — 如何從先前由Adobe設定的記錄轉送移至自助方法

## 設定 {#setup}

1. 建立名為`logForwarding.yaml`的檔案。 它應該包含中繼資料，如[設定管道文章](/help/operations/config-pipeline.md#common-syntax)中所述（**kind**&#x200B;應該設定為`LogForwarding`且版本設定為&quot;1&quot;），其設定類似於以下內容（我們使用Splunk作為範例）。

   ```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
   ```

1. 將檔案放置在名為&#x200B;*config*&#x200B;或類似名稱的頂層資料夾之下，如[使用設定管道](/help/operations/config-pipeline.md#folder-structure)中所述。

1. 針對RDE （使用命令列工具）以外的環境型別，在Cloud Manager中建立目標部署設定管道，如[此區段](/help/operations/config-pipeline.md#creating-and-managing)所參考；請注意，完整棧疊管道和Web層管道不會部署設定檔案。

1. 部署設定。

設定中的權杖（例如`${{SPLUNK_TOKEN}}`）代表不應儲存在Git中的秘密。 請改為宣告為Cloud Manager [秘密環境變數](/help/operations/config-pipeline.md#secret-env-vars)。 請務必選取「**全部**」作為「已套用服務」欄位的下拉式清單值，以便將記錄檔轉送至作者、發佈及預覽層級。

您可以在CDN記錄檔與AEM記錄檔(包括Apache/Dispatcher)之間設定不同的值，方法是在&#x200B;**預設**&#x200B;區塊之後加入額外的&#x200B;**cdn**&#x200B;和/或&#x200B;**aem**&#x200B;區塊，其中的屬性可以覆寫&#x200B;**預設**&#x200B;區塊中定義的屬性；只需要啟用的屬性。 一個可能的使用案例是對CDN記錄使用不同的Splunk索引，如以下範例所示。

```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
       cdn:
         enabled: true
         token: "${{SPLUNK_TOKEN_CDN}}"
         index: "AEMaaCS_CDN"   
```

另一種情況是停用CDN記錄或AEM記錄(包括Apache/Dispatcher)的轉送。 例如，若只要轉送CDN記錄檔，即可設定下列專案：

```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "splunk-host.example.com"
         token: "${{SPLUNK_TOKEN}}"
         index: "AEMaaCS"
       aem:
         enabled: false
```

## 傳輸與進階網路 {#transport-advancednetworking}

有些組織會選擇限制記錄目的地可以接收哪些流量，有些組織則可能需要使用HTTPS (443)以外的連線埠。  如果是，則必須先設定[進階網路](/help/security/configuring-advanced-networking.md)，才能部署記錄轉送設定。

根據您是否使用連線埠443，以及您是否需要在固定IP位址顯示日誌，使用下表檢視進階網路和記錄組態的需求。
<html>
<style>
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
  text-align: center;
}
</style>
<table>
  <tbody>
    <tr>
      <th>目的地連線埠</th>
      <th>需要從固定IP顯示記錄嗎？</th>
      <th>需要進階網路</th>
      <th>需要LogForwarding.yaml連線埠定義</th>
    </tr>
    <tr>
      <td rowspan="2">HTTPS (443)</td>
      <td>否</td>
      <td>否</td>
      <td>否</td>
    </tr>
    <tr>
      <td>是</td>
      <td>是，<a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">專用輸出</a></td>
      <td>否</td>
    <tr>
    <tr>
      <td rowspan="2">非標準連線埠（例如8088）</td>
      <td>否</td>
      <td>是，<a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress">彈性輸出</a></td>
      <td>是</td>
    </tr>
    <tr>
      <td>是</td>
      <td>是，<a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">專用輸出</a></td>
      <td>是</td>
  </tbody>
</table>
</html>

>[!NOTE]
>是否從單一IP位址顯示記錄取決於您選擇的進階網路設定。  必須使用專用輸出來處理這個問題。
>
> 進階網路設定是[兩步驟程式](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling)，需要在程式和環境層級啟用。

對於AEM記錄檔(包括Apache/Dispatcher)，如果您已設定[進階網路](/help/security/configuring-advanced-networking.md)，則可以使用`aem.advancedNetworking`屬性從專用輸出IP位址或透過VPN轉送記錄檔。

以下範例說明如何使用進階網路在標準HTTPS連線埠上設定登入。

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

針對CDN記錄，您可以將IP位址加入允許清單，如[Fastly檔案 — 公用IP清單](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/)中所述。 如果共用IP位址清單太大，請考慮傳送流量至https伺服器或(非Adobe) Azure Blob存放區，其中可寫入邏輯，以將已知IP的記錄傳送至其最終目的地。

>[!NOTE]
>CDN記錄無法顯示來自您AEM記錄顯示來源的IP位址，因為記錄會直接從Fastly傳送，而非AEM Cloud Service。

## 記錄目的地組態 {#logging-destinations}

以下列出支援的記錄目的地的設定以及任何特定考量。

### Azure Blob儲存體 {#azureblob}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  azureBlob:
    default:
      enabled: true       
      storageAccountName: "example_acc"
      container: "aem_logs"
      sasToken: "${{AZURE_BLOB_SAS_TOKEN}}
      
```

SAS權杖應該用於驗證。 應從共用存取權杖頁面而非共用存取權杖頁面中建立，並應使用下列設定進行設定：

* 允許的服務：必須選取Blob。
* 允許的資源：必須選取物件。
* 允許的許可權：必須選取「寫入」、「新增」、「建立」。
* 有效的開始和到期日期/時間。

以下是範例SAS權杖設定的熒幕擷圖：

![Azure Blob SAS權杖組態](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

如果記錄檔在先前正常運作後停止傳遞，請檢查您所設定的SAS權杖是否仍然有效，因為它可能已過期。

#### Azure Blob儲存CDN記錄 {#azureblob-cdn}

每個全域分散式記錄伺服器每隔幾秒會在`aemcdn`資料夾下產生一個新檔案。 建立後，檔案將不再附加到。 檔案名稱格式為YYYY-MM-DDThh:mm:ss.sss-uniqueid.log。 例如，2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log。

例如，在某個時間點：

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

然後30秒後：

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

每個檔案包含多個json記錄專案，每個專案位於一行中。 記錄專案格式在[AEM as a Cloud Service的記錄](/help/implementing/developing/introduction/logging.md)下描述，每個記錄專案也包含以下[記錄專案格式](#log-formats)區段中提及的其他屬性。

#### Azure Blob儲存體AEM記錄檔 {#azureblob-aem}

AEM記錄(包括Apache/Dispatcher)會顯示在具有以下命名慣例的資料夾下方：

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

在每個資料夾下，將建立單一檔案並附加至其中。 客戶應負責處理和管理此檔案，以免檔案變得太大。

請參閱[AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md)的記錄下的記錄專案格式。 記錄專案也會包含以下[記錄專案格式](#log-formats)區段中提及的其他屬性。

### Datadog {#datadog}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  datadog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      tags:
         tag1: value1
         tag2: value2
      
```

考量事項：

* 建立API金鑰，而不與特定雲端提供者進行任何整合。
* 標籤屬性是選用的
* 對於AEM記錄檔，Datadog來源標籤設定為`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`或`aemhttpderror`其中之一
* 對於CDN記錄，Datadog來源標籤設為`aemcdn`
* Datadog服務標籤已設定為`adobeaemcloud`，但您可以在標籤區段中覆寫它
* 如果您的內嵌管道使用Datadog標籤來決定轉送記錄的適當索引，請確認這些標籤已在記錄轉送YAML檔案中正確設定。 如果管道相依於缺少標籤，則這些標籤可能會阻止成功的記錄擷取。

### Elasticsearch和OpenSearch {#elastic}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
      pipeline: "ingest pipeline name"
```

考量事項：

* 依預設，連線埠為443。 您可以選擇使用名為`port`的屬性覆寫
* 對於認證，請務必使用部署認證，而不是帳戶認證。 這些是在畫面中產生的認證，可能類似於此影像：

![彈性部署認證](/help/implementing/developing/introduction/assets/ec-creds.png)

* 對於AEM記錄檔，`index`設定為`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`或`aemhttpderror`其中之一
* 選用管線屬性應設為Elasticsearch或OpenSearch擷取管線的名稱，可將其設定為將記錄專案路由至適當的索引。 管道的處理器型別必須設定為&#x200B;*指令碼*，而且指令碼語言應設定為&#x200B;*無痛苦的*。 以下是指令碼片段範例，可將記錄專案路由至索引，例如aemaccess_dev_26_06_2024：

```text
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

考量事項：

* URL字串必須包含&#x200B;**https://**，否則驗證將會失敗。
* url可能包含連線埠。 例如 `https://example.com:8443/aem_logs/aem`。如果url字串中未包含任何連線埠，則會假設是連線埠443 （預設的HTTPS連線埠）。

#### HTTPS CDN記錄 {#https-cdn}

Web要求(POST)將持續傳送，其有json裝載（記錄專案陣列），其記錄專案格式說明於[AEM as a Cloud Service記錄](/help/implementing/developing/introduction/logging.md#cdn-log)。 以下[Log Entry Formats](#log-formats)區段中提及其他屬性。

還有名稱為`sourcetype`的屬性，其設定為值`aemcdn`。

>[!NOTE]
>
> 在傳送第一個CDN記錄專案之前，您的HTTP伺服器必須成功完成一次性質詢：傳送至路徑``/.well-known/fastly/logging/challenge``的要求必須在內文中以星號``*``回應，且狀態碼為200。

#### HTTPS AEM記錄 {#https-aem}

對於AEM記錄檔（包括apache/dispacher），網路要求(POST)將持續傳送，其包含記錄專案陣列的json裝載，並具有各種記錄專案格式，如[AEM as a Cloud Service的記錄](/help/implementing/developing/introduction/logging.md)中所述。 以下[Log Entry Formats](#log-formats)區段中提及其他屬性。

也有名為`Source-Type`的屬性，其設定為下列其中一個值：

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### Splunk {#splunk}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
```

考量事項：

* 依預設，連線埠為443。 您可以選擇使用名為`port`的屬性覆寫它。
* 根據特定記錄，sourcetype欄位會有下列其中一個值： *aemaccess*，*aemerror*，
  *aemrequest*，*aemdispatcher*，*aemhttpdaccess*，*aemhttpderror*，*aemcdn*
* 如果必要的IP已加入允許清單，但尚未傳遞記錄，請確認沒有防火牆規則強制執行Splunk權杖驗證。 Fastly會執行初始驗證步驟，其中有意傳送無效的Splunk權杖。 如果您的防火牆設定為終止使用無效Splunk權杖的連線，則驗證程式將失敗，導致Fastly無法將記錄傳送給您的Splunk執行個體。

>[!NOTE]
>
> [如果將](#legacy-migration)從舊版記錄轉送移轉到此自助模型，則傳送至您的Splunk索引的`sourcetype`欄位值可能已變更，因此請適當的調整。

<!--
### Sumo Logic {#sumologic}

   ```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "https://collectors.de.sumologic.com"
         uri: "/receiver/v1/http"
         privateKey: "${{SomeOtherToken}}"
   
   ```   
-->

## 記錄專案格式 {#log-formats}

請參閱[AEM as a Cloud Service的記錄](/help/implementing/developing/introduction/logging.md)，以瞭解每個個別記錄型別(CDN記錄檔和包括Apache/Dispatcher在內的AEM記錄檔)的格式。

由於來自多個程式和環境的記錄可能會轉發到相同的記錄目標，除了記錄文章中所述的輸出之外，以下屬性將包含在每個記錄專案中：

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

例如，屬性可以有下列值：

```text
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## 從舊版記錄檔轉送移轉 {#legacy-migration}

在透過自助模型完成記錄轉送設定之前，已要求客戶開啟支援票證，Adobe將在其中啟動整合。

若客戶是透過Adobe以這種方式進行設定，歡迎在方便時調整為自助服務模式。 進行此轉換有幾個原因：

* 已布建新環境（例如，新的開發環境或RDE）。
* 變更您現有的Splunk端點或認證。
* Adobe已在CDN記錄可用之前設定記錄轉送，您想要接收CDN記錄。
* 主動因應自助服務模式的明智決策，讓貴組織在需要進行時效性變動之前便已掌握相關知識。

準備移轉時，只需依照前幾節所述設定YAML檔案即可。 使用Cloud Manager設定管道來部署至應套用設定的每個環境。

我們建議（但非必要）將設定部署到所有環境，以便它們都處於自助控制之下。 如果沒有，您可能會忘記哪些環境已由Adobe設定，哪些是以自助方式設定。

>[!NOTE]
>傳送至您Splunk索引的`sourcetype`欄位值可能已變更，因此請適當的調整。
>
>當記錄轉送部署至先前由Adobe支援設定的環境時，您可能會收到長達數小時的重複記錄。 這最終會自動解決。
