---
title: AEMas a Cloud Service的記錄轉送
description: 瞭解如何在AEMas a Cloud Service將記錄轉送給Splunk和其他記錄廠商
hide: true
hidefromtoc: true
source-git-commit: d41390696383f8e430bb31bd8d56a5e8843f1257
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 3%

---


# 記錄轉送 {#log-forwarding}

>[!NOTE]
>
>此功能尚未發行，某些記錄目的地在發行時可能不可用。 同時，您可以開啟支援票證以將記錄轉送到 **Splunk**，如 [記錄文章](/help/implementing/developing/introduction/logging.md).

擁有記錄廠商的授權或託管記錄產品的客戶可以將AEM、Apache/Dispatcher和CDN記錄轉送至關聯的記錄目的地。 AEMas a Cloud Service支援下列記錄目的地：

* Azure Blob儲存體
* DataDog
* Elasticsearch或OpenSearch
* HTTPS
* Splunk

以自助方式設定記錄轉送，方法是在Git中宣告設定，並透過Cloud Manager設定管道將其部署到生產（非沙箱）程式中的開發、中繼和生產環境型別。

請注意，與傳送至記錄目的地的記錄檔相關聯的網路頻寬，會視為您組織網路I/O使用量的一部分。


## 本文的結構方式 {#how-organized}

本文章的編排方式如下：

* 設定 — 適用於所有記錄目的地
* 記錄目的地設定 — 每個目的地的格式稍有不同
* 進階網路 — 透過專用出口或VPN傳送AEM和Apache/Dispatcher記錄檔


## 設定 {#setup}

1. 在Git中專案的頂層資料夾中建立以下資料夾和檔案結構：

   ```
   config/
        logForwarding.yaml
   ```

1. logForwarding.yaml應包含中繼資料及類似於以下格式的設定（我們使用Splunk作為範例）。

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

   基於未來的相容性原因，必須包含預設節點。

   kind引數應該設定為LogForwarding，而版本應該設定為結構描述版本，即1。

   設定中的權杖(例如 `${{SPLUNK_TOKEN}}`)代表不應儲存在Git中的秘密。 請改為宣告他們為Cloud Manager  [環境變數](/help/implementing/cloud-manager/environment-variables.md) 型別為「機密」。 請務必選取 **全部** 作為「已套用服務」欄位的下拉式清單值，因此可將記錄檔轉送至作者、發佈和預覽層級。

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

考量事項：

* 使用SAS權杖進行驗證，該權杖應具有最小驗證期。
* SAS權杖應在帳戶頁面上建立，而不是在容器頁面上建立。

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

## 進階網路 {#advanced-networking}

如果您有組織需求來鎖定流向記錄目的地的流量，您可以設定記錄轉送以通過 [進階網路](/help/security/configuring-advanced-networking.md). 檢視以下三種進階網路型別的模式，它們使用選購的 `port` 引數，以及 `host` 引數。

### 彈性連接埠輸出 {#flex-port}

如果記錄流量是傳送到443以外的連線埠（例如，下面的8443），請設定進階網路，如下所示：

```
{
    "portForwards": [
        {
            "name": "mylogging.service.logger.com",
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
      host: "proxy.tunnel"
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
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### VPN {#vpn}

如果記錄流量需要通過VPN，請設定進階網路，如下所示：

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
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
      host: "mylogging.service.com"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```
