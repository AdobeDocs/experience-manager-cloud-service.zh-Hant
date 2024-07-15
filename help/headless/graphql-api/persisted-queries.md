---
title: 持續性 GraphQL 查詢
description: 了解如何在 Adobe Experience Manager as a Cloud Service 中保留 GraphQL 查詢，以將效能最佳化。用戶端應用程式可以使用 HTTP GET 方法要求持續性查詢，回應可以在 Dispatcher 和 CDN 層快取，最終提高用戶端應用程式的效能。
feature: Headless, Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 79%

---

# 持續性 GraphQL 查詢 {#persisted-graphql-queries}

持續性查詢是在 Adobe Experience Manager (AEM) as a Cloud Service 伺服器上建立和儲存的 GraphQL 查詢。用戶端應用程式可以透過 GET 要求來要求它們。GET 要求的回應可以在 Dispatcher 和 CDN 層快取，最終提高發出要求之用戶端應用程式的效能。這與標準的 GraphQL 查詢不同，後者使用 POST 要求執行，其回應無法輕鬆快取。

>[!NOTE]
>
>建議使用持續性查詢。如需詳細資訊以及相關的 Dispatcher 設定，請參閱 [GraphQL 查詢最佳做法 (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices)。

AEM 有提供 [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)，可讓您在[傳送到生產環境](#transfer-persisted-query-production)之前，開發、測試和保留您的 GraphQL 查詢。如果需要自訂 (例如[自訂快取](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)時)，您可以使用 API，請參閱[如何保留 GraphQL 查詢](#how-to-persist-query)中提供的 cURL 範例。

## 持續性查詢和端點 {#persisted-queries-and-endpoints}

持續性查詢必須一律使用與[適當的 Sites 設定](graphql-endpoint.md)相關的端點；所以可以使用以下其中之一，或兩者都使用：

* 全域設定和端點
查詢可以存取所有內容片段模型。
* 特定 Sites 設定和端點
為特定 Sites 設定建立持續性查詢時，需要相應的 Sites 設定專屬端點 (以提供相關內容片段模型的存取權)。
例如，若要專門為 WKND Sites 設定建立持續性查詢，必須提前建立相應的 WKND 專屬 Sites 設定和 WKND 專屬端點。

>[!NOTE]
>
>如需詳細資料，請參閱[在設定瀏覽器中啟用內容片段功能](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)。
>
>必須為適當的 Sites 設定啟用 **GraphQL 持續性查詢**。

例如，如果有一個名為 `my-query` 的特定查詢，它使用 Sites 設定 `my-conf` 中的模型 `my-model`：

* 您可以使用 `my-conf` 專屬端點建立查詢，然後查詢會儲存為：
  `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用 `global` 端點建立相同查詢，然後查詢會儲存為：
  `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>這是兩個不同的查詢 - 儲存在不同的路徑下。
>
>他們只是碰巧使用相同的模型，但透過不同的端點。

## 如何保留 GraphQL 查詢 {#how-to-persist-query}

建議最初在 AEM 編寫環境中保留查詢，然後[將查詢傳輸到](#transfer-persisted-query-production)生產 AEM 發佈環境，以供應用程式使用。

有多種保留查詢的方法，包括：

* GraphiQL IDE - 請參閱[儲存持續性查詢](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) (首選方法)
* cURL - 請參閱以下範例
* 其他工具，包括 [Postman](https://www.postman.com/)

GraphiQL IDE 是保留查詢的&#x200B;**首選**&#x200B;方法。若要使用 **cURL** 命令列工具保留特定查詢：

1. 透過將查詢放入新端點 URL `/graphql/persist.json/<config>/<persisted-label>` 來準備查詢。

   例如，建立持續性查詢：

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

1. 此時，檢查回應。

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

1. 然後，您可以透過取得 URL `/graphql/execute.json/<shortPath>` 來要求持續性查詢。

   例如，使用持續性查詢：

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 透過發佈到一個已經存在的查詢路徑來更新持續性查詢。

   例如，使用持續性查詢：

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

1. 建立已包裝的普通查詢。

   例如：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 建立含快取控制的已包裝普通查詢。

   例如：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 建立含參數的持續性查詢：

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


## 如何執行持續性查詢 {#execute-persisted-query}

若要執行持續性查詢，用戶端應用程式使用以下語法發出 GET 要求：

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

其中 `PERSISTENT_PATH` 是持續性查詢儲存所在的縮短路徑。

1. 例如 `wknd` 是設定名稱，`plain-article-query` 是持續性查詢的名稱。若要執行查詢：

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. 執行含參數的查詢。

   >[!NOTE]
   >
   > 執行持續性查詢時，查詢變數和值必須正確[編碼](#encoding-query-url)。

   例如：

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   如需詳細資料，請參閱使用[查詢變數](#query-variables)。

## 使用查詢變數 {#query-variables}

查詢變數可以與持續性查詢一起使用。查詢變數使用變數名稱和值附加到開頭為分號 (`;`) 的要求。多個變數會用分號分隔。

模式如下所示：

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

例如，以下查詢包含一個變數 `activity` 以根據活動值篩選清單：

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

此查詢可以保留在路徑 `wknd/adventures-by-activity` 下。若要在 `activity=Camping` 呼叫持續性查詢，要求將如下所示：

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

UTF-8編碼`%3B`適用於`;`，而`%3D`是`=`的編碼。 查詢變數和任何特殊字元必須[正確編碼](#encoding-query-url)才能執行持續性查詢。

### 使用查詢變數 — 最佳實務 {#query-variables-best-practices}

在查詢中使用變數時，有一些最佳實務需要遵循：

* 編碼
一般而言，建議您一律編碼所有特殊字元；例如`;`、`=`、`?`、`&`等。

* 分號
使用多個變數（以分號分隔）的持續性查詢必須具備下列其中一項：
   * 以分號編碼(`%3B`)；對URL進行編碼也會達到此目的
   * 或在查詢結尾加上分號

* `CACHE_GRAPHQL_PERSISTED_QUERIES`
為Dispatcher啟用`CACHE_GRAPHQL_PERSISTED_QUERIES`時，其值中包含`/`或`\`字元的引數會在Dispatcher層級編碼兩次。
若要避免此情況：

   * 在Dispatcher上啟用`DispatcherNoCanonURL`。
這會指示Dispatcher將原始URL轉送至AEM，以避免重複編碼。
不過，此設定目前僅適用於`vhost`層級，因此如果您已有Dispatcher設定可重寫URL （例如使用縮短的URL時），則持續查詢URL可能需要個別的`vhost`。

   * 傳送`/`或`\`個未編碼的字元。
呼叫持久查詢URL時，請確定所有`/`或`\`字元在持久查詢變數的值中保持未編碼。
     >[!NOTE]
     >
     >只有由於任何原因而無法實作`DispatcherNoCanonURL`解決方案時，才建議使用此選項。

* `CACHE_GRAPHQL_PERSISTED_QUERIES`

  為Dispatcher啟用`CACHE_GRAPHQL_PERSISTED_QUERIES`時，`;`字元不能用於變數的值。

## 快取持續性查詢 {#caching-persisted-queries}

建議使用持續性查詢，因為可以在 [Dispatcher](/help/headless/deployment/dispatcher.md) 和內容傳遞網路 (CDN) 層進行快取，最終提升發出要求的用戶端應用程式效能。

依預設，AEM 將根據存留時間 (TTL) 定義使快取失效。這些 TTL 可以依照以下參數定義。這些參數可以透過各種方式存取，根據所使用的機制，名稱會有所不同：

| 快取類型 | [HTTP 標頭](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) | cURL | OSGi 設定 | Cloud Manager |
|--- |--- |--- |--- |--- |
| 瀏覽器 | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` | `graphqlCacheControl` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` | `graphqlSurrogateControl` | 60 |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` | `graphqlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` | `graphqlStaleIfError` |

{style="table-layout:auto"}

### 編寫執行個體 {#author-instances}

對於編寫執行個體，預設值為：

* `max-age`：60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

這些：

* 不可被覆寫：
   * 使用 OSGi 設定
* 可以被覆寫：
   * 透過使用 cURL 定義 HTTP 標頭設定的請求；它應該包括合適的 `cache-control` 設定和/或 `surrogate-control`；例如，請參閱[管理持續性查詢層級的快取](#cache-persisted-query-level)
   * 如果您在 [GraphiQL IDE](#http-cache-headers-graphiql-ide) 的&#x200B;**標頭**&#x200B;對話框中指定值。

### 發佈執行個體 {#publish-instances}

對於發佈執行個體，預設值為：

* `max-age`：60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

這些可以被覆寫：

* [從 GraphQL IDE](#http-cache-headers-graphiql-ide)

* [在持續性查詢層級](#cache-persisted-query-level)；這涉及在命令列介面中使用 cURL 將查詢發佈到 AEM，以及發佈持續性查詢。

* [使用 Cloud Manager 變數](#cache-cloud-manager-variables)

* [使用 OSGi 設定](#cache-osgi-configration)

### 管理 GraphiQL IDE 中的 HTTP 快取標頭 {#http-cache-headers-graphiql-ide}

GraphiQL IDE - 請參閱[儲存持續性查詢](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### 在持續性查詢層級管理快取 {#cache-persisted-query-level}

這涉及在命令列介面中使用 cURL 將查詢發佈到 AEM。

對於 PUT (建立) 方法的範例：

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

對於 POST (更新) 方法的範例：

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

`cache-control` 可以在建立時 (PUT) 或稍後 (例如透過 POST 要求) 設定。建立持續性查詢時，快取控制是選用的，因為 AEM 可以提供預設值。如需有關如何使用 cURL 保留查詢的範例，請參閱[如何保留 GraphQL 查詢](#how-to-persist-query)。

### 使用 Cloud Manager 變數管理快取 {#cache-cloud-manager-variables}

[Cloud Manager 環境變數](/help/implementing/cloud-manager/environment-variables.md)可以使用 Cloud Manager 來定義以定義所需的值：

| 名稱 | 值 | 套用的服務 | 類型 |
|--- |--- |--- |--- |
| `graphqlStaleIfError` | 86400 | *依需要* | *依需要* |
| `graphqlSurrogateControl` | 600 | *依需要* | *依需要* |

{style="table-layout:auto"}

### 使用 OSGi 設定管理快取 {#cache-osgi-configration}

若要全域管理快取，您可以為&#x200B;**持續性查詢服務設定**[進行 OSGi 設定](/help/implementing/deploying/configuring-osgi.md)。

>[!NOTE]
>
>對於快取控制，OSGi 設定僅適用於發佈執行個體。設定存在於編寫執行個體，但受到忽略。

>[!NOTE]
>
>此&#x200B;**持續性查詢服務設定**&#x200B;也用於[設定查詢回應代碼](#configuring-query-response-code)。

發佈執行個體的預設 OSGi 設定：

* 讀取 Cloud Manager 變數 (若有)：

  | OSGi 設定屬性 | 讀取此 | Cloud Manager 變數 |
  |--- |--- |--- |
  | `cacheControlMaxAge` | 讀取 | `graphqlCacheControl` |
  | `surrogateControlMaxAge` | 讀取 | `graphqlSurrogateControl` |
  | `surrogateControlStaleWhileRevalidate` | 讀取 | `graphqlStaleWhileRevalidate` |
  | `surrogateControlStaleIfError` | 讀取 | `graphqlStaleIfError` |

  {style="table-layout:auto"}

* 如果沒有，OSGi 設定會使用[發佈執行個體的預設值](#publish-instances)。

## 設定查詢回應代碼 {#configuring-query-response-code}

預設情況下，`PersistedQueryServlet` 執行查詢時，會傳送 `200` 回應，無論實際結果如何。

您可以[設定&#x200B;**持續查詢服務組態**&#x200B;的OSGi設定](/help/implementing/deploying/configuring-osgi.md)，以便在持續查詢發生錯誤時，控制`/execute.json/persisted-query`端點是否傳回更詳細的狀態代碼。

>[!NOTE]
>
>此&#x200B;**持續性查詢服務設定**&#x200B;也用於[管理快取](#cache-osgi-configration)。

欄位 `Respond with application/graphql-response+json`(`responseContentTypeGraphQLResponseJson`) 可依要求定義：

* `false` (預設值)：持續性查詢成功與否並不重要。傳回的`Content-Type`標頭是`application/json`，`/execute.json/persisted-query` *一律*&#x200B;會傳回狀態碼`200`。

* `true`：
傳回的`Content-Type`是`application/graphql-response+json`，當執行持續查詢時發生任何形式的錯誤時，端點會傳回適當的回應代碼：

  | 程式碼 | 說明 |
  |--- |--- |
  | 200 | 成功的回應 |
  | 400 | 表示缺少標頭，或持續查詢路徑有問題。 例如，未指定組態名稱、未指定尾碼及其他。<br>請參閱[疑難排解 — 未設定GraphQL端點](/help/headless/graphql-api/persisted-queries-troubleshoot.md#missing-path-query-url)。 |
  | 404 | 找不到請求的資源。 例如，伺服器上無法使用Graphql端點。<br>請參閱[疑難排解 — GraphQL持續查詢URL](/help/headless/graphql-api/persisted-queries-troubleshoot.md#graphql-endpoint-not-configured)中缺少路徑。 |
  | 500 | 內部伺服器錯誤。 例如，驗證錯誤、持續性錯誤和其他。 |

  >[!NOTE]
  >
  >另請參閱https://graphql.github.io/graphql-over-http/draft/#sec-Status-Codes

## 編碼查詢 URL 以供應用程式使用 {#encoding-query-url}

為供應用程式使用，建構查詢變數時使用的任何特殊字元 (即分號 (`;`)、等號 (`=`)、斜線 `/`) 必須是轉換為使用相應的 UTF-8 編碼。

例如：

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL 可以分解成以下幾個部分：

| URL 部分 | 說明 |
|----------| -------------|
| `/graphql/execute.json` | 持續性查詢端點 |
| `/wknd/adventure-by-path` | 持續性查詢路徑 |
| `%3B` | `;` 編碼 |
| `adventurePath` | 查詢變數 |
| `%3D` | `=` 編碼 |
| `%2F` | `/` 編碼 |
| `%2Fcontent%2Fdam...` | 內容片段的已編碼路徑 |

在純文字中，要求 URI 如下所示：

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

若要在用戶端應用程式中使用持續性查詢，AEM Headless 用戶端 SDK 應該用於 [JavaScript](https://github.com/adobe/aem-headless-client-js)、[Java](https://github.com/adobe/aem-headless-client-java) 或 [NodeJS](https://github.com/adobe/aem-headless-client-nodejs)。Headless 用戶端 SDK 會自動將要求中的任何查詢變數適當地編碼。

## 將持續性查詢轉移到您的生產環境  {#transfer-persisted-query-production}

持續性查詢應一律建立在 AEM Author 服務上，然後發佈 (複製) 到 AEM Publish 服務。通常，持續性查詢是在低層環境 (例如本機或開發環境) 中建立和測試的。然後，必須將持續性查詢提升到高層環境，最終使它們能在生產 AEM Publish 環境中供用戶端應用程式使用。

### 封裝持續性查詢

持續性查詢可以內建在 [AEM 套件](/help/implementing/developing/tools/package-manager.md) 中。然後，AEM 套件可以下載和安裝在不同的環境中。AEM 套件也可以從 AEM 編寫環境複製到 AEM 發佈環境。

若要建立套件：

1. 導覽至&#x200B;**工具** > **部署** > **套件**。
1. 點選&#x200B;**建立套件**&#x200B;來建立新套件。這會開啟一個對話方塊以定義封裝。
1. 在套件定義對話框中，在 **一般**&#x200B;下輸入&#x200B;**名稱**，例如「wknd-persistent-queries」。
1. 輸入版本號碼，例如「1.0」。
1. 在&#x200B;**篩選器**&#x200B;下加入新&#x200B;**篩選器**。使用路徑尋找工具選取設定下方的 `persistentQueries` 資料夾。例如，對於 `wknd` 設定，完整路徑將為 `/conf/wknd/settings/graphql/persistentQueries`。
1. 選取&#x200B;**儲存**&#x200B;以儲存新的封裝定義並關閉對話方塊。
1. 選取已建立封裝定義中的&#x200B;**建置**&#x200B;按鈕。

建置套件後，您可以：

* **下載**&#x200B;套件並在不同環境中重新上傳。
* 點選&#x200B;**更多** > **複製**&#x200B;來&#x200B;**複製**&#x200B;套件。這會將套件複製到連接的 AEM 發佈環境。

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
