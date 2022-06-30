---
title: 無頭as a Cloud Service入AEM門
description: 在「無頭開發AEM者之旅」的這一部分，瞭解無AEM頭先決條件。
exl-id: 9661e17b-fa9f-4689-900c-412b068e942c
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '3058'
ht-degree: 0%

---

# 無頭as a Cloud Service入AEM門 {#getting-started}

在 [無AEM頭開發者之旅，](overview.md) 瞭解使用AEMHeadless啟動您自己的項目所需的內容。

## 到目前為止的故事 {#story-so-far}

在前一篇無頭旅AEM程中， [瞭解CMS無頭開發](learn-about.md) 你學到了無頭CMS的基本理論，現在你應該：

* 瞭解無頭內容交付的基本概念和術語
* 瞭解為什麼和何時需要無頭
* 在高級別瞭解如何使用無頭概念及其相互關係

本文基於這些基礎知識，以便您瞭解如何使用AEM無頭解決方案。

## 目標 {#objective}

此文檔可幫助您在AEM自己項目的上下文中瞭解Headless。 閱讀完後，您應：

* 瞭解無頭功能AEM的基本知識。
* 瞭解使用無頭功能AEM的先決條件。
* 瞭解無頭AEM的整合級別。
* 能夠根據範圍定義項目。

## 基AEM礎 {#aem-basics}

在定義無頭項目之AEM前，瞭解一些基本概AEM念很重要。

### 作者實例 {#author}

