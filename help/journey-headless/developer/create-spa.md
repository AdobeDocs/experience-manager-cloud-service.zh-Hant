---
title: 選擇性 - 如何使用 Adobe Experience Manager (AEM) 建立單頁應用程式 (SPA)
description: 在 AEM Headless 開發人員歷程的此延續部分 (選擇性)，您將了解 AEM 如何將 Headless 傳遞與傳統的全堆疊 CMS 功能相結合，以及如何使用 AEM 的 SPA 編輯器框架建立可編輯的 SPA。
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 100%

---

# 如何使用 AEM 建立單頁應用程式 (SPA) {#create-spa}

在 [AEM Headless 開發人員歷程](overview.md)的此延續部分 (選擇性)，您將了解 AEM 如何將 Headless 傳遞與傳統的全堆疊 CMS 功能相結合。您也會了解如何使用 AEM 的 SPA 編輯器框架建立可編輯的 SPA，以及整合外部 SPA，以便視需要啟用編輯功能。

## 到目前為止 {#story-so-far}

此時，您應該已經完成了整個[AEM Headless 開發人員歷程](overview.md)並了解 AEM Headless 傳遞的基本知識，包括了解：

*  Headless 和 Headful 內容傳遞之間的差異。
* AEM 的 Headless 功能。
* 如何組織 AEM Headless 專案。
* 如何在 AEM 建立 Headless 內容。
* 如何在 AEM 擷取和更新 Headless 內容。
* 如何使 AEM Headless 專案上線。

到現在，您現在已經將您的第一個 AEM Headless 專案上線，或是已經掌握完成此作業的知識。恭喜！

