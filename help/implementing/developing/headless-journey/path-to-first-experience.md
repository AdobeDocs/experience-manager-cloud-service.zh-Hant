---
title: 使用無頭體驗的首次體AEM驗
description: 在這部分的AEM無頭開發人員歷程中，您將瞭解實作您第一次無頭體驗的步驟，包括規劃考量AEM，並學習最佳實務，讓您的路途盡可能順暢。
hide: true
hidefromtoc: true
index: false
exl-id: 257fc173-6bfb-4b60-b66c-6d6bdd5cf13f
translation-type: tm+mt
source-git-commit: 635768f63c604d1c1892de57c55693da6a0fe954
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 0%

---

# 使用無頭&lt;a0/AEM>的首次體驗路徑{#path-to-first-experience}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

在[AEM Headless Developer Journey（無頭開發人員歷程）中，您將瞭解實作您第一次無頭體驗（包括規劃考量）的步驟，並學習最佳實務，讓您的路徑盡可能順暢。](overview.md)

## 到目前為止的故事{#story-so-far}

在上一份無頭歷程的AEM檔案中，[開始使用無頭作為Cloud Service](getting-started.md)您瞭解了無頭CMS的基本理論，您現在應該：

* 瞭解無頭功能AEM的基本概念。
* 瞭解使用無頭功能的必AEM要條件。
* 請注意無AEM頭整合等級。
* 能夠根據範圍定義專案。

本文以這些基礎為基礎，讓您瞭解如何準備自己的無頭AEM專案。

## 目標 {#objective}

本檔案可協助您瞭解建置第一個專案所需的步驟。 閱讀後，您應：

* 瞭解設計內容時的重要規劃考量。
* 瞭解在中實作無頭的步驟AEM。
* 瞭解需要哪些必要AEM的工具和配置。
* 瞭解最佳實務，讓您的無頭體驗更順暢、讓內容製作更有效率，並確保內容能快速傳遞。

## 要求{#requirements}

繼續本檔案之前，請確定您已檢閱AEMHeadless Developer Journey [Getting Started with AEM Headless as a direction](getting-started.md)中的先前檔案，確定您：

* 滿足所列要求。
* 已考慮您自己的項目定義，包括範圍、角色和績效。

## 成功規劃{#planning-for-success}

若要開始您的第AEM一個無頭專案，您需要確保您擁有的內容模型，以支援您想要在所有通道上進行的個人化和更新。

另AEM外，如果您要建立用戶端應用程式，您也要確定您已設定適當的開發環境，以便針對Cloud Service的API呼叫來測試用戶AEM端。

### 定義內容模型和API {#defining-models}

您想要推動一致的體驗並管理跨通道的個人化宣傳，因此您可以將每個通道和表面視為其要傳遞的獨特內容結構。 然而，讓每個通道都有其專屬的內容模型，將是維護的挑戰。

相反地，您應考慮不同表面的內容如何根據組織原則（例如品牌和產品階層、商品或表麵類別或客戶歷程中的步驟）來關聯。 例如，如果您有一組表面支援您製造的特定品牌汽車，您可能想要從內容模型開始，以瞭解整部汽車的一般資訊，然後擁有更符合情境的特定元素，例如當汽車啟動時到出現服務問題時所需的內容。 這種模型將強制繼承一般汽車品牌內容，同時允許根據所需的特定上下文進行變更。 它也有助於未來管理此內容的更新，因為您可以根據角色（例如整個汽車品牌的整體行銷人員或產品經理）與負責「起動車」體驗的作者)，來實施控制。

一旦您擁有內容模型並清楚檢視內容需要呈現的各種用戶端後，您就需要確保將與存取各種內容模型相關的GraphQL/API發佈給所有需要這些內容的用戶端。 存取特定內容的方式有不同的選項。 您可以要求靜態的特定內容片段，以啟用內容快取和更高效能。 您也可以要求動態產生的內容，而需要進行更多處理。 確保客戶運用最符合其商業需求的API。

## 瞭解您的環境{#understanding-environments}

在AEM三種環境類型中：開發、測試和生產。

開發環境（您可擁有多個開發環境）是您進行實驗和嘗試創意的安全場所。 在項目的初始階段，Adobe建議使用開發環境來嘗試各種內容模型，並查看哪些模型提供了曲面的預期輸出。

無頭專案的測試環境可用來在新產品AEM推出至生產環境之前驗證新產品版本。 保留生產內容模型的最新清單和內容子集，讓您讓轉譯的JSON檔案進行比較，仍能提供相同的輸出，因為您進行變更或發行AEM會引入變更

製作是內容作者建立和管理其實際內容的地方。 生產中的模型變更必須謹慎，並且要考慮到向後相容性。

在開發階段，建議您使用開發和測試環境。 當您轉向效能測試時，您會想要移至生產環境。

### 開發人員與內容作者的合作{#cooperation}

開發人員需AEM要使用已填入的內容模型來設定開發環境。 開發人員會開發用戶端，當內容作者仍在建AEM立內容時，會從無頭部使用內容。 這就是為什麼API定義非常重要。 借由運用AEMSDK，開發人員可建立測試掛接，以建立用戶端和裝置測試，以確保用戶端能夠正確呈現內容。

內容作者會根據已在測試環境中定義的內容模型來建立內容。 使用內容片段製作工具，作者會建立新的內容片段或編輯現有的內容片段。 在發佈之前，作者可與開發人員合作，將內容模型推播至開發上，或設定開發人員環境，讓作者預覽它在用戶端中的外觀，以預覽它在用戶端中的外觀。

## 設定 {#setup}

