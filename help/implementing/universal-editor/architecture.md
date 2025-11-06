---
title: Universal Editor 架構
description: 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
exl-id: e6f40743-0f21-4fb6-bf23-76426ee174be
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 100%

---


# Universal Editor 架構 {#architecture}

了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。

## 架構建置區塊 {#building-blocks}

Universal Editor 由四個基本建置區塊組成，這些建置區塊可進行互動，讓內容作者在任意實作中編輯任何方面的內容，以便提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。

1. [編輯](#editors)
1. [遠端應用程式](#remote-app)
1. [API 層](#api-layer)
1. [持續性層](#persistence-layer)

本文件概述所有建置區塊，及其如何交換資料。

![Universal Editor 的架構](assets/architecture.png)

>[!TIP]
>
>若要查看 Universal Editor 及其架構，請參閱[AEM 中 Universal Editor 快速入門](getting-started.md)，了解如何存取 Universal Editor，和如何開始檢測您的第一個 AEM 應用程式以使用它。

### 編輯 {#editors}

* **Universal Editor** - Universal Editor 使用經過檢測的 DOM 來就地編輯內容。如需必要中繼資料的詳細資訊，請參閱[屬性和類型](attributes-types.md)。請參閱 [AEM 中通用編輯器快速入門](getting-started.md)文件，了解 AEM 中的檢測範例。
* **屬性面板** - 元件的某些屬性無法在內容中進行編輯，例如輪播的切換時間，或哪個摺疊式標籤應該一直開啟或關閉。為了能夠編輯這類元件資訊，編輯器的側面板提供表單型編輯器。

### 遠端應用程式 {#remote-app}

要在 Universal Editor 中編輯應用程式內容，就必須對 DOM 進行檢測。遠端應用程式必須在 DOM 中呈現某些屬性。如需必要中繼資料的詳細資訊，請參閱[屬性和類型](attributes-types.md)。請參閱 [AEM 中通用編輯器快速入門](getting-started.md)文件，了解 AEM 中的檢測範例。

Universal Editor 致力於最小化 SDK，因此檢測是遠端應用程式實作的責任。

### API 層 {#api-layer}

* **內容資料** - 對於 Universal Editor，內容資料的來源系統和使用方式都不重要。使用內容中可編輯資料定義和提供所需的屬性很重要。
* **持續性資料** - 每個可編輯資料都有 URN 識別碼。此 URN 用於將持續性路由到正確的系統和資源。

### 持續性層 {#persistence-layer}

* **內容片段模型** - 若要支援編輯內容片段屬性的面板、內容片段編輯器和表單型編輯器，需要每個元件和內容片段的模型。
* **內容** - 內容可以儲存在任何地方，例如 AEM、Magento 等等。

![持續性層](assets/persistence-layer.png)

## Universal Editor 服務和後端系統分派 {#service}

Universal Editor 將所有內容變更分派到稱為 Universal Editor Service 的集中服務。該服務是在 Adobe I/O Runtime 上執行，其會根據提供的 URN 載入擴展註冊表中可用的外掛程式。該外掛程式負責與後端通訊並傳回統一的回應。

![Universal Editor 服務](assets/universal-editor-service.png)

## 轉譯管道 {#rendering-pipelines}

### 伺服器端轉譯 {#server-side}

![伺服器端轉譯](assets/server-side.png)

### 靜態網站生成 {#static-generation}

![靜態網站生成](assets/static-generation.png)

### 用戶端轉譯 {#client-side}

![用戶端轉譯](assets/client-side.png)
