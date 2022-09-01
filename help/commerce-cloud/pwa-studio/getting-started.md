---
title: AEM擴充功能for PWA Studio快速入門
description: 了解如何使用PWA Studio部署AEM無頭內容與商務專案。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: a7c187ba-885e-45bf-a538-3c235b09a0f1
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---

# AEM擴充功能for PWA Studio快速入門 {#getting-started-pwa}

立即可用，PWA Studio可透過GraphQL與Adobe Commerce無縫整合，提供無限選項，用於建立創新、吸引人的店面和其他數位體驗。

內容片段是具有預先定義結構的內容片段，可讓您以無周邊方式使用GraphQL作為不同格式（例如JSON、Markdown）的API，並獨立轉譯。 內容片段包含GraphQL所需的所有資料類型和欄位，以確保您的應用程式只要求可用項目並接收預期項目。 它們在結構上提供的彈性，使其非常適合用於多個位置和多個管道。

使用Adobe Experience Manager中的內容片段模型編輯器，輕鬆設計您需要的結構。 將Adobe Experience Manager內容片段（或任何其他資料）與您的PWA Studio應用程式整合的主要挑戰，是從多個GraphQL端點擷取資料。 這是因為PWA Studio可立即用於單一Adobe Commerce GraphQL端點。

## 架構 {#architecture}

![PWA無頭架構](/help/commerce-cloud/assets/PWA-Studio_Architecture.png)

## 設定PWA Studio {#setup-pwa}

關注Adobe Commerce [PWA Studio檔案](https://developer.adobe.com/commerce/pwa-studio/tutorials/) 來設定您的PWA Studio應用程式。

若要將PWA Studio與AEM的GraphQL端點連線，您可以使用 [AEM擴充功能for PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. 簽出儲存庫

1. 在您的PWA Studio應用程式中，新增擴充功能作為開發相依性。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. 將Apollo Link包裝函式新增至您的PWA Studio應用程式。 在pwa-root/src/index.js中進行下列變更：

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   如需Apollo客戶自訂的詳細資訊，請參閱 [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. 若要使用部落格項目擴充導覽元件，請將下列變更新至pwa-root/local-intercept.js :

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   如需自訂導覽元件的詳細資訊，請參閱 [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) 和 [可擴充性框架](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) PWA Studio檔案。

1. Apollo客戶端將預期AEM GraphQL端點位於 `<https://pwa-studio/endpoint.js>`. 若要將端點對應至此位置，您需要自訂PWA Studio應用程式的向上設定：a.將AEM_CFM_GRAPHQL變數新增至pwa-root/.env，並將其調整為指向您的AEM內容片段GraphQL端點。

   範例: `AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>`

   b.將代理解析器新增至UPPRAD設定。 向上配置的示例如下所示：

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## 設定AEM {#setup-aem}

請依照AEM內容片段檔案中的說明，為AEM專案設定GraphQL端點。 此外，在您的AEM專案中，新增下列設定，讓您的PWA Studio應用程式存取GraphQL端點：

* AdobeGranite跨原始資源共用原則(com.adobe.granite.cors.impl.CORSPolicyImpl)

   將allowedorigin屬性設定為PWA應用程式的完整主機名。

   範例:  `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Apache Sling Referrer Filter(org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   將allow.hosts屬性設定為PWA應用程式的主機名。

   範例: `pwa-studio-test-vflyn.local.pwadev`

您可以在這裡找到這兩種設定的完整範例： <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

為了展示GraphQL端點，我們透過內容套件準備了一些內容片段模型和資料範例。 這些功能可與PWA Studio擴充功能隨附的React元件搭配使用。

## 使用方式 {#how-to-use}

此擴充功能被視為如何將PWA Studio應用程式與AEM連結，以透過GraphQL擷取及呈現內容的範例實作。

根據您的使用案例，您想要建立自己的自訂內容片段模型，進而產生自訂GraphQL架構，供您自己的React元件使用。

生產設定可能有多方面差異。

* 您可以有單一同盟的GraphQL端點，此端點結合AEM和Adobe Commerce GraphQL資料，而非自訂Apollo用戶端。
* 您的PWA Studio應用程式可以直接使用AEM GraphQL端點URL，不需要具有UPPRASH的代理。 也可以將代理移至不同層（例如CDN）。
* 哪種方法最適合您，還取決於您如何將PWA Studio應用程式提供給最終用戶。

此擴充功能提供兩個範例。

### 部落格 {#blog}

根據某些內容片段模型顯示部落格貼文。 此外，它還包含如何配置Apollo客戶端以與AEM GraphQL端點協作以及如何在PWA Studio中擴展導航元件的示例。 請參閱 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) 以取得更多詳細資訊。

### PDP擴充 {#pdp-enrichment}

讓行銷人員能透過管理為內容片段的其他內容，輕鬆豐富PDP內容。  請參閱 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) 以取得更多詳細資訊。
