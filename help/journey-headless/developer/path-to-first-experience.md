---
title: 使用無頭設備獲得第一次體AEM驗
description: 在「無頭開發AEM者之旅」的這一部分，您將瞭解實施第一次無頭體驗的步驟AEM，包括規劃考慮事項，還將學習最佳實踐，使您的路徑盡可能順暢。
exl-id: 172ad8d8-5067-4452-bf91-1eea9a39a7bc
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 0%

---

# 使用無頭設備獲得第一次體AEM驗 {#path-to-first-experience}

在 [無AEM頭開發者之旅，](overview.md) 您將瞭解在規劃考慮事項等方面實施第AEM一次無頭體驗的步驟，並學習最佳實踐，使您的路徑盡可能順暢。

## 到目前為止的故事 {#story-so-far}

在前一篇無頭旅AEM程中， [無頭as a Cloud Service入AEM門](getting-started.md) 你學到了無頭CMS的基本理論，現在你應該：

* 瞭解無頭功能AEM的基本知識。
* 瞭解使用無頭功能AEM的先決條件。
* 瞭解無頭AEM的整合級別。
* 能夠根據範圍定義項目。

本文基於這些基礎知識，以便您瞭解如何準備自己的無AEM頭項目。

## 目標 {#objective}

本文檔可幫助您瞭解實施第一個項目所需的步驟。 讀完後，您應：

* 瞭解設計內容時的重要規劃考慮事項。
* 瞭解中實施無頭的步驟AEM。
* 瞭解需要哪些必要AEM的工具和配置。
* 瞭解最佳做法，使您的無頭之旅順暢，保持內容生成的高效性，並確保內容能快速交付。

## 要求 {#requirements}

在繼續本文檔之前，請確保您已審閱了「無頭開發人員旅程」中AEM的上一文檔， [無頭as a Cloud Service入AEM門](getting-started.md) 確保您：

* 滿足所列要求。
* 已考慮了您自己的項目定義，包括範圍、角色和效能。

## 成功規劃 {#planning-for-success}

要啟動第一個無AEM頭項目，您需要確保您擁有一個內容模型，該模型支援您想要在所有渠道中進行的個性化和更新。

另AEM外，您還希望確保在構建客戶端應用程式時設定了適當的開發環境，以便您能夠針對as a Cloud Service的API調用test客戶端AEM。

### 定義內容模型和API {#defining-models}

您希望推動一致的體驗，並管理跨渠道的個性化活動，因此您可以將每個渠道和表面視為其要交付的獨特內容結構。 但是，讓每個頻道都有自己的內容模型將是一個挑戰。

相反，您應根據組織原則考慮不同曲面上的內容如何關聯，如品牌和產品層次結構、商品或曲面的類別或客戶行程中的步驟。 例如，如果您有一組曲面支援您製造的特定品牌的汽車，則您可能希望從內容模型開始，以瞭解適用於整個汽車的一般資訊，然後包含更多特定元素，例如汽車啟動時到出現服務問題時所需的內容。 這種模型將強制對一般汽車品牌內容進行繼承，同時允許根據需要的特定上下文進行轉換。 它還有助於將來對此內容的更新進行管理，因為您可以根據角色強制實施控制，例如整個汽車品牌的整體營銷員或產品經理與負責「起步汽車」體驗的作者。

一旦您擁有了內容模型並清楚地查看了內容需要呈現到的各種客戶端，您需要確保將與訪問各種內容模型相關聯的GraphQL/API發佈給所有需要此內容的客戶端。 如何訪問某些內容有不同的選項。 您可以請求靜態的特定內容，這樣可以快取內容並提高效能。 您還可以請求動態生成的內容，這將需要更多處理。 確保客戶機正在利用最高效的API來滿足其業務需要。

## 瞭解您的環境 {#understanding-environments}

在AEM以下三種環境中：開發、分段和生產。

開發環境（您可以有多個環境）是進行實驗和嘗試想法的安全場所。 在項目的初始階段，Adobe建議使用開發環境來嘗試內容模型的變化，並查看哪些內容為曲面提供了預期的輸出。

無頭項目的登台環境用於在新產品AEM發佈到生產之前驗證新產品發佈。 保留生產內容模型的最新清單以及內容的子集，這樣您就可以讓已呈現的JSON檔案進行比較，以便在您進行更改或版本引入更改時仍提供相同的輸出AEM。

製作是內容作者建立和管理其實際內容的地方。 生產中的模型更改必須謹慎進行，並且要考慮到向後相容性。

在開發階段，建議您使用開發和試運行環境。 在轉到效能測試時，您將希望移到生產環境。

### 開發人員與內容作者的合作 {#cooperation}

開發人員需AEM要使用填充的內容模型設定開發環境。 開發人員開發客戶端，該客戶端將從無AEM頭部使用內容，因為內容作者仍在建立內容。 這就是為什麼API定義非常重要。 通過利AEM用SDK，開發人員可以建立test掛接，以便建立客戶端和設備test，以確保客戶端能夠正確呈現內容。

內容作者根據在暫存環境中定義的內容模型建立內容。 使用內容片段創作工具，作者將建立新內容片段或編輯現有內容片段。 在發佈之前，作者可以通過與開發人員合作將內容模型推入開發或設定開發人員環境，以便作者預覽其在客戶端中的外觀，從而預覽其在客戶端中的外觀。

## 設定 {#setup}

