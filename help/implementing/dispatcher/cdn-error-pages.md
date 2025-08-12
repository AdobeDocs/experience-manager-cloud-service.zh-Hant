---
title: 設定CDN錯誤頁面
description: 瞭解如何在自行託管的儲存體(例如Amazon S3或Azure Blob儲存體)中託管靜態檔案，並在使用Cloud Manager設定管道部署的設定檔案中參照這些檔案，藉此覆寫預設錯誤頁面。
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---


# 設定CDN錯誤頁面 {#cdn-error-pages}

萬一[Adobe管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)無法連線至AEM來源，CDN預設會提供不記名的一般錯誤頁面，指出無法連線至伺服器。 您可以在自行託管的儲存體(例如Amazon S3或Azure Blob儲存體)中託管靜態檔案，並在使用Cloud Manager [設定管道](/help/operations/config-pipeline.md#managing-in-cloud-manager)部署的設定檔案中參照這些檔案，藉此覆寫預設錯誤頁面。

## 設定 {#setup}

您必須先執行下列操作，才能覆寫預設錯誤頁面：

1. 參照下方的語法區段，建立名為`cdn.yaml`或類似的檔案。

1. 將檔案放置在名為&#x200B;*config*&#x200B;或類似名稱的頂層資料夾之下，如[使用設定管道](/help/operations/config-pipeline.md#folder-structure)中所述。

1. 在Cloud Manager中建立設定管道，如[使用設定管道](/help/operations/config-pipeline.md#managing-in-cloud-manager)中所述。

1. 部署設定。

### 語法 {#syntax}

錯誤頁面會實作為單頁應用程式(SPA)，並參考一些屬性，如下列範例所示。  URL參考的靜態檔案應由您透過網際網路可存取的服務(例如Amazon S3或Azure Blob Storage)來託管。

設定範例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```

請參閱[使用設定管道](/help/operations/config-pipeline.md#common-syntax)，以取得資料節點上方屬性的說明。 kind屬性值應該是&#x200B;*CDN*，且`version`屬性應該設定為&#x200B;*1*。


| 名稱 | 允許的屬性 | 含義 |
|-----------|--------------------------|-------------|
| **spa** | 標題 | 錯誤頁面的標題。 |
|     | icoUrl | 圖示檔案的URL。 |
|     | cssUrl | CSS檔案的URL。 |
|     | jsUrl | JavaScript檔案的URL。 |

### 產生的範例HTML {#sample-generated-html}

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

### 教學課程

請參閱[CDN錯誤頁面](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/content-delivery/custom-error-pages#cdn-error-pages)教學課程，以取得如何建立、部署和測試CDN提供的錯誤頁面的逐步指示。


