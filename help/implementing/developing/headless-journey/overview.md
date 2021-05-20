---
title: AEM Headless Developer Journey
description: 從這裡開始，引導您逐步了解AEM強大且有彈性的無頭式功能、其功能，以及如何在您的第一個開發專案中運用這些功能。
hide: true
hidefromtoc: true
index: false
exl-id: 4524c92a-8f19-497a-b4f2-c3e23f555d37
source-git-commit: 9e06419f25800199dea92b161bc393e6e9670697
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---

# AEM無頭開發者歷程{#aem-headless-developer-journey}

>[!CAUTION]
>
>過時 — 此草稿內容已由新的[無頭開發人員歷程檔案取代。](/help/journey-headless/developer/overview.md)

從這裡開始，引導您逐步了解AEM強大且有彈性的無頭式功能、其功能，以及如何在您的第一個無頭式開發專案中運用這些功能。

## 簡介 {#introduction}

無頭式實作對於將體驗提供給對象（無論對象在何處、無論管道為何）越來越重要。

無頭實作會放棄頁面和元件管理，如同在完整堆疊解決方案中的傳統做法，並著重於建立不受管道影響、可重複使用的內容片段及其跨管道傳送。 這是實作Web體驗的現代化、動態開發模式。

本指南會引導您了解最重要的主題，以便您在完成時：

* 充分了解無頭式內容傳遞的內容及其優點。
* 了解AEM無頭功能，以及它們如何共同合作以提供無頭體驗。
* 能夠採取實作第一個AEM無頭專案的前幾個步驟。

## 對象 {#audience}

此歷程專為開發人員角色而設計，從開發人員的角度規劃AEM Headless專案的需求、步驟和方法。 歷程會定義其他角色，開發人員必須與這些角色互動，才能順利完成專案，但歷程的觀點是開發人員的觀點。

此歷程中的資訊當然對其他角色有用，但某些資訊對某些角色來說會是多餘的。 請持續關注即將提供的歷程，涵蓋其他角色。

## 無頭式開發人員歷程{#the-journey}

您將在此歷程中探索許多主題。 以下文章提供您AEM中無頭的基礎知識，並連結至詳細的技術檔案。

雖然您可以直接前往歷程的特定部分，但許多概念都是以先前文章中的概念為基礎而建立。 因此，如果您剛接觸AEM中的無頭部，建議您從頭開始，依序進行。

| # | 文章 | 說明 |
|---|---|---|
| 0 | AEM Headless Developer Journey | 此文檔 |
| 1 | [了解CMS無頭開發](learn-about.md) | 了解無頭技術及其使用時機。 |
| 2 | [開始使用AEM Headless作為Cloud Service](getting-started.md) | 了解AEM Headless必要條件 |
| 3 | [使用AEM Headless的第一次體驗路徑](path-to-first-experience.md) | 設定您的開發環境，並了解如何將簡單應用程式與AEM Headless整合 |
| 4 | [如何建立內容模型](model-your-content.md) | 了解如何建立內容結構的模型。 然後，使用內容片段模型和內容片段來實現Adobe Experience Manager(AEM)的結構，以便跨頻道重複使用。 |
| 5 | [如何透過AEM傳送API存取您的內容](access-your-content.md) | 了解如何使用GraphQL查詢來存取您的內容片段內容。 |
| 6 | [如何透過AEM Assets API更新您的內容](update-your-content.md) | 了解如何使用REST API存取和更新您的內容片段內容。 |
| 7 | [如何將所有內容放在一起 — 您的應用程式和AEM Headless中的內容](put-it-all-together.md) | 了解如何取得您的AEM專案，包括內容片段、GraphQL呼叫、REST API呼叫和應用程式，並為其上線做準備。 |
| 8 | [如何與無頭應用程式一起運行](go-live.md) | 了解如何即時部署應用程式，並在Git中取用您的本機程式碼，並移至Cloud Manager Git，以便使用CI/CD管道。 |
| 9 | [選用 — 如何使用AEM建立單頁應用程式(SPA)](create-spa.md) | 了解AEM無頭功能後，請探索如何結合無頭和無頭傳送，並了解如何使用AEM SPA Editor架構建立可編輯的SPA。 |

## 下一步是什麼{#what-is-next}

您現在已準備好開始Adobe無頭歷程。 我們鼓勵您繼續前往歷程的下一個部分，並閱讀[了解CMS無頭開發。](learn-about.md)

### 選擇自己的冒險{#choose-your-path}

不過，無論您的學習風格如何，Adobe都希望您在開始使用AEM Headless專案時能成功。 所以請考慮這兩個選擇。

* 如果您偏好繼續&#x200B;**了解無頭概念和AEM無頭技術**，您應繼續依建議進行AEM無頭歷程，接下來檢閱檔案[如何將內容模型為AEM內容模型](model-your-content.md)，了解如何在AEM中建立內容結構模型。
* 如果您偏好透過&#x200B;**學習**，您可以跳至[AEM Headless實作快速入門教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)，透過實作簡單專案以公開AEM Headless內容，直接跳至AEM Headless開發。
