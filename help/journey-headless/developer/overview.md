---
title: AEM無頭CMS開發人員歷程
description: 了解如何使用Adobe Experience Manager(AEM)作為無頭式CMS進行無頭式開發。 了解如何使用內容模型、內容片段和GraphQL API等功能，強化無頭式內容傳送。
landing-page-description: 了解無頭式內容的傳送和實作。 進一步了解如何在您的企業中開發您的策略。
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: b3a3fbaf9a18e15cfba4f240b6f3abdd9aed077c
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 7%

---

# AEM無頭CMS開發人員歷程 {#aem-headless-developer-journey}

歡迎參閱Adobe Experience Manager無頭式CMS新手開發人員的檔案！

了解功能強大、靈活的無頭式功能、其功能，以及如何在您的第一個無頭式開發專案中運用這些功能。 此歷程提供您開發第一個無頭應用程式所需的所有資訊。

## 簡介 {#introduction}

AEM的無頭式實作使用內容片段模型和內容片段，著重於建立結構化、通道中性且可重複使用的內容片段及其跨頻道傳送。 要達到此目的，它會放棄頁面和元件管理，如同傳統的完整堆疊解決方案一樣。 這是實作數位體驗的現代化、動態開發模式。

本指南會引導您了解AEM中的無頭式實作主題，因此在您完成時：

* 全面了解無頭式內容的傳遞方式及其優點。
* 了解AEM無頭功能，以及它們如何共同合作以提供無頭體驗。
* 能夠採取實作第一個AEM無頭專案的前幾個步驟。

>[!TIP]
>
> 如果您偏好 **學習** 並具備AEM的現有知識，請造訪AEM Headless教學課程，這些教學課程由API和架構組織，並可在 [「其他資源」部分](#additional-resources) 在此文檔的末尾。

## 對象 {#audience}

此歷程專為開發人員角色而設計，從開發人員的角度規劃AEM Headless專案的需求、步驟和方法。 歷程會定義開發人員在成功的專案中必須與其互動的其他角色，但歷程的觀點是開發人員的角色。

以下是在此歷程中互動的角色。

| 角色 | 說明 | 此歷程中的角色 |
|---|---|---|
| 開發人員（目標受眾） | 具有開發無頭應用程式的經驗，這些應用程式會從不同的來源消費內容 | 鎖定此歷程的受眾 |
| 內容作者 | 建立和管理無謂傳送的內容 | 內容作者建立開發人員無端提供的內容。 |
| 管理員 | 管理AEM的基本設定和配置 | 開發人員與管理員合作，以變更開發所需的設定。 |
| 內容架構師 | 分析必須無謂傳送的資料需求，並定義此資料的結構 | 開發人員與內容架構師合作，了解資料的結構，以及無端傳送資料的需求。 |

## 無頭式開發人員歷程 {#the-journey}

我們將在此歷程中涵蓋許多主題，提供您AEM中無頭的基礎知識。

雖然您可以直接前往歷程的特定部分，但許多概念都是以先前文章中的概念為基礎而建立。 建議您從頭開始，依序進行。

| # | 文章 | 說明 |
|---|---|---|
| 0 | AEM Headless Developer Journey | 本文件 |
| 1 | [了解 CMS Headless 開發](learn-about.md) | 了解無頭技術及其使用時機。 |
| 2 | [AEM Headless as a Cloud Service 快速入門](getting-started.md) | 了解AEM Headless必要條件 |
| 3 | [踏上使用 AEM Headless 初體驗之路](path-to-first-experience.md) | 設定您的開發環境，並了解如何將簡單應用程式與AEM Headless整合 |
| 4 | [如何建立內容模型](model-your-content.md) | 了解如何建立內容結構的模型。 |
| 5 | [如何透過 AEM Delivery API 存取您的內容](access-your-content.md) | 了解如何使用GraphQL查詢存取您的內容片段內容。 |
| 6 | [如何透過 AEM Assets API 更新您的內容](update-your-content.md) | 了解如何使用REST API存取和更新您的內容片段內容。 |
| 7 | [如何將所有內容放在一起 — 您的應用程式和AEM Headless中的內容](put-it-all-together.md) | 了解如何取得您的AEM專案，並準備以使用AEM Headless SDK上線。 |
| 8 | [如何使用無周邊應用程式](go-live.md) | 了解如何即時部署應用程式，並在Git中取用您的本機程式碼，並移至Cloud Manager Git，以便使用CI/CD管道。 |
| 9 | [選用 — 如何使用AEM建立單頁應用程式(SPA)](create-spa.md) | 探索如何結合無頭式和無頭式傳送，並了解如何使用AEM SPA Editor架構建立可編輯的SPA。 |

{style=&quot;table-layout:auto&quot;}

## 下一步 {#what-is-next}

查看下一篇文章以開始： [了解CMS無頭開發。](learn-about.md)

### 選擇自己的冒險 {#choose-your-path}

你喜歡按自己的步調學習嗎？ 查看以下選項：

* 如果您偏好繼續 **了解無頭概念和AEM無頭技術**，您應依建議繼續進行AEM無頭歷程，接下來檢閱檔案 [如何將內容模型為AEM內容模型](model-your-content.md) 可在此了解如何在AEM中建立內容結構模型。
* 如果您偏好 **學習**，您可以跳到 [AEM Headless實作教學課程快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) 透過實作簡單專案來公開AEM無頭式內容，您將直接進入AEM開發。

## 其他資源 {#additional-resources}

說明檔案歷程說明AEM如何透過提供敘述來引導您了解相關流程和功能，進而解決業務問題。 歷程說明多個功能如何搭配運作以滿足單一業務需求。

請查看這些其他歷程，深入了解AEM強大功能如何搭配運作。

* [AEM Headless教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 如果您偏好透過執行和掌握AEM的現有知識來學習，請利用我們按API和架構組織的實作教學課程，探索如何建立和使用以AEM Headless建置的應用程式。
* [AEM無頭翻譯歷程](/help/journey-headless/translation/overview.md)  — 本檔案歷程可讓您廣泛了解無頭式技術、AEM如何提供無頭式內容，以及如何翻譯內容。
* [無頭製作歷程](/help/journey-headless/author/overview.md)  — 從這裡開始，引導您一路探索AEM強大且有彈性的無頭式功能、其功能，以及如何在您的第一個無頭式專案中建立內容模型。
* [無頭架構師歷程](/help/journey-headless/architect/overview.md)  — 從這裡開始，介紹Adobe Experience Manager as a Cloud Service強大、靈活、無頭的功能，以及如何為專案建立內容模型。
* [AEMas a Cloud Service技術檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已對AEM和無頭技術有深入的了解，請查看我們的深入技術檔案。
