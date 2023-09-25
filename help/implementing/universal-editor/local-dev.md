---
title: 使用通用編輯器的本機AEM開發
description: 瞭解通用編輯器如何支援在本機AEM執行個體上編輯以進行開發。
source-git-commit: bf09c31baf209f5315e35f47c0d79c2b4365d3d3
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# 使用通用編輯器的本機AEM開發 {#local-dev-ue}

瞭解通用編輯器如何支援在本機AEM執行個體上編輯以進行開發。

本檔案將說明如何在HTTPS中連同通用編輯器服務的本機復本一起執行AEM，以便您可以使用通用編輯器在AEM上本機開發。

## 設定AEM以在HTTPS上執行 {#aem-https}

在使用HTTPS固定的外部框架中，無法載入不安全的HTTP框架。 Universal Editor服務會在HTTPS上執行，因此AEM或任何其他遠端頁面也必須在HTTPS上執行。

若要這麼做，您必須設定AEM在HTTPS上執行。 出於開發目的，您可以使用自我簽署憑證。

請參閱本檔案以瞭解如何設定在HTTPS上執行的AEM，包括您可使用的自我簽署憑證。

## 安裝通用編輯器服務 {#install-ue-service}

通用編輯器服務是繫結通用編輯器和後端系統的工具。 由於官方Universal Editor服務是在全球各地託管，因此您的本機AEM執行個體必須向網際網路公開。 若要避免此問題，您可以執行Universal Editor服務的本機副本。

[NodeJS版本16](https://nodejs.org/en/download/releases) 需要才能執行通用編輯器服務的本機復本

Universal Editor服務由AEM Engineering直接發佈。 請洽詢您在VIP計畫中的工程聯絡人，以取得本機復本。

工程部門會提供您 `universal-editor-service.cjs` 檔案。 將此專案儲存至本機開發環境。

## 建立憑證以使用HTTPS執行通用編輯器服務 {#ue-https}

Universal Editor服務也需要在開發環境的HTTPS上執行憑證。

執行以下命令。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

指令會產生 `key.pem` 和 `certificate.pem` 檔案。 將這些檔案儲存到與您的檔案相同的路徑 `universal-editor-service.cjs` 檔案。

## 設定Universal Editor服務組態 {#setting-up-service}

必須在NodeJS中設定許多環境變數，才能在本機執行Universal Editor服務。

路徑與您的相同 `universal-editor-service.cjs`， `key.pem` 和 `certificate.pem` 檔案，建立 `.env` 檔案包含下列內容。

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

變數具有以下含義：

* `EXPRESS_PORT`：定義通用編輯器服務監聽的連線埠
* `EXPRESS_PRIVATE`：指向您的 [先前建立的私密金鑰，](#ue-https) `key.pem`
* `EXPRESS_CERT`：指向您的 [先前建立的憑證，](#ue-https) `certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`：接受自我簽署憑證

## 執行Universal Editor服務 {#running-ue}

若要啟動Universal Editor服務，請執行下列命令：

```text
$ node ./universal-editor-service.cjs
```

它應該會將以下內容輸出到您的終端機：

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

確定服務啟動HTTPS伺服器而非HTTP伺服器。

## 使用本機通用編輯器服務，而非全域服務 {#using-local-ue}

通用編輯器會根據頁面的檢測方式，知道要使用哪種Universal Editor服務來編輯頁面。 這是透過在Universal Editor中載入的頁面中的中繼標籤來完成。

對於要使用本機通用編輯器服務編輯的頁面，必須設定以下中繼標籤：

```
<meta name="urn:adobe:aem:editor:endpoint" content="https://localhost:8000">
```

設定後，您應該會看到每個內容更新呼叫前往 `https://localhost:8000` 而不是預設的Universal Editor服務。

>[!TIP]
>
>如需有關使用全域通用編輯器服務時如何檢測頁面的更多詳細資訊，請參閱檔案 [AEM中的通用編輯器快速入門](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本機通用編輯器服務編輯頁面 {#editing}

使用 [Universal Editor服務在本機執行](#running-ue) 以及您的 [使用本機服務的內容頁面，](#using-loca-ue) 您現在可以啟動編輯器。

1. 開啟瀏覽器，前往 `https://localhost:8000/`.
1. 引導您的瀏覽器接受 [您的自我簽署憑證。](#ue-https)
1. 一旦自我簽署憑證受到信任，您就可以使用本機的Universal Editor Service編輯頁面。
