---
title: 開始使用AEM無頭Cloud Service
description: 在這部分的無頭開AEM發人員歷程中，瞭解無頭開AEM發的先決條件。
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 9fb18dbe60121f46dba1e11d4133e5264a6d538d
workflow-type: tm+mt
source-wordcount: '3087'
ht-degree: 0%

---


# 開始使AEM用無頭Cloud Service{#getting-started}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[無頭開發人AEM員旅程的這部分，](overview.md)瞭解開始使用無頭專案所需的AEM內容。

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，[瞭解CMS無頭開發](learn-about.md)您瞭解了無頭CMS的基本理論，您現在應：

* 瞭解無頭內容傳送的基本概念和術語
* 瞭解何時需要無頭
* 高階瞭解無頭概念的使用方式及其相互關係

本文以這些基本概念為基礎，讓您瞭解如何使用AEM無頭解決方案。

## 目標 {#objective}

本檔案可協助您了AEM解Headless在您自己專案中的運用。 閱讀後，您應：

* 瞭解無頭功能AEM的基本概念。
* 瞭解使用無頭功能的必AEM要條件。
* 請注意無AEM頭整合等級。
* 能夠根據範圍定義專案。

## 基AEM礎{#aem-basics}

在定義您的無頭專案之AEM前，請務必瞭解一些基本AEM概念。

### 作者實例{#author}