開始使用無頭功能之AEM前，您需要確定所有必要的功能都已啟用。 本節概述了所需的內容。 要完成這些步驟的實際步驟將在[無頭開發人AEM員歷程中詳細說明。](#overview.md)

您也可以選擇參考[其他資源](#additional-resources)，以取得個別主題的詳細資訊。

### 設定 {#configuration}

1. 啟用內容片段
1. 啟用GraphQL
1. 設定無頭SDK

## 實作您的第一個無AEM頭應用程式

這是建置您第一個無頭應用程式以傳遞內容所需AEM的概觀。 如何執行這些步驟，將會在無頭開發人員旅程的後續部分詳細說明。

1. 建立內容片段模型
1. 建立內容片段
1. 使用GraphQL查詢內容

## 最佳作法 {#best-practices}

一個無頭項目之所以成功，不僅是因為實施了技術，還因為良好的規劃和項目治理。 以下是內容作者和開發人員在規劃專案時應牢記的一些最佳實務。

### 組織您的內容{#organizing-content}

* 使結構盡可能複雜，但盡可能保持簡單。 更簡單的內容結構有助於簡化內容管理並改善系統效能。
* 在策略中優先重複使用內容。 建立子模型和內容參考，以便跨多個較高層級的模型和通道重複使用。
* 讓內容結構盡可能自我解釋，讓內容作者可以快速學習並調整以執行編寫工作。
* 如果您有存取限制，請嘗試將內容模型與存取要求一致。
* 當您有存取需求時，這些需求應會驅動您的內容階層。 將由同一群人編輯的內容分組在一起。
* 將類似內容分組至資料夾。
   * 內容作者更可能會複製並貼上現有的內容，以建立新內容。 因此，在相同資料夾中執行此動作可提高效率。
   * 允許AEM為每個資料夾設定允許的型號，因此&#x200B;**建立新**&#x200B;按鈕將僅顯示該位置支援的型號。
* 如果在模型中設定根資料夾，則可簡化建立新內容片段的內嵌內容片段編輯器。 從業人員不必選擇位置，只需提供名稱，就可以開始編輯新參照。

### 編寫內容{#authoring}

* 針對特定頻道版本的內容，請考慮使用內容片段變化。 變數會與內容主版同步，以簡化內容變更管理。
* 邀請其他內容製作者檢閱內容，並提供附註和注釋意見回饋，這些註解和注釋可在內容片段編輯器中使用，而全域可在內容片段管理控制台中跨片段使用。
* 只要盡可能少的必備元素，就能讓事物保持動態。 強制元素可以封鎖工作流程。

### 編寫全域內容{#localization}

* 建立內容翻譯的規則與管理。 為了減少系統負載，請將轉換建立為非同步過程，該過程可以在較長的時間間隔內運行。 為本地化質量控制和錯誤修正留出時間。
* 利用翻譯技術系統提供的所有功能，與翻譯記憶庫AEM等整合。
* 瞭解多媒體內容（例如影像和視訊）是否需要本地化。

## 下一個{#what-is-next}

現在，您已完成這部分的無AEM頭開發人員旅程，您應：

* 瞭解設計內容時的重要規劃考量。
* 瞭解在中實作無頭的步驟AEM。
* 瞭解需要哪些必要AEM的工具和配置。
* 瞭解最佳實務，讓您的無頭體驗更順暢、讓內容製作更有效率，並確保內容能快速傳遞。

我們希望您以此基礎知識為基礎，充分瞭解AEMHeadless的強大功能和靈活性，以便您能夠將其運用在自己的專案中。 要做到這一點，您有選擇。

### 選擇您自己的冒險{#choose-your-path}

不論您的學習風格為何，Adobe都希望您能成功開始使用您的AEMHeadless專案。

* 如果您偏好&#x200B;**繼續學習無頭概念和無頭技術AEM**，您應繼續無頭歷程AEM，先檢閱檔案[如何將您的內容建模為內容模型AEM](model-your-content.md)，以瞭解如何在中建模您的內容結構AEM。
* 如果您偏好&#x200B;**透過執行**&#x200B;來學習，可跳至[開始使用AEMHeadless實作教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)，透過實作簡單專案來公開無頭內容，您將直接跳至無頭開AEM發。

## 其他資源 {#additional-resources}

雖然建議您透過檢閱檔案[如何將您的內容模型化為內容模型，進入無頭開發歷程的下一部分，但](model-your-content.md)以下是一些額外的可選資源，可讓您更深入地瞭解本檔案中提及的一些概念，但您不需要繼續進行無頭開發歷程。

* [AEM Sites的無頭開發(Headless Development forCloud Service)](/help/implementing/developing/headless/introduction.md) -簡介，讓無頭開發人員具備必要AEM的功能
* [AEM無頭Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) -使用這些實際操作教學課程來探索如何使用各種選項，將內容傳送至無頭端點，AEM並選擇適合您的內容。
* [使用GraphQL API進行無頭內容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) -請遵循本課程，以瞭解中實施的GraphQL APIAEM。需要透過AdobeID進行驗證。
* [指AEM南WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  —— 此GitHub專案包含反白顯示GraphQL API的AEM範例應用程式。
* [Adobe Experience Manager建築Cloud Service簡介](/help/core-concepts/architecture.md) —建築概AEM述
* [無頭入門指南](/help/implementing/developing/headless/introduction.md#getting-started) -為已熟悉的使用AEM者快速簡介無頭功AEM能。
* [建立內容片段模型](/help/assets/content-fragments/content-fragments-models.md) -內容片段模型的技術檔案
* [建立內容片段](/help/assets/content-fragments/content-fragments.md) -內容片段的技術檔案
* [使用GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md)  - GraphQL API的技術文檔查詢內容
