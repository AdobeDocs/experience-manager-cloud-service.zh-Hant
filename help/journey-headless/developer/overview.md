---
title: 無AEM頭開發者之旅
description: 從此開始，在將Adobe Experience Manager(AEM)as a Cloud Service用作無頭內容管理系統(CMS)時，進行有指導的旅行。 此過程為您提供開發第一個無頭應用程式所需的所有資訊。
landing-page-description: 從這裡開始，逐步引導您了解 AEM 的無周邊功能、其功能，以及如何在您的第一個開發專案中運用這些功能。
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: 0c8cddd65ad3b297b58f8ee618ba176edcf51a45
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 3%

---

# 無AEM頭開發者之旅 {#aem-headless-developer-journey}

從此開始，在將Adobe Experience Manager(AEM)as a Cloud Service用作無頭內容管理系統(CMS)時，進行有指導的旅行。 瞭解功能強大、靈活的無頭功能、功能，以及如何在您的第一個無頭開發項目中利用它們。 此過程為您提供開發第一個無頭應用程式所需的所有資訊。

## 簡介 {#introduction}

無頭實施將放棄頁面和元件管理，這與整個堆棧解決方案中的傳統做法一樣，並側重於建立不依賴渠道、可重複使用的內容片段及其跨渠道交付。 它是一種實現數字型驗的現代動態發展模式。

本指南引導您瞭解中最無頭的實施主AEM題，以便在完成後：

* 全面瞭解無頭內容交付的內容及其好處。
* 了AEM解無頭功能以及它們如何協作以提供無頭體驗。
* 能夠採取實施第一個無頭項目的AEM第一步。

## 文檔AEM旅程 {#documentation-journeys}

[文檔旅程](/help/journey-documentation/documentation-journeys.md) 通過提供幫助讀者瞭解和解決商業問題的敘事，將許多不同的、或許複雜的主題和特徵聯繫起來AEM，讀者可以從頭到尾對商業問題有新意，但只要假設事先的主題或知AEM識很少。

文檔旅程是圍繞最佳做法原則設計的，這些原則由Adobe的最新研究、Adobe顧問的經驗證的實施經驗和客戶項目的反饋所指導。

如果您想瞭解Adobe如何推薦解決無頭業務案例AEM, [無AEM頭遊記](/help/journey-documentation/documentation-journeys.md) 是從哪開始的。

