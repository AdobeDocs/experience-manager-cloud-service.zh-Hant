---
title: 可選——如何使用
description: 在此無頭開發人AEM員旅程的選購續約中，您瞭解AEM如何結合無頭傳送與傳統的完整堆疊CMS功能，以及如何使用編輯器架構來SPA建AEM立可SPA編輯。
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 1b6dbf401ff921964537f6c79d12544789e93c92
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---


# 如何使用&lt;a0/SPA>建立單頁AEM應用程式(){#create-spa}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在此[無頭開發人員歷程的選購續航中，您瞭解如何結合無頭傳送與AEM傳統全堆疊CMS功能，以及如何使用SPAEditor架構來建立可編輯的SPAAEM，以及視需要整合外部Headless Developer Journey，啟用編輯功能。](overview.md)

## 到目前為止的故事{#story-so-far}

此時，您應已完成整個[AEM Headless Developer Journey](overview.md)，並瞭解無頭傳送的基本概念，包括AEM瞭解：

* 無頭內容與無頭內容傳送的差異。
* 無頭AEM功能。
* 如何組織和無AEM頭專案。
* 如何在中建立無頭內容AEM。
* 如何擷取和更新中的無頭內容AEM。
* 如何與無頭專案AEM一起上線。

因此，您現在要麼已與您的第一個AEMHeadless專案同時上線，要麼已具備所需的所有知識。 恭喜！

