---
title: Universal Editor 簡介
description: Universal Editor是現代化的視覺化撰寫工具，旨在讓您的行銷組織能夠產生具影響力的Web體驗。
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 08997c760bf1d609dce1dd17de0c549a26083917
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 13%

---


# Universal Editor 簡介 {#introduction}

Universal Editor是現代化的視覺化撰寫工具，旨在讓您的行銷組織能夠產生具影響力的Web體驗。

## 概觀 {#overview}

通用編輯器是多功能的視覺化編輯器，屬於Adobe Experience Manager Sites的一部分。 它可讓作者對任何Headless或Headful體驗執行「所見即所得」(WYSIWYG)編輯。 它提供：

* **即時編輯**：作者可以直接在預覽體驗中編輯內容，不需要尋找並導覽至個別內容來源。
* **Visual Editing**：進行變更時，作者會立即看到變更如何影響實際訪客體驗，將摩擦減至最低。
* **可探索的選項**：標籤清楚的選項和直覺式UI可讓作者輕鬆設定中繼資料和撰寫版面配置。
* **非技術性**：不需要專業知識即可進行編輯，而公司品牌指引會自動強制執行，方便您組織內內容工作的擴展。
* **整合與擴充性**：與AEM完全整合，Universal Editor的彈性[擴充點](#extensibility)可讓所有重要工具在單一內建介面中整合。 從AI支援的功能，到根據您獨特業務需求量身打造的自訂擴充功能，讓團隊能夠輕鬆簡化工作流程並提高生產力。

摘要：

* **作者受益於**&#x200B;通用編輯器的彈性，因為它支援對所有形式的AEM內容進行相同一致的視覺化編輯。
* **開發人員受益於** Universal Editor的多功能性，因為它支援實作的真正解耦。

作為真正的editor-as-a-service並且整體上更靈活，通用編輯器打算最終取代[頁面編輯器。](/help/sites-cloud/authoring/page-editor/introduction.md)

## 支援的架構 {#supported-architectures}

Universal Editor支援下列兩個AEM主要設定：

1. **[Edge Delivery Services](/help/edge/overview.md)**：這是首選的方法，因為其簡單性、更快的價值實現和增強效能。
1. **[Headless實作](/help/headless/introduction.md)**：如果您有現有的Headless專案或分離轉譯的特定需求，通用編輯器可讓您進行企業級視覺化編輯，而不需要重構整個專案。 它幾乎與任何架構(SSR、CSR)、Web架構（Next.js、React、Astro等）和託管模型（「自備應用程式」）相容。

>[!TIP]
>
>如需有關受支援架構的詳細資訊，請參閱檔案[通用編輯器使用案例和學習路徑](/help/implementing/universal-editor/use-cases.md)。

## 支援的AEM版本 {#aem-versions}

下列專案支援通用編輯器：

* AEM as a Cloud Service （版本`2023.8.13099`或更新版本）
* [AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * 同時支援內部部署和AMS託管。
* [AEM 6.5](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * 同時支援內部部署和AMS託管。

本檔案用於搭配使用Universal Editor與AEM as a Cloud Service。

## 功能 {#features}

Universal Editor提供許多功能，可支援各種使用案例，以實現有效的內容管理。

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**：對任何形式的網頁內容（包括純文字、RTF、媒體和中繼資料）執行您看到的編輯。
* **[構成](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**：建立、編輯、重新排序、巢狀內嵌或刪除各種型別（標題、按鈕、Teaser、區段、內嵌等）的內容區塊。
* **[版面配置](/help/sites-cloud/authoring/universal-editor/templates.md)**：利用頁面範本、套用視覺樣式，並以欄、輪播和摺疊式功能表等區塊撰寫版面配置。
* **[裝置模擬](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**：編輯時預覽並最佳化不同訪客裝置的內容。
* **全管道**：在多個管道中重複使用結構化和非結構化內容。
* **[本地化](/help/sites-cloud/authoring/universal-editor/inheritance.md)**：透過多網站管理員，簡化內容翻譯工作流程，並有效處理本地化的內容繼承。
* **一致性**：確保符合品牌方針，並維持所有內容的一致性。
* **安全性**： [強制存取控制](/help/implementing/universal-editor/authentication.md)、保護內容完整性，以及使用[健全的版本設定追蹤變更。](/help/sites-cloud/authoring/sites-console/page-versions.md)
* **[發佈](/help/sites-cloud/authoring/universal-editor/publishing.md)**：直接在編輯器中整合檢閱、核准和發佈工作流程。
* **整合**：與AEM工具（例如[網站主控台、](/help/sites-cloud/authoring/sites-console/introduction.md) [內容片段編輯器、](/help/sites-cloud/administering/content-fragments/overview.md)等等）完全整合，提供整合式撰寫體驗。

## 擴展性 {#extensibility}

Universal Editor不僅提供立即可用的強大功能，更提供多種擴充功能。

* **擴充功能**&#x200B;數量眾多且已準備好支援需求，例如支援工作流程、產生變數以及啟用實驗以列舉一些專案。
* **可擴充的UI**&#x200B;可讓您使用與現成擴充功能相同的基礎架構，建立自己的擴充功能，讓擴充功能具備極致彈性，可因應您的專案需求。
* **擴充功能點** （例如區塊、自訂資料型別和事件）允許在UI之外順暢整合自訂業務需求。

>[!TIP]
>
>如需通用編輯器擴充性的詳細資訊，請參閱檔案[擴充通用編輯器。](/help/implementing/universal-editor/extending.md)

## Universal Editor 和內容片段編輯器 {#universal-editor-content-fragment-editor}

乍看之下，Universal Editor 和內容片段編輯器的編輯功能似乎很相似。然而，這些編輯器的功能大不相同，其完成的工作與行銷從業人員不同。

### 內容片段編輯器 {#content-fragment-editor}

行銷從業人員希望建立內容而不必關心其版面，以便它可以在多種體驗環境中重複使用。

* 要達成的基本工作是擴展內容策略。

### Universal Editor {#universal-editor}

行銷從業人員會想建立根據指定內容版面量身定制的內容，以提供卓越的體驗。

* 要達成的基本工作是與讀者建立可靠的聯繫。

## 限制 {#limitations}

當您探索通用編輯器並在您自己的專案中進一步實作時，請記住以下限制。

* 不應超過25個AEM資源(內容片段、頁面、體驗片段、Assets等)在單一頁面上作為檢測參照。
* AEM as a Cloud Service、[AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)和[AEM 6.5](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)是唯一受支援的AEM後端。
* AEM as a Cloud Service需要版本`2023.8.13099`或更新版本。
* 內容作者必須擁有自己的個別Experience Cloud帳戶。
* 作為AEM的一部分，通用編輯器[支援與AEM相同的案頭瀏覽器。](/help/overview/supported-platforms.md)
   * 不支援這些瀏覽器的行動版本。

{{ip-allow-lists-ue}}

## 後續步驟 {#next-steps}

請參閱檔案[通用編輯器使用案例和學習路徑](/help/implementing/universal-editor/use-cases.md)，深入瞭解通用編輯器的常見使用案例，並探索可在專案中為您提供支援的正確檔案資源。
