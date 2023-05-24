---
title: 開始在 AEM 中使用 Angular 建立 SPA
description: 本文介紹了一個SPA應用計畫範例，說明它是如何組合在一起的，並可讓您使用Angular框架快速啟動並執行您自己的SPA。
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 11%

---

# 開始在 AEM 中使用 Angular 建立 SPA {#getting-started-with-spas-in-aem-using-angular}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能夠使用SPA架構建立網站，而作者則希望能夠順暢地編輯使用SPA架構建立之網站的AEM內容。

SPA製作功能提供全方位的解決方案，可支援AEM中的SPA。 本文介紹Angular架構上的簡化SPA應用程式，說明它是如何組合在一起的，讓您能夠快速啟動並執行自己的SPA。

>[!NOTE]
>
>本文章以Angular架構為基礎。 如需React架構的對應檔案，請參閱 [AEM中的SPA快速入門 — React](getting-started-react.md).

## 簡介 {#introduction}

本文概述簡單的SPA的基本功能，以及您需要瞭解的最低運作要求。

如需SPA在AEM中運作方式的詳細資訊，請參閱下列檔案：

* [SPA 簡介和逐步解說](introduction.md)
* [SPA 編輯器概觀](editor-overview.md)
* [SPA 藍圖](blueprint.md)

>[!NOTE]
>
>為了能夠在SPA內製作內容，內容必須儲存在AEM中，並由內容模型公開。
>
>若在SPA外部開發的AEM不遵守內容模型合約，將無法編寫。

本檔案將逐步解說簡化SPA的結構，並說明其運作方式，讓您可將此瞭解套用至自己的SPA。

## 相依性、設定和建置 {#dependencies-configuration-and-building}

除了預期的Angular相依性之外，範例SPA還可以運用其他程式庫，以更有效率地建立SPA。

### 相依性 {#dependencies}

此 `package.json` file定義整體SPA套件的需求。 此處列出最低必要的AEM相依性。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

此 `aem-clientlib-generator` 會運用，以便在建置流程中自動建立使用者端程式庫。

`"aem-clientlib-generator": "^1.4.1",`

如需更多相關詳細資訊，請參閱 [在此填入GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

此 `aem-clientlib-generator` 已設定於 `clientlib.config.js` 檔案如下所示。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

實際建立應用程式運用 [網頁元件](https://webpack.js.org/) 用於整合，以及用於自動建立使用者端程式庫的aem-clientlib-generator。 因此， build指令將類似於：

`"build": "ng build --build-optimizer=false && clientlib",`

建置後，可將套件上傳至AEM執行個體。

### AEM 專案原型 {#aem-project-archetype}

任何 AEM 專案都應利用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，它支援使用 React 或 Angular 的 SPA 專案並利用 SPA SDK。

## 應用程式結構 {#application-structure}

如前所述，包含相依性並建置應用程式後，您將會擁有可上傳至AEM執行個體的有效SPA套件。

本檔案的下一節將帶您瞭解AEM中SPA的結構、驅動應用程式的重要檔案，以及它們如何協同運作。

簡化的影像元件可作為範例，但應用程式的所有元件都以相同的概念為基礎。

### app.module.ts {#app-module-ts}

SPA的進入點為 `app.module.ts` 此處顯示的檔案已簡化，以專注於重要內容。

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

此 `app.module.ts` file是應用程式的起點，並包含初始專案設定和使用 `AppComponent` 以啟動應用程式。

#### 靜態具現化 {#static-instantiation}

使用元件範本以靜態方式例項化元件時，值必須從模型傳遞至元件的屬性。 模型的值會以屬性的形式傳遞，以便稍後作為元件屬性使用。

### app.component.ts {#app-component-ts}

一次 `app.module.ts` 啟動程式 `AppComponent`，然後它可以初始化應用程式，此處以簡化版顯示，以專注於重要內容。

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

透過處理頁面， `app.component.ts` 呼叫 `main-content.component.ts` 此處以簡化版列出。

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

此 `MainComponent` 擷取頁面模型的JSON表示法，並處理內容以包裝/裝飾頁面的每個元素。 進一步詳細資訊，請參閱 `Page` 可以在檔案中找到 [SPA Blueprint](blueprint.md).

### image.component.ts {#image-component-ts}

此 `Page` 是由元件所組成。 擷取JSON後， `Page` 可以處理這些元件，例如 `image.component.ts` 如下所示。

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

AEM中SPA的核心想法是將SPA元件對應至AEM元件，並在修改內容時更新元件（反之亦然）。 檢視檔案 [SPA編輯器概觀](editor-overview.md) 以取得此通訊模式的摘要。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

此 `MapTo` 方法會將SPA元件對應至AEM元件。 它支援使用單一字串或字串陣列。

`ImageEditConfig` 是組態物件，可為編輯器提供產生預留位置所需的中繼資料，進而協助您啟用元件的製作功能

如果沒有內容，則會提供標籤做為預留位置，以代表空白內容。

#### 動態傳遞的屬性 {#dynamically-passed-properties}

來自模型的資料會以元件屬性的形式動態傳遞。

### image.component.html {#image-component-html}

最後，影像可以在中演算 `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA元件之間共用資訊 {#sharing-information-between-spa-components}

單頁應用程式內的元件通常需要共用資訊。 有幾種建議的方法可以達成此目的，依複雜度遞增的順序列示如下。

* **選項1：** 將邏輯集中並廣播至必要的元件，例如使用util類別作為純物件導向的解決方案。
* **選項2：** 使用NgRx等狀態程式庫共用元件狀態。
* **選項3：** 自訂和擴充容器元件，以善用物件階層。

## 後續步驟 {#next-steps}

* [開始在 AEM 中使用 React 建立 SPA](getting-started-react.md)展示如何在 AEM 中使用 React 建立基本 SPA 以與 SPA 編輯器搭配運作.
* [SPA 編輯器概述](editor-overview.md)更深入地介紹 AEM 和 SPA 之間的通訊模型。
* [WKND SPA專案](wknd-tutorial.md) 是逐步教學課程，在AEM中實作簡單的SPA專案。
* [SPA的動態模型到元件對應](model-to-component-mapping.md) 說明動態模型到元件的對應，以及它如何在AEM的SPA中運作。
* [SPA Blueprint](blueprint.md) 讓您深入瞭解SPA SDK for AEM的運作方式，以防您想要在AEM中針對React或Angular以外的架構實作SPA，或只是想要更深入的瞭解。
