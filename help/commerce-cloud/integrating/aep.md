---
title: AEM CIF核心元件和Adobe Experience Platform集成
description: 了解如何使用 CIF - Experience Platform 連接器將店面事件資料從 AEM 呈現的產品頁面發送到Experience Platform。
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
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 1%

---


# AEM CIF核心元件和Adobe Experience Platform集成 {#aem-cif-aep-integration}

[商務集成框架 （CIF）](https://github.com/adobe/aem-core-cif-components) 核心元件為緊密整合[提供了從用戶端交互（如添加到購物車&#x200B;__）__&#x200B;轉發店面事件及其數據的Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en)。

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)專案為Adobe Systems Commerce提供了一個稱為Adobe Experience Platform連接器的[JavaScript 資料庫，用於從Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector)店面收集事件資料。該事件資料被發送到用於其他Adobe Experience Cloud產品（如Adobe Analytics和Adobe Target）的Experience Platform，以版本編號覆蓋客戶歷程的 360 度設定檔。 通過將商務數據連接到Adobe Experience Cloud中的其他產品，您可以執行任務按讚分析網站上的用戶行為、執行 AB 測試以及創建個人化廣告系列。

詳細了解 [Experience Platform 数据收集](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) 技術套件，這些技術允許您從用戶端源收集客戶體驗數據。

## 傳送 `addToCart` 要Experience Platform的事件資料 {#send-addtocart-to-aep}

以下步驟演示如何使用 CIF - Experience Platform 連接器將事件資料從AEM呈現的產品頁面發送到 `addToCart` Experience Platform。 使用 Adobe Experience Platform 調試程序 瀏覽器 擴充功能，可以測試和檢閱提交的數據。

![在 Adobe Experience Platform Debugger 中檢閱 addToCart 事件資料](../assets/aep-integration/EventData-AEM-AEP.png)

## 先決條件 {#prerequisites}

