---
title: RemotePage元件
description: RemotePage元件是自訂頁面元件，可用於編輯AEM內的遠端React SPA。
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: eaa59b6ecfa50c4a6b4e316e5e305e48cb3d5676
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# RemotePage元件{#remote-page-component}

在決定[您要在外部SPA和AEM之間擁有的整合層級](/help/implementing/developing/headful-headless.md)時，通常很清楚，您需要在AEM中檢視和編輯SPA。 RemotePage元件是專門用於此目的的自定義頁面元件。

## 概覽 {#overview}

RemotePage元件從應用程式產生的`asset-manifest.json`中擷取所有必要資產，並使用它在AEM中轉譯SPA。

* RemotePage允許您在AEM Page元件的主體中插入SPA的指令碼和樣式表。
* 虛擬前端元件可讓您在AEM SPA編輯器中將區段標示為可編輯。
* 托管於不同網域的SPA可在AEM中設為可編輯。

如需AEM中可編輯外部SPA的詳細資訊，請參閱[在AEM中編輯外部SPA一文。](editing-external-spa.md)

## 需求 {#requirements}

* 啟用開發中的CORS
* 在頁面屬性中設定遠端URL
* 在AEM中呈現SPA
* Web應用程式必須使用捆綁資產資訊清單（如下列其中一項），並在網域根目錄中公開`asset-manifest.json`檔案，該根目錄會列出要載入的所有CSS和JS檔案：`entrypoints property`
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
      ![entrypoints屬性示例](assets/asset-manifest-entrypoints.png)
* 應用程式必須能夠在`body`元素下的`<div id="root"></div>`中初始化。 如果應用程式需要不同的標籤才能實例化，則必須在具有`sling:resourceSuperType="spa-project-core/components/remotepage`之Proxy元件的HTL指令碼中相應調整。

## 限制 {#limitations}

* RemotePage元件的當前實施僅支援遠程React應用程式。
* 在AEM中執行遠端轉譯時，應用程式根HTML檔案中定義的內部CSS以及根DOM節點上的內嵌CSS將無法使用。

## 技術詳細資訊{#technical-details}

與AEM SPA專案的其餘部分一樣， RemotePage元件是開放原始碼。 有關RemotePage元件的完整技術詳細資訊，請參閱GitHub儲存庫。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)[