最簡單的AEM是，由作者實例和[publish實例](#publish)組成，可搭配運作以建立、管理和發佈您的內容。

內容從作者實例開始。 您的內容作者可在此建立其內容。 作者環境提供多種工具，讓作者可建立、組織和重複使用其內容。

### 發佈實例{#publish}

內容在作者例項中建立後，就必須發佈，才能供其他服務使用。 發佈例項包含所有已發佈的內容。

### 複寫 {#replication}

複製是指將內容從作者實例傳輸到發佈實例的行為。 當作者或其他擁有適當權AEM限的使用者發佈內容時，會自動執行此動作。

### AEM基本摘要{#aem-basics-summary}

在最簡單的層次上，建立數位體驗AEM需要下列步驟：

1. 您的內容作者將在作者實例中建立您的無頭內容。
1. 當此內容準備就緒時，就會複製到發佈實例。 然後可呼叫API以擷取此內容。

AEM此技術基礎的無頭基礎提供強大的工具來管理下一節所述的無頭內容。](#aem-headless-basics)[

## AEM無頭基礎{#aem-headless-basics}

其無頭功能AEM以幾項主要功能為基礎。 這些將在旅程的後半段詳細說明。 現在，只有瞭解他們的基本工作以及他們的名稱，才是重要的。

### 內容片段模型 {#content-fragment-models}

內容片段模型定義您要在中建立和管理的資料和內容結構AEM。 它們是您內容的支架。 選擇建立內容時，您的作者會從您定義的「內容片段模型」中選取，以引導他們建立內容。

### 內容片段 {#content-fragments}

內容片段可讓您設計、建立、組織和發佈不受頁面影響的內容。 它們可讓您準備內容，以便在多個位置和多個通道上使用。

內容片段包含結構化內容，可以以JSON格式傳送。

### GraphQL和REST API {#apis}

若要無端修改您的內容，AEM請提供兩個強穩的API。

* GraphQL API允許您建立訪問和傳遞內容片段的請求。
* 資產REST API可讓您建立和修改內容片段（和其他資產）。

您將瞭解這些API，以及如何在後續的無頭歷程中使AEM用它們。 或者，請參閱以下[其他資源](#additional-resources)一節以取得其他檔案。

## 無頭整合級別{#integration-levels}

支AEM援CMS的全無頭和傳統的完整堆疊或頭型機型。 不過AEM，不僅提供這兩種獨家選擇，還能支援結合兩者優點的混合模型，為您的無頭專案提供獨特的彈性。

為確保您瞭解無頭的概念，本AEM次無頭開發人員歷程著重於純粹的無頭模型，讓您盡快上手使用，毋需撰寫程式碼AEM。

但是，一旦您瞭解無頭功能，您應該會注意到您所面臨的其他混合AEM功能。 我們將這些案例列在下面，以便您瞭解。 在旅程結束時，您將更詳細地介紹這些概念，以備專案需要有此種彈性。

### 您已有無頭內容的外部使用，例如單頁應用程式(SPA)。{#already-have-a-spa}

我們假設您的基本需求至少是要將內容從現有的AEM外部服務傳送。

#### 層級1:內容片段整合——傳統無頭模型{#level-1}

此整合層級是傳統的無頭模型，可讓內容作者在中建立內容AEM，並使用GraphQL將內容無頭地傳送至任何數量的外部服務，或使用Assets API從外部服務編輯內容。 中不需要編AEM碼。

在此模型中，AEM僅用於透過使用「內容片段」來建立和提供AEM內容。 轉譯內容並與內容互動的功能會委派給使用中的外部應用程式，通常是單頁應用程式(SPA)。

#### 層級2:內嵌SPA於AEM-混合型號{#level-2}

此整合層級建立在第一層級上，但也允許外部應用程式(SPA)內嵌在AEM其中，讓內容作者可以在外部應用程式的內容中檢視內容AEM。 此應用程式也可支援有限編輯內部的外部應用程式AEM。

此層級的優點在於，可讓內容作者以有頭有腦的方式靈活製作內容AEM，其內容會與內嵌的外部內容一起呈現SPA，同時仍能毫無頭緒地傳送內容。

#### 第3級：嵌入和完SPA全啟AEM用——混合型號{#level-3}

此整合層級可建立在層級2上，讓外部的大部分內容都可在SPA其中編輯AEM。

### 您尚未擁有無頭內容的外部使用者，例如單一頁面應用程式(SPA)。{#do-not-have-a-spa}

如果您的目標是建立無SPA頭無腦地取用內AEM容的新功能，您可以使用內容片段等功能來管理無頭內容，並使用編輯器架構SPA來建AEM立SPA架構。

使用編SPA輯器，您不SPA僅可從中取用內容AEM，而且內容作者也可在AEM內部完全編輯，讓您既有無頭傳送的彈性，也能在內容中編輯內AEM容。

## 要求和先決條件{#requirements-prerequisites}

在開始無頭專案之前，有許多需AEM求。

### 知識{#knowledge}

* GraphQL
* 使用React或Angular架SPA構進行創作的開發經驗
* 建立內AEM容片段和使用編輯器的基本技巧

### 工具 {#tools}

* 測試專案部署的沙盒存取
* 資料建模與測試的本端開發例項
* 您的無SPA頭內容的現有外部或其他消AEM費者

## 定義您的項目{#defining-your-project}

對於任何成功的項目，不僅要明確項目的要求，而且要明確其角色和責任。

### 範圍 {#scope}

明確項目範圍非常重要。 範圍可通知接受標準，並允許您建立完成的定義。

您需要問自己的第一個問題是「我嘗試使用Headless實現AEM什麼？」 一般而言，答案應該是，您擁有或將來會擁有使用您自己開發工具建立的體驗應用程式，而不是搭配使用AEM。 此體驗應用程式可以是行動應用程式、網站或任何其他使用者對應體驗應用程式。 使用AEMHeadless的目的，是為您的體驗應用程式提供使用最新的API建立、儲存和管理的內容，這些API會呼叫AEMHeadless，以直接從體驗應用程式擷取內容，甚至完整的CRUD內容。 如果您不想這麼做，您可能想要[返回說明檔案AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)，並尋找更符合您想要完成之事的章節。

### 角色和責任{#roles-responsibilities}

任何個別專案的角色都會有所不同，但無頭開發內容中需要考慮的重AEM要角色是：

* [管理員](#administrator)
* [內容作者](#content-author)
* [內容建立工具](#content-modeler)
* [開發人員](#developer)

#### 管理員 {#administrator}

管理員負責系統的基本設定和配置。 例如，管理員將在Adobe用戶管理系統內設定您的組織，請參閱Identity Management系統(IMS)。 一旦您的組織在IMS中由Adobe建立後，管理員將是組織中第一個收到來自Adobe的電子郵件邀請的使用者。 管理員可登入IMS並新增其他角色的使用者。

一旦管理員設定好使用者後，就會授與他們存取所有資源的權限，以完成其工作，並讓他AEM們以無頭的方式提供體驗應用程AEM式。

管理員應是設定並準備執行階段環境的使用者AEM，讓[內容作者](#content-author)可建立並更新內容，而[開發人員](#developer)則可使用API來擷取或修改其體驗應用程式的內容。

#### 內容作者{#content-author}

內容作者建立並管理無端傳遞的內AEM容。 內容作者AEM使用內容片段和資產主控台等功能來管理其內容。

內容作者應牢記下列最佳實務。

#### 本地化計畫{#localization}

在專案開始時規劃翻譯和當地語系化。 將「國際化專案經理」視為個別角色，負責定義哪些內容應翻譯，哪些內容應翻譯，哪些翻譯內容可由區域或本地內容製作者修改。

針對您需要的內容本土化制定計畫。

* 您只需要不同的語言或語言，才能適應地區的具體情況嗎？
* 您是否需要針對不同地區設定不同的豐富型媒體內容（例如影像或視訊）?

請清楚瞭解您的內容更新工作流程。 系統需要支援哪些核准程式？ 是否可AEM運用工作流程來自動化此程式？

請注意，您的[內容階層](#content-hierarchy)可以運用，讓本地化更輕鬆。

有關工作流和本地化工具的其他文檔，請參閱[其他資源](#additional-resources)AEM部分。

##### 運用內容階層{#content-hierarchy}

資料夾階層可解決內容管理的兩大問題：

* [本地化](#localization) -在AEM特定地區的資料夾中維護內容副本，以管理內容的本地化。
* 組織——檔案夾可用來定義支援當地化需求以及邏輯管理內容片段所需的內容階層。

允許AEM非常靈活的內容結構和任意大的層次結構。 但是，必須認識到，資料夾結構中的任何更改都可能對[依賴內容路徑的現有查詢產生意想不到的後果。](#developer) 因此，預先明確設定的明確定義階層，對內容作者非常有幫助。

資料夾也可以限制為僅允許特定類型的內容（根據內容片段模型）。 通常建議始終明確指定允許在層次結構中的所有資料夾使用哪些模型。 指定指定資料夾的允許內容：

* 防止內容作者製作不屬於資料夾的內容。
* 透過篩選資料夾中在建立期間允許的內容類型，以僅顯示有效的內容類型，最佳化內容建立程式。

透過建立適當的內容結構，跨通道協調無頭內容製作，以便將內容重複使用率提高到最大。 跨多個通道利用內容可大幅提升內容製作效率和變更管理。

##### 建立良好的命名慣例{#naming-conventions}

內容片段名稱必須對內容作者進行描述。 透明地AEM處理轉義和／或截斷儲存庫級別上使用的ID的名稱。 因此，內容作者提供的邏輯名稱應始終是可讀的，並代表內容。

* 名稱錯誤：`cta_btn_1`
* 好名稱：`Call To Action Button`

有關頁面命名慣例的其他文檔，請參閱[additional resources](#additional-resources)AEM一節。

##### 不要過度延伸內容巢狀{#content-nesting}

[內容](#content-fragments) 片段用於建AEM立無頭內容。支援最AEM多10個內容片段巢狀層次的內容。 但請記住，必須反覆解析父「內容片段」中AEM定義的每個參照，然後檢查所有同級中是否有子參照。 這些操作可以快速加總，並成為效能方面的考慮。

作為一般的經驗法則，「內容片段」參考不應巢狀化超過五個層級。

#### 內容建立工具{#content-modeler}

內容建模器會分析需要無端傳遞之資料的需求，並定義此資料的結構。 這些結構稱為[中的內容片段模型](#content-fragment-models)AEM。 內容片段模型是內容作者建立之內容片段的基礎。

定義「內容片段模型」時，有一個實用的方法是建立對應至將使用內容之應用程式的UX元件的模型。

由於內容作者在建立新內容時會持續與模型互動，因此將模型與UX對齊有助於他們視覺化產生的數位體驗。 更進一步，您可以指派圖示給代表UX元素的「內容片段模型」，讓作者能夠根據視覺提示，以直覺方式選取正確的模型。

#### 開發人員 {#developer}

開發人員負責將所建立的內容無端結合AEM至該內容的消費者，這些內容通常可以是單頁應用程式(SPA)、漸進式網路應用程式(PWA)、網頁商店或外部的其他服務AEM。

GraphQL是無頭內容的使AEM用者與使用者之間的「黏合劑」。 GraphQL是查詢必AEM要內容的語言。

開發人員在規劃查詢時，應牢記一些基本建議：

* 查詢不應依賴固定路徑(`ByPath`)來擷取內容片段。
   * [內容作者對內容片段階層有完](#content-hierarchy) 整的控制權，並可進行會中斷此類查詢的變更。
   * 查詢應改為選擇具有動態查詢參數的內容片段模型參考，以篩選結果以產生所需的裝載。
* 為獲得最佳查詢效能，請始終在中使用持續查詢AEM。 在旅程的稍後階段將討論這些問題。
* GraphQL是按照以下格言設計的宣告性的： 「請確切地詢問您需要的，並獲得所需的。」 這表示在建立GraphQL查詢時，始終避免在關係資料庫中建立`select *`類型查詢。

對於使用[典型無頭實作，AEM](#level-1)開發人員不需要編碼知識AEM。

### 效能要求{#performance-requirements}

若要成功建立任何專案，在建立任何內容之前，必須先考慮效能。

您必須瞭解您的使用者／訪客期望，並為之設計。 設定服務層級目標(SLO)，並測量這些目標以瞭解您是否符合使用者的期望。

#### 流量模式{#traffic-patterns}

要瞭解流量和流量模式，首先收集您過去所掌握的資訊，然後預測未來幾年的預期增長。 需要考慮的一些最重要變數：

* 您預期每小時／天/月會有多少個API呼叫，而且有可能出現尖峰和季節性？
* 有多少不同的內容作者？
* 您預計有多少內容作者同時工作？
* 內容更新的頻率為何？
* 需要多少個內容模型？
* 需要多少個模型實例？

#### 更新頻率{#update-frequency}

通常不同的體驗區段會有不同的內容更新頻率。 瞭解這一點對於能夠微調CDN和快取組態非常重要。 這也是[內容建模器](#content-modeler)設計模型以呈現您的內容時的重要輸入。 請考慮：

* 某些類型的內容必須在特定時段後過期嗎？
* 是否有使用者特定的元素，因此無法快取？

## 下一個{#what-is-next}

現在，您已完成這部分的無AEM頭開發人員旅程，您應：

* 瞭解無頭功能AEM的基本概念。
* 瞭解使用無頭功能的必AEM要條件。
* 請注意無AEM頭整合等級。
* 能夠根據範圍定義專案。

您應繼AEM續無頭歷程，接下來檢閱檔案[使用無頭體驗的第一次體驗路徑&lt;a1/AEM>，您將學習如何設定必要的工具，以及如何開始考慮在中建立資料模型AEM。](path-to-first-experience.md)

## 其他資源 {#additional-resources}

雖然建議您閱讀檔案[「使用無頭體驗初次體驗的路徑」，以進入無頭開發旅程的下一部分，但以下是一些額外的選用資源，可讓您更深入地瞭解本檔案中提及的一些概念，但不需要繼續無頭開發旅程。](path-to-first-experience.md)

* [Adobe Experience ManagerCloud Service建築簡介](/help/core-concepts/architecture.md) —AEMCloud Service結構解讀
* [AEM無頭Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) -使用這些實際操作教學課程來探索如何使用各種選項，將內容傳送至無頭端點，AEM並選擇適合您的內容。
* [使用GraphQL API進行無頭內容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) -請遵循本課程，以瞭解中實施的GraphQL APIAEM。需要透過AdobeID進行驗證。
* [指AEM南WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  —— 此GitHub專案包含反白顯示GraphQL API的AEM範例應用程式。
* [編寫概念](/help/sites-cloud/authoring/getting-started/concepts.md) -編寫環境的技術檔案，其中AEM包含作者——發佈設定的詳細資訊
* [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) -在
* [命名慣例](/help/implementing/developing/introduction/naming-conventions.md) -中頁面命名限制的技術檔案AEM
* [多站點管理員和翻譯](/help/sites-cloud/administering/msm-and-translation.md) -關於強大翻譯功能AEM的技術文檔
* [工AEM作流程——有關如何在](/help/sites-cloud/authoring/workflows/overview.md) 
* [內容片段](/help/assets/content-fragments/content-fragments.md) -內容片段的技術檔案。
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) -內容片段模型的技術檔案。
* [GraphQL技術文檔](https://graphql.org) - GraphQL定義（外部連結）
* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)  —— 說明如何建立存取和傳送內容片段要求的技術檔案
* [Assets REST API](/help/assets/content-fragments/assets-api-content-fragments.md)  —— 說明如何建立和修改內容片段（和其他資產）的技術檔案
* [持續查詢](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching) -有關持續查詢的技術文檔，位於AEM
* [Headful and Headless inAEM](/help/implementing/developing/headful-headless.md) -完整討論無頭整合等級，於AEM
