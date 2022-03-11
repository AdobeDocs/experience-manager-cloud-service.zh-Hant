---
title: RemotePage元件
description: RemotePage元件是一個自定義頁面元件，用於編輯遠程SPAReact在AEM中。
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: eaa59b6ecfa50c4a6b4e316e5e305e48cb3d5676
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# RemotePage元件 {#remote-page-component}

在決定 [整合級別](/help/implementing/developing/headful-headless.md) 您希望在外部和SPAAEM之間使用，您通常需要能夠查看和編輯SPA內部AEM。 RemotePage元件是僅用於此目的的自定義頁面元件。

## 概覽 {#overview}

RemotePage元件從應用程式生成的所有必需資產中提取 `asset-manifest.json` 並用於在中SPA顯示AEM。

* RemotePage允許您在Page元件的正文中SPA插入指令碼和樣AEM式表。
* 虛擬前端元件允許在編輯器中將節標籤為可AEM編SPA輯。
* 同時，可SPA以在中將托管在不同域上的內容AEM編輯。

請參閱文章 [編輯SPA外部AEM](editing-external-spa.md) 的子菜單。

## 要求 {#requirements}

* 在開發中啟用CORS
* 在頁屬性中配置遠程URL
* 在SPA中呈AEM現
* Web應用程式必須使用綁定器資產清單（如下列之一），並公開 `asset-manifest.json` 列在 `entrypoints property` 要載入的所有CSS和JS檔案：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
      ![entrypoints屬性示例](assets/asset-manifest-entrypoints.png)
* 應用程式必須能夠在 `<div id="root"></div>` 下面 `body` 的子菜單。 如果應用程式需要不同的標籤來實例化，則必須在具有 `sling:resourceSuperType="spa-project-core/components/remotepage`。

## 限制 {#limitations}

* RemotePage元件的當前實現僅支援遠程React應用程式。
* 在中執行遠程呈現時，應用程式的根HTML檔案中定義的內部CSS以及根DOM節點上的內聯CSS將不可AEM用。

## 技術詳細資訊 {#technical-details}

與項目的其AEM余部SPA分一樣，RemotePage元件是開源的。 有關RemotePage元件的全部技術詳細資訊， [請參閱GitHub儲存庫。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
