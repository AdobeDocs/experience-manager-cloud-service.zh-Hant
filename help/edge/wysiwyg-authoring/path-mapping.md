---
title: Edge Delivery Services 的路徑對應
description: 了解如何將 AEM 製作執行個體上使用的頁面路徑對應到網站上使用的公開頁面路徑，並管控要將哪些內容發佈到 Edge Delivery Services。
feature: Edge Delivery Services
role: User
exl-id: 3d68135d-e84c-4bf4-93d1-38a0be70ce4a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '567'
ht-degree: 100%

---

# Edge Delivery Services 的路徑對應 {#path-mapping}

了解如何將 AEM 製作執行個體上使用的頁面路徑對應到網站上使用的公開頁面路徑，並控制要將哪些內容發佈到 Edge Delivery Services。

## 概觀 {#overview}

為了能夠使用 AEM 製作所見即所得內容，並將其發佈到 Edge Delivery Services，您必須設定專案的路徑對應。這樣的對應有兩個目的。

* 對應並建立您 AEM 製作執行個體上使用的頁面路徑與您網站上使用的公開頁面路徑之間的關係。
* 控制要將哪些內容 (頁面、工作表、資產等) 發佈到 Edge Delivery Services。

必須根據專案的內容和 URL 結構，為每個專案獨立設定路徑對應。AEM 在內容發佈期間以及在[通用編輯器](/help/sites-cloud/authoring/universal-editor/navigation.md)中編輯內容時會加以使用。

## 設定格式 {#configuration-format}

路徑對應設定的格式包含兩個部分 (`mappings` 和 `includes`)，類似於以下範例。

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

### 對應 {#mappings}

`mappings` 設定的內容具有內部路徑 (在 AEM 製作執行個體上) 和外部 URL 路徑 (在公開網站上) 的陣列。

格式為 `<internal paths>:<external path>`。通常至少會包含兩個項目。

1. 範例中的第一個項目是網站頁面的路徑對應。
1. 第二個項目會控制 `.helix/config.json` 對 AEM 製作存放庫中相對應試算表頁面的對應。

在此範例中，所有儲存在 `/content/aem-boilerplate/...` 下的頁面，都能夠在 `https://main--my-site--org.aem.live/....` 正下方的 Edge Delivery Services 網站上公開存取。

>[!TIP]
>
>所有以試算表形式管理的表格資料 (例如，中繼資料、重新導向以及分類法)，通常會在 Edge Delivery Services 上發佈為 `.json` API URL。為此，必須在對應設定中將其單獨列出。
>
>如需更多資訊，請參閱文件：[使用試算表管理表格資料](/help/edge/wysiwyg-authoring/tabular-data.md)。

### 包含 {#includes}

`includes` 設定會控制有哪些內容路徑會實際複製到 Edge Delivery Services。它也能保存任何路徑陣列，且通常包含網站的頂層根頁面。

Edge Delivery Services 頁面上使用的資產通常會與網頁一起發佈。它們會從 AEM 製作執行個體自動匯出到 Edge Delivery Services。

>[!TIP]
>
>如果您的使用案例是希望將資產直接發佈到 Edge Delivery Services (例如，您希望可以在頁面環境之外，直接由影像或 PDF 的 URL 進行存取)，則同時也必須將 DAM 路徑新增至設定中的 `includes` 區段。
>
>例如，若要使一個資產根資料夾 (例如包含一組 PDF 的 `/content/dam/my-site/documents`) 能透過 `/assets/...` 公開存取，則必須在設定中的 `includes` 部分新增一個項目。

## 如何設定 {#how-to-configure}

依據您專案的設定，您的路徑對應可以透過兩種方式之一進行設定。

1. 如果專案設定為 `aem.live` 並使用[設定服務](https://www.aem.live/docs/config-service-setup)進行集中式設定，則每個網站的路徑對應都會透過此設定服務來設定。

   * 以下是設定路徑對應的 cURL 請求範例。

   ```text
   curl --request POST \
     --url https://admin.aem.page/config/{org}/sites/{site}/public.json \
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

1. 如果專案未使用設定服務，則會透過您專案 GitHub 存放庫的 `paths.json` 檔案進行路徑對應設定。

   * 如需範例，請參閱 [`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json)。

在這兩種情況下，當您設定路徑對應後，都可以透過可公開存取的設定 URL `https://<branch>--<site>--<org>.aem.page/config.json` 來檢查設定。
