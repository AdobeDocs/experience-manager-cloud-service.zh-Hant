---
title: 如何使用AFP輸出同步API？
description: 瞭解如何使用AFP Output Sync API來擷取及同步輸出轉譯。
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, User
exl-id: 5602fc63-ef74-44eb-b3be-61b8f8a2795a
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 14%

---

# 使用 AEM Forms API 產生 AFP 輸出

<span class="preview">這是一項預先發佈功能，可透過我們的[預先發佈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)存取。</span>

進階功能簡報(AFP)是專為列印目的而設計的高效能檔案格式。\
本指南概述使用AEM Forms產生AFP輸出所需的所有必要步驟和設定。

<!--
## Prerequisites

To support AFP output generation, the following OSGi bundles must be present and in an **active** state:

* **AFP Core Bundle** – Available in the AFP repository
* **Forms Output Core** – Found in the Forms Output comments package
* **Bedrock Connector** – Provided by the Forms Output API
* **Cloud Ready Implementation** – Available through the Forms installer

>[!NOTE]
>
> * If any bundle is inactive, resolve dependency issues or reinstall manually.
> * To enable AFP generation, the `FT_FORMS-17887` toggle configurations must be set in AEM configuration manager.-->

## AFP Generation API

使用XDP範本和輸入資料產生AFP （進階函式簡報）檔案。

### 授權

您可以將&#x200B;**BasicAuth** （管理員認證）用於本機環境，或將&#x200B;**BearerAuth**&#x200B;授權用於AEM Cloud執行個體。

### 請求

**端點：**
`POST http://<server>:<port>/adobe/forms/document/generate/afp`

### 標頭

| 索引鍵 | 值 |
| --------------- | ------------------------------------------------------ |
| `Content-Type` | `application/pdf` |
| `Authorization` | `(Bearer Access token)` |

### 要求內文

**Content-Type： multipart/form-data**

| 索引鍵 | 類型 | 必要 | 說明 |
| ---------- | ---- | -------- | ------------------------------------------------------------------------- |
| `template` | 檔案/文字 | 是 | XDP檔案用作AFP產生的範本（例如，`demo.xdp`） |
| `data` | 檔案/文字 | 否 | 要與範本合併的資料檔案（XML或JSON） （例如`data.xml`） |
| `options` | 文字 | 否 | JSON字串，其中包含控制AFP輸出的選項（例如解析度、地區設定） |

**範例`options` JSON （文字欄位）：**

```json
{
  "pdfVersion": "1.7",
  "resolution": 300,
  "locale": "en-US",
  "embedFonts": true,
  "contentRoot": "/usr/tmp"
}
```

### 回應

| 代碼 | 說明 |
| ----- | ------------------------------------------------------------------------- |
| `200` | 作業成功。 傳回AFP檔案資料流。 |
| `400` | 錯誤請求。 請求承載的格式錯誤或缺少必填欄位。 |
| `500` | 內部伺服器錯誤。 請稍後再試。 |

### Curl指令

```
curl --location 'http://<server>:<port>/adobe/forms/document/generate/afp' \
--header 'Authorization: Bearertoken <base64-encoded-credentials>' \
--form 'template=@"<path-to-template>.xdp"' \
--form 'data=@"<path-to-data-file>.xml"' \
--form 'options=<JSON-options-string>'
```

### 測試API

您可以下載.yaml檔案並將其上傳到Postman以檢查API的功能。

![AFP Postman影像](/help/forms/assets/afp-postman.png)

您可以儲存回應，並在AFP讀取器中開啟儲存的檔案進行檢視。

![PDF讀取器](/help/forms/assets/afp-pdf.png)
