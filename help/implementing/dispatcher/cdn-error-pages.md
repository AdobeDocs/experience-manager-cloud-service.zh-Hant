---
title: 設定CDN錯誤頁面
description: 瞭解如何在自行託管的儲存體(例如Amazon S3或Azure Blob儲存體)中託管靜態檔案，並在使用Cloud Manager設定管道部署的設定檔案中參照這些檔案，以覆寫預設錯誤頁面。
feature: Dispatcher
source-git-commit: 11036c3e95f0444fc5d865232a7dccab5b7f26ae
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---


# 設定CDN錯誤頁面 {#cdn-error-pages}

>[!NOTE]
>此功能尚未正式推出。若要加入率先採用者計畫，請傳送電子郵件至 `aemcs-cdn-config-adopter@adobe.com` 並說明您的使用案例。

萬一發生下列罕見情況 [Adobe管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) 無法連線至AEM來源，CDN預設會提供不具品牌的一般錯誤頁面，指出無法連線至伺服器。 您可以將靜態檔案託管於自行託管的儲存體(例如Amazon S3或Azure Blob儲存體)中，並在使用部署的設定檔案中參照這些檔案，藉此覆寫預設錯誤頁面。 [Cloud Manager設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

## 設定 {#setup}

您必須先執行下列操作，才能覆寫預設錯誤頁面：

* 首先，在Git專案的頂層資料夾中建立此資料夾和檔案結構：

```
config/
     cdn.yaml
```

* 其次， `cdn.yaml` 設定檔案應包含中繼資料和錯誤頁面參照，如下所述。

### 設定 {#configuration}

錯誤頁面會實作為單頁應用程式(SPA)，並參考一些屬性，如以下範例所示。  URL參考的靜態檔案應由您透過網際網路可存取的服務(例如Amazon S3或Azure Blob Storage)來託管。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```

| 名稱 | 允許的屬性 | 含義 |
|-----------|--------------------------|-------------|
| **spa** | 標題 | 錯誤頁面的標題。 |
|     | icoUrl | 圖示檔案的URL。 |
|     | cssUrl | CSS檔案的URL。 |
|     | jsUrl | JavaScript檔案的URL。 |

### 範例產生的HTML {#sample-generated-html}

CDN產生並提供給使用者端（例如瀏覽器）的HTML程式碼會類似（但不完全相同）下列程式碼片段：

```
<!DOCTYPE html>
<html lang="en">
    <head>
        ...
        <title>the error page</title>
        <link rel="icon" href="https://www.example.com/error.ico">
        <link rel="stylesheet" href="https://www.example.com/error.css">
    </head>
    <body>
        ...
        <div id="root" status="403"></div>
        <script src="https://www.example.com/error.js"> </script>
    </body>
</html>
```

### 測試 {#testing}

為了測試目的，請使用支援的錯誤代碼呼叫專用端點，例如：

```
curl "https://publish-pXXXXX-eXXXXXX.adobeaemcloud.com/cdnstatus?code=403"
```

支援的程式碼為：403、404、406、500和503。

如此一來，您就能直接觸發CDN的錯誤處理常式，以測試指定錯誤碼的綜合回應。
