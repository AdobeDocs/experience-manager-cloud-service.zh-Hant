---
title: 無存放庫階段及生產環境
description: 瞭解如何以重寫方式運用單一程式碼基底，為您的中繼和生產環境設定個別網站。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 701bd9bc-30e8-4654-8248-a06d441d1504
source-git-commit: 42218450ab03201c69c59053f720954183f4b652
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 2%

---

# 無存放庫階段及生產環境 {#repoless-stage-prod}

瞭解如何以重寫方式運用單一程式碼基底，為您的中繼和生產環境設定個別網站。

## 概觀 {#overview}

您可能想要為生產環境設定一個站台，並將此站台與您的測試環境分開。 為個別測試和生產設定設定第二個網站，類似於多網站管理所需的[設定。](/help/edge/wysiwyg-authoring/repoless-msm.md)事實上，如果需要，它可以與MSM網站結構結合。

本檔案使用個別測試環境和生產環境的典型範例。 您可以為想要的任何環境建立個別的環境。

## 設定 {#configuration}

本檔案說明如何使用相同的程式碼基底，為您的專案設定不同的生產網站。 會進行下列假設。

* 測試網站已設定，您現在想要建立生產網站的設定。
* AEM編寫中的內容結構類似。
* 相同的路徑對應將用於測試和生產。

在此範例中，我們假設已針對名為wknd的專案建立生產網站，其GitHub存放庫也稱為wknd。

設定個別生產網站有兩個步驟。

1. [為您的生產環境建立新的Edge Delivery Services網站。](#create-edge-site)
1. [為您的生產網站更新AEM中的雲端設定。](#update-cloud-configuration)

### 為您的生產環境建立新的Edge Delivery Services網站 {#create-edge-site}

1. 擷取您的驗證權杖和計畫的技術帳戶。
   * 請參閱檔案&#x200B;**跨網站重複使用程式碼**，以取得如何[取得您的存取權杖](/help/edge/wysiwyg-authoring/repoless.md#access-token)以及您程式的[技術帳戶](/help/edge/wysiwyg-authoring/repoless.md#access-control)的詳細資料。
1. 對設定服務進行下列呼叫，以建立新網站。 請考慮：
   * POSTURL中的專案名稱必須是您正在建立的新網站名稱。 在此範例中，它是`wknd-prod`。
   * `code`設定應該與您用於初始專案建立的設定相同。
   * `content` > `source` > `url`必須調整為您正在建立的新網站的名稱。 在此範例中，它是`wknd-prod`。
   * 也就是說，POSTURL中的網站名稱必須與`content` > `source` > `url`相同。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "code": {
           "owner": "<your-github-org>",
           "repo": "wknd",
           "source": {
               "type": "github",
               "url": "https://github.com/<your-github-org>/wknd"
           }
       },
       "content": {
           "source": {
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-prod/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
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
       }
   }'
   ```

1. 透過對設定服務進行以下呼叫，為您的新網站新增路徑對應。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/:/"
           ],
           "includes": [
               "/content/wknd/"
           ]
       }
   }'
   ```

呼叫`https://main--wknd-prod--<your-github-org>.aem.page/config.json`並驗證傳回的JSON內容，以確認新網站的公用設定正常運作。

### 為您的生產網站更新AEM中的雲端設定 {#update-cloud-configuration}

您的生產AEM必須設定為使用您在上一節中建立的新Edge Delivery網站作為專用生產網站。 在此範例中，您的生產環境中`/content/wknd`下的內容需要知道如何使用您建立的`wknd-prod`網站。

1. 登入AEM生產執行個體並移至&#x200B;**工具** -> **Cloud Service** -> **Edge Delivery Services設定**。
1. 選取為您的專案自動建立的設定。
1. 在工具列中點選或按一下&#x200B;**屬性**。
1. 在&#x200B;**Edge Delivery Services組態**&#x200B;視窗中：
   * 在&#x200B;**組織**&#x200B;欄位中提供您的GitHub組織。
   * 將場地名稱變更為您在前一節中建立的場地名稱。 在這種情況下，應該是`wknd-prod`。
   * 將專案型別變更為&#x200B;**aem.live，使用重新設定設定**。
1. 點選或按一下「**儲存並關閉**」。

## 驗證您的設定 {#verify}

現在您已進行所有必要的設定變更，請確認一切都如預期般運作。

1. 登入您的AEM生產製作執行個體。
1. 移至&#x200B;**導覽** -> **網站**，以瀏覽至&#x200B;**網站主控台**。
1. 在您的網站中選取頁面。
1. 點選或按一下工具列中的&#x200B;**編輯**。
1. 確保頁面在通用編輯器中正確轉譯，並使用與網站根目錄相同的程式碼。
1. 變更頁面並重新發佈。
1. 請於`https://main--wknd-prod--<your-github-org>.aem.page`造訪您對該頁面的新Edge Delivery Services網站。

如果看到您所做的變更，表示您的個別生產網站設定正常運作。
