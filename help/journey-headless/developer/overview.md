---
title: AEM Headless CMS 開發人員歷程
description: 了解如何使用 Adobe Experience Manager (AEM) as a Headless CMS 進行 Headless 開發。了解如何使用內容模型、內容片段和 GraphQL API 等功能來增強 Headless 內容傳遞。
landing-page-description: 了解 Headless 內容傳遞和實作。了解更多如何在制定您的業務策略。
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 20914cde3be3ff3061b061d930154bd72da45d11
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 100%

---

# AEM Headless CMS 開發人員歷程 {#aem-headless-developer-journey}

歡迎使用專為初學 Adobe Experience Manager Headless CMS 的開發人員製作的文件！

了解強大且靈活的 Headless 特性、其功能，以及如何在您的第一個 Headless 開發專案中使用這些功能。此歷程為您提供了開發第一個 Headless 應用程式所需的所有資訊。

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="AEM Headless 開發人員資源和進階文件"
>abstract="了解 AEM Headless CMS 以及建置和交付更好的應用程式和更快體驗所需的一切。"


## 簡介 {#introduction}

AEM Headless 實作使用內容片段模型和內容片段來專注於建位結構化、管道中立和可重複使用的內容片段及其跨管道傳遞。為了實現這一點，它放棄了全堆疊解決方案的頁面和元件管理傳統做法。它是實作數位體驗的現代動態開發模式。

本指南將引導您完成 AEM Headless 實施主題，完成後您便可以：

* 充分了解什麼是 Headless 內容傳遞及其優勢。
* 了解 AEM 的 Headless 功能以及它們如何共同運作以傳遞 Headless 體驗。
* 邁出實施第一個 AEM Headless 專案的第一步。

>[!TIP]
>
> 如果您偏好&#x200B;**做中學**&#x200B;並具備 AEM 現有知識，請造訪 AEM Headless 教學課程，其由 API 和框架所組織，位在此文件結尾處的[其他資源區段](#additional-resources)。

## 客群 {#audience}

此歷程專為開發人員所設計，從開發人員的角度闡述了 AEM Headless 專案的要求、步驟和方法。此歷程定義了為使專案成功開發人員必須與之互動的其他角色，但歷程是以開發人員的角度出發。

以下是在此歷程中會互動的角色。

| 角色 | 描述 | 此歷程中的角色 |
|---|---|---|
| 開發人員 (目標客群) | 有經驗曾開發取用不同來源之內容的 Headless 應用程式 | 此歷程的目標客群 |
| 內容作者 | 建立和管理以 Headless 方式傳遞的內容 | 內容作者建立開發人員以 Headless 方式傳遞的內容。 |
| 管理員 | 管理 AEM 的基本設定和配置 | 開發人員與管理員合作以進行開發所需的設定變更。 |
| 內容架構師 | 分析必須以 Headless 方式傳遞之資料的要求並定義該資料的結構 | 開發人員與內容架構師合作，了解資料結構和 Headless 傳遞資料的要求。 |

## Headless 開發人員歷程 {#the-journey}

我們將在此歷程中涵蓋許多主題，這將為您提供 AEM Headless 的基礎知識。

儘管您可以直接進入歷程的特定部分，但許多概念都是以先前文章中的概念為基礎。Adobe 建議您從頭開始，然後循序漸進。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM Headless 開發人員歷程 | 本文件 |
| 1 | [了解 CMS Headless 開發](learn-about.md) | 了解 Headless 技術以及使用時機。 |
| 2 | [AEM Headless as a Cloud Service 快速入門](getting-started.md) | 了解 AEM Headless 先決條件 |
| 3 | [踏上首次使用 AEM Headless 之路](path-to-first-experience.md) | 設定您的開發環境並了解如何將簡單的應用程式與 AEM Headless 相整合 |
| 4 | [如何建立為您的內容建立模型](model-your-content.md) | 了解如何為您的內容結構建立模型。 |
| 5 | [如何透過 AEM Delivery API 存取您的內容](access-your-content.md) | 了解如何使用 GraphQL 查詢來存取您的內容片段內容。 |
| 6 | [如何透過 AEM Assets API 更新您的內容](update-your-content.md) | 了解如何使用 REST API 來存取並更新您的內容片段內容。 |
| 7 | [如何在 AEM Headless 中將您的應用程式和內容組合在一起](put-it-all-together.md)  | 了解如何取用 AEM 專案並使其準備就緒可上線與 AEM Headless SDK 搭配使用。 |
| 8 | [如何將 Headless 應用程式上線](go-live.md) | 了解如何線上部署應用程式，並在 Git 中取用您的本機程式碼然後移至 Cloud Manager Git 用於 CI/CD 管道。 |
| 9 | [選擇性 - 如何使用 AEM 建立單頁應用程式 (SPA)](create-spa.md) | 探索如何結合 Headful 和 Headless 傳遞，並了解如何使用 AEM 的 SPA 編輯器框架建立可編輯的 SPA。 |

{style="table-layout:auto"}

## 後續步驟 {#what-is-next}

查看下一篇文章以開始使用：[了解 CMS Headless 開發。](learn-about.md)，

### 選擇你自己的冒險 {#choose-your-path}

你偏好依自己的節奏學習嗎？查看這些選項：

* 如果您希望繼續&#x200B;**了解 Headless 概念和 AEM Headless 技術**，您應該接著檢閱此文件[如何為您的內容建立 AEM 內容模型](model-your-content.md)來繼續您的 AEM Headless 歷程，此文件可讓您了解如何在 AEM 為內容結構建立模型。
* 如果您偏好&#x200B;**做中學**，您可以移至 [AEM Headless 入門實作教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hant)，在這裡您將直接進入 AEM Headless 開發，方式是實作一個簡單專案以公開 AEM Headless 內容。

## 其他資源 {#additional-resources}

文件歷程藉由描述文字指引您完成相關流程和功能，向您說明 AEM 如何解決業務問題。此歷程說明了多個功能如何共同運作以解決單一業務需求。

查看這些額外的歷程，進一步了解 AEM 的強大功能如何共同運作。

* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hant)
* [AEM Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hant) - 如果您偏好做中學並具備 AEM 現有知識，請參閱我們的實作教學課程，其由 API 和框架所組織，其在探索如何建立並使用在 AEM Headless 建立的應用程式。
* [AEM Headless 翻譯歷程](/help/journey-headless/translation/overview.md) - 此文件歷程讓您對 Headless 技術、AEM 如何提供 Headless 內容以及如何翻譯它，有廣泛的了解。
* [Headless 製作歷程](/help/journey-headless/author/overview.md) - 從這裡開始，此歷程會逐步引導您了解 AEM 強大且靈活的 Headless 特性、其功能，以及如何在您的第一個 Headless 專案中建立內容模型。
* [Headless 架構師歷程](/help/journey-headless/architect/overview.md) - 從這裡開始介紹 Adobe Experience Manager as a Cloud Service 的強大、靈活、 Headless 功能，以及如何為您的專案建立內容模型。
* [AEM as a Cloud Service 技術文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=zh-Hant) - 如果您已經對 AEM 和 Headless 技術有紮實的了解，請查看我們深入的技術文件。
   * [AEM as a Headless CMS 簡介](/help/headless/introduction.md)
