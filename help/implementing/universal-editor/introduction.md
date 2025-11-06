---
title: 通用編輯器簡介
description: 通用編輯器是一種現代的視覺化製作工具，可以協助您的行銷組織創造具有影響力的網頁體驗。
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 100%

---


# 通用編輯器簡介 {#introduction}

通用編輯器是一種現代的視覺化製作工具，可以協助您的行銷組織創造具有影響力的網頁體驗。

## 概觀 {#overview}

通用編輯器是一個多功能視覺化編輯器，是 Adobe Experience Manager Sites 的一部分。作者可以使用此編輯器透過所見即所得 (WYSIWYG) 的方式編輯任何無周邊或有周邊體驗。其提供以下功能：

* **即時編輯**：作者可以在預覽體驗中直接編輯內容，不需要尋找並導覽至個別內容來源。
* **視覺化編輯**：進行變更時，作者可以立即看到會如何影響實際訪客體驗，藉此將摩擦減至最低。
* **可探索的選項**：清晰標記的選項和直覺易用的使用者介面，讓作者能夠輕鬆設定後設資料及編排版面。
* **非技術性**：不需具備專業知識即可進行編輯，同時會自動執行企業品牌指引，讓整個組織能夠更容易地擴展其內容任務。
* **整合和可擴充性**：通用編輯器與 AEM 完全整合，其靈活的[擴充點](#extensibility)讓所有必要的工具能統一在單一且有凝聚力的介面內。從 AI 驅動的功能到根據您獨特業務需求而量身打造的擴充功能，讓團隊能夠簡化工作流程並輕鬆提高生產力。

總結而言：

* **作者受益**&#x200B;於通用編輯器的靈活性，因為所有形式的 AEM 內容均可使用一致的視覺化編輯功能。
* **開發人員受益於**&#x200B;通用編輯器的多功能性，因為其支援實施的真正解耦。

通用編輯器是真正的「編輯器即服務」，整體上更靈活，而最終會取代[頁面編輯器。](/help/sites-cloud/authoring/page-editor/introduction.md)

## 支援的架構 {#supported-architectures}

通用編輯器支援以下兩種主要 AEM 設定：

1. **[Edge Delivery Services](/help/edge/overview.md)**：此為首選方法，因為簡單、價值實現速度更快且效能更強。
1. **[無周邊實施](/help/headless/introduction.md)**：若您有一個現有的無周邊專案，或對於分離轉譯有特定需求，通用編輯器能進行企業級視覺化編輯，而不需要重構整個專案。其幾乎與任何架構 (SSR、CSR)、網頁框架 (Next.js、React、Astro 等)，以及託管模型 (「自備應用程式」) 相容。

>[!TIP]
>
>關於支援架構的更多詳細資訊，請參閱[通用編輯器使用案例和學習路徑](/help/implementing/universal-editor/use-cases.md)文件。

## 支援的 AEM 版本 {#aem-versions}

以下工具支援通用編輯器：

* AEM as a Cloud Service (版本 `2023.8.13099` 或以上)
* [AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * 內部部署和 AMS 託管皆支援。
* [AEM 6.5](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * 內部部署和 AMS 託管皆支援。

本文件內容為關於搭配 AEM as a Cloud Service 使用通用編輯器。

## 功能 {#features}

通用編輯器提供許多功能支援各種的使用案例，以便提高內容管理的效率。

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**：對於任何形式的網頁內容 (包括純文字、RTF 文字、媒體和後設資料) 以所見即所得的方式進行編輯。
* **[編排](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**：建立、編輯、重新排列、巢狀或刪除各種類型的內容區塊 (標題、按鈕、Teaser、區段、嵌入等)。
* **[版面](/help/sites-cloud/authoring/universal-editor/templates.md)**：運用頁面範本、套用視覺樣式，及使用欄、輪播和摺疊式等區塊來編排版面。
* **[裝置模擬](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**：在編輯時，預覽在不同訪客裝置上呈現的內容並進行最佳化。
* **全通路**：在多個通道上重複使用結構化和非結構化的內容。
* **[本地化](/help/sites-cloud/authoring/universal-editor/inheritance.md)**：透過 MSM 簡化內容翻譯工作流程，並有效率地處理本地化內容繼承。
* **一致性**：確保遵守品牌指引，並保持所有內容的一致性。
* **安全性**：[強制執行存取控制](/help/implementing/universal-editor/authentication.md)、保護內容完整性，並透過[強大的版本設定](/help/sites-cloud/authoring/sites-console/page-versions.md)來追蹤變更。
* **[發佈](/help/sites-cloud/authoring/universal-editor/publishing.md)**：直接在編輯器中整合審閱、核准和發佈工作流程。
* **統一**：與 AEM 工具 (例如 [Sites 控制台、](/help/sites-cloud/authoring/sites-console/introduction.md)[內容片段編輯器](/help/sites-cloud/administering/content-fragments/overview.md)等) 完全整合，提供統一的製作體驗。

## 可擴充性 {#extensibility}

通用編輯器不僅開箱即可用而且功能強大，還提供許多擴充的可能性。

* **擴充功能**&#x200B;數量眾多而且隨時可用，能夠支援各種需求，例如支援工作流程、產生變化版本，以及支援實驗等等。
* **可擴充的使用者介面**&#x200B;讓您能夠善用與現成擴充功能相同的底層框架，建立自己的擴充功能並獲得最大的靈活性，以便適應您的專案需求。
* **擴充點** (例如區塊、自訂資料類型和事件) 能夠在使用者介面以外，與自訂業務需求緊密整合。

>[!TIP]
>
>關於通用編輯器可擴充性的更多詳細資訊，請參閱[擴充通用編輯器](/help/implementing/universal-editor/extending.md)文件。

## Universal Editor 和內容片段編輯器 {#universal-editor-content-fragment-editor}

乍看之下，Universal Editor 和內容片段編輯器的編輯功能似乎很相似。然而，這些編輯器的功能大不相同，其完成的工作與行銷從業人員不同。

### 內容片段編輯器 {#content-fragment-editor}

行銷從業人員希望建立內容而不必關心其版面，以便它可以在多種體驗環境中重複使用。

* 要達成的基本工作是擴展內容策略。

### Universal Editor {#universal-editor}

行銷從業人員會想建立根據指定內容版面量身定制的內容，以提供卓越的體驗。

* 要達成的基本工作是與讀者建立可靠的聯繫。

## 限制 {#limitations}

當您探索通用編輯器並進一步在您的專案中實施時，請務必記住以下限制。

* 單一頁面上作為檢測所參照的 AEM 資源 (內容片段、頁面、體驗片段、資產等)，不得超過 25 項。
* 所支援的 AEM 後端僅包括 AEM as a Cloud Service、[AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)，以及 [AEM 6.5](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)。
* AEM as a Cloud Service 的版本必須是 `2023.8.13099` 或以上。
* 內容作者必須擁有其自己的個人 Experience Cloud 帳戶。
* 做為 AEM 的一部分，通用編輯器[與 AEM 支援相同的桌面瀏覽器。](/help/overview/supported-platforms.md)
   * 不支援這些瀏覽器的行動版本。

{{ip-allow-lists-ue}}

## 後續步驟 {#next-steps}

請參閱[通用編輯器使用案例和學習路徑](/help/implementing/universal-editor/use-cases.md)文件，了解更多關於通用編輯器常見使用案例的詳細資訊，並找到合適的文件資源來支援您的專案。
