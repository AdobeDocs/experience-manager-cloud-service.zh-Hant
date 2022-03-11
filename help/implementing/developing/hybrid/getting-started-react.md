---
title: 使用SPA反AEM應
description: 本文介紹了一SPA個示例應用程式，說明了它的組合方式，並允許您使用React框架快速啟動和運SPA行自己的應用程式。
exl-id: 13998526-65e7-4d1b-bd47-452bad3780a2
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 1%

---

# 使用SPA反AEM應 {#getting-started-with-spas-in-aem-using-react}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能夠使用框架構建站SPA點，而作者希望無縫地編輯AEM使用框架構建的站SPA點的內容。

創SPA作功能提供了全面的解決方案，可支SPA持內AEM部。 本文介紹了SPAReact框架上的簡化應用程式，並說明了它的組合方式，使您能夠快速啟動並運SPA行。

>[!NOTE]
>
>本文基於React框架。 有關Angular框架的相應文檔，請參見 [入門 — SPAAngular](getting-started-angular.md)。

## 簡介 {#introduction}

本文概括了簡單功能的基本功SPA能，以及使您的運行所需要知道的最低值。

有關如何工作的SPA詳細AEM資訊，請參閱以下文檔：

* [介SPA紹和漫遊](introduction.md)
* [編SPA輯器概述](editor-overview.md)
* [藍SPA圖](blueprint.md)

>[!NOTE]
>
>為了能夠在內部創作內容，SPA必須將內容儲存在內AEM容模型中並由內容模型公開。
>
>如SPA果不遵守內AEM容模型合同，則在外部開發的項目將無法授權。

本文檔將介紹使用React框架建立SPA的簡化結構，並說明其工作原理，以便您可以將此理解應用到您自己SPA的。

## 依賴項、配置和構建 {#dependencies-configuration-and-building}

除了預期的React依賴關係外，示例還SPA可以利用其他庫來提高創SPA建效率。

### 相依關係 {#dependencies}

的 `package.json` 檔案定義了整個包的SPA要求。 此處列AEM出了工作的最SPA小依賴關係。

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

由於此示例基於React框架，因此有兩個React-specific依賴項在 `package.json` 檔案：

```
 react
 react-dom
```

的 `aem-clientlib-generator` 可使建立客戶端庫成為生成過程的一部分。

`"aem-clientlib-generator": "^1.4.1",`

有關此項的進一步詳細資訊，請參閱 [在GitHub上](https://github.com/wcm-io-frontend/aem-clientlib-generator)。

的 `aem-clientlib-generator` 在 `clientlib.config.js` 的下界。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### 正在建置 {#building}

實際構建應用可利用 [Webpack](https://webpack.js.org/) 除aem-clientlib-generator外，還用於自動建立客戶端庫。 因此，build命令將類似於：

`"build": "webpack && clientlib --verbose"`

生成後，可以將包上載到實AEM例。

### AEM 專案原型 {#aem-project-archetype}

任何AEM項目都應利用 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支SPA持使用React或Angular的項目，並利SPA用SDK。

## 應用程式結構 {#application-structure}

包括依賴項和生成應用程式（如前所述）將為您留SPA下一個工作包，您可以將其上載到AEM實例。

本文檔的下一節將介紹如何SPA構AEM建in 、驅動應用程式的重要檔案以及它們如何協同工作。

以簡化的影像元件為例，但應用程式的所有元件都基於相同的概念。

### index.js {#index-js}

當然，SPA進入的切入點 `index.js` 此處顯示的檔案經過簡化，可以專注於重要內容。

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

C.C.C.的主要功能 `index.js` 就是利用 `ReactDOM.render` 函式，以確定在DOM中注入應用程式的位置。

這是此函式的標準使用，不是此示例應用所獨有。

#### 靜態實例化 {#static-instantiation}

當使用元件模板（如JSX）靜態實例化元件時，必須將值從模型傳遞到元件的屬性。

### App.js {#app-js}

通過呈現應用， `index.js` 呼叫 `App.js`，此處以簡化版本顯示，重點介紹重要內容。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主要用於包裝構成應用的根元件。 任何應用的入口點都是頁面。

### Page.js {#page-js}

通過呈現頁面， `App.js` 呼叫 `Page.js` 以簡化版本列出。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

在此示例中， `AppPage` 類擴展 `Page`，其中包含可隨後使用的內容方法。

的 `Page` 接收頁面模型的JSON表示，並處理內容以包裝/裝飾頁面的每個元素。 有關 `Page` 可在文檔中找到 [藍SPA圖。](blueprint.md)

### Image.js {#image-js}

在呈現頁面時， `Image.js` 如圖所示。

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

中的核心SPA思想AEM是將元件映射SPA到元件AEM，並在修改內容時更新元件（反之亦然）。 查看文檔 [編SPA輯器概述](editor-overview.md) 獲取此通信模型的摘要。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

的 `MapTo` 方法將組SPA件映射到AEM元件。 它支援使用單個字串或字串陣列。

`ImageEditConfig` 是配置對象，它通過為編輯器提供生成佔位符所需的元資料來幫助啟用元件的創作功能

如果沒有內容，則將標籤作為佔位符提供以表示空內容。

#### 動態傳遞的屬性 {#dynamically-passed-properties}

來自模型的資料作為元件的屬性動態傳遞。

## 導出可編輯內容 {#exporting-editable-content}

可以導出元件並使其保持可編輯狀態。

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

的 `MapTo` 函式返回 `Component` 這是擴展了所提供的 `PageClass` 類名和屬性。 此元件可以導出，以便以後在應用程式的標籤中實例化。

使用 `MapTo` 或 `withModel` 函式。 `Page` 元件，用 `ModelProvider` 提供標準元件訪問頁面模型最新版本或該頁面模型中精確位置的元件。

有關詳細資訊，請參閱 [藍SPA圖文檔](blueprint.md)。

>[!NOTE]
>
>預設情況下，使用 `withModel` 的子菜單。

## 元件之間共用信SPA息 {#sharing-information-between-spa-components}

對於單頁應用程式中的元件來說，經常需要共用資訊。 有幾種建議的方法來執行此操作，其複雜程度的增加順序如下所列。

* **選項1:** 例如，使用React Context將邏輯和廣播集中到必要的元件。
* **選項2:** 使用狀態庫（如Redux）共用元件狀態。
* **備選3:** 通過自定義和擴展容器元件來利用對象層次結構。

## 後續步驟 {#next-steps}

* [使用AngularSPA入門AEM](getting-started-angular.md) 顯示如何構SPA建基本，以在使SPA用AngularAEM時與編輯器一起工作。
* [編SPA輯器概述](editor-overview.md) 更深入地瞭解和之間AEM的通SPA信。
* [WKND項SPA目](wknd-tutorial.md) 是在中實現簡單項目的逐步SPA教程AEM。
* [動態模型到元件的映SPA射](model-to-component-mapping.md) 將動態模型解釋為元件映射，並說明其在中SPA的工AEM作。
* [藍SPA圖](blueprint.md) 深入瞭解SPASDK的工作方AEM式，以備您希望在React或Angular之外的SPA框架AEM中實施，或只是希望更深入地瞭解。
