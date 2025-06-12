---
title: SPA 頁面元件
description: 在SPA中，頁面元件不提供其子元件的HTML元素，而是將其委派給SPA框架。 本檔案說明如何藉此讓SPA的頁面元件具有唯一性。
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 7%

---


# SPA 頁面元件 {#spa-page-component}

SPA的頁面元件不會透過JSP或HTL檔案和資源物件提供其子元件的HTML元素。 此操作委派給 SPA 框架。子元件的表示會擷取為JSON資料結構（即模型）。 接著，系統就會根據提供的JSON模型將SPA元件新增至頁面。 因此，頁面元件初始內文構成與其預先轉譯的HTML對應內容不同。

{{ue-over-spa}}

## 頁面模型管理 {#page-model-management}

頁面模型的解析度和管理已委派給提供的[`PageModelManager`](blueprint.md#pagemodelmanager)模組。 SPA在初始化以擷取初始頁面模型並註冊模型更新時（大多在作者透過頁面編輯器編輯頁面時產生），必須與`PageModelManager`模組互動。 SPA專案可以作為npm套件存取`PageModelManager`。 `PageModelManager`身為AEM與SPA之間的口譯員，應隨附SPA。

若要允許編寫頁面，必須新增名為`cq.authoring.pagemodel.messaging`的使用者端資料庫，以提供SPA與頁面編輯器之間的通訊通道。 如果SPA頁面元件繼承自頁面wcm/核心元件，則有以下選項可讓`cq.authoring.pagemodel.messaging`使用者端程式庫類別可用：

* 如果範本可編輯，請將使用者端程式庫類別新增至頁面原則。
* 使用頁面元件的`customfooterlibs.html`新增使用者端程式庫類別。

別忘了將`cq.authoring.pagemodel.messaging`類別的包含限制在頁面編輯器的內容中。

## 通訊資料類型 {#communication-data-type}

通訊資料型別是使用`data-cq-datatype`屬性在AEM頁面元件中設定HTML元素。 當通訊資料型別設為JSON時，GET請求會點選元件的Sling模型端點。 在頁面編輯器中完成更新後，已更新元件的 JSON 表示將傳送到頁面模型庫。然後，頁面模型程式庫會警告SPA有更新。

**SPA頁面元件 —`body.html`**

```
<div id="page"></div>
```

除了避免延遲DOM產生的良好實務外，SPA框架還要求將指令碼新增至內文結尾。

**SPA頁面元件 —`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

說明SPA內容的中繼資源屬性：

**SPA頁面元件 —`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>請求元件的Sling模型表示時，會靜態設定預設模型選取器。

## 中繼屬性 {#meta-properties}

* `cq:wcmmode`：編輯器的WCM模式（例如，頁面、範本）
* `cq:pagemodel_root_url`：應用程式根模型的URL。 由於子頁面模型是應用程式根模型的片段，因此直接存取子頁面時十分重要。 然後，`PageModelManager`會系統地將應用程式初始模型重新組合為從根進入點進入應用程式。
* `cq:pagemodel_router`：啟用或停用`PageModelManager`資料庫的[`ModelRouter`](routing.md)
* `cq:pagemodel_route_filters`：以逗號分隔的清單或規則運算式，提供[`ModelRouter`](routing.md)必須忽略的路由。

## 頁面編輯器覆蓋同步 {#page-editor-overlay-synchronization}

由`cq.authoring.page`類別所提供的變異觀察器可以保證覆蓋的同步化。

## Sling模型JSON匯出的結構設定 {#sling-model-json-exported-structure-configuration}

啟用路由功能時，假設是SPA的JSON匯出包含應用程式的不同路由，這要歸功於AEM導覽元件的JSON匯出。 AEM導覽元件的JSON輸出可透過下列兩個屬性，在SPA的根頁面內容原則中設定：

* `structureDepth`：與匯出之樹狀結構深度對應的數字
* `structurePatterns`：對應至要匯出之頁面的規則運算式陣列規則運算式
