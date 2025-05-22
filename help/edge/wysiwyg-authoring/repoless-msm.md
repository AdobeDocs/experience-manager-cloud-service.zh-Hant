---
title: 無存放庫多網站管理
description: 了解如何以無存放庫方式，透過利用單一程式碼基底並個別託管於 Edge Delivery Services 的本地化網站來設定專案的最佳實務建議。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: f6b861ed-18e4-4c81-92d2-49fadfe4669a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1260'
ht-degree: 100%

---

# 無存放庫多網站管理 {#repoless-msm}

了解如何以無存放庫方式，透過利用單一程式碼基底並個別託管於 Edge Delivery Services 的本地化網站來設定專案的最佳實務建議。

## 概觀 {#overview}

[多網站管理器 (MSM)](/help/sites-cloud/administering/msm/overview.md)及其 Live Copy 功能，讓您可以在多個位置使用相同的網站內容，同時允許變化版本。您可以製作一次內容然後建立 Live Copy。MSM 維護您的來源內容及其 Live Copy 之間的即時關係，以便當您變更來源內容時，可以同步此來源和 Live Copy。

您可以使用 MSM 為您的品牌建立涵蓋多個地區和多種語言的完整內容結構，並在中央製作內容。然後，您的本地化網站均可透過 Edge Delivery Services 利用中央程式碼基底進行傳遞。

## 要求 {#requirements}

若要在無存放庫的使用案例中設定 MSM，您必須先完成下列工作：

* 此文件假設您已根據[使用 Edge Delivery Services 進行所見即所得製作的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)，為專案建立網站。
* 您必須已經[為專案啟用無存放庫功能](/help/edge/wysiwyg-authoring/repoless.md)。

## 使用案例 {#use-case}

此文件假設您已為專案建立基本的本地化網站結構。其使用在瑞士或德國均有據點的 wnkd 品牌所採用的結構為例。

```text
/content/wknd
/content/wknd/language-masters
/content/wknd/language-masters/en
/content/wknd/language-masters/de
/content/wknd/language-masters/fr
/content/wknd/language-masters/it
/content/wknd/ch
/content/wknd/ch/de
/content/wknd/ch/fr
/content/wknd/ch/it
/content/wknd/ch/en
/content/wknd/de
/content/wknd/de/de
/content/wknd/de/en
```

`language-masters` 的內容為本地化網站的 Live Copy 來源：德國 (`de`) 和瑞士 (`ch`)。此文件的目標是建立每個本地化網站均使用相同的程式碼基底的 Edge Delivery Services 網站。

## 設定 {#configuration}

下列為設定 MSM 無存放庫使用案例的數個步驟。

