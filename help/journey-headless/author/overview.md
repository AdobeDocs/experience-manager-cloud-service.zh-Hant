---
title: AEM無頭內容製作歷程
description: 從這裡開始，引導您逐步了解AEM強大且有彈性的無頭式功能、其功能，以及如何為專案製作內容。
index: true
hide: false
hidefromtoc: false
source-git-commit: 387e75faeccb0671a32a54ff0c12f05219844311
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 1%

---


# AEM無頭內容製作歷程 {#aem-headless-author-journey}

從這裡開始，引導您逐步了解AEM強大且有彈性的無頭式功能，以及如何為無頭式專案製作內容。

## 簡介 {#introduction}

無頭式實作對於將體驗提供給對象（無論對象在何處、無論管道為何）越來越重要。

無頭式內容並非以傳統的頁面和元件結構為基礎。 而是以建立不受管道影響、可重複使用的內容片段及其跨管道傳送為基礎。

在AEM中，這是透過內容片段來實現。 您在個別內容片段中製作內容，然後供應用程式視需要選取及使用。

這種彈性表示無頭式是實作數位體驗的現代化、動態開發模式。

本指南會引導您了解最重要的主題，以便您在完成時：

* 基本了解無頭式內容傳遞的內容及其優點。
* 了解AEM無頭功能，以及它們如何共同合作以提供無頭體驗。
* 能夠為您的AEM無頭專案製作內容。

## AEM檔案歷程 {#documentation-journeys}

[說明檔](/help/journey-documentation/home.md) 案記錄將許多不同且可能複雜的主題和功能結合在一起，提供說明來協助讀者(對AEM而言是新手)從頭到尾了解並解決業務問題，同時假設先前主題或AEM知識最少。

說明檔案歷程是根據最佳實務原則而設計，根據Adobe的最新研究、Adobe顧問經驗證的實作經驗，以及客戶專案的意見回饋。

如果您想了解Adobe建議如何使用AEM解決無頭業務案例，從[AEM無頭歷程](/help/journey-headless/home.md)開始。

## 對象 {#audience}

此歷程專為內容作者角色而設計。 作為內容作者，您將在內容片段中建立實際內容。

此歷程列出為AEM Headless專案製作內容的需求、步驟和方法。 歷程會定義其他角色，作者必須與這些角色互動，才能使專案成功，但歷程的觀點是內容作者的觀點。

此歷程中的資訊當然對其他角色有用，但某些資訊對某些角色來說會是多餘的。 請持續關注即將提供的歷程，涵蓋其他角色。

## 無頭內容製作歷程 {#the-journey}

您將在此歷程中探索許多主題。 以下文章提供您AEM中無頭的基礎知識，並連結至詳細的技術檔案。

雖然您可以直接前往歷程的特定部分，但許多概念都是以先前文章中的概念為基礎而建立。 因此，如果您剛接觸AEM中的無頭部，建議您從頭開始，依序進行。

| # | 文章 | 說明 |
|---|---|---|
| 0 | AEM無頭內容製作歷程 | 此文檔 |
| 1 | [AEM Headless as aCloud Service的編寫 — 簡介](introduction.md) | 介紹Adobe Experience Manager as aCloud Service的無頭式功能，以及如何為專案製作內容。 |
| 2 | [使用AEM製作無頭的基本知識](basics.md) | 了解使用內容片段為無頭CMS製作內容的概念和機制。 |
| 3 | [了解如何在內容片段中使用參考](references.md) | 了解如何在內容片段中使用參考。 這些功能也可讓您使用巢狀片段，為無頭式CMS建立和管理多個層級的結構。 |
| 4 | [了解如何定義內容片段的中繼資料和標籤](metadata-tagging.md) | 了解如何定義內容片段的中繼資料和標籤。 |

## 下一步 {#what-is-next}

您現在已準備好開始Adobe無頭歷程。 建議您繼續前往歷程的下一個部分，並閱讀[Authoring for AEM Headless as a Autoring - An Introduction一文。](introduction.md)

<!--
### Choose Your Own Adventure {#choose-your-path}

However, Adobe wants you to succeed as you get started with your AEM Headless project, regardless of your learning style. So please consider these two options.

* If you prefer to continue to **learn about headless concepts and AEM's headless technologies**, you should continue your AEM headless journey as recommended by next reviewing the document [How to Model Your Content as AEM Content Models](model-your-content.md) where you learn how to model your content structure in AEM.
* If you prefer to **learn by doing**, you can jump to the [Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) where you will jump directly into AEM Headless development by implementing a simple project to expose AEM headless content.
-->

## 其他資源 {#additional-resources}

說明檔案歷程會告訴您AEM如何透過提供敘述性，引導您完成複雜、相互關聯的程式和功能，進而解決業務問題。 歷程說明多個功能如何搭配運作以滿足單一業務需求。

因此，這些旅程的設計是獨立的。 但是，其中許多是可以相互關聯的。 請查看這些其他歷程，深入了解AEM強大功能如何搭配運作。

* [AEM無頭式翻譯歷程](/help/journey-headless/translation/overview.md)  — 本檔案歷程可讓您廣泛了解無頭式技術、AEM如何提供無頭式內容，以及如何翻譯內容。
* [AEM無頭式開發人員歷程](/help/journey-headless/developer/overview.md)  — 從這裡開始，引導您一路探索AEM強大而有彈性的無頭式功能、其功能，以及如何在您的第一個開發專案中運用這些功能。
* [無頭架構師歷程](/help/journey-headless/architect/overview.md)  — 從這裡開始，介紹Adobe Experience Manager作為Cloud Service的強大、靈活、無頭式功能，以及如何為專案建立內容模型。
* [AEM as a Cloud Service技術檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已對AEM和無頭式技術有深入了解，建議您直接參閱我們的深入技術檔案。
* [AEM無頭教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 如果您偏好透過執行學習，且在技術上有傾向，請利用我們的實作教學課程，由API和架構組織，探索建立和使用AEM無頭上建置的應用程式。
