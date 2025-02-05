---
title: RemotePage 元件
description: RemotePage元件是自訂頁面元件，用於在AEM內編輯遠端React SPA。
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---

# RemotePage 元件 {#remote-page-component}

在決定您要在外部SPA和AEM之間進行[何種程度的整合](/help/implementing/developing/headful-headless.md)時，通常很清楚您需要能夠檢視和編輯AEM中的SPA。 RemotePage元件是僅用於此目的的自訂頁面元件。

{{ue-over-spa}}

## 概觀 {#overview}

RemotePage元件會從應用程式產生的`asset-manifest.json`擷取所有必要的資產，並用來在AEM中轉譯SPA。

* RemotePage可讓您將SPA的指令碼和樣式表插入AEM Page元件的內文中。
* 虛擬前端元件允許在AEM SPA編輯器中將區段標示為可編輯。
* 將託管在不同網域上的SPA放在一起，即可在AEM中編輯。

請參閱[在AEM](editing-external-spa.md)中編輯外部SPA一文，以取得有關AEM中可編輯外部SPA的更多詳細資料。

## 要求 {#requirements}

* 在開發中啟用CORS
* 在頁面屬性中設定遠端URL
* 在AEM中轉譯SPA
* Web應用程式必須使用類似下列其中一種的套件組合工具資產資訊清單，並在網域根目錄公開`asset-manifest.json`檔案，該檔案會在`entrypoints property`中列出所有要載入的CSS和JS檔案：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
     ![entrypoints屬性範例](assets/asset-manifest-entrypoints.png)
* 應用程式必須能夠在`body`專案底下的`<div id="root"></div>`中初始化。 如果應用程式需要不同的標籤才能具現化，則必須在具有`sling:resourceSuperType="spa-project-core/components/remotepage`的Proxy元件的HTL指令碼中據以調整。

## 限制 {#limitations}

* RemotePage元件預期實作會提供資產資訊清單，例如此處](https://github.com/shellscape/webpack-manifest-plugin)所找到的資產[。 不過，RemotePage元件僅經過測試可用於React架構（以及透過remote-page-next元件的Next.js），因此不支援從其他架構(例如Angular)從遠端載入應用程式。
* 在AEM中執行遠端轉譯時，在應用程式的根HTML檔案中定義的內部CSS以及根DOM節點上的內嵌CSS將不可用。

## 技術細節 {#technical-details}

如同其他的AEM SPA專案，RemotePage元件是開放原始碼。 如需RemotePage元件的完整技術詳細資訊，[請參閱GitHub存放庫](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)。