1. [更新 AEM 網站設定](#update-aem-configurations)。
1. [為您的本地化頁面建立新的 Edge Delivery Services 網站](#create-edge-sites)。
1. [在 AEM 中更新本地化網站的雲端設定](#update-cloud-configurations)。

### 更新 AEM 網站設定 {#update-aem-configurations}

[設定](/help/implementing/developing/introduction/configurations.md)可被視為用於收集多組設定及其相關內容以供組織使用的工作區。當您在 AEM 中建立網站時，會自動為其建立設定。

您通常希望在網站之間共用某些內容，例如：

* 根據藍圖內容所建立的範本
* 內容片段模型、持續性、查詢等。

您可以建立其他設定以促進此類共用。針對 wknd 使用案例，我們需要下列路徑的設定。

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

即您將擁有藍圖所使用的 wknd 品牌內容的根目錄設定 (`/content/wknd`)，和每個本地化網站 (瑞士和德國) 所使用的設定。

1. 登入您的 AEM 製作執行個體。
1. 前往「**工具**」->「**一般**」->「**設定瀏覽器**」，以導覽至「**設定瀏覽器**」。
1. 選取自動為您的專案建立的設定 (在此案例中為「wknd」)，然後點選或按一下工具列的「**建立**」。
1. 在「**建立設定**」對話框中，為您的本地化網站提供描述性「**名稱**」(例如「`Switzerland`」)，而「**標題**」則使用與本地化網站相同的標題 (在此案例中為`ch`)。
1. 選取「**雲端設定**」功能以及您的專案可能需要的任何其他功能，例如「**可編輯範本**」。
1. 點選或按一下「**建立**」。

為您需要的每個本地化網站建立設定。如果是「wknd」，除了 `ch` 設定以外，您也需要建立 `de` 的設定。

建立設定後，您需要確保本地化網站使用這些設定。

1. 登入您的 AEM 製作執行個體。
1. 前往「**導覽**」->「**Sites**」，以導覽至「**Sites 主控台**」。
1. 選擇本地化網站，例如「`Switzerland`」。
1. 點選或按一下工具列中的「**屬性**」。
1. 在頁面屬性視窗中，選取「**進階**」索引標籤，然後在「**設定**」標題下，取消選取「**從 /content/wknd 繼承**」選項，其中 `wknd` 為此網站根目錄。
1. 在「**雲端設定**」欄位中，使用路徑瀏覽器來選取您為本地化網站所建立的設定，例如 `/conf/wknd/ch` 下的 `Switzerland`。
1. 點選或按一下「**儲存並關閉**」。

將個別設定指派至其他本地化網站。如果是 wknd，您還需要將 `/conf/wknd/de` 設定指派給德國網站。

### 為您的本地化頁面建立新的 Edge Delivery Services 網站 {#create-edge-sites}

若要將更多網站連線至 Edge Delivery Services 以打造多區域、多語言的網站環境，您必須為每個 AEM MSM 網站設定一個新的 aem.live 網站。AEM MSM 網站和 aem.live 網站之間存在 1:1 關係，而且共用 Git 存放庫和程式碼基底。

在此範例中，我們將為 wknd 的瑞士據點建立 `wknd-ch` 網站，而其本地化內容位於 AEM 路徑 `/content/wknd/ch` 下。

1. 獲取您的授權權杖和您方案的技術帳戶。
   * 請參閱&#x200B;**跨網站重複使用程式碼**&#x200B;的文件，詳細了解如何[取得存取權杖](/help/edge/wysiwyg-authoring/repoless.md#access-token)和您的方案之[技術帳戶](/help/edge/wysiwyg-authoring/repoless.md#access-control)。
1. 透過對設定服務進行下列呼叫來建立新網站。請考量下列事項：
   * POST URL 中的專案名稱必須是您正在建立的新網站名稱。在此範例中，其名稱為 `wknd-ch`。
   * `code` 設定應與您初次建立專案時所使用的設定相同。
   * `content` > `source` > `url` 必須根據您正在建立的新網站名稱進行調整。在此範例中，其名稱為 `wknd-ch`。
   * 即 POST URL 中的網站名稱與 `content` > `source` > `url` 必須相同。
   * 調整 `admin` 區塊，以定義應該具有網站完整管理存取權的使用者。
      * 這個區塊包含許多電子郵件。
      * 可以使用萬用字元「`*`」。
      * 請參閱[設定作者驗證](https://www.aem.live/docs/authentication-setup-authoring#default-roles)的文件，以了解更多資訊。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
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
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-ch/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
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
       }
   }'
   ```

1. 透過對設定服務進行下列呼叫，加入新網站的路徑對應。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/ch/:/"
           ],
           "includes": [
               "/content/wknd/ch/"
           ]
       }
   }'
   ```

1. 透過呼叫 `https://main--wknd-ch--<your-github-org>.aem.page/config.json` 並驗證傳回的 JSON 內容，確認新網站的公開設定可以正常運作。

重複這些步驟來建立其他本地化網站。如果是 wknd，您還需要為德國據點建立 `wknd-de` 網站。

### 在 AEM 中更新本地化頁面的雲端設定 {#update-cloud-configurations}

AEM 中的頁面必須設定為使用您在上一個區段中，為本地化據點建立的新 Edge Delivery Sites。在此範例中，`/content/wknd/ch` 下的內容需要知道使用您建立的 `wknd-ch` 網站。在 `/content/wknd/de` 下的類似內容需要使用 `wknd-de` 網站。

1. 登入 AEM 作者實例，並前往「**工具**」->「**雲端服務**」->「**Edge Delivery Services 設定**」。
1. 選取為您的專案自動建立的設定，然後選取為本地化頁面建立的資料夾。在此情況下，名稱將是「Switzerland」(`ch`)。
1. 點選或按一下工具列中的「**建立**」>「**設定**」。
1. 在 **Edge Delivery Services 設定**&#x200B;視窗中：
   * 在「**組織**」欄位中提供您的 GitHub 組織。
   * 將此網站名稱變更為您在上一個區段中建立的網站名稱。在此情況下，名稱將為「`wknd-ch`」。
   * 將專案類型變更為「**無存放庫設定的 aem.live**」。
1. 點選或按一下「**儲存並關閉**」。

## 驗證您的設定 {#verify}

現在您已完成所有必要的設定變更，請檢查一切是否按預期運作。

1. 登入您的 AEM 製作執行個體。
1. 前往「**導覽**」->「**Sites**」，以導覽至「**Sites 主控台**」。
1. 選擇本地化網站，例如「`Switzerland`」。
1. 點選或按一下工具列中的「**編輯**」。
1. 確保此頁面在通用編輯器中正確轉譯，並使用與網站根目錄相同的程式碼。
1. 對此頁面進行變更並重新發佈。
1. 請造訪新的 Edge Delivery Services 網站以瀏覽該本地化頁面，網址為 `https://main--wknd-ch--<your-github-org>.aem.page`。

如果您看到已完成的變更，表示您的 MSM 設定正常運作。
