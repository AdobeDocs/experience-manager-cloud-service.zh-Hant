---
title: AEM-CIF核心元件和Adobe Experience Platform一體化
description: 瞭解如何使用CIF -Experience Platform連接器AEM將呈現的產品頁面中的儲存事件資料發送到Experience Platform。
sub-product: Commerce
version: Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Architect, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
exl-id: 30bb9b2c-5f00-488e-ad5c-9af7cd2c4735
source-git-commit: 73fe6ce5bbdf0ad437ae4b47b892ad05e016ab68
workflow-type: tm+mt
source-wordcount: '2080'
ht-degree: 1%

---

# AEM-CIF核心元件和Adobe Experience Platform一體化 {#aem-cif-aep-integration}

的 [商業整合框架(CIF)](https://github.com/adobe/aem-core-cif-components) 核心元件提供無縫整合 [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) 從客戶端交互轉發儲存事件及其資料，如 __添加到購物車__。

的 [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components) project提供名為 [Adobe Experience PlatformAdobe Commerce連接器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) 從您的Commerce商店收集事件資料。 該事件資料會被發送到Adobe Experience Cloud其他產品(如Adobe Analytics和Adobe Target)中使用的Experience Platform，以構建360度的概要資訊，涵蓋客戶旅程。 通過將Commerce資料連接到Adobe Experience Cloud的其他產品，您可以執行分析站點上的用戶行為、執行AB測試和建立個性化市場活動等任務。

瞭解有關 [Experience Platform資料收集](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) 一套技術，使您能夠從客戶端源收集客戶體驗資料。

## 發送 `addToCart` 要Experience Platform的事件資料 {#send-addtocart-to-aep}

以下步驟顯示如何發送 `addToCart` 使用CIF -AEMExperience Platform連接器將事件資料從呈現的產品頁發送到Experience Platform。 通過使用Adobe Experience Platform調試器瀏覽器擴展，您可以test和查看提交的資料。

![在Adobe Experience Platform調試器中查看addToCart事件資料](../assets/aep-integration/EventData-AEM-AEP.png)

## 必備條件 {#prerequisites}

您必須使用本地開發環境來完成此演示。 這包括已配置並AEM連接到Adobe Commerce實例的運行實例。 查看 [使用AEMas a Cloud ServiceSDK設定本地開發](../develop.md)。

您還需要訪問 [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) 以及為資料收集建立模式、資料集和資料流的權限。 有關詳細資訊，請參見 [權限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html)。

## 商AEM務as a Cloud Service設定 {#aem-setup}

工作 __商AEM務as a Cloud Service__ 本地環境中包含必要的代碼和配置，請完成以下步驟。

### 本地設定

關注 [本地設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) 使Commerceas a Cloud Service環境AEM工作的步驟。

### 項目設定

關注 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) 建立全新商AEM務(CIF)項目的步驟。

>[!TIP]
>
>在以下示例中，AEM Commerce項目名為： `My Demo Storefront`但是，您可以選擇自己的項目名稱。

![商AEM務項目](../assets/aep-integration/aem-project-with-commerce.png)


通過從項目的根目AEM錄運行以AEM下命令，將新建立的Commerce項目構建並部署到本地SDK。

```bash
$ mvn clean install -PautoInstallSinglePackage
```

本地部署 `My Demo StoreFront` 具有預設代碼和內容的商業網站如下所示：

![預設AEM商業網站](../assets/aep-integration/demo-aem-storefront.png)

### 安裝Peregrine和CIF-AEP連接器依賴項

要從此Commerce網站的類別和產品頁收集和發送事AEM件資料，需要安裝密鑰 `npm` 包 `ui.frontend` Commerce項AEM目模組。

導航到 `ui.frontend` 命令行中運行以下命令，安裝所需的軟體包。

```bash
npm i --save lodash.get@^4.4.2 lodash.set@^4.3.2
npm i --save apollo-cache-persist@^0.1.1
npm i --save redux-thunk@~2.3.0
npm i --save @adobe/apollo-link-mutation-queue@~1.1.0
npm i --save @magento/peregrine@~12.5.0
npm i --save @adobe/aem-core-cif-react-components --force
npm i --save-dev @magento/babel-preset-peregrine@~1.2.1
npm i --save @adobe/aem-core-cif-experience-platform-connector --force
```

