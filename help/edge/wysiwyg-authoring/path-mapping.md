---
title: Edge Delivery Services的路徑對應
description: 瞭解如何將AEM編寫執行個體上使用的頁面路徑對應到網站上使用的公開頁面路徑，並控制要將哪些內容發佈到Edge Delivery Services。
feature: Edge Delivery Services
role: User
source-git-commit: 51a2b453ccce39cb42c927a088bc088083545542
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Edge Delivery Services的路徑對應 {#path-mapping}

瞭解如何將AEM編寫執行個體上使用的頁面路徑對應到網站上使用的公開頁面路徑，並控制要將哪些內容發佈到Edge Delivery Services。

## 概觀 {#overview}

若要能夠使用AEM編寫WYSIWYG內容並將其發佈到Edge Delivery Services，您必須設定專案的路徑對應。 此對應有兩個用途。

* 它會對應並建立您AEM編寫執行個體上使用的頁面路徑，與您的網站上使用的公開頁面路徑之間的關係。
* 這可控制哪些內容（頁面、工作表、資產等） 發佈至Edge Delivery Services。

每個專案都必須個別地並根據專案的內容和URL結構設定路徑對應。 AEM在內容發佈期間以及在[通用編輯器](/help/sites-cloud/authoring/universal-editor/navigation.md)中編輯內容時，會使用它。

## 設定格式 {#configuration-format}

路徑對應設定的格式包含兩個區段（`mappings`和`includes`），類似於以下範例。

```json
{
  "mappings": [
    "/content/aem-boilerplate/:/",
    "/content/aem-boilerplate/configuration:/.helix/config.json"
  ],
  "includes:" [
    "/content/aem-boilerplate/"
  ]
}
```

### 對映 {#mappings}

`mappings`設定包含內部路徑(在AEM編寫執行個體上)和外部URL路徑（在公用網站上）的陣列。

格式為`<internal paths>:<external path>`。 通常至少包含兩個專案。

1. 範例中的第一個專案是網站頁面的路徑對應。
1. 第二個專案控制`.helix/config.json`與AEM編寫存放庫中對應試算表頁面的對應。

在此範例中，所有儲存在`/content/aem-boilerplate/...`下的頁面將可以在Edge Delivery Services網站上直接在`https://main--my-site--org.aem.live/....`下公開存取。

>[!TIP]
>
>所有以試算表管理的表格式資料（例如中繼資料、重新導向和分類法）通常會以Edge Delivery Services上的`.json` API URL發佈。 要執行此操作，它們必須個別列在對應設定中。
>
>如需詳細資訊，請參閱檔案[使用試算表來管理表格式資料](/help/edge/wysiwyg-authoring/tabular-data.md)。

### 包含 {#includes}

`includes`設定會控制哪些內容路徑實際復寫到Edge Delivery Services。 它也可以保留任何路徑陣列，且通常包含網站頂層根頁面。

Edge Delivery Services頁面上使用的Assets通常會與網頁一起發佈。 它們會自動從AEM編寫執行個體匯出至Edge Delivery Services。

>[!TIP]
>
>如果您有使用案例，希望將資產直接發佈至Edge Delivery Services(例如，您希望影像或PDF在頁面內容之外的URL可直接存取這些影像或資產)，您也必須將DAM路徑新增至設定的`includes`區段。
>
>例如，如果應透過`/assets/...`公開存取包含一組PDF的資產根資料夾（例如`/content/dam/my-site/documents`），則必須將專案新增至設定的`includes`區段。

## 如何設定 {#how-to-configure}

您可以根據專案的設定，以兩種方式之一設定路徑對應。

1. 如果專案是針對`aem.live`設定，且使用[設定服務](https://www.aem.live/docs/config-service-setup)進行集中設定，則每個網站的路徑對應會透過此設定服務進行設定。

   * 以下是設定路徑對應的範例cURL要求。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/{org}/sites/{site}/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: ......' \
     --data '{
       "paths": {
       "mappings": [
         "/content/aem-boilerplate/:/",
         "/content/aem-boilerplate/configuration:/.helix/config.json"
       ],
       "includes": [
         "/content/aem-boilerplate/"
       ]
   }
   }'
   ```

1. 如果專案未使用設定服務，路徑對應會透過專案GitHub存放庫中的paths.json檔案進行設定。

   * 如需範例，請參閱[`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](/https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json)。

在這兩種情況下，設定路徑對應後，您就可以透過可公開存取的設定URL `https://<branch>--<site>--<org>.aem.page/config.json`檢查設定。