那麼你為什麼要閱讀這個額外的、選擇性的歷程延續部分呢？您回想起[快速入門](getting-started.md#integration-levels)中我們曾討論到 AEM 不僅支援 Headless 傳遞和傳統全堆疊模型，而且還支援結兩者優點的混合模型。雖然不是傳統的 Headless 模型，但這類混合模型可以為特定專案提供前所未有的靈活性。

本文章以您對 AEM Headless 的了解為基礎，深入探討如何建立您自己的單頁應用程式 (SPA)，這些應用程式可在 AEM 中編輯。如此一來，您可以建立內容並將其以 Headless 方式傳遞到 SPA，但該 SPA 在 AEM 中仍然是可編輯的。

## 目標 {#objective}

本文件可協助您了解如何使用 AEM SPA 編輯器框架開發單頁應用程式。閱讀本文件後，您應該：

* 了解 SPA 編輯器的基本功能。
* 了解為 AEM 建立完全可編輯的 SPA 的要求。
* 了解如何將外部 SPA 整合到 AEM 中。
* 了解為何伺服器端呈現可以或不可以實作。

## 要求和先決條件 {#requirements-prerequisites}

有一些要求必須符合，才能開始在 AEM 使用 SPA。

### 知識 {#knowledge}

* 使用 React 或 Angular 框架建立 SPA 的開發經驗
* 建立內容片段和使用編輯器的基本 AEM 技能
* 務必查看文件：[AEM Headful 和 Headless 技術](/help/implementing/developing/headful-headless.md)，以便了解可能的各種 SPA 整合層級。

### 工具 {#tools}

* 用於測試部署專案的沙箱存取權
* 用於資料模型和測試的本機開發執行個體
* 現有的外部 SPA (選擇性，取決於所選的整合模型)
* AEM 專案原型

## 什麼是 SPA？ {#what-is-a-spa}

單頁應用程式 (SPA) 與傳統頁面的不同之處在於它是在用戶端呈現並且主要由 JavaScript 驅動，依賴 Ajax 呼叫來載入資料和動態更新頁面。在單頁載入時一次擷取大部分或所有內容，並根據使用者與頁面的互動，視需要非同步載入其他資源。

此功能減少了頁面重新整理的需要，讓使用者擁有順暢、快速且像是使用原生應用程式的體驗。

AEM SPA 編輯器允許前端開發人員建立可整合到 AEM 網站的 SPA，從而允許內容作者輕鬆編輯 SPA 內容，像編輯任何其他 AEM 內容一樣輕鬆。

## 為什麼是 SPA？ {#why-spa}

SPA 可以更流暢、快速且像是原生應用程式，使其成為極具吸引力的體驗。由於 SPA 的運作本質，不僅網頁訪客受益，行銷人員和開發人員也受益。

如需 SPA 的完整說明以及使用它們的原因，請參閱[其他資源](#additional-resources)章節以取得更多深入文件的連結。

## AEM 如何處理 SPA

在 AEM 開發單頁應用程式是假設前端開發人員在建立 SPA 時有遵守標準最佳做法。如果作為前端開發人員，您遵循這些一般最佳做法和一些 AEM 的特定原則，您的 SPA 可透過 AEM 及其內容編寫功能運作。

* **可攜性** - 如同任何元件，SPA 元件應盡可能建置為具可攜性。SPA 應該使用可攜帶和可重複使用的元件建置。
* **AEM 促成網站結構** - 前端開發人員建立元件並擁有其內部結構，但依賴 AEM 來定義網站的內容結構。
* **動態呈現** - 所有呈現都應該是動態的。
* **動態路由** - SPA 負責路由，AEM 會偵聽並據此進行擷取。任何路由也應該是動態的。

如需 AEM 如何處理 SPA 的完整說明，請參閱[其他資源](#additional-resources)章節以取得更多深入文件的連結。

## AEM SPA 編輯器 {#aem-spa-editor}

使用常見 SPA 框架 (例如 React 和 Angular) 建置的網站是透過動態 JSON 載入其內容。它們不提供 AEM 頁面編輯器放置編輯控制項時所需的 HTML 結構。

若要能在 AEM 中編輯 SPA，SPA 的 JSON 輸出與 AEM 存放庫中的內容模型之間必須要有對應，才能儲存內容的變更。

AEM 中的 SPA 支援帶入一個薄 JavaScript 層，在頁面編輯器中載入內容時會與 SPA JavaScript 程式碼互動，如此可以傳送事件。可以啟動編輯控制項的位置以允許進行情境式編輯。此功能是以內容服務 API 端點概念為建置基礎，因為來自 SPA 的內容必須透過內容服務載入。

如需 AEM SPA 編輯器的完整說明，請參閱[其他資源](#additional-resources)章節以取得更多深入文件的連結。

## 容納現有的 SPA {#existing-spas}

如果您已有 SPA，AEM 支援將其嵌入到 AEM，以便您的內容作者可在 AEM 編輯器看到它。對於透過內容片段建立的內容，此功能可大力協助在終端應用程式 (其會取用該內容) 的情境下檢視該內容。

此外，只需少量變更，您就可以在 AEM 編輯器中對外部 SPA 進行特定編輯。

RemotePage 元件允許在 AEM 中呈現外部 SPA。

如需如何讓外部 SPA 可在 AEM 中編輯的完整說明，請參閱[其他資源](#additional-resources)章節以取得更多深入文件的連結。

## 下一步 {#what-is-next}

若要開始開發您自己的 SPA 以在 AEM 中使用，請查看以下文件：

* [SPA WKND 教學課程](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [使用 React 快速入門](/help/implementing/developing/hybrid/getting-started-react.md)
* [使用 Angular 快速入門](/help/implementing/developing/hybrid/getting-started-angular.md)

如果您必須調整現有 SPA 以在 AEM 使用它，請查看以下文件：

* [RemotePage 元件](/help/implementing/developing/hybrid/remote-page.md)
* [在 AEM 中編輯外部 SPA](/help/implementing/developing/hybrid/editing-external-spa.md)

請參閱下面的[其他資源](#additional-resources)，可以讓您更深入地了解 AEM 的 SPA 主題。

## 其他資源 {#additional-resources}

以下是一些其他資源，它們對本文件提到的一些概念有更深入的探討。

* [AEM Headful 和 Headless 技術](/help/implementing/developing/headful-headless.md) - 描述 AEM 提供的不同傳遞模型
* [SPA 簡介和逐步解說](/help/implementing/developing/hybrid/introduction.md)- 對 AEM 中的 SPA 有很好的介紹。
* [開發 SPA 以在 AEM 中使用](/help/implementing/developing/hybrid/developing.md) - 說明如何開發 SPA 以在 AEM 中使用
* [SPA 編輯器概觀](/help/implementing/developing/hybrid/editor-overview.md) - 詳細說明 SPA 編輯器的運作原理
* [SPA 參考文件](/help/implementing/developing/hybrid/reference-materials.md) - 開放原始碼 AEM SPA GitHub 專案的 JavaScript API 參考和連結
* [內容片段](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments) - 如何建立內容片段
* [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant) - 一種 Maven 範本，其依照最佳做法建立簡化的 Adobe Experience Manager (AEM) 專案，作為您網站的起點。
