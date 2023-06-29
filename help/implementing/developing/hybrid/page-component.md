---
title: SPA 頁面元件
description: 在SPA中，頁面元件不會提供其子元件的HTML元素，而是將其委派給SPA架構。 本檔案說明如何藉此讓SPA的頁面元件具有唯一性。
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 8%

---

# SPA 頁面元件 {#spa-page-component}

SPA的頁面元件不會透過JSP或HTL檔案和資源物件提供其子元件的HTML元素。 此操作委託給 SPA 框架。子元件的表示會擷取為JSON資料結構（即模型）。 SPA元件會接著根據提供的JSON模型新增至頁面。 因此，頁面元件初始內文構成與其預先演算的HTML對應內容不同。

## 頁面模型管理 {#page-model-management}

頁面模型的解析度和管理會委派給提供的 [`PageModelManager`](blueprint.md#pagemodelmanager) 模組。 SPA必須與 `PageModelManager` 模組時，用來擷取初始頁面模型並註冊模型更新 — 大多是在作者透過頁面編輯器編輯頁面時產生。 此 `PageModelManager` 可透過SPA project以npm套件的形式存取。 身為AEM與SPA之間的口譯員， `PageModelManager` 旨在搭配SPA。

若要允許編寫頁面，使用者端程式庫命名為 `cq.authoring.pagemodel.messaging` 必須新增，才能在SPA和頁面編輯器之間提供通訊通道。 如果SPA頁面元件繼承自頁面wcm/核心元件，則可使用下列選項來 `cq.authoring.pagemodel.messaging` 可用的使用者端資料庫類別：

* 如果範本可編輯，請將使用者端程式庫類別新增至頁面原則。
* 使用新增使用者端程式庫類別 `customfooterlibs.html` 頁面元件的URL編號。

別忘了限制納入 `cq.authoring.pagemodel.messaging` 類別至頁面編輯器的內容。

## 通訊資料類型 {#communication-data-type}

HTML通訊資料型別是在AEM頁面元件內使用 `data-cq-datatype` 屬性。 當通訊資料型別設為JSON時，GET請求會點選元件的Sling模型端點。 在頁面編輯器中完成更新後，已更新元件的 JSON 表示將傳送到頁面模型庫。然後，頁面模型程式庫會警告SPA有更新。

**SPA 頁面元件 -`body.html`**

```
<div id="page"></div>
```

除了避免延遲DOM產生的良好做法外，SPA架構還要求在本體的結尾新增指令碼。

**SPA 頁面元件 -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述SPA內容的中繼資源屬性：

**SPA 頁面元件 -`customheaderlibs.html`**

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
* `cq:pagemodel_root_url`：應用程式根模型的URL。 由於子頁面模型是應用程式根模型的片段，因此直接存取子頁面時十分重要。 此 `PageModelManager` 然後系統地將應用程式初始模型重新構成為從根進入點進入應用程式。
* `cq:pagemodel_router`：啟用或停用 [`ModelRouter`](routing.md) 的 `PageModelManager` 資料庫
* `cq:pagemodel_route_filters`：以逗號分隔的清單或規則運算式，用於提供路由 [`ModelRouter`](routing.md) 必須忽略。

## 頁面編輯器覆蓋同步 {#page-editor-overlay-synchronization}

覆蓋圖的同步化是由以下專案所提供的完全相同的變異觀察器所保證： `cq.authoring.page` 類別。

## Sling模型JSON匯出結構設定 {#sling-model-json-exported-structure-configuration}

啟用路由功能時，假設是SPA的JSON匯出包含應用程式的不同路由，這歸功於AEM導覽元件的JSON匯出。 AEM導覽元件的JSON輸出可透過下列兩個屬性，在SPA根頁面內容原則中設定：

* `structureDepth`：與匯出的樹狀結構深度對應的數字
* `structurePatterns`：對應至要匯出之頁面的規則運算式陣列規則運算式
