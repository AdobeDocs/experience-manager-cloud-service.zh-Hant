---
title: AEM as a Cloud Service的記錄轉送
description: 瞭解如何在AEM as a Cloud Service中將記錄轉送給記錄廠商
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: afa88d89b24ac425ba1b69ee9062e589d49ebee9
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 3%

---

# 記錄轉送 {#log-forwarding}

>[!NOTE]
>
>記錄轉送現在以自助方式設定，有別於傳統方法(需要提交Adobe支援票證)。 如果您的記錄轉送是由Adobe設定，請參閱[移轉](#legacy-migration)區段。

擁有記錄廠商授權或託管記錄產品的客戶可以將AEM記錄(包括Apache/Dispatcher)和CDN記錄轉送至相關聯的記錄目的地。 AEM as a Cloud Service支援下列記錄目的地：

<table>
  <tbody>
    <tr>
      <th>記錄技術</th>
      <th>AEM</th>
      <th>Dispatcher</th>
      <th>CDN</th>
    </tr>
    <tr>
      <td>Amazon S3</td>
      <td>是</td>
      <td>是</td>
      <td style="background-color: #ffb3b3;">未來</td>
    </tr>
    <tr>
      <td>Azure Blob儲存體</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>DataDog</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>Dynatrace</td>
      <td>是</td>
      <td>是</td>
      <td style="background-color: #ffb3b3;">未來</td>
    </tr>
    <tr>
      <td>Elasticsearch<br>OpenSearch</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>HTTPS</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>New Relic</td>
      <td>是</td>
      <td>是</td>
      <td style="background-color: #ffb3b3;">未來</td>
    </tr>
    <tr>
      <td>Splunk</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>相撲邏輯</td>
      <td>是</td>
      <td>是</td>
      <td style="background-color: #ffb3b3;">未來</td>
    </tr>
  </tbody>
</table>

>[!NOTE]
>
> 對於未來計畫推出的CDN記錄技術，請傳送電子郵件至[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)以報名關注。

記錄轉送是透過在Git中宣告設定以自助方式設定，並可透過Cloud Manager設定管道部署至開發、中繼和生產環境型別。 可以使用命令列工具將設定檔案部署至快速開發環境 (RDE) 中。

AEM和Apache/Dispatcher記錄檔可選擇透過AEM的進階網路基礎結構（例如專用輸出IP）進行路由。

請注意，與傳送至記錄目的地的記錄檔相關聯的網路頻寬，會視為您組織網路I/O使用量的一部分。

## 本文的結構方式 {#how-organized}

本文章的編排方式如下：

* 設定 — 適用於所有記錄目的地
* 傳輸與進階網路 — 在建立記錄組態之前，應考慮網路設定
* 記錄目的地設定 — 每個目的地的格式稍有不同
* 記錄專案格式 — 記錄專案格式的相關資訊
* 從舊版記錄轉送移轉 — 如何從Adobe先前設定的記錄轉送移至自助方法

## 設定 {#setup}

1. 建立一個名為 `logForwarding.yaml` 的檔案。它應該包含中繼資料，如[設定管道](/help/operations/config-pipeline.md#common-syntax)文章中所述（**kind**&#x200B;應該設定為`LogForwarding`且版本設定為&quot;1&quot;），其設定類似於以下內容（我們使用Splunk作為範例）。

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

<table>
  <tbody>
    <tr>
      <th>目的地連線埠</th>
      <th>需要從固定IP顯示記錄嗎？</th>
      <th>需要進階網路</th>
      <th>需要LogForwarding.yaml連線埠定義</th>
    </tr>
    <tr>
      <td rowspan="2" ro>HTTPS (443)</td>
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
>
>CDN記錄無法顯示來自與您的AEM記錄顯示來源相同的IP位址，因為記錄會直接從Fastly傳送，而不是AEM Cloud Service。
>
>因此，無法將記錄轉送與進階網路VPN設定搭配使用。

## 記錄目的地組態 {#logging-destinations}

以下列出支援的記錄目的地的設定以及任何特定考量。

### Amazon S3 {#amazons3}

記錄轉送至Amazon S3支援AEM和Dispatcher記錄，目前尚不支援CDN記錄。

>[!NOTE]
>
>記錄檔會定期寫入S3，每種記錄檔型別每10分鐘寫入一次。  此功能切換後，這可能會造成將記錄寫入S3的初始延遲。  [此行為的進一步資訊](https://docs.fluentbit.io/manual/pipeline/outputs/s3#differences-between-s3-and-other-fluent-bit-outputs)。

```yaml
kind: "LogForwarding"
version: "1.0"
metadata:
  envTypes: ["dev"]
data:
  awsS3:
    default:
      enabled: true
      region: "your-bucket-region"
      bucket: "your_bucket_name"
      accessKey: "${{AWS_S3_ACCESS_KEY}}"
      secretAccessKey: "${{AWS_S3_SECRET_ACCESS_KEY}}"
```

若要使用S3記錄轉寄站，您需要預先設定AWS IAM使用者，並為該使用者提供存取S3儲存貯體的適當原則。  如需如何建立IAM使用者認證，請參閱[AWS IAM使用者檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

IAM原則應該允許使用者使用`s3:putObject`。  例如：

```json
 {
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "s3:PutObject"
        ],
        "Resource": "arn:aws:s3:::your_bucket_name/*"
    }]
}
```

如需如何實作的詳細資訊，請參閱[AWS貯體原則檔案](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html)。

>[!NOTE]
>已規劃在未來提供AWS S3的CDN記錄支援。 請傳送電子郵件給[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)以註冊感興趣的內容。

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

#### 考量事項

* 建立API金鑰，而不與特定雲端提供者進行任何整合。
* 標籤屬性是選用的
* 對於AEM記錄檔，Datadog來源標籤設為`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`或`aemhttpderror`其中之一
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

#### 考量事項

* 依預設，連線埠為443。 您可以選擇使用名為`port`的屬性覆寫
* 對於認證，請務必使用部署認證，而不是帳戶認證。 這些是在畫面中產生的認證，可能類似於此影像：

![彈性部署認證](/help/implementing/developing/introduction/assets/ec-creds.png)

* 針對AEM記錄檔，`index`設定為`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`或`aemhttpderror`其中之一
* 選用管道屬性應該設定為Elasticsearch或OpenSearch擷取管道的名稱，可以將其設定為將記錄專案路由到適當的索引。 管道的處理器型別必須設定為&#x200B;*指令碼*，而且指令碼語言應設定為&#x200B;*無痛苦的*。 以下是指令碼片段範例，可將記錄專案路由至索引，例如aemaccess_dev_26_06_2024：

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

#### 考量事項

* URL字串必須包含&#x200B;**https://**，否則驗證將會失敗。
* url可能包含連線埠。 例如 `https://example.com:8443/aem_logs/aem`。如果url字串中未包含任何連線埠，則會假設是連線埠443 （預設的HTTPS連線埠）。

#### HTTPS CDN記錄 {#https-cdn}

Web要求(POST)將持續傳送，其有json裝載（記錄專案陣列），其記錄專案格式說明於[AEM as a Cloud Service記錄](/help/implementing/developing/introduction/logging.md#cdn-log)。 以下[Log Entry Formats](#log-formats)區段中提及其他屬性。

還有名稱為`sourcetype`的屬性，其設定為值`aemcdn`。

>[!NOTE]
>
> 在傳送第一個CDN記錄專案之前，您的HTTP伺服器必須成功完成一次性質詢：傳送至路徑``/.well-known/fastly/logging/challenge``的要求必須在內文中以星號``*``回應，且狀態碼為200。

#### HTTPS AEM記錄 {#https-aem}

對於AEM記錄檔（包括apache/dispacher），網路要求(POST)將會持續傳送，其json裝載為記錄專案陣列，並具有各種記錄專案格式，如[AEM as a Cloud Service記錄](/help/implementing/developing/introduction/logging.md)中所述。 以下[Log Entry Formats](#log-formats)區段中提及其他屬性。

也有名為`Source-Type`的屬性，其設定為下列其中一個值：

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### New Relic記錄API {#newrelic-https}

記錄轉送至New Relic會利用New Relic HTTPS API來擷取。  目前僅支援AEM和Dispatcher的記錄檔，尚不支援CDN記錄檔。

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    newRelic:
      default:
        enabled: true
        uri: "https://log-api.newrelic.com/log/v1"
        apiKey: "${{NR_API_KEY}}"
```

>[!NOTE]
>
>記錄轉送至New Relic僅適用於客戶擁有的New Relic帳戶。
>
>已規劃在未來提供New Relic記錄API的CDN記錄支援。 請傳送電子郵件給[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)以註冊感興趣的內容。
>
>New Relic會根據您的New Relic帳戶布建位置，提供區域特定的端點。  如需進一步資訊，請參閱[New Relic檔案](https://docs.newrelic.com/docs/logs/log-api/introduction-log-api/#endpoint)。

### Dynatrace記錄API {#dynatrace-https}

記錄轉送至Dynatrace會利用Dynatrace HTTPS API來擷取。  目前僅支援AEM和Dispatcher的記錄檔，尚不支援CDN記錄檔。

Token需要「擷取記錄檔」範圍屬性。

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    dynatrace:
      default:
        enabled: true
        environmentId: "${{DYNATRACE_ENVID}}"
        token: "${{DYNATRACE_TOKEN}}"  
```

>[!NOTE]
>已規劃在未來提供Dynatrace記錄API的CDN記錄支援。 請傳送電子郵件給[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)以註冊感興趣的內容。

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

#### 考量事項

* 依預設，連線埠為443。 您可以選擇使用名為`port`的屬性覆寫它。
* 根據特定記錄，sourcetype欄位會有下列其中一個值： *aemaccess*，*aemerror*，
  *aemrequest*，*aemdispatcher*，*aemhttpdaccess*，*aemhttpderror*，*aemcdn*
* 如果必要的IP已加入允許清單，但尚未傳遞記錄，請確認沒有防火牆規則強制執行Splunk權杖驗證。 Fastly會執行初始驗證步驟，其中有意傳送無效的Splunk權杖。 如果您的防火牆設定為終止使用無效Splunk權杖的連線，則驗證程式將失敗，導致Fastly無法將記錄傳送給您的Splunk執行個體。

>[!NOTE]
>
> [如果將](#legacy-migration)從舊版記錄轉送移轉到此自助模型，則傳送至您的Splunk索引的`sourcetype`欄位值可能已變更，因此請適當的調整。

### 相撲邏輯 {#sumologic}

記錄檔轉送至Sumo Logic支援AEM和Dispatcher記錄檔；尚不支援CDN記錄檔。

在設定Sumo Logic以進行資料擷取時，您將會看到「HTTP Source位址」，該位址會在單一字串中提供主機、接收者URI和私密金鑰。  例如：

`https://collectors.de.sumologic.com/receiver/v1/http/ZaVnC...`

您需要複製URL的最後一個區段（沒有前置的`/`），並將其新增為[CloudManager秘密環境變數](/help/operations/config-pipeline.md#secret-env-vars)，如上方[設定](#setup)區段所述，然後在您的設定中參考該變數。  以下提供範例。

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  sumoLogic:
    default:
      enabled: true
      collectorURL: "https://collectors.de.sumologic.com/receiver/v1/http"
      privateKey: "${{SUMOLOGIC_PRIVATE_KEY}}"
      index: "aem-logs"
```

>[!NOTE]
>已規劃在未來提供SumoLogic的CDN記錄支援。 請傳送電子郵件給[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)以註冊感興趣的內容。
>
> 您需要Sumo Logic Enterprise訂閱才能使用「索引」欄位功能。  非企業訂閱的記錄檔會以標準形式路由至`sumologic_default`資料分割。  如需詳細資訊，請參閱[Sumo邏輯分割檔案](https://help.sumologic.com/docs/search/optimize-search-partitions/)。

## 記錄專案格式 {#log-formats}

請參閱[AEM as a Cloud Service的記錄](/help/implementing/developing/introduction/logging.md)，以瞭解每個個別記錄型別(CDN記錄檔和AEM記錄檔，包括Apache/Dispatcher)的格式。

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

若客戶是以Adobe的方式進行設定，歡迎他們在方便時改用自助服務模式。 進行此轉換有幾個原因：

* 已布建新環境（例如，新的開發環境或RDE）。
* 變更您現有的Splunk端點或認證。
* Adobe已在CDN記錄可用之前設定記錄轉送，您想要接收CDN記錄。
* 主動因應自助服務模式的明智決策，讓貴組織在需要進行時效性變動之前便已掌握相關知識。

準備移轉時，只需依照前幾節所述設定YAML檔案即可。 使用Cloud Manager設定管道來部署至應套用設定的每個環境。

我們建議（但非必要）將設定部署到所有環境，以便它們都處於自助控制之下。 如果沒有，您可能會忘記哪些環境已由Adobe設定，哪些是以自助方式設定。

>[!NOTE]
>
>傳送至您Splunk索引的`sourcetype`欄位值可能已變更，因此請適當的調整。
>
>當記錄轉送部署至先前由Adobe支援設定的環境時，您可能會收到長達數小時的重複記錄。 這最終會自動解決。