在開始使用無頭功能之前AEM，需要確保啟用所有必需的功能。 本節概述了所需內容。 完成這些步驟的實際步驟將在 [無AEM頭開發者之旅。](#overview.md)

您還可以根據需要參考 [額外資源](#additional-resources) 的子菜單。

### 設定 {#configuration}

1. 啟用內容片段
1. 啟用GraphQL
1. 設定無頭SDK

## 實施您的第一個無AEM頭應用

這是對實施第一個無頭應用所需內容的AEM概述。 如何執行這些步驟將在無頭開發人員旅程的後半部分中詳細描述。

1. 建立內容片段模型
1. 建立內容片段
1. 使用GraphQL查詢內容

## 最佳作法 {#best-practices}

一個無頭項目之所以成功，不僅是因為實施了技術，還因為良好的規劃和項目治理。 以下是內容作者和開發人員在規劃項目時要牢記的一些最佳做法。

### 組織內容 {#organizing-content}

* 使結構盡可能複雜，但盡可能簡單。 更簡單的內容結構有助於優化內容治理並提高系統效能。
* 在您的策略中優先重用內容。 建立子模型和內容引用，這些子模型和內容引用可以跨多個更高級別的模型和渠道重複使用。
* 使內容結構盡可能自我解釋，以便內容作者可以快速學習和適應創作任務。
* 如果您有訪問限制，請嘗試將內容模型與訪問要求相協調。
* 當您有訪問要求時，他們應驅動您的內容層次結構。 將由同一組人員編輯的內容分組在一起。
* 將類似內容分組到資料夾中。
   * 內容作者更有可能複製和貼上現有內容以建立新內容。 因此，在同一資料夾中執行此操作會使其效率更高。
   * 允AEM許按資料夾設定允許的模型 **新建** 按鈕將僅顯示該位置支援的模型。
* 如果在模型中設定了根資料夾，則可以簡化新內容片段的串聯內容片段編輯器建立。 這樣，從業人員就不必選擇一個位置，只需提供一個名稱，就可以開始編輯新參照。

### 創作內容 {#authoring}

* 對於內容的頻道特定版本，請考慮使用內容片段變體。 變體將與內容主節點同步以優化內容更改管理。
* 邀請其他內容製作者審閱內容並提供帶有注釋和注釋的反饋，這些注釋和注釋可在內容片段編輯器中提供，並可在內容片段Admin Console中的片段之間進行全局訪問。
* 保持動態，盡可能少地使用強制元素。 強制元素可以阻止工作流。

### 創作全局內容 {#localization}

* 建立內容翻譯的規則和治理。 要減少系統負載，請將轉換建立為可以以較長時間間隔運行的非同步進程。 為本地化質量控制和錯誤修復留出時間。
* 利用您的翻譯技術系統提供的所有功能，這些功能可AEM以與翻譯記憶庫整合。
* 瞭解富媒體內容（如影像和視頻）是否需要本地化。

## 下一步是什麼 {#what-is-next}

現在，您已完成了「無頭開發AEM者之旅」的這一部分，您應：

* 瞭解設計內容時的重要規劃考慮事項。
* 瞭解中實施無頭的步驟AEM。
* 瞭解需要哪些必要AEM的工具和配置。
* 瞭解最佳做法，使您的無頭之旅順暢，保持內容生成的高效性，並確保內容能快速交付。

我們希望您以這一基礎知識為基礎，充分瞭解AEM Headless的威力和靈活性，以便您能夠利用它進行自己的項目。 要做到這一點，你有選擇。

### 選擇您自己的冒險 {#choose-your-path}

無論你的學習方式如何，Adobe都希望你在開始你的無頭項目時AEM獲得成功。

* 如果您希望繼續 **瞭解無頭概念和無頭AEM技術**，您應通過下AEM次查看文檔來繼續無頭旅行 [如何將內容建模為內AEM容模型](model-your-content.md) 學習如何在中建模內容結AEM構。
* 如果你願意 **學習**&#x200B;你可以跳到 [無頭AEM動手教程入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) 通過實施一個簡單的項AEM目來公開無頭內容，您將直接進入無頭AEM開發。

## 其他資源 {#additional-resources}

雖然建議您通過查看文檔來進入無頭開發旅程的下一部分 [如何將內容建模為內AEM容模型，](model-your-content.md) 下面是一些附加的可選資源，這些資源對本文檔中提到的一些概念進行了更深入的探討，但不需要繼續進行無頭之旅。

* [無AEM頭翻譯之旅](/help/journey-headless/translation/overview.md)  — 此文檔記錄過程讓您能夠全面瞭解無頭技術、如何AEM處理無頭內容以及如何翻譯。
* [AEM Sitesas a Cloud Service](/help/headless/introduction.md)  — 快速介紹Headless開發AEM人員的定位及其必要功能
* [無AEM頭Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 使用這些實踐教程，瞭解如何使用各種選項向無頭端點提供內容，並AEM選擇適合您的內容。
* [使用GraphQL API實現無頭內容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses)  — 請按照本課程瞭解中實施的GraphQL API的概AEM述。 需要通過AdobeID進行身份驗證。
* [參考AEM線WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  — 此GitHub項目包含突出顯示GraphQL APIAEM的示例應用程式。
* [Adobe Experience Manager as a Cloud Service建築](/help/overview/architecture.md)  — 體系結構的完整概AEM述
* [無頭設定](/help/headless/introduction.md#getting-started)  — 快速介紹AEM已熟悉的無頭功能AEM。
* [建立內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 內容片段模型技術文檔
* [建立內容片段](/help/assets/content-fragments/content-fragments.md)  — 有關內容片段的技術文檔
* [使用GraphQL查詢內容](/help/headless/graphql-api/content-fragments.md) - GraphQL API的技術文檔
