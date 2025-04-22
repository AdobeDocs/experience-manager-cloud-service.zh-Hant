---
title: 無存放庫多網站管理
description: 瞭解最佳實務建議，瞭解如何透過利用單一程式碼基底(由Edge Delivery Services提供)的本地化網站，以粗略方式設定專案。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: f6b861ed-18e4-4c81-92d2-49fadfe4669a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '1260'
ht-degree: 2%

---

# 無存放庫多網站管理 {#repoless-msm}

瞭解最佳實務建議，瞭解如何透過利用單一程式碼基底(由Edge Delivery Services提供)的本地化網站，以粗略方式設定專案。

## 概觀 {#overview}

[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md)及其Live Copy功能可讓您在多個位置使用相同的網站內容，同時允許變化。 您可以製作內容一次，並建立即時副本。 MSM會維護您的來源內容與其即時副本之間的即時關係，以便在您變更來源內容時，來源與即時副本可以同步。

您可以使用MSM為您的品牌建立跨地區設定和語言的完整內容結構，並集中撰寫內容。 接著，您就可以利用中央程式碼庫，透過Edge Delivery Services提供每個當地語系化的網站。

## 要求 {#requirements}

若要在重複使用案例中設定MSM，您必須先完成下列工作：

* 本檔案假設您已根據[使用Edge Delivery Services進行WYSIWYG編寫的開發人員快速入門手冊](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)為專案建立網站。
* 您必須已[啟用專案的重新導向功能](/help/edge/wysiwyg-authoring/repoless.md)。

## 使用案例 {#use-case}

本檔案假設您已為專案建立基本的本地化網站結構。 以瑞士和德國的wknd品牌為例，其使用下列結構。

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

`language-masters`中的內容是本地化網站的即時副本來源：德國(`de`)和瑞士(`ch`)。 本檔案的目標是建立Edge Delivery Services網站，讓所有網站都針對每個當地語系化網站使用相同的程式碼基底。

## 設定 {#configuration}

設定MSM重新導向使用案例有數個步驟。

