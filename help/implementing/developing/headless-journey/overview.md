---
title: 無頭開AEM發人員歷程
description: 從這裡開始進行引導式歷程，瞭解其強大而有彈性的無頭功能AEM、功能，以及如何在您的第一個開發專案中運用這些功能。
hide: true
hidefromtoc: true
index: false
exl-id: 4524c92a-8f19-497a-b4f2-c3e23f555d37
source-git-commit: 83ed6295d2b29581025f5410236f2618ceb59012
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# 無AEM頭開發人員歷程{#aem-headless-developer-journey}

>[!CAUTION]
>
>正在進行中的工作——本檔案的建立工作正在進行中，不應將其理解為完整或明確，也不應將其用於生產目的。

從這裡開始進行引導式歷程，瞭解其強大而有彈性的無頭功能、AEM其功能，以及如何將它們運用在您的第一個無頭開發專案中。

## 簡介 {#introduction}

無頭實作對於為受眾提供體驗變得越來越重要，無論他們身在何處，無論通道如何。

無頭實作會與完整堆疊解決方案中的傳統方式一樣，將頁面和元件管理轉換為無頭實作，並著重於建立不受通道限制、可重複使用的內容片段及其跨通道傳送。 它是一種現代化的動態開發模式，可用來建置網頁體驗。

本指南會引導您瞭解最重要的主題，讓您在完成時：

* 充分瞭解無頭內容的傳遞方式及其優點。
* 瞭解無AEM頭功能，以及它們如何搭配運作，以提供無頭體驗。
* 能夠採取實作第一個無頭專案的AEM第一步。

## 對象 {#audience}

本旅程是專為開發人員人物所設計，從開發人員的角度來規劃AEMHeadless專案的需求、步驟和方法。 此歷程將定義開發人員在成功專案中必須與之互動的額外角色，但歷程的觀點是開發人員。

這段旅程中的資訊當然對其他角色有用，但有些資訊對某些角色是多餘的。 敬請期待即將到來的旅程，涵蓋更多角色。

## 無頭開發人員歷程{#the-journey}

您將在此歷程中探索許多主題。 以下文章提供您無頭的基本知識，並AEM連結至詳細的技術檔案。

雖然您可以直接進入旅程的特定部分，但許多概念都建立在先前文章中的概念上。 因此，如果您不熟悉無頭AEM功能，建議您從開頭開始並依序進行。

| # | 文章 | 說明 |
|---|---|---|
| 0 | 無頭開AEM發人員歷程 | 本檔案 |
| 1 | [瞭解CMS無頭開發](learn-about.md) | 瞭解無頭技術，以及其使用時機。 |
| 2 | [開始使用AEM無頭Cloud Service](getting-started.md) | 瞭解無頭AEM先決條件 |
| 3 | [使用無頭體驗，獲得您第一次體AEM驗的途徑](path-to-first-experience.md) | 設定您的開發環境，並瞭解如何將簡單的應用程式與AEMHeadless整合 |
| 4 | [如何建立內容模型](model-your-content.md) | 瞭解如何建立內容結構的模型。 然後，瞭解Adobe Experience Manager(AEM)使用內容片段模型和內容片段的結構，以便跨通道重複使用。 |
| 5 | [如何透過傳送API存取您AEM的內容](access-your-content.md) | 瞭解如何使用GraphQL查詢來存取您的內容片段內容。 |
| 6 | [如何透過資產API更新AEM您的內容](update-your-content.md) | 瞭解如何使用REST API存取和更新您的內容片段內容。 |
| 7 | [如何將所有內容整合在一起——您的應用程式和您的內容AEM在Headless](put-it-all-together.md) | 瞭解如何將您的專AEM案（包括內容片段）、您的GraphQL呼叫、您的REST API呼叫和您的應用程式)準備上線。 |
| 8 | [如何與無頭應用程式一起上線](go-live.md) | 瞭解如何即時部署應用程式並將您的本機程式碼以Git格式移至Cloud Manager Git for CI/CD管道。 |
| 9 | [貼文啟動](post-launch.md) | 瞭解如何維持您的無頭體驗。 |
| 10 | [可選——如何使用](create-spa.md) | 瞭解無頭功AEM能後，請探索如何結合無頭和無頭傳送，並瞭解如何使用編輯器架構來SPA建AEM立可編SPA輯的內容。 |

## 下一個{#what-is-next}

您現在已準備好開始Adobe無頭之旅。 我們鼓勵您繼續下一段旅程，並閱讀[「瞭解CMS無頭開發」文章。](learn-about.md)

### 選擇您自己的冒險{#choose-your-path}

不過，Adobe希望您在開始使用Headless專案時AEM，不論您的學習風格為何，都能獲得成功。 所以請考慮這兩個選項。

* 如果您想要繼續&#x200B;**瞭解無頭概念和無頭技術AEM**，您應繼續建議的無頭歷程，請先閱讀[如何將您的內容建模為內容模型(AEMContent Models](model-your-content.md))檔案，以瞭解如何在中建模您的內容結構AEM。
* 如果您偏好&#x200B;**透過執行**&#x200B;來學習，可跳至[開始使用AEMHeadless實作教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)，透過實作簡單專案來公開無頭內容，您將直接跳至無頭開AEM發。
