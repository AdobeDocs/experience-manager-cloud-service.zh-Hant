---
title: 開始使用PWA Studio的AEM擴充功能
description: 瞭解如何使用PWA Studio部署AEM Headless Content and Commerce專案。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: a7c187ba-885e-45bf-a538-3c235b09a0f1
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# 開始使用PWA Studio的AEM擴充功能 {#getting-started-pwa}

開箱即用的PWA Studio透過GraphQL與Adobe Commerce緊密整合，提供無限制選項來建立創新且吸引人的店面和其他數位體驗。

內容片段是預先定義結構的內容片段，可讓您以Headless方式使用GraphQL作為不同格式（例如JSON、Markdown）的API並獨立轉譯。 內容片段包含GraphQL所需的所有資料型別和欄位，以確保您的應用程式僅請求可用內容並接收預期內容。 在架構方式上，這類模組提供的彈性使其非常適合在多個位置及多個管道上使用。

使用Adobe Experience Manager中的內容片段模式編輯器，可輕鬆設計所需的結構。 整合Adobe Experience Manager內容片段（或任何其他資料）與您的PWA Studio應用程式的主要挑戰是從多個GraphQL端點擷取資料。 這是因為PWA Studio可立即使用單一Adobe Commerce GraphQL端點。

## 架構 {#architecture}

![PWAHeadless架構](/help/commerce-cloud/assets/PWA-Studio_Architecture.png)

## 設定PWA Studio {#setup-pwa}

遵循Adobe Commerce [PWA Studio檔案](https://developer.adobe.com/commerce/pwa-studio/tutorials/) 以設定您的PWA Studio應用程式。

若要將PWA Studio連線至AEM的GraphQL端點，您可以使用 [PWA Studio的AEM擴充功能](https://github.com/adobe/aem-pwa-studio-extensions).

1. 簽出存放庫

1. 在您的PWA Studio應用程式中，將擴充功能新增為開發相依性。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. 將Apollo連結包裝函式新增至您的PWA Studio應用程式。 在pwa-root/src/index.js中，進行下列變更：

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   有關Apollo使用者端自訂的詳細資訊，請參閱 [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. 若要使用Blog專案擴充導覽元件，請在pwa-root/local-intercept.js中新增下列改寫專案：

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   有關導覽元件自訂的詳細資訊，請參閱 [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) 和 [擴充性框架](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) PWA Studio檔案。

1. Apollo使用者端預期的AEM GraphQL端點位於 `<https://pwa-studio/endpoint.js>`. 若要將端點對應至此位置，請自訂PWA Studio應用程式的「向上」設定： a.將AEM_CFM_GRAPHQL變數新增至pwa-root/.env，並將其調整為指向您的AEM內容片段GraphQL端點。

   範例： `AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>`

   b.將Proxy解析器新增至您的UPPER設定。 UPPER設定的範例看起來可能像這樣：

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

依照AEM內容片段檔案指示，為您的AEM專案設定GraphQL端點。 此外，在您的AEM專案中新增下列設定，以允許您的PWA Studio應用程式存取GraphQL端點：

* AdobeGranite跨原始資源共用原則(com.adobe.granite.cors.impl.CORSPolicyImpl)

  將allowedorigin屬性設定為PWA應用程式的完整主機名稱。

  範例：  `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Apache Sling反向連結篩選器(org.apache.sling.security.impl.ReferrerFilter.cfg.json)

  將allow.hosts屬性設定為PWA應用程式的主機名稱。

  範例： `pwa-studio-test-vflyn.local.pwadev`

您可以在這裡找到這兩個設定的完整範例： <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

為了展示GraphQL端點，我們準備了一些透過內容封裝的範例內容片段模型和資料。 這些可與PWA Studio擴充功能隨附的React Components搭配使用。

## 使用方式 {#how-to-use}

此擴充功能被視為如何連線PWA Studio應用程式與AEM的範例實作，以透過GraphQL擷取及呈現內容。

根據您的使用案例，您想要建立自己的自訂內容片段模式，這會產生自訂GraphQL結構描述，然後可以由您自己的React元件使用。

生產設定可能因多方面而異。

* 您可以有單一同盟GraphQL端點，結合AEM和Adobe Commerce GraphQL資料，而非自訂Apollo使用者端。
* 您的PWA Studio應用程式可以直接使用AEM GraphQL端點URL，而不需要具有UPLOAD的Proxy。 Proxy也可以移至其他圖層（例如CDN）。
* 哪一種方法最適合您也很取決於您如何將PWA Studio應用程式提供給使用者。

此擴充功能提供兩個範例。

### 部落格 {#blog}

根據某些內容片段模型顯示部落格。 此外，它包含如何設定Apollo使用者端以與AEM GraphQL端點搭配使用，以及如何在PWA Studio中擴充導覽元件的範例。 另請參閱 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) 以取得更多詳細資料。

### PDP擴充 {#pdp-enrichment}

可讓行銷人員透過作為內容片段管理的其他內容輕鬆擴充PDP。  另請參閱 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) 以取得更多詳細資料。