最簡單的AEM是作者實例和 [發佈實例](#publish) 它們協同工作以建立、管理和發佈您的內容。

內容從作者實例開始。 這是內容作者建立其內容的地方。 作者環境為作者提供了各種工具來建立、組織和重用其內容。

### 發佈實例 {#publish}

在作者實例中建立內容後，必須發佈該內容，以便其他服務可以使用。 發佈實例包含已發佈的所有內容。

### 複寫 {#replication}

複製是將內容從作者實例傳輸到發佈實例的操作。 當具有適當權限的AEM作者或其他用戶發佈內容時，會自動執行此操作。

### 基AEM礎摘要 {#aem-basics-summary}

在最簡單的層次上，在中建立數字型驗AEM需要以下步驟：

1. 您的內容作者在作者實例中建立您的無頭內容。
1. 當此內容準備就緒時，它將複製到發佈實例。
1. 然後可以調用API以檢索此內容。

AEM無頭內容通過提供強大的工具來管理無頭內容， [下一節中介紹。](#aem-headless-basics)

## 無AEM頭基礎 {#aem-headless-basics}

其無頭功AEM能基於幾個關鍵功能。 在旅程的後半部分對這些作了詳細說明。 現在，只要瞭解他們的基本行為和他們的名字，就變得很重要了。

### 內容片段模型 {#content-fragment-models}

內容片段模型定義在中建立和管理的資料和內容的結AEM構。 它們是你內容的腳手架。 選擇建立內容時，作者會從您定義的內容片段模型中選擇內容，這將指導他們建立內容。

### 內容片段 {#content-fragments}

內容片段允許您設計、建立、建立和發佈與頁面無關的內容。 它們使您能夠準備內容，以便在多個位置和多個渠道中使用。

內容片段包含結構化內容，可以以JSON格式傳送。

### GraphQL和REST API {#apis}

要不經意地修改您的內容，AEM請提供兩個強健的API。

* GraphQL API允許您建立訪問和傳遞內容片段的請求。
* Assets REST API允許您建立和修改內容片段（和其他資產）。

您將學習這些API，以及如何在無頭旅行的後AEM半部分使用它們。 或參考 [額外資源](#additional-resources) 下面的部分，瞭解其他文檔。

## 無頭整合級別 {#integration-levels}

支AEM持CMS的全無頭和傳統的全堆棧或全頭模型。 但AEM是，它不僅提供了這兩種獨家選擇，而且還提供了支援混合模型的能力，這兩種模型結合了兩者的優點，為無頭項目提供了獨特的靈活性。

為確保您對無頭概念的理解，此AEMHeadless Developer Journey將重點放在純無頭模型上，以便您盡快啟動並運行，而且不需要編AEM碼。

但是，一旦您瞭解了無頭功能，您應該瞭解您所面臨的其他混合AEM可能性。 這些案件在下面列出，以供您瞭解。 在旅程結束時，您將更詳細地介紹這些概念，以備您的項目需要如此靈活。

### 您已經有了無頭內容的外部使用，如單頁應用程式(SPA)。 {#already-have-a-spa}

讓我們假設您的基本要求至少是將內容從現有外部AEM服務傳送到現有服務。

#### 第1級：內容片段整合 — 傳統無頭模型 {#level-1}

此整合級別是傳統的無頭模型，它允許內容作者在中建立內容AEM，然後使用GraphQL將其無頭地交付給任何數量的外部服務，或使用Assets API從外部服務編輯這些內容。 中不需要編AEM碼。

在此模AEM型中，僅用於使用內容片段建立和AEM服務內容。 呈現和與內容的交互被委託給使用的外部應用程式，通常是單頁應用程式(SPA)。

#### 第2級：嵌入SPA — 混AEM合模型 {#level-2}

此整合級別在第一級別上構建，但還允許將外部應用程式(SPA)嵌入AEM其中，以便內容作者可以查看內部外部應用程式上下文中的內AEM容。 該應用程式還可支援內部外部應用程式的有限編AEM輯。

此級別的優勢在於，允許內容作者以一種頭腦十足的方式靈活地創作內容AEM，其內容以嵌入的外部內容在上下文中呈現SPA，同時仍無頭地提供內容。

#### 第3級：嵌入和完全啟SPA用AEM — 混合模型 {#level-3}

此整合級別建立在第二級上，它使外部中的大多數內SPA容在中可編AEM輯。

### 您尚未擁有無頭內容的外部用戶，如單頁應用程式(SPA)。 {#do-not-have-a-spa}

如果您的目標是建立一SPA個無頭地使用AEM內容的新內容，則您可以使用內容片段等功能來管理無頭內容，還可以使用編輯器SPA框架AEM構SPA建一個。

使用SPA編輯器SPA，不僅會使用內容AEM，而且內容作者在其中也完全可編AEM輯，使您既可以靈活地進行無頭傳送，又可以在內部進行上下文編AEM輯。

## 要求和先決條件 {#requirements-prerequisites}

在開始無頭項目之前，有許多要AEM求。

### 知識 {#knowledge}

* GraphQL
* 使用反應或SPAAngular框架建立開發經驗
* 建立內AEM容片段和使用編輯器的基本技能

### 工具 {#tools}

* 用於測試部署項目的沙盒訪問
* 用於資料建模和測試的本地開發實例
* 您的無SPA頭內容的現有外部或其他用AEM戶

## 定義項目 {#defining-your-project}

對於任何成功的項目，不僅要明確界定項目的要求，還要明確其角色和責任。

### 範圍 {#scope}

必須明確界定項目範圍。 範圍通知接受條件，並允許您建立完成的定義。

你必須問的第一個問題是&quot;我在用Headless實現AEM什麼？&quot; 一般來說，答案應是您擁有或將來擁有您使用自己開發工具構建的體驗應用程式，而不是使用AEM。 此體驗應用程式可以是移動應用程式、網站或任何其他面向客戶的體驗應用程式。 使用AEMHeadless的目標是將建立、儲存和管理的內容提供給您的體驗應用程式，這些內容使用最新的APIAEM，這些API將調用AEMHeadless直接從體驗應用程式獲取內容，甚至完全CRUD內容。 如果這不是你想做的，你可能想 [返回文檔AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) 找到更符合你想完成的部分。

### 角色和職責 {#roles-responsibilities}

任何單個項目的作用各不相同，但在無頭開發內容中需要考慮的重AEM要作用是：

* [管理員](#administrator)
* [內容作者](#content-author)
* [內容架構師](#content-architect)
* [開發人員](#developer)

#### 管理員 {#administrator}

管理員負責系統的基本設定和配置。 例如，管理員在Adobe用戶管理系統中設定您的組織，該系統指Identity Management系統(IMS)。 一旦您的組織通過IMS內的Adobe建立，管理員就是組織中第一個從Adobe接收電子郵件邀請的用戶。 管理員能夠登錄IMS並添加其他角色的用戶。

管理員配置用戶後，將授予他們訪問所有資源的權限AEM，以完成其作為貢獻者使用無頭功能交付體驗應用程式的AEM工作。

管理員應是設定並準備運行AEM時環境以啟用的用戶 [內容作者](#content-author) 建立和更新內容 [開發者](#developer) 使用API獲取或修改其體驗應用程式的內容。

#### 內容作者 {#content-author}

內容作者建立並管理直接由提供的內AEM容。 內容作者使AEM用內容片段和資產控制台等功能來管理其內容。

內容作者應牢記以下最佳做法。

#### 翻譯計畫 {#translation}

在項目開始時計畫翻譯。 請將「翻譯專家」視為一個單獨的角色，其職責是定義哪些內容應被翻譯，哪些內容不應被翻譯，哪些翻譯內容可能由區域或本地內容製作者修改。

建立您需要哪些內容翻譯的計畫。

* 您是否需要不同的語言或語言來適應區域性的具體情況？
* 您是否需要不同語言環境的富媒體內容（如影像或視頻）不同？

請清除內容更新工作流。 系統必須支援哪些審批流程？ 是否可AEM以利用工作流來自動化此過程？

請注意 [內容層次](#content-hierarchy) 可以利用它來簡化翻譯。

查看 [額外資源](#additional-resources) 文檔和翻譯工AEM具(包括無頭翻譯行程AEM的連結)。

##### 利用內容層次結構 {#content-hierarchy}

資料夾層次結構可以解決內容管理方面的兩個主要問題：

* [翻譯](#translation)  — 通AEM過在特定於區域設定的資料夾中維護內容副本來管理內容翻譯。
* 組織 — 資料夾用於定義支援翻譯需要以及邏輯管理內容片段所需的內容層次結構。

允許AEM靈活的內容結構，並且層次可以任意大。 但是，必須認識到，資料夾結構的任何更改都可能對現有查詢產生意外的後果，這些查詢 [依靠內容路徑。](#developer) 因此，預先明確定義的層次結構對內容作者很有幫助。

資料夾也可以限制為僅允許某些類型的內容（基於內容片段模型）。 建議始終明確指定層次中所有資料夾允許使用哪些模型。 指定給定資料夾的允許內容：

* 禁止內容作者創作不屬於該資料夾的內容。
* 通過篩選在建立期間資料夾中允許的內容類型來優化內容建立過程，以僅顯示有效的內容類型。

通過建立適當的內容結構，跨渠道協調無頭內容創作變得更容易，以便最大限度地提高內容重複利用。 跨多個渠道利用內容極大地提高了內容生產效率和更改管理。

##### 建立良好的命名約定 {#naming-conventions}

內容片段名稱必須為內容作者的描述性。 透AEM明地處理轉義和/或截斷儲存庫級別上使用的ID的名稱。 因此，內容作者提供的邏輯名稱應始終是可讀的，並代表內容。

* 錯誤名稱： `cta_btn_1`
* 好名： `Call To Action Button`

查看 [額外資源](#additional-resources) 頁命名約AEM定中的其他文檔。

##### 不過度顯示內容嵌套 {#content-nesting}

[內容片段](#content-fragments) 用於創AEM建無頭內容。 支AEM持多達十級內容片段嵌套。 但是，必須記住，必須AEM迭代地解析父內容片段中定義的每個引用，然後檢查所有同級中是否存在任何子引用。 這些操作可以快速合併，並成為效能問題。

作為一般的經驗法則，不應將內容片段引用嵌套在五個級別之上。

#### 內容架構師 {#content-architect}

內容架構師分析對必須直接提供的資料的需求，並定義此資料的結構。 這些結構稱為 [內容片段模型](#content-fragment-models) 的上AEM界。 內容片段模型用作內容作者建立的內容片段的基礎。

在定義內容片段模型時，一種有用的方法是建立映射到使用內容的應用程式的UX元件的模型。

因為內容作者在建立新內容時不斷與模型進行交互，所以將模型與UX相協調有助於他們直觀地看到最終的數字型驗。 將此對齊進一步，您可以將表徵圖指定給表示UX元素的內容片段模型，以便作者能夠根據視覺提示直觀地選擇正確的模型。

#### 開發人員 {#developer}

開發人員負責將正在建立的內容直接與該內容的消費者AEM相結合，這些內容通常可以是單頁應用程式(SPA)、漸進式Web應用程式(PWA)、Web商店或外部的其AEM他服務。

GraphQL是無頭內容與AEM用戶之間的「粘合」。 GraphQL是查詢必AEM要內容的語言。

開發人員在規劃查詢時應牢記一些基本建議：

* 查詢不應依賴於固定路徑(`ByPath`)以檢索內容片段。
   * [內容作者對內容片段層次結構具有完全控制](#content-hierarchy) 並可以做出改變，打破這樣的查詢。
   * 查詢應選擇包含動態查詢參數的內容片段模型引用，以篩選結果以生成所需負載。
* 為獲得最佳查詢效能，請始終在中使用保留的查AEM詢。 這些將在旅途的稍後部分討論。
* GraphQL是口號「請求您確切需要的內容，並完全獲取」的聲明性。 這意味著在建立GraphQL查詢時，始終避免 `select *`-type查詢，您可以在關係資料庫中建立該查詢。

對於 [典型的無頭實AEM施](#level-1) 開發者不需要編碼知識AEM。

### 效能要求 {#performance-requirements}

要使任何項目成功，必須在建立任何內容之前考慮效能。

您必須瞭解用戶/訪問者對這些方面的期望和設計。 設定服務級別目標(SLO)，並測量它們以瞭解您是否滿足用戶的期望。

#### 通信模式 {#traffic-patterns}

要瞭解交通和交通模式，首先要收集過去所瞭解的資訊，然後預測未來幾年的預期增長。 需要考慮的一些最重要的變數：

* 您預期每小時/每天/月會調用多少個API，是否可能出現峰值和季節性？
* 有多少不同的內容作者？
* 您預計有多少內容作者同時工作？
* 內容更新的頻率是多少？
* 需要多少個內容模型？
* 需要多少個模型實例？

#### 更新頻率 {#update-frequency}

通常不同的體驗部分具有不同的內容更新頻率。 瞭解這一點對於能夠優化CDN和快取配置非常重要。 這也是 [內容架構師](#content-architects) 他們設計模型來表示您的內容。 請考慮：

* 某些類型的內容是否在特定時間段後過期？
* 是否存在特定於用戶的因素，因此無法快取？

## 下一步 {#what-is-next}

現在，您已完成了「無頭開發AEM者之旅」的這一部分，您應：

* 瞭解無頭功能AEM的基本知識。
* 瞭解使用無頭功能AEM的先決條件。
* 瞭解無頭AEM的整合級別。
* 能夠根據範圍定義項目。

您應繼續無AEM頭之旅，下次查看文檔 [使用無頭設備獲得第一次體AEM驗](path-to-first-experience.md) 您將在何處學習如何設定必要的工具以及如何開始考慮在中建模資料AEM。

## 其他資源 {#additional-resources}

雖然建議您通過查看文檔來進入無頭開發旅程的下一部分 [用無頭機實現第一次體AEM驗，](path-to-first-experience.md) 下面是一些附加的可選資源，這些資源對本文檔中提到的一些概念進行了更深入的探討，但不需要繼續進行無頭之旅。

* [無AEM頭翻譯之旅](/help/journey-headless/translation/overview.md)  — 此文檔記錄過程讓您能夠全面瞭解無頭技術、如何AEM處理無頭內容以及如何翻譯。
* [Adobe Experience Manager as a Cloud Service建築](/help/overview/architecture.md)  — 瞭解AEMas a Cloud Service的結構
* [無AEM頭Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 使用這些實踐教程，瞭解如何使用各種選項向無頭端點提供內容，並AEM選擇適合您的內容。
* [使用GraphQL API實現無頭內容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses)  — 請按照本課程瞭解中實施的GraphQL API的概AEM述。 需要通過AdobeID進行身份驗證。
* [參考AEM線WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  — 此GitHub項目包含突出顯示GraphQL APIAEM的示例應用程式。
* [創作概念](/help/sites-cloud/authoring/getting-started/concepts.md)  — 創作環境的技術文檔，AEM包括有關作者發佈設定的詳細資訊
* [發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)  — 在上發佈內容的技術文AEM檔
* [命名約定](/help/implementing/developing/introduction/naming-conventions.md)  — 中頁面命名限制的技術文AEM檔
* [多站點管理器和翻譯](/help/sites-cloud/administering/msm-and-translation.md)  — 有關強大翻譯功AEM能的技術文檔
* [AEM工作流](/help/sites-cloud/authoring/workflows/overview.md)  — 關於如何自動執行中的工作流的技術文AEM檔
* [內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)  — 內容片段的技術文檔。
* [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)  — 內容片段模型的技術文檔。
* [GraphQL技術文檔](https://graphql.org) - GraphQL定義（外部連結）
* [GraphQL API](/help/headless/graphql-api/content-fragments.md)  — 技術文檔，說明如何建立訪問和傳遞內容片段的請求
* [資產REST API](/help/assets/content-fragments/assets-api-content-fragments.md)  — 說明如何建立和修改內容片段（和其他資產）的技術文檔
* [永續查詢](/help/headless/graphql-api/persisted-queries.md)  — 關於持久查詢的技術文AEM檔
* [無頭AEM](/help/implementing/developing/headful-headless.md)  — 全面討論中提供的無頭整合級AEM別
