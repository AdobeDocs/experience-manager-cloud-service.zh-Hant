---
title: 選用 — 如何使用Adobe Experience Manager (SPA)建立單頁應用程式(AEM)
description: 在 AEM Headless 開發人員歷程的此延續部分 (選擇性)，您將了解 AEM 如何將無周邊傳遞與傳統的全堆疊 CMS 功能相結合，以及如何使用 AEM 的 SPA 編輯器框架建立可編輯的 SPA。
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 48%

---

# 如何使用 AEM 建立單頁應用程式 (SPA) {#create-spa}

在此選用的延續 [AEM Headless開發人員歷程](overview.md)，您將瞭解AEM如何將Headless傳送與傳統全棧疊CMS功能結合。 您也會瞭解如何使用AEM SPA Editor架構建立可編輯的SPA，以及整合外部SPA，以視需要啟用編輯功能。

## 到目前為止 {#story-so-far}

此時，您應該已經完成了整個[AEM Headless 開發人員歷程](overview.md)並了解 AEM 無周邊傳遞的基本知識，包括了解：

* 無周邊和有周邊內容傳遞之間的差異。
* AEM 的無周邊功能。
* 如何組織 AEM Headless 專案。
* 如何在 AEM 建立無周邊內容。
* 如何在 AEM 擷取和更新無周邊內容。
* 如何使 AEM Headless 專案上線。

到目前為止，您已經上線執行第一個AEM Headless專案，或具備執行此作業的知識。 恭喜！

