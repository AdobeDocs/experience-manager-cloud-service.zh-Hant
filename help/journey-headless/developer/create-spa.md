---
title: 可選 — 如何使用建立單頁應用SPA程式(AEM)
description: 在此可選的無AEM頭開發人員旅程的繼續中，您將了AEM解如何將無頭交付與傳統的全堆棧CMS功能結合起來，以及如何使用編輯器框架SPA創AEM建可SPA編輯。
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 1%

---

# 如何使用建立單頁應用SPA程式(AEM) {#create-spa}

在此可選的繼續 [無AEM頭開發者之旅，](overview.md) 您將了AEM解如何將無頭傳遞與傳統的全堆棧CMS功能結合起來，以及如何使用SPAAEM Editor框架建立可編輯SPA，以及如何整合外SPA部，從而根據需要啟用編輯功能。

## 到目前為止的故事 {#story-so-far}

此時，您應該已完成 [無AEM頭開發者之旅](overview.md) 並瞭解無頭遞送的基本知識，AEM包括瞭解：

* 無頭內容和有頭內容交付之間的區別。
* 無AEM頭部特徵。
* 如何組織和AEM無頭項目。
* 如何在中建立無頭內AEM容。
* 如何檢索和更新中的無頭內AEM容。
* 如何與無頭項目AEM共處。

因此，你要麼接受了你的第一個AEM無頭項目，要麼擁有了實現這一目標所需的所有知識。 恭喜！

