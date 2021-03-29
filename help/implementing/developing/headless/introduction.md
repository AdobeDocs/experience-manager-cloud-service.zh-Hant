---
title: AEM Sites作為Cloud Service的無頭髮展
description: 了AEM解Cloud Service的強大無頭功能（例如內容模型、內容片段和GraphQL API）如何搭配運作，讓您集中管理體驗並跨通道提供。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---


# AEM Sites作為Cloud Service的無頭髮展{#headless-development}

了AEM解Cloud Service的強大無頭功能（例如內容模型、內容片段和GraphQL API）如何搭配運作，讓您集中管理體驗並跨通道提供。

## 概覽 {#overview}

無頭實作對於為受眾提供體驗變得越來越重要，無論其身在何處，無論其通道為何。

無頭實作會與完整堆疊和混合解決方案中的傳統方式一樣，將頁面和元件管理轉換為無頭實作，並著重於建立不受通道限制、可重複使用的內容片段及其跨通道傳送。 它是一種現代化的動態開發模式，可用來建置網頁體驗。

![實AEM施模型](assets/aem-implementation-models.png)

## 比較Headful和Headless {#headful-headless}

本文著重於的完全無頭實作模AEM型。 不過，無頭與無頭不一定是二進位選擇AEM。 無頭功能可用來管理內容並將內容傳送至多種端點，同時讓內容作者編輯單頁應用程式。 全部AEM。

>[!TIP]
>
>如需詳細資訊，請參閱](/help/implementing/developing/headful-headless.md)中的[AEM Headful和Headless檔案。

## 作AEM為Cloud Service和無頭{#aem-headless}

作AEM為Cloud Service，提供三種強大的服務，為無頭實作模型提供靈活的工具：

1. 內容模型
   * 內容模型是內容的結構化表示。
   * 這些定義由「內容片段模型」編輯器中的AEM資訊架構師定義。
   * 內容模型是內容片段的基礎。
1. 內容片段
   * 內容片段是內容模型的實例化。
   * 這些是由內容作者使用內容片段編輯器AEM建立的。
   * 它們儲存在AEM Assets，並在「資產管理員UI」中管理。
1. 內容API以進行傳送
   * GraphQL AEM API支援內容片段傳送。
   * AEM AssetsREST API支援內容片段CRUD作業。
   * 透過[內容片段核心元件的JSON匯出，也可直接傳送內容。](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

## 無頭入門手冊{#getting-started}

「無頭入門手冊」針對建立、管理和提供體驗的簡單途徑，透過五個步驟排AEM列出簡單的步驟，以做為Cloud Service。 每本指南都以前一版為基礎，因此建議您依序徹底地探索。

1. [建立配置](getting-started/create-configuration.md)
1. [建立內容片段模型](getting-started/create-content-model.md)
1. [建立資產資料夾](getting-started/create-assets-folder.md)
1. [建立內容片段](getting-started/create-content-fragment.md)
1. [存取和傳送內容片段](getting-started/create-api-request.md)

## 對象 {#audience}

[無頭入門指南](#getting-started)中描述的任務對於基本的無頭功能端到端演示是必AEM要的。 任何擁有測試例項存取權的管AEM理員都可依照這些指南來瞭解無頭傳送，AEM不過有開發人員經驗的人最適合。

但是，在生產情況下，任務將由不同角色執行，但次數不同。 例如：

* **管** 理員通常只需要設定內容的初始設定和資料夾結構一次或偶爾。
* **資訊** 體系結構通常會隨著組織需求的發展而添加新的模型。
* **內容** 作者會根據架構設計人員定義的模型，持續建立新內容作為內容片段。

《無頭入門指南》指出，一般由誰執行描述的工作以及執行頻率。

## 下一步 {#next-step}

準備好要進一步瞭解嗎？ 然後，請先閱讀《無頭入門手冊》的第一部分：[建立配置。](getting-started/create-configuration.md)