>[!IMPORTANT]
>
>的 `--force` 有時需要參數，因為 [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) 受支援的對等依賴項的限制。 通常，這不應引起任何問題。


### 將Maven配置為使用 `--force` 參數

作為Maven生成過程的一部分， npm會清除安裝(使用 `npm ci`)。 這還需要 `--force` 參數。

導航到項目的根POM檔案 `pom.xml` 找到 `<id>npm ci</id>` 執行塊。 將塊更新為如下所示：

```xml
<execution>
    <id>npm ci</id>
    <goals>
    <goal>npm</goal>
    </goals>
    <configuration>
    <arguments>ci --force</arguments>
    </configuration>
</execution>
```

### 更改Babel配置格式

從預設值切換 `.babelrc` 檔案相對配置檔案格式 `babel.config.js` 的子菜單。 這是項目範圍的配置格式，允許將插件和預設應用於 `node_module` 控制力更強。

1. 導航到 `ui.frontend` 模組並刪除現有 `.babelrc` 的子菜單。

1. 建立 `babel.config.js` 使用 `peregrine` 預設。

   ```javascript
   const peregrine = require('@magento/babel-preset-peregrine');
   
   module.exports = (api, opts = {}) => {
       const config = {
           ...peregrine(api, opts),
           sourceType: 'unambiguous'
       } 
   
       config.plugins = config.plugins.filter(plugin => plugin !== 'react-refresh/babel');
   
       return config;
   }
   ```

### 將Webpack配置為使用Babel

使用Babel載入程式傳輸JavaScript檔案(`babel-loader`)和webpack，您需要修改 `webpack.common.js` 的子菜單。

導航到 `ui.frontend` 模組和更新 `webpack.common.js` 檔案中包含以下規則 `module` 屬性值：

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### 配置Apollo客戶端