那麼，你為什麼要閱讀這段額外的，可選的旅程延續？ 你可能還記得 [入門](getting-started.md#integration-levels) 我們簡要地AEM討論了如何不僅支援無頭遞送和傳統的全棧模型，還支援結合兩者優點的混合模型。 雖然不是傳統的無頭模型，但這種混合模型可以為某些項目提供前所未有的靈活性。

本文基於您對AEMHeadless的瞭解，深入探討如何建立您自己的單頁應用程式(SPA在中實際可編AEM輯)。 這樣，您就可以建立內容並將其直接傳送到SPA，但SPA在中仍可編AEM輯。

## 目標 {#objective}

本文檔幫助您瞭解如何使用編輯器框架開發AEM單頁SPA應用程式。 閱讀此文檔後，您應：

* 瞭解編輯器的基SPA本功能。
* 瞭解為建立完全可編輯SPA的要AEM求。
* 瞭解外部SPA如何整合到AEM。
* 瞭解應如何實現或不應如何實現伺服器端呈現。

## 要求和先決條件 {#requirements-prerequisites}

在開始使用之前，有許多要SPA求AEM。

### 知識 {#knowledge}

* 使用反應或SPAAngular框架建立開發經驗
* 建立內AEM容片段和使用編輯器的基本技能
* 確保審閱文檔 [無頭AEM](/help/implementing/developing/headful-headless.md) 來瞭解整合的各SPA個層次。

### 工具 {#tools}

* 用於測試部署項目的沙盒訪問
* 用於資料建模和測試的本地開發實例
* 現有外部SPA（可選，取決於選擇的整合模型）
* AEM 專案原型

## 什麼SPA? {#what-is-a-spa}

單頁應用程SPA序(1)與常規頁不同，其是呈現客戶端，並且主要是Javascript驅動的，依靠Ajax調用載入資料並動態更新頁面。 大多數或所有內容在單個頁面負載中檢索一次，並根據用戶與頁面的交互情況根據需要非同步載入其他資源。

這減少了頁面刷新的需要，並為用戶提供了無縫、快速且更像本地應用程式體驗的體驗。

前AEM端開發SPA人員可建立可SPA整合到站點的內容，使內容作者能夠像任何其他內容一樣SPA輕鬆地編輯內容。

## 為什麼SPA? {#why-spa}

通過更快、更流暢和更像本地應用程式，SPA不僅對網頁訪問者，而且由於工作方式的性質，對營銷人員和開發人員來說，都成為非常有吸引力的體SPA驗。

有關使用它們的SPA完整說明和原因，請參閱 [額外資源](#additional-resources) 的子目錄。

## 處理方AEM式SPA

開發單頁應用程式AEM時，假定前端開發人員在建立時遵守標準的最佳SPA做法。 如果作為前端開發人員，您遵循這些一般的最佳做法以及AEM少數特定的原則，則SPA您將能夠利用其AEM內容創作功能發揮作用。

* **便攜性**  — 與任何元件一樣，SPA元件應盡可能便攜。 應該SPA使用可移植和可重複使用的元件來構建。
* **驅動AEM器站點結構**  — 前端開發人員建立元件並擁有其內部結構，但依AEM賴於定義站點的內容結構。
* **動態渲染**  — 所有渲染都應是動態的。
* **動態路由**  — 負SPA責路由並監聽路AEM由並基於路由讀取。 任何路由都應是動態的。

有關如何處理的AEM完整SPA說明，請參見 [額外資源](#additional-resources) 的子目錄。

## 編AEM輯SPA器 {#aem-spa-editor}

使用常SPA用框架(如React和Angular)構建的站點通過動態JSON載入其內容，並且不提供頁面編輯器能夠放置編輯控AEM件所必需的HTML結構。

要啟用在中的編SPA輯AEM，需要在儲存庫中的JSON輸SPA出和內容模型之AEM間進行映射以保存對內容的更改。

SPA中的AEM支援引入了一個精簡JS層，當載入到頁面編輯器中時，該層與SPAJS代碼交互，可通過該層發送事件，並激活編輯控制項的位置以允許上下文編輯。 此功能基於Content Services API端點概念，因為來自內容的內SPA容需要通過Content Services載入。

有關編輯器的AEM完整SPA說明，請參見 [額外資源](#additional-resources) 的子目錄。

## 適應現有SPA {#existing-spas}

如果您有現有SPA的AEM，則支援將其嵌入AEM到編輯器中，以便您的內容作者可以看到AEM它。 這對於查看他們通過內容片段建立的內容非常有用，這些內容將在要使用的最終應用程式的上下文中顯示。

此外，只需稍作更改，您就可以啟用編輯器內外部SPA的特定編AEM輯功能。

RemotePage元件允許在中呈現SPA外部AEM。

有關如何使外部可編輯的完SPA整說明AEM，請參見 [額外資源](#additional-resources) 的子目錄。

## 下一步 {#what-is-next}

要開始開發您自己的SPA文AEM檔，請查看以下文檔：

* [WKND教SPA程](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [開始使用React](/help/implementing/developing/hybrid/getting-started-react.md)
* [開始使用Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

如果您需要調整現有SPA文檔以在中AEM使用它，請查看以下文檔：

* [RemotePage元件](/help/implementing/developing/hybrid/remote-page.md)
* [編輯SPA外部AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

請參閱下面 [額外資源](#additional-resources) 能讓你更深入地瞭解SPA話題AEM。

## 其他資源 {#additional-resources}

以下是一些附加資源，可對本文檔中提到的一些概念進行更深入的介紹。

* [無頭AEM](/help/implementing/developing/headful-headless.md)  — 中提供的不同交付模式的說AEM明
* [介SPA紹和漫遊。](/help/implementing/developing/hybrid/introduction.md) - 2014年12月10日至2014年12SPA月AEM1
* [開SPA發AEM](/help/implementing/developing/hybrid/developing.md)  — 關於如何為
* [編SPA輯器概述](/help/implementing/developing/hybrid/editor-overview.md)  — 編輯器工作方式SPA的詳細資訊
* [伺服器端呈現](/help/implementing/developing/hybrid/ssr.md)  — 如何配置SSRAEM SPA
* [參考SPA文檔](/help/implementing/developing/hybrid/reference-materials.md) - JavaScript API引用和指向開源AEMGitHub項SPA目的連結
* [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)  — 如何建立內容片段
* [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) - Maven模板，它建立基於最佳做法的最小化Adobe Experience Manager(AEM)項目，作為您網站的起點
