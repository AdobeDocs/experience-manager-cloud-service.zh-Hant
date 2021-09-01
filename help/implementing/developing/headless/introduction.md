---
title: AEM Sites無頭開發(Headless Development as aCloud Service)
description: 了解AEM作為Cloud Service的強大無周邊功能（例如內容模型、內容片段和GraphQL API）如何搭配運作，讓您集中管理體驗，並跨管道提供體驗。
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 387e75faeccb0671a32a54ff0c12f05219844311
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---


# AEM Sites無頭開發(Headless Development as aCloud Service) {#headless-development}

了解AEM作為Cloud Service的強大無周邊功能（例如內容模型、內容片段和GraphQL API）如何搭配運作，讓您集中管理體驗，並跨管道提供體驗。

## 概覽 {#overview}

無頭式實作對於將體驗提供給對象（無論對象在何處、無論管道為何）越來越重要。

無頭實作會放棄頁面和元件管理，如同傳統的完整堆疊和混合解決方案一樣，著重於建立不受管道影響、可重複使用的內容片段及其跨管道傳送。 這是實作Web體驗的現代化、動態開發模式。

![AEM實作模型](assets/aem-implementation-models.png)

## 比較Headful和Headless {#headful-headless}

本檔案著重於AEM的完整無頭式實作模型。 不過，在AEM中，無頭與無頭並非二進位選擇。 無頭功能可用來管理內容，並將內容傳遞至各種端點，同時讓內容作者編輯單頁應用程式。 全部在AEM。

>[!TIP]
>
>如需詳細資訊，請參閱AEM](/help/implementing/developing/headful-headless.md)中的檔案[Headful和Headless 。

## AEM as aCloud Service與無頭 {#aem-headless}

AEM as aCloud Service是無頭式實作模型的彈性工具，提供三種強大的服務：

1. 內容模型
   * 內容模型是內容的結構化表示。
   * 這些由AEM內容片段模型編輯器中的資訊架構師定義。
   * 內容模型是內容片段的基礎。
1. 內容片段
   * 內容片段是內容模型的實例化。
   * 這些是由內容作者使用AEM內容片段編輯器建立。
   * 這些資產會儲存在AEM Assets中，並在Assets管理UI中進行管理。
1. 傳遞的內容API
   * AEM GraphQL API支援內容片段傳送。
   * AEM Assets REST API支援內容片段CRUD操作。
   * [內容片段核心元件的JSON匯出也可以直接傳送內容。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## 使用AEM Headless的第一步 {#first-steps}

有許多資源可供您開始使用AEM無頭功能。 這些範本適用於不同的使用案例，但都能提供AEM無頭功能的實體概述。

| 資源 | 說明 | 類型 | 對象 | Est. 時間 |
|---|---|---|---|---|
| [無頭式開發人員歷程](/help/journey-headless/developer/overview.md) | **對於剛接觸AEM和無頭式** 工具的使用者，請從這裡開始，全面介紹AEM及其無頭式功能，從無頭式理論到與您的第一個無頭式專案一起上線。 | 指南 | 開發人員&#x200B;**新增至AEM和無標題** | 1小時 |
| [無頭入門手冊](/help/implementing/developing/headless/getting-started/introduction.md) | **如果有經驗** 的AEM使用者需要主要AEM無頭功能的簡短摘要，請查看此快速入門概觀。 | 快速入門 | 開發人員、管理員&#x200B;**，具有AEM體驗** | 20分鐘 |
| [AEM Headless實作教學課程快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果您偏好使用實作方法並熟悉AEM**，本教學課程會直接深入探討如何建立簡單的無頭專案。 | 教學課程 | 開發人員 | 2小時 |
