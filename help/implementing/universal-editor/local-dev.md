---
title: 使用 Universal Editor 進行本機 AEM 開發
description: 了解 Universal Editor 如何支援為開發目的在本機 AEM 執行個體上進行編輯。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 87%

---


# 使用 Universal Editor 進行本機 AEM 開發 {#local-dev-ue}

了解 Universal Editor 如何支援為開發目的在本機 AEM 執行個體上進行編輯。

{{universal-editor-status}}

## 概觀 {#overview}

本檔案說明如何在HTTPS中連同通用編輯器服務的本機復本一起執行AEM，以便您可以使用通用編輯器在AEM上本機開發。

## 將 AEM 設定為在 HTTPS 上執行 {#aem-https}

在以HTTPS固定的外部框架中，無法載入不安全的HTTP框架。 Universal Editor 服務會在 HTTPS 上執行，因此 AEM 或任何其他遠端頁面也必須在 HTTPS 上執行。

為此，您需要將 AEM 設定為在 HTTPS 上執行。出於開發目的，您可以使用自我簽署憑證。

請參閱本檔案以瞭解如何設定在HTTPS上執行的AEM，包括您可使用的自我簽署憑證。

## 安裝 Universal Editor 服務 {#install-ue-service}

Universal Editor 服務綁定 Universal Editor 和後端系統。由於官方 Universal Editor 服務為全球託管，因此您的本機 AEM 執行個體需要暴露於網際網路。為了避免這種情況，您可以執行 Universal Editor 服務的本機副本。

[NodeJS 版本 16](https://nodejs.org/en/download/releases)需要執行 Universal Editor 服務的本機副本

Universal Editor 服務由 AEM Engineering 直接分發。請聯絡VIP程式中的工程師以取得本機復本。

工程人員將為您提供 `universal-editor-service.cjs` 檔案。將其儲存至您的本機開發環境中。

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

>[!TIP]
>
>有關如何偵測頁面以使用全域 Universal Editor 服務的更多詳情，請參閱文件[開始在 AEM 使用 Universal Editor](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本機 Universal Editor 服務編輯頁面 {#editing}

有了[本機執行的 Universal Editor 服務](#running-ue)和[經檢測可使用本機服務的內容頁面](#using-loca-ue)，現在您可以啟動編輯器。

1. 開啟您的瀏覽器，前往 `https://localhost:8000/`。
1. 指示您的瀏覽器接受[您的自我簽署憑證。](#ue-https)
1. 一旦自我簽署憑證受到信任，您就可以使用本機 Universal Editor 服務編輯頁面。
