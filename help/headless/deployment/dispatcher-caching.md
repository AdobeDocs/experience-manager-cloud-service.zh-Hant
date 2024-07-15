---
title: GraphQL 持續性查詢 - 在 Dispatcher 中啟用快取
description: Dispatcher 是 Adobe Experience Manager 發佈環境前面的快取和安全層。您可以在 AEM Headless 中啟用持續性查詢的快取。
feature: Headless, Dispatcher, GraphQL API
exl-id: 30a97e56-6699-41c4-a4eb-fc6236667f8f
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 89%

---

# GraphQL 持續性查詢 - 在 Dispatcher 中啟用快取 {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>如果啟用了 Dispatcher 的快取，就不需要 [CORS 篩選器](/help/headless/deployment/cross-origin-resource-sharing.md)，因此可以忽略該部分。

根據預設，不啟用 Dispatcher 的持續性查詢快取。因為使用具有多個來源的 CORS (跨來源資源共用) 的客戶必須檢閱，且可能更新其 Dispatcher 設定，因此無法預設啟用。

>[!NOTE]
>
>Dispatcher 不會快取 `Vary` 標頭。
>
>在 Dispatcher 中可以啟用其他 CORS 相關標頭的快取，但在有多個 CORS 來源時可能不足。

>[!NOTE]
>
>如需 Dispatcher 的詳細文件，請參閱 [Dispatcher 指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)。

## 啟用持續性查詢的快取 {#enable-caching-persisted-queries}

若要啟用持續性查詢的快取，請定義 Dispatcher 變數 `CACHE_GRAPHQL_PERSISTED_QUERIES`：

1. 將變數新增至 Dispatcher 檔案 `global.vars`：

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>若要在快取的持續性查詢上取得個別`ETag`標頭計算（針對唯一的&#x200B;*每個*&#x200B;回應），必須在Dispatcher設定虛擬主機設定（如果尚未存在）中使用`FileETag Digest`設定：
>
>```xml
><Directory />    
>   ...    
>   FileETag Digest
></Directory> 
>```

>[!NOTE]
>
>為了符合 [Dispatcher 對可快取檔案的要求](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F)，Dispatcher 會將後綴 `.json` 新增到所有持續性查詢 URL，以便快取結果。
>
>啟用持續性查詢快取後，就會重寫規則來新增此後綴。

## Dispatcher 的 CORS 設定 {#cors-configuration-in-dispatcher}

使用 CORS 要求的客戶可能必須在 Dispatcher 中檢閱和更新其 CORS 設定。

* `Origin` 標頭不得透過 Dispatcher 傳遞到 AEM 發佈：
   * 檢查 `clientheaders.any` 檔案。
* 而是必須在 Dispatcher 級別評估 CORS 要求是否為許可的來源。此方法也能確保在所有情況下，CORS 相關標頭正確設定於一個位置。
   * 如此的設定應該新增至 `vhost` 檔案。以下提供一個範例設定；為了簡單起見，僅提供了 CORS 相關部分。您可以根據特定使用案例進行調整。

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
