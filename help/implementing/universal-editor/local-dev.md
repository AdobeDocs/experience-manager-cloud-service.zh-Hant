---
title: 執行您自己的Universal Editor服務
description: 瞭解如何執行您自己的Universal Editor服務，以供本機開發或作為您自己基礎結構的一部分。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 5435f776e38abf5245c58985e747ce05443f3c2a
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 36%

---


# 執行您自己的Universal Editor服務 {#local-ue-service}

瞭解如何執行您自己的Universal Editor服務，以供本機開發或作為您自己基礎結構的一部分。

>[!NOTE]
>
>使用AEM製作與Edge Delivery Services的專案不需要或支援本機通用編輯器服務。

## 概觀 {#overview}

Universal Editor 服務綁定 Universal Editor 和後端系統。若要能夠在本機開發Universal Editor，您必須執行Universal Editor服務的本機復本。 原因如下：

* Adobe的官方Universal Editor服務於全球各地託管，而您的本機AEM執行個體必須公開至網際網路。
* 使用本機AEM SDK進行開發時，無法從網際網路存取Adobe的Universal Editor Service 。
* 如果您的AEM執行個體有IP限制，而Adobe的Universal Editor服務不在定義的IP範圍內，您可以自行託管。

## 使用案例 {#use-cases}

如果您想要：

* 在AEM上本機開發，以便與通用編輯器搭配使用。
* 將您自己的Universal Editor服務當成您自己的基礎結構的一部分來執行，獨立於Adobe的Universal Editor服務。

支援這兩個使用案例。 本檔案說明如何在HTTPS中執行AEM以及通用編輯器服務的本機復本。

如果您想要將自己的通用編輯器服務當做自己基礎結構的一部分來執行，您將遵循與本機開發範例相同的步驟。

## 將 AEM 設定為在 HTTPS 上執行 {#aem-https}

在使用HTTPS固定的外部框架中，無法載入不安全的HTTP框架。 Universal Editor 服務會在 HTTPS 上執行，因此 AEM 或任何其他遠端頁面也必須在 HTTPS 上執行。

為此，您需要將 AEM 設定為在 HTTPS 上執行。出於開發目的，您可以使用自我簽署憑證。

[請參閱此檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=zh-Hant)，瞭解如何設定在HTTPS上執行的AEM，包括您可使用的自我簽署憑證。

## 安裝 Universal Editor 服務 {#install-ue-service}

Universal Editor服務並非Universal Editor的完整復本，而是其功能的子集，可確保不會透過網際網路路由來自本機AEM環境的呼叫，而會從您控制的已定義端點路由呼叫。

需要[NodeJS版本20](https://nodejs.org/en/download/releases)才能執行通用編輯器服務的本機復本。

Universal Editor服務可透過Software Distribution取得。 如需如何存取軟體的詳細資訊，請參閱[軟體發佈檔案](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=zh-Hant)。

將`universal-editor-service.cjs`檔案從Software Distribution儲存至您的本機開發環境。

## 建立憑證以透過 HTTPS 執行 Universal Editor 服務 {#ue-https}

Universal Editor 服務還需要憑證才能在開發環境中在 HTTPS 上執行。

執行以下命令。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

該命令會產生一個 `key.pem` 和一個 `certificate.pem` 檔案。將這些檔案儲存至與您 `universal-editor-service.cjs` 檔案相同的路徑。

## 設定Universal Editor服務設定 {#setting-up-service}

必須在 NodeJS 中設定許多環境變數，才能在本機上執行 Universal Editor 服務。

在與您 `universal-editor-service.cjs`、`key.pem` 和 `certificate.pem` 檔案相同的路徑上，建立一個包含以下內容的 `.env` 檔案。

```text
UES_PORT=8000
UES_PRIVATE_KEY=./key.pem
UES_CERT=./certificate.pem
UES_TLS_REJECT_UNAUTHORIZED=false
UES_CORS_PRIVATE_NETWORK=true
```

這些是範例中本機開發所需的最小值。

>[!NOTE]
>
>如果您執行Chrome 130+版，您必須使用`UES_CORS_PRIVATE_NETWORK`選項為[私人網路存取](https://wicg.github.io/private-network-access/#private-network-request)啟用傳送CORS標頭。


下表詳細說明這些值和可用的其他值。

| 值 | 選用 | 預設 | 說明 |
|---|---|---|---|
| `UES_PORT` | 是 | `8080` | 伺服器執行所在的連線埠 |
| `UES_PRIVATE_KEY` | 是 | 無 | https伺服器私密金鑰的路徑 |
| `UES_CERT` | 是 | 無 | HTTPS伺服器憑證檔案的路徑 |
| `UES_TLS_REJECT_UNAUTHORIZED` | 是 | `true` | 拒絕未授權的TLS連線 |
| `UES_DISABLE_IMS_VALIDATION` | 是 | `false` | 停用IMS驗證 |
| `UES_ENDPOINT_MAPPING` | 是 | 空白 | 內部重寫的端點對應<br>範例： `UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>結果：通用編輯器服務將連線到`http://10.0.0.1:4502`，而不是提供的連線`https://your-public-facing-author-domain.net` |
| `UES_LOG_LEVEL` | 是 | `info` | 伺服器的記錄層級，可能的值為`silly`、`trace`、`debug`、`verbose`、`info`、`log`、`warn`、`error`和`fatal` |
| `UES_SPLUNK_HEC_URL` | 是 | 無 | 指向Splunk端點的HEC URL |
| `UES_SPLUNK_TOKEN` | 是 | 無 | Splunk權杖 |
| `UES_SPLUNK_INDEX` | 是 | 無 | 要寫入記錄的索引 |
| `UES_SPLUNK_SOURCE` | 是 | `universal-editor-service` | splunk記錄檔中的來源名稱 |
| `UES_CORS_PRIVATE_NETWORK` | 是 | `false` | 啟用傳送CORS標頭以允許[私人網路](https://wicg.github.io/private-network-access/#private-network-request)。 Chrome 130+版使用者的必要專案 |

>[!NOTE]
>
>在Universal Editor的[2024.08.13版本](/help/release-notes/universal-editor/current.md)之前，`.env`檔案中需要下列變數。 為了回溯相容性，這些值將支援直到2024年10月1日。
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
>嘗試直接存取`https://localhost:8000`導致`404`錯誤。 這是預期行為。
>
>若要測試存取您本機的Universal Editor服務，請使用`https://localhost:8000/corslib/LATEST`。 如需詳細資訊，請參閱[下一節](#editing)。

>[!TIP]
>
>有關如何偵測頁面以使用全域 Universal Editor 服務的更多詳情，請參閱文件[開始在 AEM 使用 Universal Editor](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本機 Universal Editor 服務編輯頁面 {#editing}

透過[Universal Editor Service在本機執行](#running-ue)，且您的[內容頁面已設定為使用本機服務](/help/implementing/universal-editor/getting-started.md)，您現在可以啟動編輯器。

1. 開啟您的瀏覽器，前往 `https://localhost:8000/ping`。
1. 指示瀏覽器接受[您的自我簽署憑證](#ue-https)。
1. 一旦自我簽署憑證受到信任，您就可以使用本機 Universal Editor 服務編輯頁面。

