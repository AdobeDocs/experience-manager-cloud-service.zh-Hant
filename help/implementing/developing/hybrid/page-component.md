---
title: 頁SPA面元件
description: 在頁SPA面元件中，不提供其子元件的HTML元素，而是將其委託到框架SPA中。 此文檔說明如何使頁面元件SPA唯一。
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# 頁SPA面元件 {#spa-page-component}

的頁元件不SPA會通過JSP或HTL檔案和資源對象提供其子元件的HTML元素。 此操作已委託到該SPA框架。 子元件的表示被提取為JSON資料結構（即模型）。 然SPA後，根據提供的JSON模型將元件添加到頁面。 因此，頁面元件初始主體組合不同於其預呈現的HTML對應體。

## 頁面模型管理 {#page-model-management}

頁面模型之解決方案及管理已委託 [`PageModelManager`](blueprint.md#pagemodelmanager) 中。 必SPA須與 `PageModelManager` 初始化模組以獲取初始頁面模型並註冊模型更新時生成的模組 — 主要是在作者通過頁面編輯器編輯頁面時生成的。 的 `PageModelManager` 可由項SPA目作為npm包訪問。 當一AEM個SPA翻譯 `PageModelManager` 是為了陪伴SPA。

要允許建立頁面，請使用名為 `cq.authoring.pagemodel.messaging` 必須添加以提供頁面編輯器SPA和頁面編輯器之間的通信通道。 如果頁SPA面元件從頁面wcm/core元件繼承，則有以下選項可使 `cq.authoring.pagemodel.messaging` 客戶端庫類別可用：

* 如果模板是可編輯的，請將客戶端庫類別添加到頁面策略中。
* 使用 `customfooterlibs.html` 的子菜單。

別忘了限制 `cq.authoring.pagemodel.messaging` 的上下文。

## 通信資料類型 {#communication-data-type}

通信資料類型是使用Page元件內AEM的HTML元素 `data-cq-datatype` 屬性。 當通信資料類型設定為JSON時，GET請求會命中元件的Sling Model終結點。 在頁面編輯器中發生更新後，更新元件的JSON表示形式將發送到頁面模型庫。 然後，頁面模型庫會警告SPA更新。

**頁SPA面元件 —`body.html`**

```
<div id="page"></div>
```

除了不延遲DOM生成的良好做法外，該SPA框架還要求在主體末尾添加指令碼。

**頁SPA面元件 —`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述內容的元資源屬SPA性：

**頁SPA面元件 —`customheaderlibs.html`**

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
>當請求元件的「吊帶模型」表示時，將靜態設定預設模型選取器。

## 中繼屬性 {#meta-properties}

* `cq:wcmmode`:編輯器的WCM模式（例如頁面、模板）
* `cq:pagemodel_root_url`:應用的根模型的URL。 直接訪問子頁時至關重要，因為子頁模型是應用根模型的片段。 的 `PageModelManager` 然後系統地將應用程式初始模型重構為從其根入口點進入應用程式。
* `cq:pagemodel_router`:啟用或禁用 [`ModelRouter`](routing.md) 的 `PageModelManager` 庫
* `cq:pagemodel_route_filters`:用逗號分隔的清單或規則運算式來提供路由 [`ModelRouter`](routing.md) 必須忽略。

## 頁面編輯器覆蓋同步 {#page-editor-overlay-synchronization}

覆蓋的同步由MS提供的同一變異觀測器保證 `cq.authoring.page` 的子菜單。

## Sling模型JSON導出結構配置 {#sling-model-json-exported-structure-configuration}

啟用路由功能後，假設JSON導出包含SPA應用程式的不同路由，這要歸功於導航元件的JSONAEM導出。 導航元件的JSONAEM輸出可通過以下兩SPA個屬性在根頁內容策略中配置：

* `structureDepth`:與導出的樹的深度對應的編號
* `structurePatterns`:與要導出的頁面對應的區域陣列的規則運算式
