---
title: 執行您自己的通用編輯器服務
description: 了解如何執行您自己的通用編輯器服務，無論是為了本機開發或做為基礎結構的一部分。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Developer
source-git-commit: 0df573a3d869f2718983b4e661a86c769b4d3f1a
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 93%

---


# 執行您自己的通用編輯器服務 {#local-ue-service}

了解如何執行您自己的通用編輯器服務，無論是為了本機開發或做為基礎結構的一部分。

>[!NOTE]
>
>使用AEM製作與Edge Delivery Services的專案不需要本機通用編輯器服務。

## 概觀 {#overview}

通用編輯器服務將通用編輯器和後端系統進行繫結。為讓通用編輯器能夠進行本機開發，您必須執行通用編輯器服務的本機副本。這是因為：

* Adobe 的官方通用編輯器服務為全球託管，而您的本機 AEM 實例將必須在網際網路中公開。
* 使用本機 AEM SDK 進行開發時，無法從網際網路存取 Adobe 的通用編輯器服務。
* 若您的 AEM 實例具有 IP 限制，且 Adobe 的通用編輯器服務不在所定義的 IP 範圍內，則您可以自行託管此實例。

## 使用案例 {#use-cases}

若您希望執行以下操作，則您自己的通用編輯器服務副本有很大的用處：

* 在 AEM 上進行本機開發，以便能與通用編輯器搭配使用。
* 將您自己的通用編輯器服務納入基礎結構當中執行，獨立於 Adobe 的通用編輯器服務之外。

兩種使用案例皆支援。本文件將說明如何使用 HTTPS 搭配通用編輯器服務的本機副本執行 AEM。

若您希望將自己的通用編輯器服務納入基礎結構當中執行，您可以按照與本機開發範例相同的步驟進行操作。

## 將 AEM 設定為在 HTTPS 上執行 {#aem-https}

處於由 HTTPS 保護的外部框架內，無法載入不安全的 HTTP 框架。Universal Editor 服務會在 HTTPS 上執行，因此 AEM 或任何其他遠端頁面也必須在 HTTPS 上執行。

為此，您需要將 AEM 設定為在 HTTPS 上執行。出於開發目的，您可以使用自我簽署憑證。

[參閱此文件](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=zh-Hant)了解如何設定 AEM 在 HTTPS 上執行，包括您可以使用的自我簽署憑證。

## 安裝通用編輯器服務 {#install-ue-service}

通用編輯器服務不是通用編輯器的完整副本，只包含其部分功能，以確保來自本機 AEM 環境的呼叫不會在網際網路進行路由，而是由您控制的已定義端點進行路由。

