---
title: 永續GraphQL查詢
description: 瞭解如何在Adobe Experience Manager as a Cloud Service保留GraphQL查詢以優化效能。 永續查詢可由客戶端應用使用HTTPGET方法來請求，響應可在分發程式和CDN層快取，最終改善客戶端應用程式的效能。
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 2ee21b507b5dcc9471063b890976a504539b7e10
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---

# 永續GraphQL查詢 {#persisted-queries-caching}

永續查詢是在Adobe Experience Manager()as a Cloud Service伺服器上建立和儲存的AEMGraphQL查詢。 客戶端應用程式可以通過GET請求來請求它們。 在調度器和CDN層可快取GET請求的響應，最終改善請求客戶端應用的效能。 這與標準GraphQL查詢不同，這些查詢使用無法輕鬆快取響應的POST請求執行。

的 [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) 在中可AEM供您開發、test和保留GraphQL查詢 [轉移到生產環境](#transfer-persisted-query-production)。 對於需要自定義的案例(例如， [自定義快取](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries))可以使用API;請參閱中提供的curl示例 [如何永續GraphQL查詢](#how-to-persist-query)。

## 永續查詢和終結點 {#persisted-queries-and-endpoints}

永續查詢必須始終使用與 [適當的站點配置](graphql-endpoint.md);這樣它們就可以使用其中一種或兩種：

* 全局配置和終結點查詢有權訪問所有內容片段模型。
* 特定站點配置和終結點為特定站點配置建立永續查詢需要特定於特定站點配置的相應終結點（以提供對相關內容片段模型的訪問）。
例如，要為WKND站點配置專門建立永續查詢，必須提前建立相應的WKND特定站點配置和WKND特定終結點。

>[!NOTE]
>
>請參閱 [在配置瀏覽器中啟用內容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) 的子菜單。
>
>的 **GraphQL持久查詢** 需要啟用相應的站點配置。

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

## 如何永續GraphQL查詢 {#how-to-persist-query}

建議先保留對作者環境的AEM查詢，然後 [傳送查詢](#transfer-persisted-query-production) 生產發佈AEM環境，供應用程式使用。

存在多種保留查詢的方法，包括：

* GraphiQL IDE — 請參見 [保存永續查詢](/help/headless/graphql-api/graphiql-ide.md##saving-persisted-queries)
* curl — 請參見以下示例
* 其他工具，包括 [Postman](https://www.postman.com/)

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

## 將永續查詢傳輸到生產環境  {#transfer-persisted-query-production}

最終，您的永續查詢需要位於生產發佈環境(AEMas a Cloud Service)中，客戶端應用程式可以在該環境中請求它。 要在生產發佈環境上使用永續查詢，需要複製相關的永續樹：

* 初始到生產作者，以通過查詢驗證新創作的內容，
* 最後，為生活消費發佈產品

傳輸永續查詢有幾種方法：

1. 使用包：
   1. 建立新包定義。
   1. 包括配置(例如， `/conf/wknd/settings/graphql/persistentQueries`)。
   1. 生成包。
   1. 傳輸包（下載/上載或複製）。
   1. 安裝軟體包。

1. 使用POST進行複製：

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->

查詢配置在生產中的發佈環境上後，同樣的驗證原則將適用，只使用發佈終結點。

>[!NOTE]
>
>對於匿名訪問，系統假定ACL允許「每個人」訪問查詢配置。
>
>如果情況不是這樣，它將無法執行。

## 對查詢URL進行編碼，供應用使用 {#encoding-query-url}

為供應用程式使用，需要對URL中的任何分號(&quot;;&quot;)進行編碼。

例如，與執行永續查詢的請求一樣：

```xml
curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
```

要在客戶端應用中使用永續查詢，AEM應使用無頭客戶端SDK [用AEM於JavaScript的無頭客戶端](https://github.com/adobe/aem-headless-client-js)。