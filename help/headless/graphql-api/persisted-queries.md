---
title: 持續GraphQL查詢
description: 了解如何在Adobe Experience Manager as a Cloud Service中保留GraphQL查詢，以最佳化效能。 用戶端應用程式可使用HTTPGET方法來請求持續查詢，且可在Dispatcher和CDN層快取回應，最終改善用戶端應用程式的效能。
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%

---

# 持續GraphQL查詢 {#persisted-queries-caching}

持續查詢是在Adobe Experience Manager(AEM)as a Cloud Service伺服器上建立並儲存的GraphQL查詢。 客戶應用程式可透過GET要求來要求這些ID。 可在Dispatcher和CDN層快取GET要求的回應，最終改善請求用戶端應用程式的效能。 這與標準的GraphQL查詢不同，這些查詢是使用POST請求執行，因為無法輕鬆快取回應。

>[!NOTE]
>
>建議使用持續查詢。 請參閱 [GraphQL查詢最佳作法(Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) 以取得詳細資訊，以及相關的Dispatcher設定。

此 [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) 在AEM中可供您開發、測試及保留GraphQL查詢，於之前完成 [轉移至生產環境](#transfer-persisted-query-production). 需要自訂的情況(例如 [自訂快取](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries))您可以使用API;請參閱 [如何保留GraphQL查詢](#how-to-persist-query).

## 持續查詢和端點 {#persisted-queries-and-endpoints}

持續查詢必須一律使用與 [適當的站點配置](graphql-endpoint.md);以便兩者皆可使用：

* 全域設定和端點查詢可存取所有內容片段模型。
* 特定網站配置和端點為特定網站配置建立持續查詢時，需要對應的網站配置特定端點（以提供對相關內容片段模型的存取）。
例如，要為WKND Sites配置特別建立持續查詢，必須事前建立相應的WKND特定Sites配置和WKND特定端點。

>[!NOTE]
>
>請參閱 [在設定瀏覽器中啟用內容片段功能](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) 以取得更多詳細資訊。
>
>此 **GraphQL持續查詢** 需要啟用，才能進行適當的Sites設定。

例如，如果有一個名為的特定查詢 `my-query`，此模型使用 `my-model` 從Sites配置 `my-conf`:

* 您可以使用 `my-conf` 特定端點，則查詢將儲存為下列內容：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用 `global` 端點，但查詢將儲存如下：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>這是兩個不同的查詢 — 儲存在不同的路徑下。
>
>他們只是碰巧使用相同的模型，但透過不同的端點。

## 如何保留GraphQL查詢 {#how-to-persist-query}

建議您先在AEM製作環境上保留查詢，然後再保留查詢 [傳輸查詢](#transfer-persisted-query-production) 至您的生產AEM發佈環境，供應用程式使用。

持續查詢有多種方法，包括：

* GraphiQL IDE — 請參見 [保存持續查詢](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) （偏好方法）
* curl — 請參閱下列範例
* 其他工具，包括 [Postman](https://www.postman.com/)

GraphiQL IDE是 **preder** 持續查詢的方法。 若要使用 **捲曲** 命令行工具：

1. 將查詢PUT輸入新端點URL以準備該查詢 `/graphql/persist.json/<config>/<persisted-label>`.

   例如，建立持續查詢：

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

1. 此時，請檢查回應。

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

1. 然後，您可以透過GET URL來請求持續的查詢 `/graphql/execute.json/<shortPath>`.

   例如，使用持續查詢：

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 將POSTing更新為已存在的查詢路徑，以保存查詢。

   例如，使用持續查詢：

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

1. 建立包裝的純查詢。

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

1. 使用參數建立持續查詢：

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


## 如何執行持續查詢 {#execute-persisted-query}

若要執行持續查詢，用戶端應用程式會使用下列語法提出GET要求：

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

其中 `PERSISTENT_PATH` 是儲存「持續存在」查詢的簡短路徑。

1. 例如 `wknd` 是設定名稱， `plain-article-query` 是持續查詢的名稱。 要執行查詢，請執行以下操作：

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. 使用參數執行查詢。

   >[!NOTE]
   >
   > 查詢變數和值必須正確 [編碼](#encoding-query-url) 執行持續查詢時。

   例如：

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   請參閱使用 [查詢變數](#query-variables) 以取得更多詳細資訊。

## 使用查詢變數 {#query-variables}

查詢變數可與持續查詢搭配使用。 查詢變數會附加至以分號(`;`)，使用變數名稱和值。 多個變數會以分號分隔。

模式如下所示：

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

例如，下列查詢包含變數 `activity` 若要根據活動值篩選清單：

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

此查詢可保存在路徑下 `wknd/adventures-by-activity`. 若要呼叫保存的查詢，其中 `activity=Camping` 請求如下所示：

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

請注意 `%3B` 是 `;` 和 `%3D` 是的編碼 `=`. 查詢變數和任何特殊字元必須 [編碼正確](#encoding-query-url) 以執行「持續存在」查詢。

## 快取持續查詢 {#caching-persisted-queries}

建議使用持續查詢，因為可在Dispatcher和CDN層快取查詢，最終改善提出請求的用戶端應用程式的效能。

依預設，AEM會根據預設的存留時間(TTL)，使內容傳送網路(CDN)快取失效。

此值設為：

* 7200秒是Dispatcher和CDN的預設TTL;又稱為 *共用快取*
   * 預設值：s-maxage=7200
* 60是用戶端（例如瀏覽器）的預設TTL
   * 預設值：maxage=60

如果您想要變更GraphLQ查詢的TTL，則查詢必須是：

* 在管理後持續存在 [HTTP快取標頭 — 從GraphQL IDE](#http-cache-headers)
* 持續使用 [API方法](#cache-api).

### 在GraphQL中管理HTTP快取標題  {#http-cache-headers-graphql}

GraphiQL IDE — 請參見 [保存持續查詢](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### 從API管理快取 {#cache-api}

這包括在命令列介面中使用CURL將查詢發佈至AEM。

例如：

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "https://publish-p123-e456.adobeaemcloud.com/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

此 `cache-control` 可在建立時(PUT)或稍後設定(例如，透過例項的POST請求)。 建立持續查詢時，快取控制為選用，因為AEM可提供預設值。 請參閱 [如何保留GraphQL查詢](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query)，以示使用curl保存查詢的範例。

## 對查詢URL進行編碼，以供應用程式使用 {#encoding-query-url}

為供應用程式使用，建構查詢變數時使用的任何特殊字元(即分號(`;`)，等號(`=`)，斜線 `/`)才能使用對應的UTF-8編碼。

例如：

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL可劃分為下列部分：

| URL部分 | 說明 |
|----------| -------------|
| `/graphql/execute.json` | 持續查詢端點 |
| `/wknd/adventure-by-path` | 持續查詢路徑 |
| `%3B` | 編碼 `;` |
| `adventurePath` | 查詢變數 |
| `%3D` | 編碼 `=` |
| `%2F` | 編碼 `/` |
| `%2Fcontent%2Fdam...` | 內容片段的編碼路徑 |

在純文字中，請求URI如下所示：

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

若要在用戶端應用程式中使用持續的查詢，應將AEM無標題用戶端SDK用於 [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java)，或 [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). 無頭式用戶端SDK會自動為要求中的任何查詢變數進行適當編碼。

## 將持續存在的查詢傳輸至生產環境  {#transfer-persisted-query-production}

持續的查詢應一律在AEM製作服務上建立，然後發佈（復寫）至AEM發佈服務。 持續查詢通常會在較低環境（例如本機或開發環境）中建立和測試。 接著，您必須將持續存在的查詢提升至較高層級的環境，最終讓這些查詢可在生產AEM Publish環境中供用戶端應用程式使用。

### 包持續查詢

可將持續查詢內建到 [AEM套件](/help/implementing/developing/tools/package-manager.md). 然後，可以下載AEM套件並安裝在不同的環境上。 AEM套件也可從AEM製作環境複製至AEM發佈環境。

要建立包：

1. 導覽至 **工具** > **部署** > **套件**.
1. 點選以建立新套件 **建立套件**. 這將開啟一個對話框以定義包。
1. 在「包定義」對話框中，位於 **一般** 輸入 **名稱** 例如&quot;wknd-persistent-queries&quot;。
1. 輸入版本號，如「1.0」。
1. 在 **篩選器** 新增 **篩選**. 使用路徑查找器來選擇 `persistentQueries` 資料夾。 例如， `wknd` 配置完整路徑將 `/conf/wknd/settings/graphql/persistentQueries`.
1. 點選 **儲存** 以保存新包定義並關閉對話框。
1. 點選 **建置** 按鈕。

套件建置完成後，您可以：

* **下載** 套件並重新上傳至不同環境。
* **複製** 點選 **更多** > **複製**. 這會將套件復寫至已連線的AEM發佈環境。

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