請使用本機開發環境來完成此示範。 這包括已設定並連接到 Adobe Systems Commerce 執行個體的正在運行的AEM執行個體。 檢閱使用 AEM 作為 Cloud Service SDK](../develop.md) 設定本機開發的需求[和步驟。

您還需要訪問 [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) 和許可權，才能為資料彙集創建綱要、資料集和數據流。 更多資訊，請參見 [許可權管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html)。

## AEM商務即Cloud Service設定 {#aem-setup}

要使用必要的代碼和配置使工作 __AEM Commerce 作為Cloud Service__ 本地環境，請完成以下步驟。

### 本機設定

按照「本機設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup)」[步驟操作，以便您AEM商務作為Cloud Service 環境運作。

### 專案設定

按照 [“AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) ”步驟操作，以便可以創建品牌的新AEM商務 （CIF） 專案。

>[!TIP]
>
>在以下範例中，AEM Commerce 專案的名稱為： `My Demo Storefront`，但是，您可以選擇自己的項目名稱。

![AEM商務專案](../assets/aep-integration/aem-project-with-commerce.png)


從專案的根目錄執行下列命令，建置已建立的AEM Commerce專案並將其部署至本機AEM SDK。

```bash
$ mvn clean install -PautoInstallSinglePackage
```

本機部署 `My Demo StoreFront` 具有預設程式碼和內容的商務網站如下所示：

![預設AEM Commerce網站](../assets/aep-integration/demo-aem-storefront.png)

### 安裝 Peregrine 和 CIF-AEP 連接器依賴項

若要從此 AEM Commerce 網站的類別頁和產品頁收集和發送事件資料，請將密鑰 `npm` 包安裝到 `ui.frontend` AEM Commerce 專案的模組中。

導航到 `ui.frontend` 模組並通過從命令行運行以下命令來安裝所需的包。

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
>有時需要該參數， `--force` 因為 [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) 對支援的對等依賴項有限制。 通常，這應該不會導致任何問題。


### 設定 Maven 以使用 `--force` 自變數

作為 Maven 版本編號 過程的一部分，將觸發 npm 全新安裝（使用 `npm ci`）。 這也需要 `--force` 論證。

導航到專案的根 POM 檔 `pom.xml` 並找到 `<id>npm ci</id>` 執行塊。 更新區塊，使其看起來按讚以下內容：

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

### 變更 Babel 設定格式

從預設 `.babelrc` 檔相對配置檔格式 `babel.config.js` 切換到格式。 這是一個專案範圍的配置格式，允許將外掛程式和預設應用於具有更大控制權的`node_module`

1. 導航到 `ui.frontend` 模組並刪除現有 `.babelrc` 檔。

1. `babel.config.js`建立使用`peregrine`預設集的檔。

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

### 配置 webpack 使用 Babel

要使用 Babel 載入器 （`babel-loader`） 和 webpack 轉譯 JavaScript 檔，請編輯 `webpack.common.js` 該檔。

導航到 `ui.frontend` 模組並更新 `webpack.common.js` 文件，以便在屬性值中 `module` 具有以下規則：

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### 設定 Apollo 用戶端

[Apollo 用戶端](https://www.apollographql.com/docs/react/)用於使用 GraphQL 管理本地和遠端數據。它還將 GraphQL 查詢的結果存儲在本地規範化的記憶體緩存中。

為了 [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) 有效地工作，您需要一個 `possibleTypes.js` 檔。 要生成此檔，請參閱 [自動生成](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically) possibleType。 [另請參閱PWA Studio參考實施](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120)和文件示例[`possibleTypes.js`](../assets/aep-integration/possibleTypes.js)。


1. 導航到 `ui.frontend` 模組並將檔另存為 `./src/main/possibleTypes.js`

1. 更新`DefinePlugin`檔案的`webpack.common.js`区段，以便您能在這段時間內取代必要的靜態變數版本編號。

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

### 初始化 Peregrine 和 CIF 核心元件

要初始化基於 React 的 Peregrine 和 CIF 核心元件，請創建所需的配置和JavaScript檔。

1. 瀏覽到 `ui.frontend` 模組並建立以下資料夾： `src/main/webpack/components/commerce/App`

1. 建立 `config.js` 包含下列內容的檔案：

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
           eventForwarding: {
               acds: true,
               aep: false,
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >雖然您可能已經熟悉 [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) 檔案來源 __AEM Guides - CIF Venia專案__，您必須對此檔案進行一些變更。 首先，檢閱任何 __待辦事項__ 評論。 然後，在內部 `eventsCollector` 屬性，尋找 `eventsCollector > aep` 物件並更新 `orgId` 和 `datastreamId` 屬性至正確的值。 [深入了解](./aep.md#add-aep-values-to-aem)。

1. 建立 `App.js` 檔案包含下列內容。 此檔案類似典型的React應用程式起點檔案，並包含React和自訂鉤點以及React Context使用方式，以促進Experience Platform整合。

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
           // implement a proper marketing opt-in, for demo purpose you hard-set the consent cookie
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

   匯出 `EventCollectorContext` React 上下文，其中：

   - 載入 commerce-events-sdk 和 commerce-events-collector 資料庫，
   - 使用Experience Platform和/或 ACDS 的給定配置初始化它們
   - 訂閱來自 Peregrine 的所有事件並將其轉發到事件 SDK

   您可以在此處查看實施`EventCollectorContext`[](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js)詳細信息。

### 生成並部署更新的AEM專案

若要確保上述包安裝、代碼和配置更改正確，請使用以下 Maven 命令重新生成並部署更新的 AEM Commerce 專案： `$ mvn clean install -PautoInstallSinglePackage`。

## Experience Platform設定 {#aep-setup}

要接收並商店來自 AEM Commerce 頁面（如類別和產品）的事件資料，請完成以下步驟：

>[!AVAILABILITY]
>
>確定您屬於「Adobe Experience Platform與Adobe Experience Platform數據收集&#x200B;__」下__&#x200B;的正確&#x200B;__產品設定檔。__ ____&#x200B;如有需要，請與系統管理員合作，在Admin Console下建立、更新或指派&#x200B;__產品配置檔__。[](https://adminconsole.adobe.com/)

### 使用商務欄位群組建立結構描述

若要定義商務事件資料的結構，您必須建立體驗資料模型(XDM)結構描述。 綱要是一組表示和驗證數據結構和格式的規則。

1. 在瀏覽器中，導覽至 __Adobe Experience Platform__ 產品首頁。 例如，<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 找到 __方案__ 功能表在左側導覽區段中，按一下 __建立結構描述__ 按鈕，然後選取 __XDM ExperienceEvent__.

   ![AEP建立結構描述](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. 使用架構屬性 >显示名稱字段命名&#x200B;__綱要，並使用組合>字段組添加字段組__>添加&#x200B;____&#x200B;按鈕。

   ![AEP 架構定義](../assets/aep-integration/AEP-Schema-Definition.png)

1. 在「添加欄位組&#x200B;__」__&#x200B;對話框中，搜尋`Commerce`選中「__商務詳細信息__」複選框，然後按兩下「__添加字段組__」。。

   ![AEP 架構定義](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>[有關詳細資訊，請參閱綱要組合](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html)的基礎知識。

### 建立數據集

若要商店事件資料，必須創建符合綱要定義的數據集。 資料集是包含綱要（列）和字段（行）的數據集合（通常是表）的儲存和管理構造。

1. 在瀏覽器中，導航到 __Adobe Experience Platform__ 產品主頁頁面。 例如，<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 找到 __左側導覽部分中的數據集__ 功能表，然後按下 __右上角的建立 資料集__ 按鈕。

   ![AEP 建立數據集](../assets/aep-integration/AEP-Datasets-Create.png)

1. 在新頁面上，選取 __從結構描述建立資料集__ 卡片。

   ![AEP建立資料集結構選項](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

   在新頁面上， __搜尋並選取__ 您在上一步建立的綱要，然後按一下 __下一個__ 按鈕。

   ![AEP 建立數據集 選取結構](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. 使用配置資料集 >名稱&#x200B;__字段命名__&#x200B;數據集，然後按下&#x200B;__完成__&#x200B;按鈕。

   ![AEP 建立數據集名稱](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>有關詳細資訊， [請參閱數據集概述](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) 。


### 建立數據流

完整應用程式以下步驟，以便您可以在Experience Platform中創建数据流。

1. 在瀏覽器中，導航到 __Adobe Experience Platform__ 產品主頁頁面。 例如，<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 找到左側導覽部分中的數據流&#x200B;____&#x200B;功能表，然後按下&#x200B;__右上角新__&#x200B;數據流按鈕。

   ![AEP 建立數據流](../assets/aep-integration/AEP-Datastream-Create.png)

1. 使用名稱&#x200B;__必填欄位命名__&#x200B;數據流。在事件&#x200B;__架構欄位下，選擇創建的綱要，然後按下儲存____。__

   ![AEP 定義數據流](../assets/aep-integration/AEP-Datastream-Define.png)

1. 打開創建的數據流，然後按下添加 __服務__。

   ![AEP 數據流添加服務](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. __在 服務__ 欄位下，選擇 __Adobe Experience Platform__ 選項。在事件數據集欄位下&#x200B;__，選擇上一步中的資料集名稱，然後按下儲存____。__

   ![AEP 數據流 添加服務詳細資訊](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>有關詳細資訊， [請參閱數據流概述](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) 。

## 將數據流值新增至 AEM Commerce 設定中 {#add-aep-values-to-aem}

完成上述Experience Platform設置后，您應該在數據流詳細信息的左側邊欄和`orgId`“用戶資訊&#x200B;__”模式>“個人資料圖片”>“帳戶資訊”的__&#x200B;右上角。`datastreamId`

![AEP 數據流ID](../assets/aep-integration/AEP-Datastream-ID.png)

1. 在 AEM Commerce 專案的 `ui.frontend` 模組中，更新 `config.js` 檔，特別是 `eventsCollector > aep` 對象屬性。

1. 建立並部署更新的 AEM Commerce 專案


## 觸發 `addToCart` 事件並驗證資料彙集 {#event-trigger-verify}

上述步驟即可完成 AEM Commerce 和 Experience Platform 設定。 現在 `addToCart` ，您可以使用Google鉻黃 擴充功能 _Snowplow Inspector_ 觸發事件並驗證資料彙集，並在產品UI中切換資料集 __量度和圖形__ 。

若要觸發事件，您可以使用本機設定中的AEM作者或發佈服務。 對於此示例，請通過記錄AEM帳戶來使用作者。

1. 從網站頁面，選取 __我的示範StoreFront >我們> en__ 頁面並按一下 __編輯__ 在頂端動作列中。

1. 在頂端動作列中，按一下 __以發佈的形式檢視__，然後按一下店面導覽列中的任何偏好類別。

1. 按一下中任何偏好產品卡 __產品頁面__，然後選取 __顏色，大小__ 以啟用 __加入購物車__ 按鈕。


1. __從瀏覽器的擴展面板中打開掃雪車檢查器__&#x200B;擴展，然後在左側邊欄中選擇&#x200B;__Experience Platform週三 SDK__。


1. 返回到 __產品頁面__ ，然後按下 __添加到購物車__ 按鈕。 這會將數據傳送到Experience Platform。 Adobe Experience Platform Debugger __擴充功能會顯示__&#x200B;事件詳細資訊。

   ![AEP Debugger 新增到購物車事件數據](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. 在Experience Platform產品UI中，導航到&#x200B;__“數據集活動__&#x200B;標籤>我的演示店面&#x200B;____”下的“數據集”。如果啟用了量度和圖形&#x200B;__，則__&#x200B;會顯示事件數據的統計數據。

   ![Experience Platform數據集數據統計數據](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## 實施詳細數據 {#implementation-details}

[CIF Experience Platform 連接器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector)構建在 Adobe Systems Commerce](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html) 的數據連接之上[，這是 PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) 專案的一部分[。

透過 PWA Studio 專案，您可以建立由 Adobe Systems Commerce 或 Magento Open Source 提供支援的 Progressive Web Application （PWA） 店面。 該專案還包含一個名為 Peregrin 的 [元件資料庫](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) ，用於向可視元件添加邏輯。 [Peregrin 資料庫](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/)還提供了 CIF Experience Platform Connector](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) 使用的[自定義 React 鉤子，以無縫整合 Experience Platform。


## 支援的事件 {#supported-events}

截至目前，支援以下事件：

__體驗XDM活動：__

1. 加入購物車(AEM)
1. 檢視頁面(AEM)
1. 檢視產品(AEM)
1. Search 已傳送請求 （AEM）
1. 收到Search回應 （AEM）

當 Peregrine 元件](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/)在 AEM Commerce 項目中重複使用時[：

__體驗XDM活動：__

1. 從購物車移除
1. 開啟購物車
1. 檢視購物車
1. 即時購買
1. 開始結帳
1. 完整應用程式結帳

__設定檔案 XDM 事件：__

1. 登入
1. 建立帳戶
1. 編輯帳戶


## 其他資源 {#additional-resources}

如需詳細資訊，請參閱下列資源：

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [[!DNL Data Connection] 概述](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html)
- [[!DNL Data Connection] 事件](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)
- [Adobe Experience Platform概述](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
