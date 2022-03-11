---
title: 永續GraphQL查詢
description: 瞭解如何在Adobe Experience Manager保留GraphQL查詢以優化效能。 永續查詢可由客戶端應用使用HTTPGET方法來請求，響應可在分發程式和CDN層快取，最終改善客戶端應用程式的效能。
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---

# 永續GraphQL查詢 {#persisted-queries-caching}

永續查詢是在伺服器上建立和儲存的GraphQLAEM查詢。 標準GraphQL查詢是使用POST請求執行的，無法輕鬆快取響應。 可以通過客戶端應用程式的GET請求來請求保留的查詢。 在調度器和CDN層可快取GET請求的響應，最終改善請求客戶端應用的效能。

永續查詢必須始終使用與 [適當的站點配置](graphql-endpoint.md);這樣它們就可以使用其中一種或兩種：

* 全局配置和終結點查詢有權訪問所有內容片段模型。
* 特定站點配置和終結點為特定站點配置建立永續查詢需要特定於特定站點配置的相應終結點（以提供對相關內容片段模型的訪問）。
例如，要為WKND站點配置專門建立永續查詢，必須提前建立相應的WKND特定站點配置和WKND特定終結點。

>[!NOTE]
>
>請參閱 [在配置瀏覽器中啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) 的子菜單。
>
>的 **GraphQL持久性查詢** 需要啟用相應的站點配置。

例如，如果有一個特定查詢 `my-query`，它使用模型 `my-model` 從站點配置 `my-conf`:

* 您可以使用 `my-conf` 特定端點，然後查詢將保存如下：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 可以使用 `global` 終結點，但查詢將保存如下：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>這是兩個不同的查詢 — 保存在不同的路徑下。
>
>他們只是碰巧使用了同一種模式 — 但是通過不同的端點。

## 如何永續GraphQL查詢

建議先保留對作者環境的AEM查詢，然後 [發佈查詢](#publish-persisted-query) 到發AEM布環境。 工具，如 [郵遞員](https://www.postman.com/) 或命令行工具 [捲曲](https://curl.se/) 可使用。

以下是使用 **捲曲** 命令行工具：

1. 通過將查詢PUTing到新終結點URL來準備查詢 `/graphql/persist.json/<config>/<persisted-label>`。

   例如，建立永續查詢：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. 此時，檢查響應。

   例如，檢查是否成功：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然後，可以通過獲取URL來請求保留的查詢 `/graphql/execute.json/<shortPath>`。

   例如，使用永續查詢：

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通過POSTing將永續查詢更新到已存在的查詢路徑。

   例如，使用永續查詢：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. 建立換行的純查詢。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用快取控制項建立包裝的純查詢。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用參數建立永續查詢：

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. 使用參數執行查詢。

   例如：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

## 發佈永續查詢 {#publish-persisted-query}

永續查詢可以發佈到AEM發佈環境，在該環境中客戶端應用程式可以請求它們。 要在發佈時使用永續查詢，需要複製相關的持久樹。

發佈永續查詢有幾種方法：

* **使用POST進行複製**:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

* **使用包**:
   1. 建立新包定義。
   1. 包括配置(例如， `/conf/wknd/settings/graphql/persistentQueries`)。
   1. 生成包。
   1. 複製包。

* **使用複製/分發工具**:
   1. 轉到分發工具。
   1. 為配置選擇樹激活(例如， `/conf/wknd/settings/graphql/persistentQueries`)。

* **使用工作流（通過工作流啟動程式配置）**:
   1. 定義工作流啟動程式規則，用於執行將在不同事件上複製配置的工作流模型（例如，建立、修改等）。

在發佈上查詢配置後，同樣的驗證原則將適用，只使用發佈終結點。

>[!NOTE]
>
>對於匿名訪問，系統假定ACL允許「每個人」訪問查詢配置。
>
>如果情況不是這樣，它將無法執行。

>[!NOTE]
>
>需要對URL中的任何分號(&quot;;&quot;)進行編碼。
>
>例如，與執行永續查詢的請求一樣：
>
>
```xml
>curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
>```
