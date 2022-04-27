---
title: 無AEM頭翻譯之旅
description: 從此開始，通過使用功能強大的翻譯工具翻譯無頭內AEM容，進行指導性的旅程。
exl-id: b677f691-5257-43c3-a4b9-c34932577b31
source-git-commit: ad47148237fe8a8b7c0b4fc4eb293f1155dae560
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 1%

---

# 無AEM頭翻譯之旅 {#aem-headless-translation-journey}

從此開始，通過使用功能強大的翻譯工具翻譯無頭內AEM容，進行指導性的旅程。

## 簡介 {#introduction}

無頭實施對於向您的觀眾提供體驗越來越重要，無論他們身在何處，無論渠道、地區或地區如何。

無頭實施將放棄頁面和元件管理，這與整個堆棧解決方案中的傳統做法一樣，並側重於建立不依賴渠道、可重複使用的內容片段及其跨渠道交付。 通過使AEM用強大的翻譯工具，這些可重複使用的片段可以輕鬆翻譯並交付給您的觀眾，無論它在何處。

本指南引導您瞭解最重要的無頭翻譯主題，以便在完成後：

* 概括瞭解什麼是無頭內容交付。
* 瞭解基本的無AEM頭功能。
* 了AEM解翻譯功能及其與無頭內容的關係。
* 能夠開始翻譯您自己的無頭內容。

目標是讓您對無頭技術、如何服務無AEM頭內容以及如何翻譯它有廣泛的瞭解。 如果您不熟悉這些主題，這就是您的理想起點。

如果您已經熟悉AEM、無頭和翻譯，您可能已經掌握了此旅程的基本知識。 請考慮參考我們在 [下面的其他資源部分。](#additional-resources)

## 文檔AEM旅程 {#documentation-journeys}

[文檔旅程](/help/journey-documentation/documentation-journeys.md) 通過提供幫助讀者瞭解和解決商業問題的敘事，將許多不同的、或許複雜的主題和特徵聯繫起來AEM，讀者可以從頭到尾對商業問題有新意，但只要假設事先的主題或知AEM識很少。

文檔旅程是圍繞最佳做法原則設計的，這些原則由Adobe的最新研究、Adobe顧問的經驗證的實施經驗和客戶項目的反饋所指導。

如果您想瞭解Adobe如何推薦解決無頭業務案例AEM, [無AEM頭遊記](/help/journey-documentation/documentation-journeys.md) 是從哪開始的。

## 對象 {#audience}

此旅程專為翻譯專家人員設計，通常稱為翻譯項目經理或TPM。 此過程列出了翻譯中無頭內容的要求、步驟和方AEM法。 此旅程可能定義翻譯專家必須與之互動的其他角色，但此旅程的視點是翻譯專家的觀點。

這一旅程假定讀者在大型CMS系統上具有翻譯內容的經驗，但假定讀者不瞭解無頭技術或AEM。

以下是這段旅程中互動的人物。

| 角色 | 說明 | 《旅程中的角色》 |
|---|---|---|
| 翻譯專家 | 定義應翻譯的內容並管理這些工作流 | 這次旅程的觀眾 |
| 內容作者 | 建立和管理無拘無束地提供的內容 | 內容作者建立翻譯專家必須翻譯的內容。 |
| 管理員 | 管理基本設定和配AEM置 | 翻譯專家會與管理員協作，對翻譯所需的配置進行更改，例如安裝翻譯連接器。 |
| 內容架構師 | 分析對必須直接提供的資料的要求，並定義此資料的結構 | 翻譯專家與內容架構師合作定義內容的組織，以便輕鬆翻譯。 |

此過程中的資訊當然對所有角色都有用，但某些資訊對某些角色來說可能是多餘的。 繼續關注 [即將到來的旅程，涉及其他角色。](/help/journey-documentation/documentation-journeys.md#journeys)

## 無頭翻譯之旅 {#the-journey}

您將在此旅途中探索許多主題。 以下文章為您提供了翻譯無頭內容的基本知識，AEM並連結到詳細的技術文檔。

雖然你可以直接進入旅程的某個特定部分，但許多概念都建立在先前文章中的概念之上。 因此，如果您在中不熟悉無頭AEM翻譯，我們建議您從開始開始按順序進行。

| # | 文章 | 說明 |
|---|---|---|
| 0 | 無AEM頭翻譯之旅 | 此文檔 |
| 1 | [瞭解無頭內容以及如何將其翻譯AEM到](learn-about.md) | 學習無頭概念，它們如何AEM映射，以及翻AEM譯理論。 |
| 2 | [開始無AEM頭翻譯](getting-started.md) | 瞭解如何組織無頭內容以及翻譯工AEM具的工作。 |
| 3 | [配置翻譯連接器](configure-connector.md) | 瞭解如何連AEM接到翻譯服務。 |
| 4 | [翻譯內容](translate-content.md) | 使用翻譯連接器和規則來翻譯無頭內容。 |
| 5 | [發佈已翻譯的內容](publish-content.md) | 瞭解如何在更新基礎內容時發佈已翻譯的內容並更新翻譯。 |

## 下一步是什麼 {#what-is-next}

您現在已準備好開始Adobe無頭翻譯之旅。 我們鼓勵您繼續下一段旅程，閱讀文章 [瞭解無頭內容以及如何將其翻譯AEM到](learn-about.md)

## 其他資源 {#additional-resources}

文檔旅程向您介AEM紹如何通過提供一種說明來解決業務問題，該說明可指導您完成複雜且相互關聯的流程和功能。 一段旅程說明了多種功能如何協同工作，以滿足單一業務需求。

因此，這種旅行是設計為獨立的。 但是，其中的一些是相互關聯的。 查看這些附加旅程，瞭解有關功能強大的功能AEM如何協同工作的詳細資訊。

* [無頭創作旅程](/help/journey-headless/author/overview.md)  — 從此開始，引導您瞭解功能強大、靈活的無頭功能AEM、功能，以及如何在您的第一個無頭項目上對內容建模。
* [無頭建築師之旅](/help/journey-headless/architect/overview.md)  — 從此處開始，介紹Adobe Experience Manager as a Cloud Service強大、靈活、無頭的功能，以及如何為您的項目建模內容。
* [無AEM頭開發者之旅](/help/journey-headless/developer/overview.md)  — 從此開始，引導您瞭解功能強大、靈活的無頭功能AEM、功能，以及如何在您的第一個開發項目中利用這些功能。
* [AEMas a Cloud Service技術文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已經對無頭技術有了AEM深入的瞭解，您可能希望直接咨詢我們的深入技術文檔。
* [無AEM頭教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 如果您喜歡通過實踐來學習，並且在技術上有傾向，請參閱我們按API和框架組織的動手教程，該教程將探討建立和使用基於AEMHeadless的應用程式。
