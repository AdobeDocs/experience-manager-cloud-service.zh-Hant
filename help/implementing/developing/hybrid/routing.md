---
title: SPA模型路由
description: 若為AEM中的單頁應用程式，則由應用程式負責路由。 本檔案說明路由機制、合約及可用的選項。
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# SPA模型路由{#spa-model-routing}

若為AEM中的單頁應用程式，則由應用程式負責路由。 本檔案說明路由機制、合約及可用的選項。

{{ue-over-spa}}

## 專案路由 {#project-routing}

應用程式擁有路由，並由專案前端開發人員實作。 本檔案說明AEM伺服器傳回之模式的特定路由。 頁面模型資料結構會公開基礎資源的URL。 前端專案可以使用任何提供路由功能的自訂或第三方資料庫。 一旦路由預期模型片段，即可呼叫`PageModelManager.getData()`函式。 當模型路由已變更時，必須觸發事件，以警告聆聽程式庫，例如「頁面編輯器」。

## 架構 {#architecture}

如需詳細說明，請參閱SPA Blueprint檔案的[PageModelManager](blueprint.md#pagemodelmanager)區段。

## 模型路由器 {#modelrouter}

`ModelRouter` （啟用時）會封裝HTML5 History API函式`pushState`和`replaceState`，以確保預先擷取且可存取模型的指定片段。 然後通知註冊的前端元件模型已被修改。

## 手動與自動模型製程 {#manual-vs-automatic-model-routing}

`ModelRouter`會自動擷取模型的片段。 但就像任何自動化工具一樣，它也伴隨著限制。 如有需要，可停用`ModelRouter`，或將其設定為使用中繼屬性略過路徑(請參閱[SPA頁面元件](page-component.md)檔案的「Meta屬性」一節)。 前端開發人員可以透過請求`PageModelManager`使用`getData()`函式載入任何指定的模型片段，來實作他們自己的模型路由層。

>[!CAUTION]
>
>目前版本的`ModelRouter`僅支援使用指向Sling模型進入點實際資源路徑的URL。 不支援使用虛名URL或別名。

## 路由合約 {#routing-contract}

目前的實施是根據SPA專案使用HTML5 History API路由傳送到不同應用程式頁面的假設。

### 設定 {#configuration}

`ModelRouter`在偵聽`pushState`和`replaceState`預先擷取模型片段的呼叫時，支援模型路由的概念。 在內部，它會觸發`PageModelManager`載入對應到指定URL的模型，並引發其他模組可以監聽的`cq-pagemodel-route-changed`事件。

依預設，此行為會自動啟用。 若要停用，SPA應該呈現以下中繼屬性：

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

SPA的每個路由都應該對應至AEM中的可存取資源（例如，「 `/content/mysite/mypage"`」），因為一旦選取路由，`PageModelManager`將自動嘗試載入對應的頁面模型。 不過，如有需要，SPA也可以定義應由`PageModelManager`忽略的路由「區塊清單」：

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
