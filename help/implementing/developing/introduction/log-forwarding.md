---
title: AEM as a Cloud Service的記錄轉送
description: 瞭解如何在AEM as a Cloud Service中將記錄轉送給Splunk和其他記錄廠商
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 1%

---

# 記錄轉送 {#log-forwarding}

>[!NOTE]
>
>此功能尚未發行，並且某些記錄目的地在發行時可能不可用。 同時，您可以開啟支援票證以將記錄轉送至&#x200B;**Splunk**，如[AEM as a Cloud Service記錄](/help/implementing/developing/introduction/logging.md)中所述。

擁有記錄廠商授權或託管記錄產品的客戶可以將AEM記錄(包括Apache/Dispatcher)和CDN記錄轉送至關聯的記錄目的地。 AEM as a Cloud Service支援下列記錄目的地：

* Azure Blob儲存體
* DataDog
* Elasticsearch或OpenSearch
* HTTPS
* Splunk

以自助方式設定記錄轉送，方法是在Git中宣告設定，並透過Cloud Manager設定管道將其部署到生產（非沙箱）程式中的開發、中繼和生產環境型別。

AEM和Apache/Dispatcher記錄檔可選擇透過AEM的進階網路基礎結構路由，例如專用輸出IP。

請注意，與傳送至記錄目的地的記錄檔相關聯的網路頻寬，會視為您組織網路I/O使用量的一部分。


## 本文的結構方式 {#how-organized}

本文章的編排方式如下：

* 設定 — 適用於所有記錄目的地
* 記錄目的地設定 — 每個目的地的格式稍有不同
* 記錄專案格式 — 記錄專案格式的相關資訊
* 進階網路 — 透過專用出口或VPN傳送AEM和Apache/Dispatcher記錄


## 設定 {#setup}

1. 在Git中專案的頂層資料夾中建立以下資料夾和檔案結構：

   ```
   config/
        logForwarding.yaml
   ```

1. `logForwarding.yaml`應包含中繼資料及類似以下格式的設定（我們使用Splunk作為範例）。

   ```
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

   **kind**&#x200B;引數應該設定為`LogForwarding`，而版本應該設定為結構描述版本，即1。

   設定中的權杖（例如`${{SPLUNK_TOKEN}}`）代表不應儲存在Git中的秘密。 請改為宣告它們為&#x200B;**密碼**&#x200B;型別的Cloud Manager [環境變數](/help/implementing/cloud-manager/environment-variables.md)。 請務必選取「**全部**」作為「已套用服務」欄位的下拉式清單值，以便將記錄檔轉送至作者、發佈及預覽層級。

   您可以在CDN記錄檔與AEM記錄檔(包括Apache/Dispatcher)之間設定不同的值，方法是在&#x200B;**預設**&#x200B;區塊之後加入額外的&#x200B;**cdn**&#x200B;和/或&#x200B;**aem**&#x200B;區塊，其中的屬性可以覆寫&#x200B;**預設**&#x200B;區塊中定義的屬性；只需要啟用的屬性。 一個可能的使用案例是對CDN記錄使用不同的Splunk索引，如以下範例所示。

   ```
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

   ```
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

1. 對於RDE以外的環境型別（目前不支援），在Cloud Manager中建立目標部署設定管道；請注意，完整棧疊管道和Web層管道不會部署設定檔案。

   * [參閱設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)。
   * [參閱設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

## 記錄目的地組態 {#logging-destinations}

以下列出支援的記錄目的地的設定以及任何特定考量。

### Azure Blob儲存體 {#azureblob}

```
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

#### Azure Blob儲存CDN記錄 {#azureblob-cdn}

每個全域分散式記錄伺服器每隔幾秒會在`aemcdn`資料夾下產生一個新檔案。 建立後，檔案將不再附加到。 檔案名稱格式為YYYY-MM-DDThh:mm:ss.sss-uniqueid.log。 例如，2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log。

例如，在某個時間點：

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

然後30秒後：

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

