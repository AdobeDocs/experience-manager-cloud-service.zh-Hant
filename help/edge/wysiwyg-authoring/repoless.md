---
title: 跨網站重複使用程式碼
description: 如果您有許多相似的網站，大部分外觀和行為相同，但內容不同，請瞭解如何在一個重寫模式中跨多個網站共用程式碼。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
source-git-commit: 7b37f3d387f0200531fe12cde649b978f98d5d49
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 0%

---

# 跨網站重複使用程式碼 {#repoless}

如果您有許多相似的網站，大部分外觀和行為相同，但內容不同，請瞭解如何在一個重寫模式中跨多個網站共用程式碼。

## 適用於多個網站的一個程式碼基底 {#one-codebase}

依預設，AEM會與您的程式碼存放庫緊密繫結，以符合大部分的使用案例。 不過，您可能有多個網站的主要內容不同，但可能利用相同的程式碼基底。

AEM支援從相同程式碼基底執行多個網站，而不需建立多個GitHub存放庫並在專用GitHub存放庫之外執行每個網站，同時保持同步。

這個簡化的設定可免除程式碼復寫的需求，也稱為[「repoless」，](https://www.aem.live/docs/repoless)，因為除了您的第一個網站以外，其他網站不需要自己的GitHub存放庫。

如果您的專案需要重複使用跨網站程式碼的靈活性，您可以啟動該功能。

無論您最終想要以粗略方式建立多少網站，都必須建立您的第一個網站，做為您的基礎網站。 本檔案說明如何建立您的第一個網站以供重複使用。

## 先決條件 {#prerequisites}

若要利用此功能，請確定您已完成下列操作。

* 依照檔案[使用Edge Delivery Services進行WYSIWYG編寫的開發人員快速入門手冊，您的網站已完整設定。](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* 您至少要執行AEM as a Cloud Service 2024.08。

您還需要要求Adobe為您設定兩個專案。 請透過您的Slack管道聯絡Adobe，或提出支援問題以提出這些請求。

* [aem.live設定服務](https://www.aem.live/docs/config-service-setup#prerequisites)在您的環境中使用中，而且您已設定為管理員。
* 必須依Adobe為您的方案啟用重新導向功能。

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

1. 移至`https://admin.hlx.page/login`並使用`login_adobe`位址登入Adobe識別提供者。
1. 您將會轉寄到`https://admin.hlx.page/profile`。
1. 使用瀏覽器的開發人員工具，從`admin.hlx.page`頁面設定的JSON Web權杖Cookie複製`x-auth-token`的值。

取得存取Token後，就能在cURL要求的標頭中，以下列格式傳遞。

```text
--header 'x-auth-token: <your-token>'
```

### 設定您的設定服務 {#config-service}

如[必要條件](#prerequisites)中所述，必須為您的環境啟用組態服務。 您可以使用此cURL命令檢查您的組態服務設定。

```text
curl  --location 'https://admin.hlx.page/config/<your-github-org>.json' \
--header 'x-auth-token: <your-token>'
```

如果設定服務已正確設定，則會傳回類似以下的JSON。

```json
{
  "title": "<your-github-org>",
  "description": "Your GitHub Org",
  "lastModified": "2024-11-14T12:14:04.230Z",
  "created": "2024-11-14T12:13:37.032Z",
  "version": 1,
  "users": [
    {
      "email": "justthisguyyouknow@adobe.com",
      "roles": [
        "admin"
      ],
      "id": "<your-id>"
    }
  ]
}
```

請透過您的專案Slack頻道聯絡Adobe，或如果您的設定服務未啟用，則提出支援問題。 取得Token並確認啟用設定服務後，您就可以繼續設定。

1. 檢查您的內容來源是否已正確設定。

   ```text
   curl --request GET \
   --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>.json \
   --header 'x-auth-token: <your-token>'
   ```

1. 新增路徑對應至公用設定。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```

建立公用組態之後，您可以透過類似`https://main--<your-aem-project>--<your-github-org>.aem.page/config.json`的URL存取它，以便驗證。

### 新增網站設定的路徑對應並設定技術帳戶 {#access-control}

您需要建立網站設定，並將其新增至路徑對應。

1. 在網站的根目錄建立新頁面，並選擇&#x200B;[**組態**&#x200B;範本。](/help/edge/wysiwyg-authoring/tabular-data.md#other)
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

1. 在您的瀏覽器中，擷取技術帳戶以回應下列連結。

   ```text
   https://author-p<programID>-e<envionmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/<your-aem-project>/main/.helix/config.json
   ```

1. 回應將與以下內容類似。

   ```json
   {
     "total": 1,
     "offset": 0,
     "limit": 1,
     "data": [
       {
         "key": "admin.role.publish",
         "value": "<tech-account-id>@techacct.adobe.com"
       }
     ],
     ":type": "sheet"
   }
   ```

1. 使用類似以下的cURL命令在您的設定中設定技術帳戶。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "admin": {
           "role": {
               "admin": [
                   "*@adobe.com"
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

1. 登入AEM作者執行個體並移至&#x200B;**工具** -> **Cloud Service** -> **Edge Delivery Services組態**，然後選取為您的網站自動建立的組態，並點選或按一下工具列中的&#x200B;**屬性**。
1. 在&#x200B;**Edge Delivery Services組態**&#x200B;視窗中，將專案型別變更為&#x200B;**aem.live （使用重新設定組態）**，然後點選或按一下&#x200B;**儲存並關閉**。
   ![Edge Delivery Services組態](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. 使用通用編輯器返回您的網站，並確定它仍正確呈現。
1. 修改部分內容並重新發佈。
1. 請造訪您在`https://main--<your-aem-project>--<your-github-org>.aem.page/`發佈的網站，並確認變更已正確反映。

您的專案現已設定為可重複使用。

## 後續步驟 {#next-steps}

現在，您的基本網站已設定為可重複使用，您可以建立其他利用相同程式碼庫的網站。 根據您的使用案例，請參閱以下檔案。

* [重新整理多網站管理](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [重新報告Stage和Prod環境](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)

## 疑難排解 {#troubleshooting}

在設定可重複使用案例後，最常見的問題是通用編輯器中的頁面不再轉譯，或您收到白色頁面或一般AEM as a Cloud Service錯誤訊息。 在這種情況下：

* 檢視轉譯頁面的來源。
   * 是否確實轉譯了某些內容(包含`scripts.js`、`aem.js`和編輯器相關JSON檔案的正確HTML標題)？
* 檢查作者執行個體的AEM `error.log`是否有例外。
   * 最常見的問題是頁面元件因404錯誤而失敗。
   * 無法載入`config.json or paths.json`
   * `component-definition.json`等 無法載入
