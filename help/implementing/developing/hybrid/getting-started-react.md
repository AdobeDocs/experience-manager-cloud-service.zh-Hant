---
title: 在AEM中使用React快速入門SPA
description: 本文提供範例SPA應用程式，說明其組合方式，並讓您使用React架構快速啟動並執行您自己的SPA。
translation-type: tm+mt
source-git-commit: cdd92032c627740c66de7b2f3836fa1dcd2ee2ca
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---


# 在AEM中使用React {#getting-started-with-spas-in-aem-using-react}快速入門使用SPA

單頁應用程式(SPA)可為網站使用者提供引人入勝的體驗。 開發人員希望能夠使用SPA架構建立網站，而作者則想在AEM中為使用SPA架構建立的網站順暢地編輯內容。

SPA製作功能提供完整的解決方案，以支援AEM中的SPA。 本文介紹React架構上的簡化SPA應用程式，並說明其組合方式，讓您快速啟動並執行自己的SPA。

>[!NOTE]
>
>本文基於React框架。 有關Angular框架的相應文檔，請參閱[AEM中SPA快速入門- Angular](getting-started-angular.md)。

## 簡介 {#introduction}

本文摘述了簡單SPA的基本功能，以及您需要瞭解的最低功能，以便讓您的SPA運作。

如需SPA在AEM中運作的詳細資訊，請參閱下列檔案：

* [SPA簡介與逐步說明](introduction.md)
* [SPA編輯器概述](editor-overview.md)
* [SPA藍圖](blueprint.md)

>[!NOTE]
>
>為了能夠在SPA中製作內容，內容必須儲存在AEM中，並由內容模型公開。
>
>如果AEM以外開發的SPA不遵守內容模型合約，則無法授權。

本檔案將逐步介紹使用React架構建立的簡化SPA的結構，並說明其運作方式，讓您將此理解套用至您自己的SPA。

## 相依性、配置和構建{#dependencies-configuration-and-building}

除了預期的React相依性外，範例SPA還可運用其他程式庫，讓建立SPA更有效率。

### 相依關係 {#dependencies}

`package.json`檔案定義了整個SPA包的要求。 此處列出工作SPA的最低AEM相依性。

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

由於此示例基於React框架，因此`package.json`檔案中必須有兩個React-specific依賴項：

```
 react
 react-dom
```

`aem-clientlib-generator`可讓建立用戶端程式庫的作業自動化，做為建立程式的一部分。

`"aem-clientlib-generator": "^1.4.1",`

有關它的詳細資訊，請在GitHub上[這裡](https://github.com/wcm-io-frontend/aem-clientlib-generator)找到。

`aem-clientlib-generator`在`clientlib.config.js`檔案中的配置如下。

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

實際建立應用程式時，除了aem-clientlib-generator以外，還運用[Webpack](https://webpack.js.org/)進行轉譯，以建立自動用戶端程式庫。 因此，build命令將類似：

`"build": "webpack && clientlib --verbose"`

建立後，套件就可以上傳至AEM例項。

### AEM Project Archetype {#aem-project-archetype}

任何AEM專案都應運用[AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)，它支援使用React或Angular的SPA專案，並運用SPA SDK。

## 應用程式結構{#application-structure}

納入相依性並依照先前所述建立應用程式，將會留下您可上傳至AEM例項的正常SPA套件。

本檔案的下一節將帶您瞭解AEM中的SPA結構、驅動應用程式的重要檔案，以及它們如何搭配運作。

以簡化的影像元件為例，但應用程式的所有元件都是以相同的概念為基礎。

### index.js {#index-js}

進入SPA的入口點當然是此處顯示的`index.js`檔案，可簡化為關注重要內容。

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

`index.js`的主要功能是運用`ReactDOM.render`函式來判斷在DOM中插入應用程式的位置。

這是此函式的標準使用，並非此範例應用程式的唯一使用。

#### 靜態實例化{#static-instantiation}

當使用元件模板（如JSX）靜態實例化元件時，必須將值從模型傳遞到元件的屬性。

### App.js {#app-js}

透過轉譯應用程式，`index.js`會呼叫`App.js`，此處會以簡化版本顯示，以專注於重要內容。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主要用來包住構成應用程式的根元件。任何應用程式的入口點都是頁面。

### Page.js {#page-js}

透過轉譯頁面，`App.js`會呼叫此處列示的簡化版本`Page.js`。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

在此示例中，`AppPage`類擴展了`Page` ，其中包含了內部內容方法，然後可以使用。

`Page`會擷取頁面模型的JSON表示法，並處理內容以包覆／裝飾頁面的每個元素。 有關`Page`的詳細資訊，請參閱[SPA Blueprint。](blueprint.md)

### Image.js {#image-js}

在呈現頁面時，可呈現如下所示的元件，如`Image.js`。

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

AEM中SPA的核心理念是將SPA元件對應至AEM元件，並在修改內容時更新元件（反之亦然）。 有關此通信模型的摘要，請參見文檔[SPA編輯器概述](editor-overview.md)。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

`MapTo`方法將SPA元件對應至AEM元件。 它支援使用單一字串或字串陣列。

`ImageEditConfig` 是配置對象，通過為編輯器提供生成佔位符所需的元資料來啟用元件的編寫功能

如果沒有內容，則會提供標籤作為預留位置來表示空內容。

#### 動態傳遞的屬性{#dynamically-passed-properties}

來自模型的資料會動態傳遞為元件的屬性。

## 導出可編輯內容{#exporting-editable-content}

您可以匯出元件並保留其可編輯性。

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

`MapTo`函式返回`Component`，該&lt;a1/>是使用類名和屬性擴展提供的`PageClass`的構圖的結果，該類名和屬性啟用了編寫。 此元件可匯出為稍後在應用程式的標籤中執行個體化。

使用`MapTo`或`withModel`函式匯出時，`Page`元件會與`ModelProvider`元件包住，此元件可讓標準元件存取頁面模型的最新版本或該頁面模型中的精確位置。

如需詳細資訊，請參閱[SPA Blueprint檔案](blueprint.md)。

>[!NOTE]
>
>預設情況下，使用`withModel`函式時，會收到元件的整個模型。

## 在SPA元件之間共用資訊{#sharing-information-between-spa-components}

單頁應用程式中的元件必須定期共用資訊。 有幾種建議的方法可做到，如下列出，增加了複雜性。

* **選項1:** 例如使用React Context將邏輯集中化並廣播至必要的元件。
* **選項2：使** 用狀態庫（如Redux）共用元件狀態。
* **選項3：自** 訂和擴充容器元件，以運用物件階層。

## 後續步驟{#next-steps}

* [使用](getting-started-angular.md) Angularar在AEM中開始使用SPA說明如何建立基本SPA，以搭配使用Angular的AEM中的SPA編輯器。
* [SPA編輯](editor-overview.md) 器概觀深入探討AEM與SPA之間的通訊模型。
* [WKND SPA ](wknd-tutorial.md) Project是在AEM中實作簡單SPA專案的逐步教學課程。
* [SPA的動態模型至元件對](model-to-component-mapping.md) 應將動態模型展示至元件對應，以及它在AEM的SPA中的運作方式。
* [SPA ](blueprint.md) Blueprintoffers深入探討AEM的SPA SDK如何運作，以防您想在AEM中針對React或Angular以外的架構實作SPA，或只是想要深入瞭解。