每個檔案包含多個json記錄專案，每個專案位於一行中。 記錄專案格式在[AEM as a Cloud Service的記錄](/help/implementing/developing/introduction/logging.md)下描述，每個記錄專案也包含以下[記錄專案格式](#log-format)區段中提及的其他屬性。

#### Azure Blob儲存體AEM記錄檔 {#azureblob-aem}

AEM記錄(包括Apache/Dispatcher)會顯示在具有以下命名慣例的資料夾下方：

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

在每個資料夾下，將建立單一檔案並附加至其中。 客戶應負責處理和管理此檔案，以免檔案變得太大。

請參閱[AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md)的記錄下的記錄專案格式。 記錄專案也會包含以下[記錄專案格式](#log-formats)區段中提及的其他屬性。


### Datadog {#datadog}

```
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
* tags屬性是選用的


### Elasticsearch和OpenSearch {#elastic}

```
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

* 對於認證，請務必使用部署認證，而不是帳戶認證。 這些是在畫面中產生的認證，可能類似於此影像：

![彈性部署認證](/help/implementing/developing/introduction/assets/ec-creds.png)

* 選用管線屬性應設為Elasticsearch或OpenSearch擷取管線的名稱，可將其設定為將記錄專案路由至適當的索引。 管道的處理器型別必須設定為&#x200B;*指令碼*，而且指令碼語言應設定為&#x200B;*無痛苦的*。 以下是指令碼片段範例，可將記錄專案路由至索引，例如aemaccess_dev_26_06_2024：

```
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com:8443/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

考量事項：

* URL字串必須包含&#x200B;**https://**，否則驗證將會失敗。 如果url字串中未包含任何連線埠，則會假設是連線埠443 （預設的HTTPS連線埠）。
* 如果您想要使用與443不同的連線埠，請將其提供為URL的一部分。

#### HTTPS CDN記錄 {#https-cdn}

Web要求(POST)將持續傳送，其有json裝載（記錄專案陣列），其記錄專案格式說明於[AEM as a Cloud Service記錄](/help/implementing/developing/introduction/logging.md#cdn-log)。 以下[Log Entry Formats](#log-formats)區段中提及其他屬性。

還有名稱為`sourcetype`的屬性，其設定為值`aemcdn`。

>[!NOTE]
>
> 在傳送第一個CDN記錄專案之前，您的HTTP伺服器必須成功完成一次性質詢：傳送至路徑``/.well-known/fastly/logging/challenge``的要求必須在內文中以星號``*``回應，且狀態碼為200。

#### HTTPS AEM記錄 {#https-aem}

對於AEM記錄檔（包括apache/dispacher），網路要求(POST)將持續傳送，其包含記錄專案陣列的json裝載，並具有各種記錄專案格式，如[AEM as a Cloud Service的記錄](/help/implementing/developing/introduction/logging.md)中所述。 以下[Log Entry Formats](#log-format)區段中提及其他屬性。

也有名為`sourcetype`的屬性，其設定為下列其中一個值：

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

### Splunk {#splunk}

```
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

<!--
### Sumo Logic {#sumologic}

   ```
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

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## 進階網路 {#advanced-networking}

>[!NOTE]
>
>此功能尚未準備好供早期採用者使用。


有些組織會選擇限制記錄目的地可接收哪些流量。

對於CDN記錄檔，您可以將IP位址加入允許清單，如[fastly檔案 — 公用IP清單](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/)中所述。 如果共用IP位址清單太大，請考慮傳送流量至(非Adobe) Azure Blob存放區，其中可寫入邏輯，以將專用IP的記錄傳送至其最終目的地。

針對AEM記錄檔(包括Apache/Dispatcher)，您可以設定記錄檔轉送以通過[進階網路](/help/security/configuring-advanced-networking.md)。 檢視以下三種進階網路型別的模式，這些型別使用選用的`port`引數以及`host`引數。

### 彈性連接埠輸出 {#flex-port}

如果記錄流量是傳送到443以外的連線埠（例如，下面的8443），請設定進階網路，如下所示：

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 8443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

並設定yaml檔案，如下所示：

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "${{AEM_PROXY_HOST}}"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### 專用輸出IP {#dedicated-egress}


如果記錄流量需要來自專用輸出IP，請設定進階網路，如下所示：

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443, 
            "portOrig": 30443
        }    
    ]
}
```

並設定yaml檔案，如下所示：

```
      
kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443    
```

### VPN {#vpn}

如果記錄流量需要通過VPN，請設定進階網路，如下所示：

```
{
    "portForwards": [
        {
            "name": "splunk-host.example.com",
            "portDest": 443,
            "portOrig": 30443
        }    
    ]
}

kind: "LogForwarding"
version: "1"
   metadata:
     envTypes: ["dev"]
data:
  splunk:
     default:
       enabled: true
       index: "index_name" 
       token: "${{SPLUNK_TOKEN}}"  
     aem:
       enabled: true
       host: "${{AEM_PROXY_HOST}}"
       port: 30443       
     cdn:
       enabled: true
       host: "splunk-host.example.com"
       port: 443     
```
