---
title: 使用AEM無頭式的第一次體驗路徑
description: 在AEM無頭式開發人員歷程的這部分中，您將了解在AEM中實作第一個無頭式體驗的步驟，包括規劃考量事項，並了解最佳實務，讓路徑盡可能順暢。
source-git-commit: ddd320ae703225584d4a2055d0f882d238d60987
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---


# 使用AEM無頭式{#path-to-first-experience}的第一個體驗路徑

在[AEM無頭開發者歷程的這部分中，您將了解在AEM中實作第一個無頭體驗的步驟，包括規劃考量事項，並了解最佳實務，讓路徑盡可能順暢。](overview.md)

## 迄今為止的故事{#story-so-far}

在AEM無頭歷程的上一份檔案中，[開始使用AEM無頭作為Cloud Service](getting-started.md)您已了解無頭CMS的基本原理，您現在應該：

* 了解AEM無頭功能的基本概念。
* 了解使用AEM無頭功能的必要條件。
* 請注意AEM無頭整合層級。
* 能夠根據範圍定義專案。

本文以這些基本知識為基礎，讓您了解如何準備您自己的AEM無頭專案。

## 目標 {#objective}

本檔案可協助您了解實作第一個專案所需的步驟。 閱讀後，您應：

* 了解設計內容時的重要規劃考量事項。
* 了解在AEM中實作無頭的步驟。
* 了解需要哪些必要工具和AEM設定。
* 了解最佳實務，讓無頭的歷程順暢、保持內容產生的效率，並確保內容能快速傳遞。

## 需求 {#requirements}

繼續閱讀本檔案之前，請確定您已檢閱AEM Headless Developer Journey中的[Getting Started with a AEM Headless as a Cloud Service](getting-started.md)上一份檔案，確定您：

* 滿足所列要求。
* 已考慮您自己的專案定義，包括範圍、角色和效能。

## 成功計畫{#planning-for-success}

若要開始您的第一個AEM無頭專案，您必須確保擁有的內容模型可支援您要在所有管道進行的個人化和更新。

與AEM分開，如果您要建置用戶端應用程式，也想要確定您已設定正確的開發環境，以便針對以AEM為Cloud Service的API呼叫測試用戶端。

### 定義內容模型和API {#defining-models}

您想要推動一致的體驗，並管理各管道的個人化行銷活動，因此您可以將每個個別管道和表面視為要交付的各自不同內容結構。 然而，要維護每個管道都有各自的內容模型，將是一項挑戰。

相反地，您應根據組織原則（例如品牌和產品階層、商品或曲面的類別或客戶歷程中的步驟），考慮不同曲面上的內容的相關性。 例如，如果您有一組表面支援您製造的特定品牌汽車，則您可能希望從內容模型開始，以獲取對整輛汽車來說是正確的常規資訊，然後具有更具上下文的特定元素，例如汽車啟動時到出現服務問題時所需的內容。 這種模型將強制繼承一般汽車品牌內容，同時允許根據所需的特定上下文進行換班。 這也有助於日後管理此內容的更新，因為您可以根據角色強制執行控制，例如整個汽車品牌的整體行銷人員或產品經理，與負責「起動汽車」體驗的作者比較。

一旦您擁有了內容模型，並清楚了解了內容需要呈現到的各種客戶端後，您就需要確保將與訪問各種內容模型相關聯的GraphQL/API發佈給所有需要這些內容的客戶端。 如何存取特定內容有不同的選項。 您可以要求靜態的特定內容片段，以啟用內容快取和高效能。 您也可以要求動態產生的內容，而這需要更多處理。 確保客戶運用最符合其業務需求的API。

## 了解您的環境{#understanding-environments}

AEM中有三種環境類型：開發、測試和生產。

開發環境（您可以有多個環境）是實驗和嘗試想法的安全場所。 在專案的初始階段，Adobe建議使用開發環境來嘗試內容模型的變異，並查看哪個模型提供曲面的預期輸出。

無頭專案的測試環境可用來在新AEM產品發行推出至生產環境之前驗證。 請保留生產內容模型的最新清單和內容的子集，這樣當您進行變更或AEM發行引入變更時，您就可以呈現JSON檔案來比較它們，仍會提供相同的輸出

內容作者可在生產環境中建立和管理其實際內容。 生產中的模型變更必須謹慎執行，並考慮到回溯相容性。

在開發階段，建議您使用開發和測試環境。 當您改用效能測試時，會想要改用生產環境。

### 開發人員與內容作者的合作 {#cooperation}

開發人員需要使用填入的內容模型來設定AEM開發環境。 開發人員開發用戶端，當內容作者仍在建立內容時，會從AEM無頭取用內容。 這就是為什麼API定義非常重要。 透過運用AEM SDK，開發人員可建立測試連結，以建立用戶端和單元測試，確保用戶端能夠正確轉譯內容。

內容作者會根據已在測試環境中定義的內容模型來建立內容。 使用內容片段製作工具，作者將建立新內容片段或編輯現有內容片段。 發佈前，作者可與開發人員合作，將內容模型推送至開發，或僅供作者預覽內容模型在用戶端中的外觀，借此預覽在用戶端中的外觀。

## 設定 {#setup}