執行通用編輯器服務的本機副本需要 [NodeJS 版本 20](https://nodejs.org/en/download/releases)。

通用編輯器服務可透過 Software Distribution 取得。關於如何存取通用編輯器的詳細資訊，請參閱 [Software Distribution 文件](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=zh-Hant)。

將來自 Software Distribution 的檔案 `universal-editor-service.cjs` 儲存到您的本機開發環境。

## 建立憑證以透過 HTTPS 執行 Universal Editor 服務 {#ue-https}

Universal Editor 服務還需要憑證才能在開發環境中在 HTTPS 上執行。

執行以下命令。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

該命令會產生一個 `key.pem` 和一個 `certificate.pem` 檔案。將這些檔案儲存至與您 `universal-editor-service.cjs` 檔案相同的路徑。

## 進行通用編輯器服務設定 {#setting-up-service}

必須在 NodeJS 中設定許多環境變數，才能在本機上執行 Universal Editor 服務。

在與您 `universal-editor-service.cjs`、`key.pem` 和 `certificate.pem` 檔案相同的路徑上，建立一個包含以下內容的 `.env` 檔案。

```text
UES_PORT=8000
UES_PRIVATE_KEY=./key.pem
UES_CERT=./certificate.pem
UES_TLS_REJECT_UNAUTHORIZED=false
UES_CORS_PRIVATE_NETWORK=true
```

這些是我們範例中本機開發所需的最低值。

>[!NOTE]
>
>如果您執行的是 Chrome 130 以上版本，則必須使用 `UES_CORS_PRIVATE_NETWORK` 選項來啟用 CORS 標頭傳送功能，才能存取[私人網路](https://wicg.github.io/private-network-access/#private-network-request)。


下列表格詳細列出這些值以及其他可用值。

| 值 | 選用 | 預設 | 說明 |
|---|---|---|---|
| `UES_PORT` | 是 | `8080` | 伺服器執行的連接埠 |
| `UES_PRIVATE_KEY` | 是 | 無 | HTTPS 伺服器私密金鑰的路徑 |
| `UES_CERT` | 是 | 無 | HTTPS 伺服器憑證檔案路徑 |
| `UES_TLS_REJECT_UNAUTHORIZED` | 是 | `true` | 拒絕未經授權的 TLS 連線 |
| `UES_DISABLE_IMS_VALIDATION` | 是 | `false` | 停用 IMS 驗證 |
| `UES_ENDPOINT_MAPPING` | 是 | 空 | 對應端點以便進行內部重寫<br>範例：`UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>結果：通用編輯器服務會連結至 `http://10.0.0.1:4502` 而非所提供的連線 `https://your-public-facing-author-domain.net` |
| `UES_LOG_LEVEL` | 是 | `info` | 伺服器的記錄等級，可能的值包括 `silly`、`trace`、`debug`、`verbose`、`info`、`log`、`warn`、`error` 以及 `fatal` |
| `UES_SPLUNK_HEC_URL` | 是 | 無 | HEC URL 至 Splunk 端點 |
| `UES_SPLUNK_TOKEN` | 是 | 無 | Splunk 權杖 |
| `UES_SPLUNK_INDEX` | 是 | 無 | 寫入記錄的索引 |
| `UES_SPLUNK_SOURCE` | 是 | `universal-editor-service` | Splunk 記錄中的來源名稱 |
| `UES_CORS_PRIVATE_NETWORK` | 是 | `false` | 啟用傳送 CORS 標頭以便允許存取[私人網路](https://wicg.github.io/private-network-access/#private-network-request)。 Chrome 版本 130 以上使用者的必要設定 |

>[!NOTE]
>
>通用編輯器 [2024.08.13 版本](/help/release-notes/universal-editor/current.md)之前，`.env` 檔案中必須擁有以下變數。為達到向後相容性，這些值在 2024 年 10 月 1 日之前皆受到支援。
>
>`EXPRESS_PORT=8000`
>`EXPRESS_PRIVATE_KEY=./key.pem`
>`EXPRESS_CERT=./certificate.pem`
>`NODE_TLS_REJECT_UNAUTHORIZED=0`

## 執行 Universal Editor 服務 {#running-ue}

若要啟動 Universal Editor 服務，請執行下列命令：

```text
$ node ./universal-editor-service.cjs
```

此命令應該會將以下內容輸出到您的終端：

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

確保服務啟動 HTTPS 伺服器而不是 HTTP 伺服器。

## 使用本機 Universal Editor 服務而不是全域服務 {#using-local-ue}

Universal Editor 會根據頁面的偵測方式，知道要使用哪個 Universal Editor 服務來編輯頁面。這是透過載入 Universal Editor 頁面的中繼標記來完成。

對於要使用您本機 Universal Editor 服務所編輯的頁面，您必須設定以下中繼標記：

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

設定完成後，您應該會看到每個內容更新呼叫都會前往 `https://localhost:8000`，而不是預設的 Universal Editor 服務。

>[!NOTE]
>
>嘗試直接存取 `https://localhost:8000` 而導致 `404` 錯誤。這是預期的行為。
>
>若要測試存取您的本機通用編輯器服務，請使用 `https://localhost:8000/corslib/LATEST`。如需詳細資訊，請參閱[下一區段](#editing)。

>[!TIP]
>
>有關如何偵測頁面以使用全域 Universal Editor 服務的更多詳情，請參閱文件[開始在 AEM 使用 Universal Editor](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本機 Universal Editor 服務編輯頁面 {#editing}

有了[在本機執行的通用編輯器服務](#running-ue)以及[經檢測為使用本機服務的內容頁面](/help/implementing/universal-editor/getting-started.md)，您現在即可啟動編輯器。

1. 開啟您的瀏覽器，前往 `https://localhost:8000/ping`。
1. 指示您的瀏覽器接受[您的自我簽署憑證](#ue-https)。
1. 一旦自我簽署憑證受到信任，就會使用您本機的Universal Editor服務載入頁面。
1. 按一下工具列中的[本機開發人員登入](/help/sites-cloud/authoring/universal-editor/navigation.md#local-developer-login)，然後驗證您的本機AEM執行個體。

您現在可以使用本機Universal Editor服務，在本機AEM測試執行個體上編輯頁面。
