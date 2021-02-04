---
title: AEM Sites雲端服務的無頭開發
description: AEM是雲端服務，可讓您透過內容模型、內容片段和GraphQL API等強大功能集中管理體驗，並跨通道提供。
translation-type: tm+mt
source-git-commit: e1db93e8f4cf8ef881b274879e800c9993753a66
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---


# AEM Sites的雲端服務無頭開發{#headless-development}

AEM是雲端服務，可讓您透過內容模型、內容片段和GraphQL API等強大功能集中管理體驗，並跨通道提供。

## 概覽 {#overview}

無頭實作對於為受眾提供體驗變得越來越重要，無論其身在何處，無論其通道為何。

無頭實作會與完整堆疊和混合解決方案中的傳統方式一樣，將頁面和元件管理轉換為無頭實作，並著重於建立不受通道限制、可重複使用的內容片段及其跨通道傳送。 它是一種現代化的動態開發模式，可用來建置網頁體驗。

![AEM實作模型](assets/aem-implementation-models.png)

## 比較Headful和Headless {#headful-headless}

本檔案著重於AEM的全無頭實作模型。 不過，在AEM中，無頭與無頭不一定是二進位選擇。 無頭功能可用來管理內容並將內容傳送至多種端點，同時讓內容作者編輯單頁應用程式。 全都在AEM中。

>[!TIP]
>
>如需詳細資訊，請參閱AEM中的檔案[ Headful和Headless。](/help/implementing/developing/headful-headless.md)

## AEM：雲端服務與無頭{#aem-headless}

AEM即雲端服務是適用於無頭實作模型的彈性工具，提供三種強大的服務：

1. 內容模型
   * 內容模型是內容的結構化表示。
   * 這些是由AEM內容片段模型編輯器中的資訊架構師所定義。
   * 內容模型是內容片段的基礎。
1. 內容片段
   * 內容片段是內容模型的實例化。
   * 這些是由內容作者使用AEM內容片段編輯器建立的。
   * 這些資產會儲存在AEM Assets中，並在「資產管理員UI」中管理。
1. 內容API以進行傳送
   * AEM GraphQL API支援內容片段傳送。
   * AEM Assets REST API支援內容片段CRUD作業。
   * 透過[內容片段核心元件的JSON匯出，也可直接傳送內容。](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

## 無頭入門手冊{#getting-started}

「無頭入門指南」針對使用AEM做為雲端服務建立、管理和提供體驗的簡單途徑，分五個步驟進行排版。 每本指南都以前一版為基礎，因此建議您依序徹底地探索。

1. [建立配置](getting-started/create-configuration.md)
1. [建立內容片段模型](getting-started/create-content-model.md)
1. [建立資產資料夾](getting-started/create-assets-folder.md)
1. [建立內容片段](getting-started/create-content-fragment.md)
1. [存取和傳送內容片段](getting-started/create-api-request.md)

## 對象 {#audience}

[無頭入門指南](#getting-started)中描述的工作是AEM無頭功能的基本端對端展示所必需的。 任何擁有測試AEM例項之管理員存取權的人，都可依照這些指南來瞭解AEM中的無頭傳送，不過有開發人員經驗的人是理想人選。

但是，在生產情況下，任務將由不同角色執行，但次數不同。 例如：

* **管** 理員通常只需要設定內容的初始設定和資料夾結構一次或偶爾。
* **資訊** 體系結構通常會隨著組織需求的發展而添加新的模型。
* **內容** 作者會根據架構設計人員定義的模型，持續建立新內容作為內容片段。

《無頭入門指南》指出，一般由誰執行描述的工作以及執行頻率。

## 下一步 {#next-step}

準備好要進一步瞭解嗎？ 然後，請先閱讀《無頭入門手冊》的第一部分：[建立配置。](getting-started/create-configuration.md)