開始使用AEM中的無頭功能前，您必須確定所有必要功能皆已啟用。 本節概述必要項目。 在[AEM無頭開發人員歷程中會詳細說明實際步驟，以完成這些步驟。](#overview.md)

您也可以選擇參閱[其他資源](#additional-resources)以取得個別主題的詳細資訊。

### 設定 {#configuration}

1. 啟用內容片段
1. 啟用GraphQL
1. 設定無頭式SDK

## 實作您的第一個AEM Headless應用程式

以下概述使用AEM實作您的第一個無頭應用程式以傳送內容所需的項目。 如需執行這些步驟的詳細說明，請參閱無頭式開發人員歷程的後續章節。

1. 建立內容片段模型
1. 建立內容片段
1. 使用GraphQL查詢內容

## 最佳作法 {#best-practices}

一個無頭的項目不僅因為實施了技術而成功，還因為有良好的規劃和項目治理。 以下是內容作者和開發人員在規劃專案時應謹記的一些最佳實務。

### 組織內容{#organizing-content}

* 盡可能使結構複雜，但請盡可能簡單。 更簡單的內容結構有助於簡化內容治理並改進系統效能。
* 在策略中優先重複使用內容。 建立子模型和內容參考，以便在多個較高層級的模型和管道中重複使用。
* 讓內容結構盡可能不言自明，讓內容作者可快速學習並適應製作工作。
* 如果您有存取限制，請嘗試將您的內容模型與存取需求一致。
* 當您有存取需求時，這些需求應會驅動您的內容階層。 將內容分組，由同一組人員編輯。
* 將類似內容分組到資料夾中。
   * 內容作者更有可能複製並貼上現有內容以建立新內容。 因此，在相同資料夾中完成此操作可讓其更有效率。
   * AEM允許設定每個資料夾允許的模型，因此&#x200B;**建立新**&#x200B;按鈕將僅顯示該位置支援的模型。
* 若在模型中設定根資料夾，則可簡化新內容片段的內嵌內容片段編輯器建立作業。 從業者不必選擇位置，只需提供名稱，即可開始編輯新參照。

### 製作內容 {#authoring}

* 針對管道特定版本的內容，請考慮使用內容片段變體。 系統會與內容主版同步變數，以簡化內容變更管理。
* 邀請其他內容製作者檢閱內容，並提供附註和意見回饋，這些可在內容片段編輯器中取得，並可在內容片段管理控制台中跨全域取得。
* 盡可能少使用必要元素，讓一切保持順暢。 強制元素可封鎖工作流程。

### 製作全域內容 {#localization}

* 建立內容翻譯的規則與控管。 要降低系統負載，請將轉換建立為非同步過程，可以以較長的時間間隔運行。 請預留時間進行本地化品質控制和錯誤修正。
* 利用翻譯技術系統提供的所有功能，這些功能可以與AEM整合，如翻譯記憶庫。
* 了解多媒體內容（例如影像和視訊）是否需要本地化。

## 下一步是什麼{#what-is-next}

現在您已完成AEM Headless Developer Journey的這一部分，您應：

* 了解設計內容時的重要規劃考量事項。
* 了解在AEM中實作無頭的步驟。
* 了解需要哪些必要工具和AEM設定。
* 了解最佳實務，讓無頭的歷程順暢、保持內容產生的效率，並確保內容能快速傳遞。

我們希望您能以此基礎知識為基礎，充分了解AEM Headless的強大功能和彈性，以便您能將其運用於自己的專案。 要執行此操作，您有選項。

### 選擇自己的冒險{#choose-your-path}

無論您的學習方式為何，Adobe都希望您在開始使用AEM Headless專案時能成功。

* 如果您偏好繼續&#x200B;**了解無頭概念和AEM無頭技術**，您應繼續進行AEM無頭歷程，方法是先檢閱檔案[如何以AEM內容模型](model-your-content.md)來建模您的內容，了解如何在AEM中建立內容結構模型。
* 如果您偏好透過&#x200B;**學習**，您可以跳至[AEM Headless實作快速入門教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)，透過實作簡單專案以公開AEM Headless內容，直接跳至AEM Headless開發。

## 其他資源 {#additional-resources}

雖然建議您透過檢閱檔案[如何以AEM內容模型為內容模型建立模型，以繼續進行無頭式開發歷程的下一個階段，但以下是一些額外的選用資源，可深入探討本檔案中提及的一些概念，但您不需要繼續進行無頭式開發歷程。](model-your-content.md)

* [AEM Sites as aCloud Service無頭開發](/help/implementing/developing/headless/introduction.md)  — 快速簡介，指導AEM無頭開發人員使用必要功能
* [AEM無頭式Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 使用這些實作教學課程，探索如何使用各種選項，透過AEM將內容傳遞至無頭式端點，並選擇適合您的方式。
* [使用GraphQL API進行無周邊內容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses)  — 請依照本課程了解在AEM中實作的GraphQL API的概觀。需要透過AdobeID進行驗證。
* [AEM指南WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  — 此GitHub專案包含醒目提示AEM GraphQL API的範例應用程式。
* [Adobe Experience Manager as a Cloud Service架構簡介](/help/core-concepts/architecture.md)  -AEM架構完整概觀
* [無頭式入門指南](/help/implementing/developing/headless/introduction.md#getting-started)  — 為熟悉AEM的使用者快速介紹AEM無頭式功能。
* [建立內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 內容片段模型的技術檔案
* [建立內容片段](/help/assets/content-fragments/content-fragments.md)  — 內容片段的技術檔案
* [使用GraphQL查詢內容](/help/assets/content-fragments/graphql-api-content-fragments.md) - GraphQL API的技術檔案
