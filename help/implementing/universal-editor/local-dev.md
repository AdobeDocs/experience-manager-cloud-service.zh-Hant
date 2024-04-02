---
title: 使用 Universal Editor 進行本機 AEM 開發
description: 了解 Universal Editor 如何支援為開發目的在本機 AEM 執行個體上進行編輯。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: 0bb649b91c42f43b852d7fdd54b367c0c5df2c99
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 61%

---


# 使用 Universal Editor 進行本機 AEM 開發 {#local-dev-ue}

了解 Universal Editor 如何支援為開發目的在本機 AEM 執行個體上進行編輯。

## 概觀 {#overview}

Universal Editor 服務綁定 Universal Editor 和後端系統。若要能夠在本機開發Universal Editor，您必須執行Universal Editor服務的本機復本。 原因如下：

* Adobe的官方Universal Editor服務託管於全球各地，而您的本機AEM執行個體必須向網際網路公開。
* 使用本機AEM SDK進行開發時，無法從網際網路存取Adobe的通用編輯器服務。
* 如果您的AEM執行個體有IP限制，而Adobe的Universal Editor服務不在定義的IP範圍內，則您可以自行託管。

本檔案說明如何在HTTPS中搭配通用編輯器服務的本機復本執行AEM，以便您可以在AEM上本機開發以與通用編輯器搭配使用。

## 將 AEM 設定為在 HTTPS 上執行 {#aem-https}

在以HTTPS固定的外部框架中，無法載入不安全的HTTP框架。 Universal Editor 服務會在 HTTPS 上執行，因此 AEM 或任何其他遠端頁面也必須在 HTTPS 上執行。

為此，您需要將 AEM 設定為在 HTTPS 上執行。出於開發目的，您可以使用自我簽署憑證。

[請參閱此檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html) 有關如何設定在HTTPS上執行的AEM，包括您可使用的自我簽署憑證。

## 安裝 Universal Editor 服務 {#install-ue-service}

Universal Editor服務並非Universal Editor的完整復本，而是其功能的子集，以確保不會透過網際網路路由來自您本機AEM環境的呼叫，而是從您控制的已定義端點路由呼叫。

[NodeJS版本16](https://nodejs.org/en/download/releases) 執行Universal Editor服務的本機副本需要。

Universal Editor服務可透過Software Distribution取得。 請參閱 [Software Distribution檔案](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html) 以取得存取它的詳細資訊。

儲存 `universal-editor-service.cjs` 檔案從Software Distribution傳至您的本機開發環境。

## 建立憑證以透過 HTTPS 執行 Universal Editor 服務 {#ue-https}

Universal Editor 服務還需要憑證才能在開發環境中在 HTTPS 上執行。

執行以下命令。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

該命令會產生一個 `key.pem` 和一個 `certificate.pem` 檔案。將這些檔案儲存至與您 `universal-editor-service.cjs` 檔案相同的路徑。

## 進行 Universal Editor 服務設定 {#setting-up-service}

必須在 NodeJS 中設定許多環境變數，才能在本機上執行 Universal Editor 服務。

在與您 `universal-editor-service.cjs`、`key.pem` 和 `certificate.pem` 檔案相同的路徑上，建立一個包含以下內容的 `.env` 檔案。

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

此變數的意義如下：

* `EXPRESS_PORT`：定義 Universal Editor 服務偵聽的連接埠
* `EXPRESS_PRIVATE`：指向您[先前建立的私鑰 ](#ue-https)`key.pem`
* `EXPRESS_CERT`：指向您[先前建立的憑證 ](#ue-https)`certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`：接受自我簽署憑證

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
>嘗試直接存取 `https://localhost:8000` 結果位於 `404` 錯誤。 這是預期行為。
>
>若要測試對您本機Universal Editor服務的存取，請使用 `https://localhost:8000/corslib/LATEST`. 請參閱 [下一節](#editing) 以取得詳細資訊。

>[!TIP]
>
>有關如何偵測頁面以使用全域 Universal Editor 服務的更多詳情，請參閱文件[開始在 AEM 使用 Universal Editor](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本機 Universal Editor 服務編輯頁面 {#editing}

有了[本機執行的 Universal Editor 服務](#running-ue)和[經檢測可使用本機服務的內容頁面](#using-loca-ue)，現在您可以啟動編輯器。

1. 開啟您的瀏覽器，前往 `https://localhost:8000/corslib/LATEST`。
1. 指示您的瀏覽器接受[您的自我簽署憑證。](#ue-https)
1. 一旦自我簽署憑證受到信任，您就可以使用本機 Universal Editor 服務編輯頁面。
