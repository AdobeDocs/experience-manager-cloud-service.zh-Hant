---
title: SPA頁面元件
description: 在SPA中，頁面元件不提供其子元件的HTML元素，而是將此元素委派至SPA架構。 本檔案說明如何讓SPA的頁面元件獨一無二。
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# SPA頁面元件{#spa-page-component}

SPA的頁面元件不會透過JSP或HTL檔案和資源物件提供其子元件的HTML元素。 此操作已委派給SPA架構。 子元件的表示方式會以JSON資料結構（即模型）擷取。 接著會根據提供的JSON模型，將SPA元件新增至頁面。 因此，頁面元件初始內文組成與其預先轉譯的HTML對應不同。

## 頁面模型管理{#page-model-management}

頁面模型的解析度和管理被委派給提供的[`PageModelManager`](blueprint.md#pagemodelmanager)模組。 SPA在初始化時必須與`PageModelManager`模組互動，以擷取初始頁面模型並註冊模型更新 — 大部分是當作者透過頁面編輯器編輯頁面時產生。 `PageModelManager`可由SPA專案作為npm套件存取。 `PageModelManager`是AEM與SPA之間的翻譯，應與SPA搭配使用。

若要允許製作頁面，必須新增名為`cq.authoring.pagemodel.messaging`的用戶端程式庫，以提供SPA與頁面編輯器之間的通訊通道。 如果SPA頁面元件繼承自頁面wcm/core元件，則有下列選項可讓`cq.authoring.pagemodel.messaging`用戶端程式庫類別可用：

* 如果模板是可編輯的，請將客戶端庫類別添加到頁面策略中。
* 使用頁面元件的`customfooterlibs.html`新增用戶端程式庫類別。

別忘了將`cq.authoring.pagemodel.messaging`類別納入頁面編輯器的內容。

## 通信資料類型{#communication-data-type}

通訊資料類型是使用`data-cq-datatype`屬性在AEM頁面元件內設定HTML元素。 當通訊資料類型設為JSON時，GET要求會點擊元件的Sling模型端點。 在頁面編輯器中發生更新後，更新元件的JSON表示會傳送至頁面模型程式庫。 然後頁面模型程式庫會警告SPA有更新。

**SPA頁面元件 —`body.html`**

```
<div id="page"></div>
```

除了非是避免延遲DOM產生的良好作法，SPA架構還需要在內文結尾新增指令碼。

**SPA頁面元件 —`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述SPA內容的元資源屬性：

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
>請求元件的「Sling模型」表示時，會靜態設定預設模型選取器。

## 中繼屬性 {#meta-properties}

* `cq:wcmmode`:編輯器的WCM模式（例如頁面、範本）
* `cq:pagemodel_root_url`:應用程式的根模型URL。直接存取子頁面時非常重要，因為子頁面模型是應用程式根模型的片段。 然後，`PageModelManager`系統地重新組合應用程式初始模型以從其根入口點進入應用程式。
* `cq:pagemodel_router`:啟用或停 [`ModelRouter`](routing.md) 用程 `PageModelManager` 式庫
* `cq:pagemodel_route_filters`:以逗號分隔的清單或規則運算式，以提供必須 [`ModelRouter`](routing.md) 忽略的路由。

## 頁面編輯器覆蓋同步{#page-editor-overlay-synchronization}

覆蓋的同步由`cq.authoring.page`類別提供的非常相同的變異觀測器保證。

## Sling模型JSON匯出結構設定{#sling-model-json-exported-structure-configuration}

啟用路由功能後，假設SPA的JSON匯出包含應用程式的不同路由，這要歸功於AEM導覽元件的JSON匯出。 AEM導覽元件的JSON輸出可透過下列兩個屬性，在SPA根頁面內容原則中設定：

* `structureDepth`:與導出的樹的深度相對應的數字
* `structurePatterns`:與要匯出的頁面對應之規則陣列的規則運算式