那麼，你為什麼要閱讀這段另外的，選擇性的旅程延續？ 您可能會記得，在[開始使用](getting-started.md#integration-levels)中，我們簡要地討論了AEM，如何不僅支援無頭傳送和傳統的全堆疊模型，還支援結合兩者優點的混合模型。 雖然不是傳統的無頭模型，但這種混合模型可為某些項目提供前所未有的靈活性。

本文章以您對AEMHeadless的瞭解為基礎，深入探討如何建立您自己的單頁應用程式(SPA)，這些應用程式實際上可在中編AEM輯。 如此，您就可以建立內容，並無頭地將它傳送SPA至，但SPA在中仍可編AEM輯。

## 目標 {#objective}

本檔案可協助您瞭解如何使用編輯器架構來開發單頁AEM應SPA用程式。 閱讀本檔案後，您應：

* 瞭解編輯器的基本SPA功能。
* 瞭解建立可完全編輯的SPA需求AEM。
* 瞭解外部SPA如何整合AEM。
* 瞭解應該或不應該如何實施伺服器端轉換。

## 要求和先決條件{#requirements-prerequisites}

在開始使用之前，有許多要求SPAAEM。

### 知識{#knowledge}

* 使用React或Angular架SPA構進行創作的開發經驗
* 建立內AEM容片段和使用編輯器的基本技巧
* 請務必檢閱](/help/implementing/developing/headful-headless.md)中的[Headful和Headless檔案，以了AEM解整合的可能SPA程度。

### 工具 {#tools}

* 測試專案部署的沙盒存取
* 資料建模與測試的本端開發例項
* 現有外部SPA（可選，視選擇的整合模型而定）
* AEM 專案原型

## 什麼是SPA?{#what-is-a-spa}

單頁應用程式(SPA)與傳統頁面不同，它是由用戶端轉譯，主要是Javascript導向，依賴Ajax呼叫來載入資料並動態更新頁面。 大部分或所有內容在單一頁面載入時都會擷取一次，並根據使用者與頁面的互動，視需要以非同步方式載入其他資源。

這可降低頁面重新整理的需求，並為使用者呈現順暢、快速且更像原生應用程式體驗的體驗。

此AEMSPAAEM編輯器可讓前端開發人員建立可整SPA合至網站的內容，讓內容製作者可像編輯其他內容一樣SPA輕鬆編輯內容。

## 為什麼SPA?{#why-spa}

如同原生應用程式一樣，更快速、流暢，SPA不僅對網頁的訪客，而且由於工作方式的性質，行銷人員和開發人員都十分有吸引力SPA。

如需詳細說SPA明及使用它們的原因，請參閱[其他資源](#additional-resources)一節，以取得更多部門內檔案的連結。

## 處理方AEM式SPA

開發單頁應用AEM程式時，前端開發人員在建立應用程式時，會遵循標準的最佳實務SPA。 如果您是前端開發人員，除了遵循這些一般最佳實務以及AEM少數特定原則外，SPA您的功能將AEM與其內容製作功能搭配運作。

* **可移植性** -與任何元件一樣，SPA元件應盡可能可攜。應使用SPA可攜式和可重複使用的元件來建立。
* **驅AEM動網站結構** -前端開發人員建立元件並擁有其內部結構，但需AEM仰賴定義網站的內容結構。
* **動態演算** -所有演算應為動態。
* **動態路由** -負責路SPA由，並監聽路AEM由並基於路由提取。任何路由都應是動態的。

如需如何處理的完AEM整說SPA明，請參閱[additional resources](#additional-resources)一節，以取得更多部門內檔案的連結。

## 編AEM輯SPA器{#aem-spa-editor}

使用通用架構(SPA例如React和Angular)建立的網站會透過動態JSON載入其內容，而不提供頁面編輯器放置編輯控制項所AEM需的HTML結構。

若要啟用在SPA中編AEM輯，則需要JSON輸出SPA與儲存庫中的內容AEM模型之間的對應。

支SPA援AEM在頁面編輯器中載入時，會引入與SPAJS程式碼互動的精簡JS層，以便傳送事件，並啟動編輯控制項的位置，以允許內容內容編輯。 此功能以Content Services API Endpoint概念為基礎，因為來自內容的內SPA容需要透過Content Services載入。

如需編輯器的完AEM整說SPA明，請參閱[additional resources](#additional-resources)一節，以取得更多部門內檔案的連結。

## 調整SPA現有{#existing-spas}

如果您有現有SPA的AEM檔案，則支援將它內嵌AEM至編輯器中，讓內容作者可以看到AEM它。 在檢視透過內容片段建立的內容時，這對於檢視要使用內容片段的終端應用程式內容非常有用。

此外，只需稍作變更，您就可在編輯器中啟用特定的外部SPA編輯AEM功能。

RemotePage元件允許在中呈現SPA外部AEM。

有關如何在中使外部可編輯的完SPA整說AEM明，請參閱[additional resources](#additional-resources)一節，以取得更多部門內檔案的連結。

## 下一個{#what-is-next}

若要開始開發您自己的SPA文AEM件，請檢閱下列檔案：

* [WKND教SPA學課程](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [開始使用React](/help/implementing/developing/hybrid/getting-started-react.md)
* [開始使用Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

如果您需要調整現有SPA檔案以AEM在中使用，請檢閱下列檔案：

* [RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)
* [在中編SPA輯外AEM部](/help/implementing/developing/hybrid/editing-external-spa.md)

請參閱以下有關[其他資源](#additional-resources)的資訊，這些資源可讓您深入瞭解SPA中的主AEM題。

## 其他資源 {#additional-resources}

以下是一些其他資源，可深入探討本檔案中提及的一些概念。

* [Headful and Headless inAEM](/help/implementing/developing/headful-headless.md) -說明中提供的不同傳送模型AEM
* [簡SPA介與逐步說明。](/help/implementing/developing/hybrid/introduction.md) -在Adobe SPA Cloud中
* [開SPA發AEM-如何開發SPA的指AEM南](/help/implementing/developing/hybrid/developing.md) 
* [編SPA輯器概觀](/help/implementing/developing/hybrid/editor-overview.md) -編輯器工作方式的詳SPA細資訊
* [伺服器端轉換](/help/implementing/developing/hybrid/ssr.md) -如何設定SSRAEM SPA
* [SPA參考檔案- JavaScript API參考與開放原始碼AEMGitHub專SPA案的連結](/help/implementing/developing/hybrid/reference-materials.md) 
* [內容片段](/help/assets/content-fragments/content-fragments.md) -如何建立內容片段
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)  - Maven範本，可建立以最小、最佳實務為基礎的Adobe Experience Manager(AEM)專案，做為您網站的起點
