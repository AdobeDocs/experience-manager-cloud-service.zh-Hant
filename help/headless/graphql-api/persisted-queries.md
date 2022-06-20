---
title: 永續GraphQL查詢
description: 瞭解如何在Adobe Experience Manager as a Cloud Service保留GraphQL查詢以優化效能。 永續查詢可由客戶端應用使用HTTPGET方法來請求，響應可在分發程式和CDN層快取，最終改善客戶端應用程式的效能。
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 8a9cdc451a5da09cef331ec0eaadd5d3a68b1985
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 0%

---

# 永續GraphQL查詢 {#persisted-queries-caching}

永續查詢是在Adobe Experience Manager()as a Cloud Service伺服器上建立和儲存的AEMGraphQL查詢。 客戶端應用程式可以通過GET請求來請求它們。 在調度器和CDN層可快取GET請求的響應，最終改善請求客戶端應用的效能。 這與標準GraphQL查詢不同，這些查詢使用無法輕鬆快取響應的POST請求執行。

>[!NOTE]
>
>建議使用保留查詢。 請參閱 [GraphQL查詢最佳做法(Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) 以及相關的Dispatcher配置。

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

* GraphiQL IDE — 請參見 [保存永續查詢](/help/headless/graphql-api/graphiql-ide.md##saving-persisted-queries) （首選方法）
* curl — 請參見以下示例
* 其他工具，包括 [Postman](https://www.postman.com/)

GraphiQL IDE是 **首選** 用於保留查詢的方法。 使用 **捲曲** 命令行工具：

1. 通過將查詢PUTing到新終結點URL來準備查詢 `/graphql/persist.json/<config>/<persisted-label>`。

   例如，建立永續查詢：

   ```shell
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

   ```json
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

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通過POSTing將永續查詢更新到已存在的查詢路徑。

   例如，使用永續查詢：

   ```shell
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

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用快取控制項建立包裝的純查詢。

   例如：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用參數建立永續查詢：

   例如：

   ```shell
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


## 如何執行永續查詢 {#execute-persisted-query}

要執行永續查詢，客戶端應用程式使用以下語法發出GET請求：

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

位置 `PERSISTENT_PATH` 是保存永久查詢的縮短路徑。

1. 例如 `wknd` 是配置名和 `plain-article-query` 是永久查詢的名稱。 要執行查詢，請執行以下操作：

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. 使用參數執行查詢。

   >[!NOTE]
   >
   > 查詢變數和值必須正確 [編碼](#encoding-query-url) 執行永久查詢時。

   例如：

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   請參閱使用 [查詢變數](#query-variables) 的子菜單。

## 使用查詢變數 {#query-variables}

查詢變數可與永續查詢一起使用。 查詢變數將附加到以分號(`;`)。 多個變數用分號分隔。

該模式如下所示：

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

例如，以下查詢包含變數 `activity` 要根據活動值篩選清單：

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

此查詢可以保留在路徑下 `wknd/adventures-by-activity`。 調用永續查詢時 `activity=Camping` 請求將如下所示：

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

請注意 `%3B` 是UTF-8編碼 `;` 和 `%3D` 是 `=`。 查詢變數和任何特殊字元必須是 [已編碼](#encoding-query-url) 執行永續查詢。

## 對查詢URL進行編碼，供應用使用 {#encoding-query-url}

為供應用程式使用，構造查詢變數時使用的任何特殊字元(即分號(`;`)，等號(`=`)，斜線 `/`)必須轉換為使用相應的UTF-8編碼。

例如：

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL可分為以下部分：

| URL部分 | 說明 |
|----------| -------------|
| `/graphql/execute.json` | 永久查詢終結點 |
| `/wknd/adventure-by-path` | 持久查詢路徑 |
| `%3B` | 編碼 `;` |
| `adventurePath` | 查詢變數 |
| `%3D` | 編碼 `=` |
| `%2F` | 編碼 `/` |
| `%2Fcontent%2Fdam...` | 內容片段的編碼路徑 |

在純文字檔案中，請求URI如下所示：

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

要在客戶端應用中使用永續查詢，AEM應使用無頭客戶端SDK [JavaScript](https://github.com/adobe/aem-headless-client-js)。 [爪哇](https://github.com/adobe/aem-headless-client-java)或 [節點JS](https://github.com/adobe/aem-headless-client-nodejs)。 無頭客戶端SDK將自動對請求中的任何查詢變數進行適當編碼。

## 將永續查詢傳輸到生產環境  {#transfer-persisted-query-production}

應始終在AEM Author服務上建立永續查詢，然後將其發佈（複製）到AEM Publish服務。 通常，永續查詢是在較低環境（如本地或開發環境）上建立和測試的。 然後，有必要將永續查詢提升到更高級別的環境，最終使這些查詢在生產AEM發佈環境中可用，供客戶端應用程式使用。

### 包持久性查詢

可將持久查詢內置到 [包AEM](/help/implementing/developing/tools/package-manager.md)。 然AEM後可以下載軟體包並將其安裝到不同環境中。 還AEM可以將包從AEM Author環境複製到AEM Publish環境。

要建立包：

1. 導航到 **工具** > **部署** > **包**。
1. 通過點擊建立新包 **建立包**。 這將開啟一個對話框來定義包。
1. 在「包定義」對話框中，在 **常規** 輸入 **名稱** 例如「wknd-persistent-querys」。
1. 輸入版本號（如「1.0」）。
1. 下 **篩選器** 添加新 **篩選**。 使用路徑查找器選擇 `persistentQueries` 資料夾。 例如 `wknd` 配置完整路徑將 `/conf/wknd/settings/graphql/persistentQueries`。
1. 點擊 **保存** 保存新包定義並關閉對話框。
1. 點擊 **生成** 按鈕。

生成包後，您可以：
* **下載** 包並重新上傳到其他環境。
* **複製** 點擊包裝 **更多** > **複製**。 這將將包複製到連接的AEM發佈環境。

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
