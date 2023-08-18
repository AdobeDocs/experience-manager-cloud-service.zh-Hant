---
title: GraphQL持續查詢 — 啟用Dispatcher中的快取
description: Dispatcher 是 Adobe Experience Manager 發佈環境前面的快取和安全層。您可以在AEM Headless中啟用持續查詢的快取。
feature: Dispatcher, GraphQL API
source-git-commit: 0066bfba3a403791c6a35b1280ae04b576315566
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---


# GraphQL持續查詢 — 啟用Dispatcher中的快取 {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>如果Dispatcher中的快取已啟用，則 [CORS篩選器](/help/headless/deployment/cross-origin-resource-sharing.md) 而不需要，因此可忽略區段。

Dispatcher中預設不會啟用持續查詢的快取。 無法啟用預設值，因為使用具有多種來源的CORS （跨來源資源共用）的客戶需要檢閱（並可能更新）其Dispatcher設定。

>[!NOTE]
>
>Dispatcher不會快取 `Vary` 標頭。
>
>可以在Dispatcher中啟用其他CORS相關標頭的快取，但是當有多個CORS來源時，該功能可能還不夠。

>[!NOTE]
>
>如需 Dispatcher 的詳細文件，請參閱 [Dispatcher 指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)。

## 啟用持續查詢的快取 {#enable-caching-persisted-queries}

若要啟用持續查詢的快取，請定義Dispatcher變數 `CACHE_GRAPHQL_PERSISTED_QUERIES`：

1. 將變數新增到Dispatcher檔案 `global.vars`：

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>若要遵循 [Dispatcher對可快取檔案的需求](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F)，Dispatcher會新增尾碼 `.json` 至所有儲存的查詢URL，以便可以快取結果。
>
>在啟用持續查詢快取後，此尾碼會由重寫規則新增。

## Dispatcher中的CORS設定 {#cors-configuration-in-dispatcher}

使用CORS請求的客戶可能需要在Dispatcher中檢閱和更新其CORS設定。

* 此 `Origin` 標題不能透過Dispatcher傳遞給AEM發佈：
   * 檢查 `clientheaders.any` 檔案。
* 相反地，必須在Dispatcher層級評估CORS請求的可允許來源。 此方法也能確保CORS相關的標頭在任何情況下都能在同一位置正確設定。
   * 此類設定應新增至 `vhost` 檔案。 以下提供設定範例；為簡化起見，僅提供CORS相關部分。 您可以根據特定使用案例進行調整。

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```
