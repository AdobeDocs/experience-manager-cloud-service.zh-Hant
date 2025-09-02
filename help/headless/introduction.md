---
title: AEM Headless 簡介
description: 了解關於 Adobe Experience Manager (AEM) 內的 Headless，以及了解詳細文件和 Headless 歷程。 了解如何使用內容片段模式、內容片段和 GraphQL API 等功能來增強無周邊體驗。
landing-page-description: 了解如何使用及管理 Adobe Experience Manager as a Cloud Service 內的 Headless。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
feature: Headless
role: Admin, Developer
source-git-commit: 920045ab4e79dc223706219bf64347649af14125
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 96%

---


# Adobe Experience Manager as a Headless CMS 簡介 {#introduction-aem-headless}

了解如何使用 Adobe Experience Manager (AEM) as a Headless CMS (內容管理系統)，它具有內容片段模型、內容片段和 GraphQL API 等功能，搭配使用可大規模強化無周邊體驗。

您可以閱讀相關的各種功能的詳細文件和/或按照所選的 [Headless 歷程](#first-steps)來大致了解第一個步驟。

>[!NOTE]
>
>另請參閱[什麼是 Headless？](/help/headless/what-is-headless.md)了解 Headless 概念和術語。

## 概觀 {#overview}

AEM Headless 是 Experience Manager 的 CMS 解決方案，它允許任何應用程式使用 GraphQL 透過 HTTP 取用 AEM 中的結構化內容 (內容片段)。Headless 實作可跨平台和管道大規模傳遞體驗。

無週邊實作放棄了全堆疊和混合解決方案的頁面和元件管理傳統做法。取而代之的是專注於建立管道中立、可重複使用的內容片段及其跨管道傳遞。它是實作網頁體驗的現代動態開發模式。

![AEM 實作模型](assets/aem-implementation-models.png)

## 功能 {#aem-headless-features}

AEM as a Cloud Service 是一種適用於無周邊實作模型的靈活工具，它提供了三個強大的功能：

1. **內容片段模型**
   * 內容片段模型是內容的結構化表示。
   * 內容片段模型由資訊架構師在 AEM 內容片段模型編輯器中定義。
   * 內容片段模型是內容片段的基礎。
1. **內容片段**
   * 內容片段是根據內容片段模型建立的。
   * 內容片段由內容作者使用 AEM 內容片段編輯器建立。
   * 內容片段會儲存為 AEM Assets，但可以透過資產主控台或[內容片段控制台](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)進行管理。
1. **用於傳遞的內容 API**
   * 請參閱[結構化內容傳遞與管理的AEM API](/help/headless/apis-headless-and-content-fragments.md)，以取得各種可用API的概觀，以及所涉及概念的比較。

   * 使用[內容片段核心元件的 JSON 匯出](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hant) 也可以直接傳遞內容。

## 您的開始步驟 {#first-steps}

有多種資源可協助開始使用 AEM 的無周邊功能。每個指南都針對不同使用案例和客群量身打造。

| 資源 | 說明 | 類型 | 客群 | 預估時間 |
|---|---|---|---|---|
| [Headless 開發人員歷程](/help/journey-headless/developer/overview.md) | **對於剛接觸 AEM 和無周邊技術的開發人員**，從這裡開始全面介紹 AEM 及其無周邊功能，從無周邊理論到實作您的第一個無周邊體驗。 | 指南 | **剛接觸 AEM 和無周邊技術** 的開發人員 | 1 小時 |
| [Headless 設定](/help/headless/setup/introduction.md) | 對於需要扼要介紹關鍵 AEM 無周邊功能的&#x200B;**有經驗 AEM 使用者**，請查看此快速入門概觀。 | 參考設定 | **具有 AEM 經驗**&#x200B;的開發人員、管理員 | 20 分鐘 |
| [Headless 實作教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hant) | **如果您偏好實作教學並且熟悉 AEM**，本教程將直接深入實作簡單無周邊應用程式。 | 教學課程 | 開發人員 | 2 小時 |
| [Headless 架構師歷程](/help/journey-headless/architect/overview.md)  | **對於剛接觸 AEM 和無周邊技術的架構師**，從這裡開始介紹 Adobe Experience Manager as a Cloud Service 的強大、靈活、無周邊功能，以及如何為您的專案建立內容模型。 | 指南 | 架構師 | 1 小時 |
| [Headless 編寫歷程](/help/journey-headless/author/overview.md) | **對於剛接觸 AEM 和無周邊技術的商業使用者**，從這裡開始介紹 Adobe Experience Manager as a Cloud Service 的強大、靈活、無周邊功能，以及如何為您的專案建立內容模型。 | 指南 | 內容建立者 | 1 小時 |
| [Headless 翻譯歷程](/help/journey-headless/translation/overview.md) | 對於那些&#x200B;**對 AEM 的無周邊翻譯方法感興趣的人**。了解無周邊技術以及在 AEM 中建立和更新翻譯專案的整個過程。 | 指南 | 翻譯專家 | 1 小時 |

## 比較有周邊和無周邊 {#headful-headless}

本指南重點介紹 AEM 的完整無周邊實作模型。然而，有周邊和無周邊在 AEM 中不必是二選一的選擇。Headless 功能可用於管理內容並傳遞給多個接觸點，同時可讓內容作者編輯單頁應用程式。全部在 AEM 中。

>[!TIP]
>
>如需詳細資訊，請參閱 [AEM Headful 和 Headless 技術](/help/implementing/developing/headful-headless.md)文件。
