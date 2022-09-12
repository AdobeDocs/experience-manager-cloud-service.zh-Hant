---
title: AEM Headless簡介
description: 了解關於身為 Headless CMS 的 Adobe Experience Manager (AEM)，以及了解詳細文件和 Headless 歷程。 了解如何使用內容模型、內容片段和 GraphQL API 等功能來增強 Headless 體驗。
landing-page-description: 了解如何使用及管理 Experience Manager Headless as a Cloud Service。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 4e64683598ced4b9811e957082932971f0ec0bb1
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 9%

---


# Adobe Experience Manager as a Headless CMS簡介 {#introduction-aem-headless}

了解如何使用Adobe Experience Manager(AEM)作為無周邊CMS，具備內容模型、內容片段和GraphQL API等功能，可大規模提供無周邊體驗。

您可以閱讀有關各種功能的詳細檔案，和/或遵循 [無頭歷程，以取得前幾個步驟的概觀](#first-steps).

>[!NOTE]
>
>另請參閱 [什麼是Headless?](/help/headless/what-is-headless.md) 了解無頭概念和術語的簡介。

## 總覽 {#overview}

AEM無周邊是CMS的Experience Manager解決方案，可讓任何應用程式透過HTTP使用GraphQL來使用AEM中的結構化內容（內容片段）。 無頭式實作可大規模跨平台和通道傳遞體驗。

無頭實作會放棄頁面和元件管理，如同傳統的完整堆疊和混合解決方案一樣，著重於建立不受管道影響、可重複使用的內容片段及其跨管道傳送。 這是實作Web體驗的現代化、動態開發模式。

![AEM實作模型](assets/aem-implementation-models.png)

## AEM Headless的功能 {#aem-headless-features}

AEM as a Cloud Service是無頭式實作模型的彈性工具，提供三項強大功能：

1. **內容模型**
   * 內容模型是內容的結構化表示。
   * 內容模型由AEM內容片段模型編輯器中的資訊架構師定義。
   * 內容模型是內容片段的基礎。
1. **內容片段**
   * 內容片段是根據內容模型建立。
   * 由內容作者使用AEM內容片段編輯器建立。
   * 內容片段儲存在AEM Assets中，並在Assets Admin UI中管理。
1. **傳遞的內容API**
   * AEM GraphQL API支援內容片段傳送。
   * AEM Assets REST API支援內容片段CRUD操作。
   * 您也可以透過 [內容片段核心元件的JSON匯出](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html).

## 使用AEM Headless的第一步 {#first-steps}

開始使用AEM無頭功能有數種資源。 每個指南都會針對不同的使用案例和對象量身打造。

| 資源 | 說明 | 類型 | 對象 | Est. 時間 |
|---|---|---|---|---|
| [無頭式開發人員歷程](/help/journey-headless/developer/overview.md) | **適用於剛接觸AEM和無頭的開發人員** 技術，請從這裡開始，全面介紹AEM及其無頭式功能，從無頭式理論到與您的第一個無頭式專案同時運作。 | 指南 | 開發人員 **新增至AEM及無頭** | 1小時 |
| [無頭設定](/help/headless/setup/introduction.md) | **適用於經驗豐富的AEM使用者** 若需要主要AEM無頭功能的簡短摘要，請查看此快速入門概述。 | 參考設定 | 開發人員、管理員 **使用AEM體驗** | 20分鐘 |
| [無頭式實作教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果您偏好實作方法，且熟悉AEM**，本教學課程會直接深入探討如何實作簡單的無頭應用程式。 | 教學課程 | 開發人員 | 2小時 |
| [無頭架構師歷程](/help/journey-headless/architect/overview.md) | **對於剛接觸AEM和無頭架構師** 技術，從這裡開始介紹Adobe Experience Manager as a Cloud Service強大、靈活、無頭的功能，以及如何為您的專案建立內容模型。 | 指南 | 建築師 | 1小時 |
| [無頭製作歷程](/help/journey-headless/author/overview.md) | **適用於剛接觸AEM和無頭的業務使用者** 技術，從這裡開始介紹Adobe Experience Manager as a Cloud Service強大、靈活、無頭的功能，以及如何為您的專案建立內容模型。 | 指南 | 內容建立者 | 1小時 |
| [無頭翻譯歷程](/help/journey-headless/translation/overview.md) | 對於那些 **對AEM的無頭翻譯方法感興趣**. 了解無頭技術，以及如何在AEM中從A到Z建立和更新翻譯專案。 | 指南 | 翻譯專家 | 1小時 |

## 比較Headful和Headless {#headful-headless}

本指南著重於AEM的完整無頭式實作模型。 不過，在AEM中，無頭與無頭並非二進位選擇。 無頭功能可用來管理內容，並將內容傳送至多個接觸點，同時讓內容作者編輯單頁應用程式。 全部在AEM。

>[!TIP]
>
>請參閱檔案 [AEM中的Headful和Headless](/help/implementing/developing/headful-headless.md) 以取得更多資訊。