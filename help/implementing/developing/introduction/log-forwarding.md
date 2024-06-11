---
title: AEMas a Cloud Service的記錄轉送
description: 瞭解如何在AEMas a Cloud Service將記錄轉送給Splunk和其他記錄廠商
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0e166e8549febcf5939e4e6025519d8387231880
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 1%

---

# 記錄轉送 {#log-forwarding}

>[!NOTE]
>
>此功能尚未發行，並且某些記錄目的地在發行時可能不可用。 同時，您可以開啟支援票證以將記錄轉送到 **Splunk**，如 [記錄文章](/help/implementing/developing/introduction/logging.md).

擁有記錄廠商的授權或託管記錄產品的客戶可以將AEM、Apache/Dispatcher和CDN記錄轉送至關聯的記錄目的地。 AEMas a Cloud Service支援下列記錄目的地：

* Azure Blob儲存體
* DataDog
* Elasticsearch或OpenSearch
* HTTPS
* Splunk

以自助方式設定記錄轉送，方法是在Git中宣告設定，並透過Cloud Manager設定管道將其部署到生產（非沙箱）程式中的開發、中繼和生產環境型別。

AEM和Apache/Dispatcher記錄檔可選擇透過AEM進階網路基礎結構（例如專用輸出IP）進行路由。

請注意，與傳送至記錄目的地的記錄檔相關聯的網路頻寬，會視為您組織網路I/O使用量的一部分。


## 本文的結構方式 {#how-organized}

本文章的編排方式如下：

* 設定 — 適用於所有記錄目的地
* 記錄目的地設定 — 每個目的地的格式稍有不同
* 記錄專案格式 — 記錄專案格式的相關資訊
* 進階網路 — 透過專用出口或VPN傳送AEM和Apache/Dispatcher記錄檔


## 設定 {#setup}

1. 在Git中專案的頂層資料夾中建立以下資料夾和檔案結構：

   ```
   config/
        logForwarding.yaml
   ```

1. `logForwarding.yaml` 應包含中繼資料及類似於以下格式的設定（我們使用Splunk作為範例）。

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

   此 **種類** 引數應設為 `LogForwarding` 版本應設定為結構描述版本，即1。

   設定中的權杖(例如 `${{SPLUNK_TOKEN}}`)代表不應儲存在Git中的秘密。 請改為宣告他們為Cloud Manager  [環境變數](/help/implementing/cloud-manager/environment-variables.md) 型別 **密碼**. 請務必選取 **全部** 作為「已套用服務」欄位的下拉式清單值，因此可將記錄檔轉送至作者、發佈和預覽層級。

   您可以在cdn記錄檔和其他所有專案(AEM和apache記錄檔)之間設定不同的值，方法是加入額外的 **cdn** 和/或 **aem** 封鎖晚於 **預設** 區塊，其中屬性可覆寫以下位置中定義的屬性： **預設** 區塊；只需要enabled屬性。 一個可能的使用案例是對CDN記錄使用不同的Splunk索引，如以下範例所示。

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

   另一種情況是停用CDN記錄或其他所有專案(AEM和apache記錄)的轉送。 例如，若只要轉送CDN記錄檔，即可設定下列專案：

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

1. 對於RDE以外的環境型別（目前不支援），請在Cloud Manager中建立目標部署設定管道。

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

![Azure Blob SAS權杖設定](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

#### Azure Blob儲存CDN記錄 {#azureblob-cdn}

每個分散於全球各地的記錄伺服器每隔幾秒會產生一個新檔案，位於 `aemcdn` 資料夾。 建立後，檔案將不再附加到。 檔案名稱格式為YYYY-MM-DDThh:mm:ss.sss-uniqueid.log. 例如：2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log。

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

每個檔案包含多個json記錄專案，每個專案位於一行中。 有關記錄專案格式的說明，請參閱 [記錄文章](/help/implementing/developing/introduction/logging.md)，每個記錄專案也包含 [記錄專案格式](#log-format) 一節。

#### 其他Azure Blob儲存體記錄檔 {#azureblob-other}

CDN記錄以外的記錄會顯示在具有以下命名慣例的資料夾下方：

* aemaccess
* aemerror
* aemdispatcher
* httpdaccess
* httpderror

在每個資料夾下，將建立單一檔案並附加至其中。 客戶應負責處理和管理此檔案，以免檔案變得太大。

請參閱以下檔案中的記錄專案格式 [記錄文章](/help/implementing/developing/introduction/logging.md). 記錄專案也包含 [記錄專案格式](#log-formats) 一節。


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  dataDog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      
```

考量事項：

* 建立API金鑰，而不與特定雲端提供者進行任何整合。


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
```

考量事項：

* 對於認證，請務必使用部署認證，而不是帳戶認證。 這些是在畫面中產生的認證，可能類似於此影像：

![彈性部署認證](/help/implementing/developing/introduction/assets/ec-creds.png)

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

#### HTTPS CDN記錄 {#https-cdn}

Web請求(POST)將會持續傳送，其json裝載為一系列記錄專案，記錄專案格式於 [記錄文章](/help/implementing/developing/introduction/logging.md#cdn-log). 有關其他屬性的詳情，請參閱 [記錄專案格式](#log-formats) 一節。

此外還有名為的屬性 `sourcetype`，此值會設定為 `aemcdn`.

#### 其他HTTPS記錄檔 {#https-other}

系統會為每個記錄專案傳送個別的網路要求(POST)，記錄專案格式請見 [記錄文章](/help/implementing/developing/introduction/logging.md). 有關其他屬性的詳情，請參閱 [記錄專案格式](#log-format) 一節。

此外還有名為的屬性 `sourcetype`，會設定為下列其中一個值：

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

檢視一般 [記錄文章](/help/implementing/developing/introduction/logging.md) （Dispatcher記錄檔、CDN記錄檔等）的格式。

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

對於CDN記錄，您可以將IP位址加入允許清單，如中所述 [本文](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). 如果共用IP位址清單太大，請考慮傳送流量至(非Adobe) Azure Blob存放區，其中可寫入邏輯，以將專用IP的記錄傳送至其最終目的地。

對於其他記錄檔，您可以設定記錄檔轉送來進行 [進階網路](/help/security/configuring-advanced-networking.md). 檢視以下三種進階網路型別的模式，它們使用選購的 `port` 引數，以及 `host` 引數。

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