那麼，為什麼您會看到這個額外的、選用的歷程延續？ 您記得在 [快速入門](getting-started.md#integration-levels)，會上討論AEM如何不僅支援headless傳送和傳統的全棧疊模型，還支援結合兩者優勢的混合模型。 雖然不是傳統的無周邊模型，但這類混合模型可以為特定專案提供前所未有的靈活性。

本文將以您對AEM Headless的知識為基礎，深入探索如何建立可在AEM中編輯的您自己的單頁應用程式(SPA)。 如此一來，您可以建立內容並直接傳送給SPA，但SPA在AEM中仍可編輯。

## 目標 {#objective}

本文件可協助您了解如何使用 AEM SPA 編輯器框架開發單頁應用程式。閱讀本文件後，您應該：

* 了解 SPA 編輯器的基本功能。
* 了解為 AEM 建立完全可編輯的 SPA 的要求。
* 了解如何將外部 SPA 整合到 AEM 中。
* 瞭解伺服器端轉譯可以如何實作或無法實作。

## 要求和先決條件 {#requirements-prerequisites}

在AEM中開始使用SPA之前，有幾項需求。

### 知識 {#knowledge}

* 使用 React 或 Angular 框架建立 SPA 的開發經驗
* 建立內容片段和使用編輯器的基本 AEM 技能
* 請務必檢閱此檔案 [AEM中的Headful和Headless](/help/implementing/developing/headful-headless.md) 以便瞭解各種SPA整合層級。

### 工具 {#tools}

* 用於測試部署專案的沙箱存取權
* 用於資料模型和測試的本機開發執行個體
* 現有的外部 SPA (選擇性，取決於所選的整合模型)
* AEM 專案原型

## 什麼是 SPA？ {#what-is-a-spa}

單頁應用程式(SPA)與傳統頁面不同，在於它是於使用者端轉譯，主要是JavaScript導向，依賴Ajax呼叫載入資料並動態更新頁面。 大部分或全部內容都會根據使用者與頁面的互動，在單一頁面載入中擷取一次，並視需要以非同步方式載入其他資源。

此功能可減少對頁面重新整理的需求，並為使用者呈現順暢、快速的體驗，且感覺更像是原生應用程式體驗。

AEM SPA 編輯器允許前端開發人員建立可整合到 AEM 網站的 SPA，從而允許內容作者輕鬆編輯 SPA 內容，像編輯任何其他 AEM 內容一樣輕鬆。

## 為什麼是 SPA？ {#why-spa}

SPA速度更快、流動性更強，並且更像原生應用程式，因此成為極具吸引力的體驗。 由於SPA的運作方式性質，這不僅對網頁的訪客有好處，對行銷人員和開發人員也有好處。

如需 SPA 的完整說明以及使用它們的原因，請參閱[其他資源](#additional-resources)章節以取得更多深入文件的連結。

## AEM 如何處理 SPA

在 AEM 開發單頁應用程式是假設前端開發人員在建立 SPA 時有遵守標準最佳做法。作為前端開發人員，如果您遵循這些一般最佳實務和一些AEM特定原則，您的SPA將可透過AEM及其內容製作功能發揮作用。

* **可攜性** - 如同任何元件，SPA 元件應盡可能建置為具可攜性。SPA 應該使用可攜帶和可重複使用的元件建置。
* **AEM磁碟機網站結構**  — 前端開發人員建立元件並擁有其內部結構，但仰賴AEM定義網站的內容結構。
* **動態呈現** - 所有呈現都應該是動態的。
* **動態路由** - SPA 負責路由，AEM 會偵聽並據此進行擷取。任何路由也應該是動態的。

如需 AEM 如何處理 SPA 的完整說明，請參閱[其他資源](#additional-resources)章節以取得更多深入文件的連結。

## AEM SPA 編輯器 {#aem-spa-editor}

使用常見SPA架構(例如React和Angular)建立的網站，會透過動態JSON載入其內容。 它們沒有提供AEM頁面編輯器放置編輯控制項所需的HTML結構。

若要在AEM內啟用SPA編輯，需要在SPA的JSON輸出與AEM存放庫中的內容模型之間建立對應，以便您可以儲存對內容的變更。

AEM中的SPA支援引進了細薄的JavaScript層，當載入頁面編輯器時，可與SPA JavaScript程式碼互動，並透過該層傳送事件。 可啟動編輯控制項的位置，以允許進行內容內編輯。 此功能以Content Services API端點概念為基礎，因為來自SPA的內容必須透過Content Services載入。

如需 AEM SPA 編輯器的完整說明，請參閱[其他資源](#additional-resources)章節以取得更多深入文件的連結。

## 容納現有的 SPA {#existing-spas}

如果您已有SPA，AEM支援將其內嵌至AEM，讓內容作者可在AEM編輯器中看見該版本。 此功能對於在使用內容的最終應用程式內容中，透過內容片段檢視他們正在建立的內容很有用。

此外，您只需進行小幅變更，即可在SPA編輯器中對外部AEM啟用特定編輯功能。

RemotePage 元件允許在 AEM 中呈現外部 SPA。

如需如何讓外部 SPA 可在 AEM 中編輯的完整說明，請參閱[其他資源](#additional-resources)章節以取得更多深入文件的連結。

## 下一步 {#what-is-next}

若要開始開發您自己的 SPA 以在 AEM 中使用，請查看以下文件：

* [SPA WKND 教學課程](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [使用 React 快速入門](/help/implementing/developing/hybrid/getting-started-react.md)
* [使用 Angular 快速入門](/help/implementing/developing/hybrid/getting-started-angular.md)

如果您必須調整現有的SPA才能在AEM中使用，請檢閱下列檔案：

* [RemotePage 元件](/help/implementing/developing/hybrid/remote-page.md)
* [在 AEM 中編輯外部 SPA](/help/implementing/developing/hybrid/editing-external-spa.md)

請參閱下面的[其他資源](#additional-resources)，可以讓您更深入地了解 AEM 的 SPA 主題。

## 其他資源 {#additional-resources}

以下是一些其他資源，它們對本文件提到的一些概念有更深入的探討。

* [AEM Headful 和 Headless 技術](/help/implementing/developing/headful-headless.md) - 描述 AEM 提供的不同傳遞模型
* [SPA簡介和逐步解說](/help/implementing/developing/hybrid/introduction.md) - AEM中的SPA簡介。
* [開發 SPA 以在 AEM 中使用](/help/implementing/developing/hybrid/developing.md) - 說明如何開發 SPA 以在 AEM 中使用
* [SPA 編輯器概述](/help/implementing/developing/hybrid/editor-overview.md) - 詳細說明 SPA 編輯器的運作原理
* [伺服器端轉譯](/help/implementing/developing/hybrid/ssr.md)  — 如何設定AEM SPA的SSR
* [SPA參考檔案](/help/implementing/developing/hybrid/reference-materials.md)  — 開放原始碼AEM SPA GitHub專案的JavaScript API參考和連結
* [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md) - 如何建立內容片段
* [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) - 一種 Maven 範本，其依照最佳做法建立簡化的 Adobe Experience Manager (AEM) 專案，作為您網站的起點。
