---
title: 使用AngularSPA入門AEM
description: 本文介紹了一SPA個示例應用程式，說明了它的組合方式，並允許您使用Angular框架快速啟動和運SPA行自己的應用程式。
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---

# 使用AngularSPA入門AEM {#getting-started-with-spas-in-aem-using-angular}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能夠使用框架構建站SPA點，而作者希望無縫地編輯AEM使用框架構建的站SPA點的內容。

創SPA作功能提供了全面的解決方案，SPA支援AEM內。 本文介紹了一SPA個簡化的Angular框架應用程式，並說明了它的組合方式，使您能夠快速啟動並運行自己的運SPA行。

>[!NOTE]
>
>本文基於Angular框架。 有關React框架的相應文檔，請參見 [入門 — SPA反AEM應](getting-started-react.md)。

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

本文檔將介紹簡化的結構，SPA並說明其工作原理，以便您可以將此理解應用到您自己的SPA結構。

## 依賴項、配置和構建 {#dependencies-configuration-and-building}

除了預期的Angular相關性外，該示例SPA還可以利用附加庫，使建立更SPA加高效。

### 相依關係 {#dependencies}

的 `package.json` 檔案定義了整個包的SPA要求。 此處列出了AEM所需的最低依賴項。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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

實際構建應用可利用 [Webpack](https://webpack.js.org/) 除aem-clientlib-generator外，還用於自動建立客戶端庫。 因此，build命令將類似於：

`"build": "ng build --build-optimizer=false && clientlib",`

生成後，可以將包上載到實AEM例。

### AEM 專案原型 {#aem-project-archetype}

任何AEM項目都應利用 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支SPA持使用React或Angular的項目，並利SPA用SDK。

## 應用程式結構 {#application-structure}

包括依賴項和生成應用程式（如前所述）將為您留SPA下一個工作包，您可以將其上載到AEM實例。

本文檔的下一節將介紹如何SPA構AEM建中的檔案、驅動應用程式的重要檔案以及它們如何協同工作。

以簡化的影像元件為例，但應用程式的所有元件都基於相同的概念。

### app.module.ts {#app-module-ts}

入口SPA是 `app.module.ts` 此處顯示的檔案經過簡化，可以專注於重要內容。

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

的 `app.module.ts` 檔案是應用程式的起點，包含初始項目配置和使用 `AppComponent` 引導應用程式。

#### 靜態實例化 {#static-instantiation}

使用元件模板靜態實例化元件時，必須將值從模型傳遞到元件的屬性。 模型中的值作為屬性傳遞，以便以後作為元件屬性可用。

### app.component.ts {#app-component-ts}

一次 `app.module.ts` 引導 `AppComponent`然後，它可以初始化應用程式，該應用程式將以簡化版本顯示在此處，以專注於重要內容。

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

通過處理頁面， `app.component.ts` 呼叫 `main-content.component.ts` 以簡化版本列出。

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

的 `MainComponent` 接收頁面模型的JSON表示，並處理內容以包裝/裝飾頁面的每個元素。 有關 `Page` 可在文檔中找到 [藍SPA圖](blueprint.md)。

### image.component.ts {#image-component-ts}

的 `Page` 是由元件組成的。 JSON接收後， `Page` 可以處理這些元件，如 `image.component.ts` 如圖所示。

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

中的核心SPA思想AEM是將元件映射SPA到元件AEM，並在修改內容時更新元件（反之亦然）。 查看文檔 [編SPA輯器概述](editor-overview.md) 獲取此通信模型的摘要。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

的 `MapTo` 方法將組SPA件映射到AEM元件。 它支援使用單個字串或字串陣列。

`ImageEditConfig` 是配置對象，它通過為編輯器提供生成佔位符所需的元資料來幫助啟用元件的創作功能

如果沒有內容，則將標籤作為佔位符提供以表示空內容。

#### 動態傳遞的屬性 {#dynamically-passed-properties}

來自模型的資料作為元件的屬性動態傳遞。

### image.component.html {#image-component-html}

最後，可在 `image.component.html`。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 元件之間共用信SPA息 {#sharing-information-between-spa-components}

對於單頁應用程式中的元件來說，經常需要共用資訊。 有幾種建議的方法來執行此操作，其複雜程度的增加順序如下所列。

* **選項1:** 將邏輯集中並廣播到必要的元件，例如，使用util類作為純物件導向的解決方案。
* **選項2:** 使用狀態庫（如NgRx）共用元件狀態。
* **備選3:** 通過自定義和擴展容器元件來利用對象層次結構。

## 後續步驟 {#next-steps}

* [使用反SPA應入AEM門](getting-started-react.md) 顯示如何構SPA建基本檔案以使用SPAReact與編AEM輯器配合使用
* [編SPA輯器概述](editor-overview.md) 更深入地瞭解和之間AEM的通SPA信。
* [WKND項SPA目](wknd-tutorial.md) 是在中實現簡單項目的逐步SPA教程AEM。
* [動態模型到元件的映SPA射](model-to-component-mapping.md) 將動態模型解釋為元件映射，並說明其在中SPA的工AEM作。
* [藍SPA圖](blueprint.md) 深入瞭解SPASDK的工作方AEM式，以備您希望在React或Angular之外的SPA框架AEM中實施，或只是希望更深入地瞭解。