的 [阿波羅客戶](https://www.apollographql.com/docs/react/) 用於管理本地和遠程資料與GraphQL。 它還將GraphQL查詢的結果儲存在本地標準化記憶體快取中。

對於 [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) 要高效工作，你需要 `possibleTypes.js` 的子菜單。 要生成此檔案，請參見 [自動生成可能的類型](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically)。 另請參見 [PWA Studio參考實施](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) 還有一個 [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) 的子菜單。


1. 導航到 `ui.frontend` 將檔案另存為 `./src/main/possibleTypes.js`

1. 更新 `webpack.common.js` 檔案 `DefinePlugin` 部分，以替換生成時所需的靜態變數。

   ```javascript
   const { DefinePlugin } = require('webpack');
   const { POSSIBLE_TYPES } = require('./src/main/possibleTypes');
   
   ...
   
   plugins: [
       ...
       new DefinePlugin({
           'process.env.USE_STORE_CODE_IN_URL': false,
           POSSIBLE_TYPES
       })
   ]
   ```

### 初始化Peregrine和CIF核心元件

要初始化基於React的Peregrine和CIF核心元件，請建立所需的配置和JavaScript檔案。

1. 導航到 `ui.frontend` 建立以下資料夾： `src/main/webpack/components/commerce/App`

1. 建立 `config.js` 檔案，其內容如下：

   ```javascript
   // get and parse the CIF store configuration from the <head>
   const storeConfigEl = document.querySelector('meta[name="store-config"]');
   const storeConfig = storeConfigEl ? JSON.parse(storeConfigEl.content) : {};
   
   // the following global variables are needed for some of the peregrine features
   window.STORE_VIEW_CODE = storeConfig.storeView || 'default';
   window.AVAILABLE_STORE_VIEWS = [
       {
           code: window.STORE_VIEW_CODE,
           base_currency_code: 'USD',
           default_display_currency_code: 'USD',
           id: 1,
           locale: 'en',
           secure_base_media_url: '',
           store_name: 'My Demo StoreFront'
       }
   ];
   window.STORE_NAME = window.STORE_VIEW_CODE;
   window.DEFAULT_COUNTRY_CODE = 'en';
   
   export default {
       storeView: window.STORE_VIEW_CODE,
       graphqlEndpoint: storeConfig.graphqlEndpoint,
       // Can be GET or POST. When selecting GET, this applies to cache-able GraphQL query requests only.
       // Mutations will always be executed as POST requests.
       graphqlMethod: storeConfig.graphqlMethod,
       headers: storeConfig.headers,
   
       mountingPoints: {
           // TODO: define the application specific mount points as they may be used by <Portal> and <PortalPlacer>
       },
       pagePaths: {
           // TODO: define the application specific paths/urls as they may be used by the components
           baseUrl: storeConfig.storeRootUrl
       },
       eventsCollector: {
           // Enable the Experience Platform Connector and define the org and datastream to use
           aep: {
               orgId: // TODO: add your orgId
               datastreamId: // TODO: add your datastreamId
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >雖然你可能已經熟悉 [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) 檔案 __指AEM南 — CIF Venia項目__，需要對此檔案進行一些更改。 首先，查看 __TODO__ 注釋。 然後，在 `eventsCollector` 屬性，查找 `eventsCollector > aed` 對象並更新 `orgId` 和 `datastreamId` 屬性到正確的值。 [深入了解](./aep.md#add-aep-values-to-aem).

1. 建立 `App.js` 檔案。 此檔案類似於典型的React應用程式起點檔案，包含React和自定義掛接以及React Context用法，以方便Experience Platform整合。

   ```javascript
   import config from './config';
   
   import React, { useEffect } from 'react';
   import ReactDOM from 'react-dom';
   import { IntlProvider } from 'react-intl';
   import { BrowserRouter as Router } from 'react-router-dom';
   import { combineReducers, createStore } from 'redux';
   import { Provider as ReduxProvider } from 'react-redux';
   import { createHttpLink, ApolloProvider } from '@apollo/client';
   import { ConfigContextProvider, useCustomUrlEvent, useReferrerEvent, usePageEvent, useDataLayerEvents, useAddToCartEvent } from '@adobe/aem-core-cif-react-components';
   import { EventCollectorContextProvider, useEventCollectorContext } from '@adobe/aem-core-cif-experience-platform-connector';
   import { useAdapter } from '@magento/peregrine/lib/talons/Adapter/useAdapter';
   import { customFetchToShrinkQuery } from '@magento/peregrine/lib/Apollo/links';
   import { BrowserPersistence } from '@magento/peregrine/lib/util';
   import { default as PeregrineContextProvider } from '@magento/peregrine/lib/PeregrineContextProvider';
   import { enhancer, reducers } from '@magento/peregrine/lib/store';
   
   const storage = new BrowserPersistence();
   const store = createStore(combineReducers(reducers), enhancer);
   
   storage.setItem('store_view_code', config.storeView);
   
   const App = () => {
       const [{ sdk: mse }] = useEventCollectorContext();
   
       // trigger page-level events
       useCustomUrlEvent({ mse });
       useReferrerEvent({ mse });
       usePageEvent({ mse });
       // listen for add-to-cart events and enable forwarding to the magento storefront events sdk
       useAddToCartEvent(({ mse }));
       // enable CIF specific event forwarding to the Adobe Client Data Layer
       useDataLayerEvents();
   
       useEffect(() => {
           // implement a proper marketing opt-in, for demo purpose we hard-set the consent cookie
           if (document.cookie.indexOf('mg_dnt') < 0) {
               document.cookie += '; mg_dnt=track';
           }
       }, []);
   
       // TODO: use the App to create Portals and PortalPlaceholders to mount the CIF / Peregrine components to the server side rendered markup
       return <></>;
   };
   
   const AppContext = ({ children }) => {
       const { storeView, graphqlEndpoint, graphqlMethod = 'POST', headers = {}, eventsCollector } = config;
       const { apolloProps } = useAdapter({
           apiUrl: new URL(graphqlEndpoint, window.location.origin).toString(),
           configureLinks: (links, apiBase) =>
               // reconfigure the HTTP link to use the configured graphqlEndpoint, graphqlMethod and storeView header
   
               links.set('HTTP', createHttpLink({
                   fetch: customFetchToShrinkQuery,
                   useGETForQueries: graphqlMethod !== 'POST',
                   uri: apiBase,
                   headers: { ...headers, 'Store': storeView }
               }))
       });
   
       return (
           <ApolloProvider {...apolloProps}>
               <IntlProvider locale='en' messages={{}}>
                   <ConfigContextProvider config={config}>
                       <ReduxProvider store={store}>
                           <PeregrineContextProvider>
                               <EventCollectorContextProvider {...eventsCollector}>
                                   {children}
                               </EventCollectorContextProvider>
                           </PeregrineContextProvider>
                       </ReduxProvider>
                   </ConfigContextProvider>
               </IntlProvider>
           </ApolloProvider>
       );
   };
   
   window.onload = async () => {
       const root = document.createElement('div');
       document.body.appendChild(root);
   
       ReactDOM.render(
           <Router>
               <AppContext>
                   <App />
               </AppContext>
           </Router>,
           root
       );
   };
   ```

   的 `EventCollectorContext` 導出React Context，其中：

   - 載入commerce-events-sdk和commerce-events-collector庫，
   - 用給定的配置初始化它們以用於Experience Platform和/或ACDS
   - 預訂來自Peregrine的所有事件並將它們轉發到事件SDK

   您可以查看 `EventCollectorContext` [這裡](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js)。

### 構建和部署更新的項AEM目

要確保上述軟體包安裝、代碼和配置更改正確，請使用以下Maven命令重新生成和部AEM署更新的Commerce項目： `$ mvn clean install -PautoInstallSinglePackage`。

## Experience Platform設定 {#aep-setup}

要接收和儲存來自Commerce頁面(AEM如類別和產品)的事件資料，請完成以下步驟：

>[!AVAILABILITY]
>
>確保您是正確的 __產品配置檔案__ 在 __Adobe Experience Platform__ 和 __Adobe Experience Platform資料收集__。 如果需要，請與系統管理員協作以建立、更新或分配 __產品配置檔案__ 下 [Admin Console](https://adminconsole.adobe.com/)。

### 使用Commerce欄位組建立架構

要定義商務事件資料的結構，必須建立體驗資料模型(XDM)架構。 模式是一組規則，用於表示和驗證資料的結構和格式。

1. 在瀏覽器中，導航到 __Adobe Experience Platform__ 產品首頁。 比如說， <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 查找 __架構__ 菜單，按一下 __建立架構__ 按鈕，然後選擇 __XDM體驗事件__。

   ![AEP建立架構](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. 使用 __方案屬性>顯示名稱__ 使用  __合成>欄位組>添加__ 按鈕

   ![AEP架構定義](../assets/aep-integration/AEP-Schema-Definition.png)

1. 在 __添加欄位組__ 對話框，搜索 `Commerce`，選擇 __商業詳細資訊__ 複選框，然後按一下 __添加欄位組__。

   ![AEP架構定義](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>查看 [架構組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) 的子菜單。

### 建立資料集

要儲存事件資料，必須建立符合架構定義的資料集。 資料集是用於資料集合（通常是表）的儲存和管理構造，該資料集包含模式（列）和欄位（行）。

1. 在瀏覽器中，導航到 __Adobe Experience Platform__ 產品首頁。 比如說， <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 查找 __資料集__ 菜單，然後按一下 __建立資料集__ 按鈕。

   ![AEP建立資料集](../assets/aep-integration/AEP-Datasets-Create.png)

1. 在新頁面上，選擇 __從架構建立資料集__ 卡。

   ![AEP建立資料集架構選項](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

- 在新頁面上， __搜索和選擇__ 在上一步中建立的架構，然後按一下 __下一個__ 按鈕

   ![AEP建立資料集選擇架構](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. 使用 __配置資料集>名稱__ ，然後按一下 __完成__ 按鈕

   ![AEP建立資料集名稱](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>查看 [資料集概述](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) 的子菜單。


### 建立資料流

完成以下步驟以在Experience Platform中建立Datastream。

1. 在瀏覽器中，導航到 __Adobe Experience Platform__ 產品首頁。 比如說， <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 查找 __資料流__ 菜單，然後按一下 __新建資料流__ 按鈕。

   ![AEP建立資料流](../assets/aep-integration/AEP-Datastream-Create.png)

1. 使用 __名稱__ 欄位。 在 __事件架構__ 欄位，選擇新建立的架構，然後按一下 __保存__。

   ![AEP定義資料流](../assets/aep-integration/AEP-Datastream-Define.png)

1. 開啟新建立的Datastream，然後按一下 __添加服務__。

   ![AEP資料流添加服務](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. 在 __服務__ ，選擇 __Adobe Experience Platform__ 的雙曲餘切值。 下 __事件資料集__ 欄位，從上一步中選擇資料集名稱，然後按一下 __保存__。

   ![AEP資料流添加服務詳細資訊](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>查看 [資料流概述](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) 的子菜單。

## 將資料流值添加AEM到Commerce配置 {#add-aep-values-to-aem}

完成上述Experience Platform設定後，您應 `datastreamId` 資料流的左欄， `orgId` 右上角 __配置檔案圖片>帳戶資訊>用戶資訊__ 模式。

![AEP資料流ID](../assets/aep-integration/AEP-Datastream-ID.png)

1. 在AEMCommerce項目中 `ui.frontend` 模組，更新 `config.js` 檔案，特別是 `eventsCollector > aep` 對象屬性。

1. 構建和部署更新的AEMCommerce項目


## 觸發器 `addToCart` 事件和驗證資料收集 {#event-trigger-verify}

上述步驟完成AEM了Commerce和Experience Platform設定。 你現在可以觸發 `addToCart` 事件和使用Experience Platform調試器和資料集驗證資料收集 __度量和圖形__ 在產品UI中切換。

要觸發事件，您可以使用AEM本地設定中的作者或發佈服務。 在本示例中，通AEM過登錄到帳戶來使用作者。

1. 從「站點」頁中，選擇 __我的演示商店前面>我們> en__ 的 __編輯__ 按鈕。

1. 在頂部操作欄中，按一下 __查看為已發佈__，然後按一下店面導航中的任何首選類別。

1. 按一下 __產品頁__，然後選擇 __顏色，大小__ 啟用 __添加到購物車__ 按鈕


1. 開啟 __Adobe Experience Platform調試器__ 從瀏覽器的擴展面板中選擇擴展 __Experience PlatformWed SDK__ 左欄。

   ![AEP調試器](../assets/aep-integration/AEP-Debugger.png)


1. 返回到 __產品頁__ 按一下 __添加到購物車__ 按鈕 這會將資料發送到Experience Platform。 的 __Adobe Experience Platform調試器__ 擴展顯示事件詳細資訊。

   ![AEP調試器添加到購物車事件資料](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. 在Experience Platform產品UI中，導航至 __資料集> My Demo StoreFront__，也請參見Wiki頁。 __資料集活動__ 頁籤。 如果 __度量和圖形__ 啟用切換，將顯示事件資料狀態。

   ![Experience Platform資料集資料統計](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## 實施詳細資訊 {#implementation-details}

的 [CIFExperience Platform連接器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) 建在 [Experience PlatformAdobe Commerce連接器](https://marketplace.magento.com/magento-experience-platform-connector.html)，是 [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) 項目。

PWA Studio項目允許您建立由Adobe Commerce或Magento Open Source提供動力的Progressive Web Application(PWA)商店。 項目還包含名為 [佩雷格林](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) 將邏輯添加到可視元件。 的 [佩雷格林庫](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) 還提供了由 [Experience Platform連接器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) 與Experience Platform無縫融合。


## 支援的事件 {#supported-events}

到目前為止，支援以下事件：

__體驗XDM事件：__

1. 添加到購物車(AEM)
1. 查看頁面(AEM)
1. 查看產品(AEM)
1. 已發送搜索請求(AEM)
1. 收到搜索響應(AEM)

當 [Peregrine元件](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/) 在AEMCommerce項目中重新使用：

__體驗XDM事件：__

1. 從購物車中刪除
1. 開啟購物車
1. 查看購物車
1. 即時購買
1. 開始簽出
1. 完成簽出

__配置XDM事件：__

1. 登入
1. 建立帳戶
1. 編輯帳戶


## 其他資源 {#additional-resources}

有關詳細資訊，請參閱以下資源：

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [Experience Platform連接器概述](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html)
- [Experience Platform連接器事件](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/event-forwarding/events.html)
- [Adobe Experience Platform概述](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