1. [更新AEM網站設定](#update-aem-configurations)。
1. [為您的本地化頁面建立新的Edge Delivery Services網站](#create-edge-sites)。
1. [在AEM中更新本地化網站的雲端設定](#update-cloud-configurations)。

### 更新AEM網站設定 {#update-aem-configurations}

[組態](/help/implementing/developing/introduction/configurations.md)可視為工作區，可用來收集設定群組及其相關內容以進行組織作業。 當您在AEM中建立網站時，會自動為其建立設定。

您通常想要在網站之間共用特定內容，例如：

* 從Blueprint中的內容建立的範本
* 內容片段模型、持續性、查詢等。

您可以建立其他設定來促進此類共用。 對於wknd使用案例，我們需要下列路徑的設定。

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

也就是說，您將會有藍圖所使用之wknd品牌內容(`/content/wknd`)的根目錄組態，以及每個本地化網站（瑞士和德國）所使用的組態。

1. 登入您的AEM編寫執行個體。
1. 瀏覽至&#x200B;**設定瀏覽器**，方法是前往&#x200B;**工具** -> **一般** -> **設定瀏覽器**。
1. 選取為您的專案自動建立的組態（在此案例中為wknd），然後點選或按一下工具列中的[建立]。****
1. 在&#x200B;**建立組態**&#x200B;對話方塊中，為您的當地語系化網站（例如`Switzerland`）提供描述性&#x200B;**名稱**，而對於&#x200B;**標題**，則使用相同標題的當地語系化大小（在此例中為`ch`）。
1. 選取&#x200B;**雲端組態**&#x200B;功能以及專案可能需要的任何其他功能，例如&#x200B;**可編輯的範本**。
1. 點選或按一下「**建立**」。

為您需要的每個本地化網站建立設定。 以wknd為例，您需要建立`de`的設定以及`ch`設定。

建立設定後，您必須確保當地語系化的網站加以使用。

1. 登入您的AEM編寫執行個體。
1. 移至&#x200B;**導覽** -> **網站**，以瀏覽至&#x200B;**網站主控台**。
1. 選取當地語系化網站，例如`Switzerland`。
1. 在工具列中點選或按一下&#x200B;**屬性**。
1. 在頁面屬性視窗中，選取&#x200B;**進階**&#x200B;索引標籤，並在&#x200B;**組態**&#x200B;標題下，取消選取&#x200B;**繼承自/content/wknd**&#x200B;選項，其中`wknd`為網站根目錄。
1. 在&#x200B;**雲端設定**&#x200B;欄位中，使用路徑瀏覽器來選取您為本地化網站建立的設定，例如`/conf/wknd/ch`下的`Switzerland`。
1. 點選或按一下「**儲存並關閉**」。

將個別設定指派給其他本地化的網站。 若是wknd，您也需要將`/conf/wknd/de`設定指派給德國網站。

### 為您的當地語系化頁面建立新的Edge Delivery Services網站 {#create-edge-sites}

若要將更多網站連線至Edge Delivery Services以進行多區域、多語言網站設定，您必須為每個AEM MSM網站設定新的aem.live網站。 AEM MSM Sites與具有共用Git存放庫和程式碼庫的aem.live網站之間會維持1:1關係。

在此範例中，我們將為瑞士的wknd建立網站`wknd-ch`，其本地化內容位於AEM路徑`/content/wknd/ch`下。

1. 擷取您的驗證權杖和計畫的技術帳戶。
   * 請參閱檔案&#x200B;**跨網站重複使用程式碼**，以取得如何[取得您的存取權杖](/help/edge/wysiwyg-authoring/repoless.md#access-token)以及您程式的[技術帳戶](/help/edge/wysiwyg-authoring/repoless.md#access-control)的詳細資料。
1. 對設定服務進行下列呼叫，以建立新網站。 請考慮：
   * POST URL中的專案名稱必須是您正在建立的新網站名稱。 在此範例中，它是`wknd-ch`。
   * `code`設定應該與您用於初始專案建立的設定相同。
   * `content` > `source` > `url`必須調整為您正在建立的新網站的名稱。 在此範例中，它是`wknd-ch`。
   * 亦即，POST URL中的網站名稱必須與`content` > `source` > `url`相同。
   * 調整`admin`區塊以定義應具備網站完整管理存取權的使用者。
      * 這是一系列電子郵件地址。
      * 可以使用萬用字元`*`。
      * 如需詳細資訊，請參閱檔案[為作者設定驗證](https://www.aem.live/docs/authentication-setup-authoring#default-roles)。

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

1. 透過對設定服務進行以下呼叫，為您的新網站新增路徑對應。

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

1. 呼叫`https://main--wknd-ch--<your-github-org>.aem.page/config.json`並驗證傳回的JSON內容，以確認新網站的公用設定正常運作。

重複這些步驟以建立其他本地化的網站。 若是wknd，您也需要為德文網站建立`wknd-de`網站。

### 為您的本地化頁面更新AEM中的雲端設定 {#update-cloud-configurations}

您在AEM中的頁面必須設定為使用您在上一節中建立的新Edge Delivery網站，才能進行當地語系化顯示。 在此範例中，`/content/wknd/ch`下的內容需要知道如何使用您建立的`wknd-ch`網站。 `/content/wknd/de`下的內容同樣需要使用`wknd-de`網站。

1. 登入AEM作者執行個體並移至&#x200B;**工具** -> **雲端服務** -> **Edge Delivery Services設定**。
1. 選取為您的專案自動建立的設定，然後選取為當地語系化頁面建立的資料夾。 在此案例中，即為瑞士(`ch`)。
1. 在工具列中點選或按一下&#x200B;**建立** > **組態**。
1. 在&#x200B;**Edge Delivery Services設定**&#x200B;視窗中：
   * 在&#x200B;**組織**&#x200B;欄位中提供您的GitHub組織。
   * 將場地名稱變更為您在前一節中建立的場地名稱。 在這種情況下，應該是`wknd-ch`。
   * 將專案型別變更為&#x200B;**aem.live，使用重新設定設定**。
1. 點選或按一下「**儲存並關閉**」。

## 驗證您的設定 {#verify}

現在您已進行所有必要的設定變更，請確認一切都如預期般運作。

1. 登入您的AEM編寫執行個體。
1. 移至&#x200B;**導覽** -> **網站**，以瀏覽至&#x200B;**網站主控台**。
1. 選取當地語系化網站，例如`Switzerland`。
1. 點選或按一下工具列中的&#x200B;**編輯**。
1. 確保頁面在通用編輯器中正確轉譯，並使用與網站根目錄相同的程式碼。
1. 變更頁面並重新發佈。
1. 請造訪您新的Edge Delivery Services網站，在`https://main--wknd-ch--<your-github-org>.aem.page`取得該當地語系化頁面。

如果看到您所做的變更，表示您的MSM設定正常運作。
