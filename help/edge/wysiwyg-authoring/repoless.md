---
title: 跨網站重複使用程式碼
description: 如果您有許多相似的網站，大部分外觀和行為相同，但內容不同，請瞭解如何在一個重寫模式中跨多個網站共用程式碼。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
source-git-commit: 7b46af35b202446fdea67e4125d74c3965d302d9
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 2%

---

# 跨網站重複使用程式碼 {#repoless}

如果您有許多相似的網站，大部分外觀和行為相同，但內容不同，請瞭解如何在一個重寫模式中跨多個網站共用程式碼。

## 適用於多個網站的一個程式碼基底 {#one-codebase}

依預設，AEM會與您的程式碼存放庫緊密繫結，以符合大部分的使用案例。 不過，您可能有多個網站的主要內容不同，但可能利用相同的程式碼基底。

AEM支援從相同程式碼基底執行多個網站，而不需建立多個GitHub存放庫並在專用GitHub存放庫之外執行每個網站，同時保持同步。

這個簡化的設定可免除程式碼復寫的需求，也稱為[「repoless」](https://www.aem.live/docs/repoless)，因為除了您的第一個網站以外，其他網站不需要自己的GitHub存放庫。

如果您的專案需要重複使用跨網站程式碼的靈活性，您可以啟動該功能。

無論您最終想要以粗略方式建立多少網站，都必須建立您的第一個網站，做為您的基礎網站。 本檔案說明如何建立您的第一個網站以供重複使用。

## 先決條件 {#prerequisites}

若要利用此功能，請確定您已完成下列操作。

* 依照檔案[使用Edge Delivery Services編寫WYSIWYG的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)，您的網站已完整設定。
* 您至少要執行AEM as a Cloud Service 2024.08。

您還需要要求Adobe為您設定下列專案。 透過您的Slack管道聯絡或提出支援問題，以請求Adobe進行這些變更：

* 要求啟用您環境的[aem.live設定服務](https://www.aem.live/docs/config-service-setup#prerequisites)，而且您已設定為管理員。
* 請求由Adobe為您的方案啟用重新導向功能。
* 要求Adobe為您建立組織。

## 啟動重新導向功能 {#activate}

若要針對您的專案啟用重新導向功能，有幾個步驟可執行。

1. [擷取存取權杖](#access-token)
1. [設定組態服務](#config-service)
1. [新增網站設定和技術帳戶](#access-control)
1. [更新AEM設定](#update-aem)
1. [驗證網站](#authenticate-site)

這些步驟以網站`https://wknd.site`為例。 適當地替換您自己的。

### 擷取存取Token {#access-token}

您首先需要存取Token才能使用設定服務，並針對重新導向使用案例進行設定。

1. 移至`https://admin.hlx.page/login`並使用`login_adobe`位址登入Adobe身分提供者。
1. 您將會轉寄到`https://admin.hlx.page/profile`。
1. 使用瀏覽器的開發人員工具，從`admin.hlx.page`頁面設定的JSON Web權杖Cookie複製`x-auth-token`的值。

取得存取Token後，就能在cURL要求的標頭中，以下列格式傳遞。

```text
--header 'x-auth-token: <your-token>'
```

### 新增網站設定的路徑對應並設定技術帳戶 {#access-control}

您需要建立網站設定，並將其新增至路徑對應。

1. 在網站的根目錄建立新頁面，並選擇&#x200B;[**組態**&#x200B;範本](/help/edge/wysiwyg-authoring/tabular-data.md#other)。
   * 您可以讓設定保持空白，只保留預先定義的`key`和`value`欄。 您只需要建立它。
1. 使用類似下列的cURL命令，在公用組態中建立與站台組態的對應。

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
1. 驗證是否已設定公用設定，以及是否可使用類似下列的cURL命令。

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

對應網站設定後，您可以定義技術帳戶以設定存取控制，使其具有發佈許可權。

1. 登入AEM作者執行個體並移至&#x200B;**工具** -> **雲端服務** -> **Edge Delivery Services設定**，然後選取為您的網站自動建立的設定，並點選或按一下工具列中的&#x200B;**屬性**。

1. 在&#x200B;**Edge Delivery Services設定**&#x200B;視窗中，選取&#x200B;**驗證**&#x200B;標籤，並複製&#x200B;**技術帳戶ID**&#x200B;的值。

   * 它看起來類似於`<tech-account-id>@techacct.adobe.com`
   * 對於單一AEM作者環境中的所有網站，技術帳戶都相同。

1. 使用類似以下的cURL命令，使用您複製的技術帳戶ID，為您的重新配置設定技術帳戶。

   * 調整`admin`區塊以定義應具備網站完整管理存取權的使用者。
      * 這是一系列電子郵件地址。
      * 可以使用萬用字元`*`。
      * 如需詳細資訊，請參閱檔案[為作者設定驗證](https://www.aem.live/docs/authentication-setup-authoring#default-roles)。

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

由於您現在使用設定服務，因此您可以從您的Git存放庫中移除`fstab.yaml`和`paths.json`。

>[!NOTE]
>
>使用設定服務並透過`config.json`公開路徑對應，會忽略`path.json`檔案。

設定AEM供重新使用後，您必須使用設定服務，並提供包含路徑對應的有效`config.json`。

### 更新AEM設定 {#update-aem}

現在您已準備好在AEM中對Edge Delivery Services進行必要的變更。

1. 登入AEM作者執行個體並移至&#x200B;**工具** -> **雲端服務** -> **Edge Delivery Services設定**，然後選取為您的網站自動建立的設定，並點選或按一下工具列中的&#x200B;**屬性**。
1. 在&#x200B;**Edge Delivery Services設定**&#x200B;視窗中，將專案型別變更為&#x200B;**aem.live （使用重新設定設定）**，然後點選或按一下&#x200B;**儲存並關閉**。
   ![Edge Delivery Services設定](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. 使用通用編輯器返回您的網站，並確定它仍正確呈現。
1. 修改部分內容並重新發佈。
1. 請造訪您在`https://main--<your-aem-project>--<your-github-org>.aem.page/`發佈的網站，並確認變更已正確反映。

您的專案現已設定為可重複使用。

## 後續步驟 {#next-steps}

現在，您的基本網站已設定為可重複使用，您可以建立其他利用相同程式碼庫的網站。 根據您的使用案例，請參閱以下檔案。

* [無存放庫多網站管理](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [無存放庫階段及生產環境](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [用於內容製作的網站驗證](/help/edge/wysiwyg-authoring/site-authentication.md)

## 疑難排解 {#troubleshooting}

在設定可重複使用案例後，最常見的問題是通用編輯器中的頁面不再轉譯，或您收到白色頁面或一般AEM as a Cloud Service錯誤訊息。 在這種情況下：

* 檢視轉譯頁面的來源。
   * 是否確實轉譯了某些內容(包含`scripts.js`、`aem.js`和編輯器相關JSON檔案的正確HTML標題)？
* 檢查作者執行個體的AEM `error.log`是否有例外。
   * 最常見的問題是頁面元件因404錯誤而失敗。
   * 無法載入`config.json or paths.json`
   * `component-definition.json`等 無法載入