>[!TIP]
>
> 如果你願意 **學習** 並且在技術上有傾向性，請訪AEM問由API和框架組織的Headless教程，這些教程可在 [「其他資源」部分](#additional-resources) 在文檔的末尾。

## 對象 {#audience}

此旅程是為開發人員角色設計的，從開發人員的角度列出AEMHeadless項目的要求、步驟和方法。 此行程定義了開發人員在成功項目中必須與之交互的其他角色，但行程的視點是開發人員的視點。

以下是這段旅程中互動的人物。

| 角色 | 說明 | 《這趟旅程中的角色》 |
|---|---|---|
| 開發人員（目標受眾） | 具有開發無頭應用程式的經驗，這些應用程式使用來自不同來源的內容 | 此旅的目標受眾 |
| 內容作者 | 建立並管理無頭地提供的內容 | 內容作者建立開發人員無故提供的內容。 |
| 管理員 | 管理基本設定和配AEM置 | 開發人員與管理員協作，以進行開發所需的配置更改。 |
| 內容架構師 | 分析對必須直接提供的資料的要求，並定義此資料的結構 | 開發人員與內容架構師合作，瞭解資料的結構和無拘無束地提供資料的要求。 |

此過程中的資訊當然對所有角色都有用，但某些資訊對某些角色來說可能是多餘的。 繼續關注 [即將到來的旅程，涉及其他角色。](/help/journey-documentation/documentation-journeys.md#journeys)

## 《無頭開發者之旅》 {#the-journey}

您將在此旅途中探索許多主題。 以下文章為您提供了有關詳細技術文檔AEM的無頭知識並提供了連結。

雖然你可以直接進入旅程的某個特定部分，但許多概念都建立在先前文章中的概念之上。 因此，如果您剛剛進入無頭AEM狀態，我們建議您從開始開始按順序進行。

| # | 文章 | 說明 |
|---|---|---|
| 0 | 無AEM頭開發者之旅 | 此文檔 |
| 1 | [瞭解CMS無頭開發](learn-about.md) | 瞭解無頭技術以及何時使用它。 |
| 2 | [無頭as a Cloud Service入AEM門](getting-started.md) | 瞭解無頭AEM必備元件 |
| 3 | [使用無頭設備獲得第一次體AEM驗](path-to-first-experience.md) | 設定您的開發環境並瞭解如何將簡單應用與AEMHeadless整合 |
| 4 | [如何對內容建模](model-your-content.md) | 瞭解如何對內容結構建模。 然後實現Adobe Experience Manager(AEM)使用內容片段模型和內容片段的結構，以便跨通道重用。 |
| 5 | [如何通過交付API訪AEM問內容](access-your-content.md) | 瞭解如何使用GraphQL查詢訪問內容片段內容。 |
| 6 | [如何通過AEM AssetsAPI更新您的內容](update-your-content.md) | 瞭解如何使用REST API訪問和更新內容片段內容。 |
| 7 | [如何將所有內容放在一起 — 您的應用和您的內容放在AEMHeadless中](put-it-all-together.md) | 瞭解如何獲取AEM您的項目並為使用無頭SDK做好準備AEM。 |
| 8 | [如何與無頭應用程式一起生活](go-live.md) | 瞭解如何即時部署應用程式並以Git格式獲取您的本地代碼並將其移到Cloud Manager Git for CI/CD管道。 |
| 9 | [可選 — 如何建立單頁應用程式(SPA)，具AEM有](create-spa.md) | 瞭解無頭功AEM能後，瞭解如何將無頭和無頭交付結合起來，並瞭解如何使用編輯器框架創SPA建可AEM編SPA輯功能。 |

## 下一步是什麼 {#what-is-next}

您現在已準備好開始Adobe無頭之旅。 我們鼓勵您繼續下一段旅程，閱讀文章 [瞭解CMS無頭開發。](learn-about.md)

### 選擇您自己的冒險 {#choose-your-path}

但是，Adobe希望您在開始使用Headless項目時AEM取得成功，無論您的學習風格如何。 所以請考慮這兩個選擇。

* 如果您希望繼續 **瞭解無頭概念和無頭AEM技術**，您應繼續按照AEM建議進行無頭旅行，方法是下次查看文檔 [如何將內容建模為內AEM容模型](model-your-content.md) 學習如何在中建模內容結AEM構。
* 如果你願意 **學習**&#x200B;你可以跳到 [無頭AEM動手教程入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) 通過實施一個簡單的項AEM目來公開無頭內容，您將直接進入無頭AEM開發。

## 其他資源 {#additional-resources}

文檔旅程向您介AEM紹如何通過提供一種說明來解決業務問題，該說明可指導您完成複雜且相互關聯的流程和功能。 一段旅程說明了多種功能如何協同工作，以滿足單一業務需求。

因此，這種旅行是設計為獨立的。 但是，其中的一些是相互關聯的。 查看這些附加旅程，瞭解有關功能強大的功能AEM如何協同工作的詳細資訊。

* [無AEM頭教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 如果您喜歡通過實踐來學習，並且具有技術傾向，請參閱我們按API和框架組織的動手教程，該教程將探討建立和使用基於AEMHeadless的應用程式。
* [無AEM頭翻譯之旅](/help/journey-headless/translation/overview.md)  — 此文檔記錄過程讓您能夠全面瞭解無頭技術、如何AEM處理無頭內容以及如何翻譯。
* [無頭創作旅程](/help/journey-headless/author/overview.md)  — 從此開始，引導您瞭解功能強大、靈活的無頭功能AEM、功能，以及如何在您的第一個無頭項目上對內容建模。
* [無頭建築師之旅](/help/journey-headless/architect/overview.md)  — 從此處開始，介紹Adobe Experience Manager as a Cloud Service強大、靈活、無頭的功能，以及如何為您的項目建模內容。
* [AEMas a Cloud Service技術文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已經對無頭技術有了AEM深入的瞭解，您可能希望直接咨詢我們的深入技術文檔。
