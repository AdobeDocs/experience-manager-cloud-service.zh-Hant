---
title: 跨網站重複使用程式碼
description: 如果您擁有許多類似的網站，其外觀和行為大多相同但擁有不同的內容，請了解如何在無存放庫模型中跨多個網站共用程式碼。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
index: false
hide: true
hidefromtoc: true
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 100%

---

# 跨網站重複使用程式碼 {#repoless}

如果您擁有許多類似的網站，其外觀和行為大多相同但擁有不同的內容，請了解如何在無存放庫模型中跨多個網站共用程式碼。

## 單一程式碼基底適用於多個網站 {#one-codebase}

在預設情況下，AEM 與您的程式碼存放庫緊密連結，可滿足大多數的使用案例。然而，您可能擁有多個網站而且其大部分內容並不相同，但可以善用相同的程式碼基底。

AEM 支援使用相同的程式碼基底執行多個網站，而非建立多個 GitHub 存放庫，並在專用 GitHub 存放庫執行每個網站並保持同步。

此簡化設定消除程式碼複寫需求，也稱為[「無存放庫」](https://www.aem.live/docs/repoless)，因為除了您的第一個網站之外，其他的所有網站均不需要自己的 GitHub 存放庫。

如果您的專案需要無存放庫的彈性，以便跨網站重複使用程式碼，您可以啟用此功能。

無論最終想以無存放庫的方式建立多少個網站，您必須建立作為基礎網站的第一個網站。此文件說明如何建立您的第一個無存放庫網站。

## 先決條件 {#prerequisites}

若要利用此功能，請確保您已執行下列動作。

* 您的網站按照[使用 Edge Delivery Services 進行所見即所得製作的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)文件，已完成所有設定。
* 您至少正在執行 AEM as a Cloud Service 2024.08。

您也需要要求 Adobe 協助您設定下列項目。透過您的 Slack 頻道聯絡或提出支援問題，要求 Adobe 進行下列變更：

* 要求為您的環境啟用「[aem.live 設定服務](https://www.aem.live/docs/config-service-setup#prerequisites)」，並將您設定為管理員。
* 要求 Adobe 為您的方案啟用無存放庫功能。
* 要求 Adobe 為您建立組織。

## 啟用無存放庫功能 {#activate}

下列是為您的專案啟用無存放庫功能所需的數個步驟。

1. [獲取存取權杖](#access-token)
1. [建置設定服務](#config-service)
1. [新增網站設定和技術帳戶](#access-control)
1. [更新 AEM 設定](#update-aem)
1. [驗證網站](#authenticate-site)

這些步驟使用 `https://wknd.site` 網站作為範例。請適當地替換成您自己的網站。

### 獲取存取權杖 {#access-token}

您首先需要存取權杖來使用設定服務，並針對無存放庫使用案例進行設定。

1. 前往 `https://admin.hlx.page/login`，並使用 `login_adobe` 位址以 Adobe 身分識別提供者的身分登入。
1. 您將轉送至 `https://admin.hlx.page/profile`。
1. 透過使用瀏覽器的開發人員工具，從 `admin.hlx.page` 頁面設定的 JSON 網頁權杖 Cookie 中複製 `x-auth-token` 的值。

您獲得存取權杖後，可使用以下列格式將其傳遞至 cURL 請求的標題中。

```text
--header 'x-auth-token: <your-token>'
```

### 新增網站設定的路徑對應，並設定技術帳戶 {#access-control}

您需要建立網站設定，並將其新增至路徑對應。

1. 在您的網站根目錄建立新頁面，並選擇&#x200B;[**設定** 範本](/help/edge/wysiwyg-authoring/tabular-data.md#other)。
   * 您可以將設定保持空白，僅保留預先定義的 `key` 和 `value` 欄。您只要建立即可。
1. 使用類似於下列內容的 cURL 命令，在公開設定中建立與網站設定的對應。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/",
               "/content/<your-site-content>/configuration:/.helix/config.json"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```

1. 使用類似下列內容的 cURL 命令，驗證公開設定是否已完成設定並可用。

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

對應網站設定後，只要定義您的技術帳戶使其具有發佈權限，即可設定存取控制。

1. 登入 AEM 作者實例，並前往「**工具**」->「**雲端服務**」->「**Edge Delivery Services 設定**」，選取為您的網站自動建立的設定，然後點選或按一下工具列中的「**屬性**」。

1. 在「**Edge Delivery Services 設定**」視窗中，選取「**驗證**」索引標籤，並複製&#x200B;**技術帳戶 ID** 的值。

   * 看起來與 `<tech-account-id>@techacct.adobe.com` 類似
   * 單一 AEM 製作環境中所有網站的技術帳戶皆相同。

1. 使用類似下列內容的 cURL 命令，並使用您複製的技術帳戶 ID，設定無存放庫設定適用的技術帳戶。

   * 調整 `admin` 區塊，以定義應該具有網站完整管理存取權的使用者。
      * 這個區塊包含許多電子郵件。
      * 可以使用萬用字元「`*`」。
      * 請參閱[設定作者驗證](https://www.aem.live/docs/authentication-setup-authoring#default-roles)的文件，以了解更多資訊。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "admin": {
           "role": {
               "admin": [
                   "<email>@<domain>.<tld>"
               ],
               "config_admin": [
                   "<tech-account-id>@techacct.adobe.com"
               ]
           },
           "requireAuth": "auto"
       }
   }'
   ```

由於您現在使用設定服務，因此您可以從 Git 存放庫移除 `fstab.yaml` 和 `paths.json`。

>[!NOTE]
>
>透過使用設定服務，並透過 `config.json` 公開路徑對應，將忽略此 `path.json` 檔案。

只要 AEM 已經設定為無存放庫的使用模式後，您必須使用設定服務並提供包含路徑對應的有效的 `config.json`。

### 更新 AEM 設定 {#update-aem}

現在您已準備好對 AEM 中的 Edge Delivery Services 進行必要的變更。

1. 登入 AEM 作者實例，並前往「**工具**」->「**雲端服務**」->「**Edge Delivery Services 設定**」，選取為您的網站自動建立的設定，然後點選或按一下工具列中的「**屬性**」。
1. 在「**Edge Delivery Services 設定**」視窗中，將專案類型變更為「**aem.live」並使用無存放庫設定**，然後點選或按一下「**儲存並關閉**」。
   ![Edge Delivery Services 設定](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. 使用通用編輯器返回您的網站，並確保其仍然正確轉譯。
1. 修改部分內容並重新發佈。
1. 請造訪您發佈的網站，網址為 `https://main--<your-aem-project>--<your-github-org>.aem.page/`，並確認是否已經正確反映相關變更。

您的專案現已設定為無存放庫的使用模式。

## 後續步驟 {#next-steps}

現在您的基本網站已設定為無存放庫的使用模式，您可以建立利用相同程式碼基底的其他網站。根據您的使用案例，請參考下列文件。

* [無存放庫多網站管理](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [無存放庫階段及生產環境](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [內容製作的網站驗證](/help/edge/wysiwyg-authoring/site-authentication.md)

## 疑難排解 {#troubleshooting}

設定無存放庫使用案例後，最常發生的問題是通用編輯器的頁面不再轉譯，或者會收到白色頁面或一般的 AEM as a Cloud Service 錯誤訊息。在這類情況下：

* 檢視轉譯頁面的來源。
   * 是否已有實際轉譯的部分內容 (具有 `scripts.js`、`aem.js` 的正確 HTML 標頭，以及與編輯器相關的 JSON 檔案)？
* 檢查作者實例的 AEM `error.log` 尋找異常狀況。
   * 最常見的問題是頁面元件失敗，並出現 404 錯誤。
   * 無法載入 `config.json or paths.json`
   * `component-definition.json` 等無法載入
