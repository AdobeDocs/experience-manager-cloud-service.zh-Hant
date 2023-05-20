---
title: AEM as a Headless CMS 內容模型 - 簡介
description: 介紹使用 Adobe Experience Manager as a Cloud Service as a Headless CMS 的功能為您的專案建立內容模型。
exl-id: 62061d73-6fdb-440b-a7dd-b0d530d49186
source-git-commit: 00ec09f327bc2f382d263970e690ed067aaa1355
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 100%

---

# AEM as a Headless CMS 內容模型 - 簡介 {#architect-headless-introduction}

在 [AEM Headless 內容架構師歷程](overview.md) 的這一部分中，您可以學習必要的 (基本) 概念和術語，以了解如何使用 Adobe Experience Manager (AEM) as a Cloud Service as a Headless CMS 建立內容模型。

此文件可協助您了解無周邊內容傳遞、AEM 如何支援無周邊以及如何建立無周邊內容模型。閱讀本文件後，您應該：

* 了解無周邊內容傳遞的基本概念。
* 熟悉 AEM 如何支援無周邊和內容模型。

## 目標 {#objective}

* **對象**：初學者
* **目標**：介紹與 Headless 內容模型相關的概念和術語。

## 全堆疊內容傳遞 {#full-stack}

自從易於使用的大型內容管理系統 (CMS) 興起以來，組織就將其作為管理訊息、品牌和通訊的中心位置。使用 CMS 做為管理體驗的中心點可以提升效率，因為就不需要在各個不同系統重複任務。

![傳統的全堆疊 CMS](/help/journey-headless/developer/assets/full-stack.png)

在全堆疊 CMS 中，所有操控內容的功能都在 CMS 中。系統的功能構成了 CMS 堆疊的不同元件。全堆疊解決方案有很多優點。

* 只需維護一個系統。
* 內容集中管理。
* 系統的所有服務都是整合在內的。
* 內容編寫可完美無縫進行。

因此，如果需要新增新管道或支援新類型的體驗，可以將一個 (或多個) 新元件插入至堆疊中，並且只有一個地方可以進行變更。

![將新管道加入到堆疊](/help/journey-headless/developer/assets/adding-channel.png)

然而，隨著堆疊中的其他項目需要調整以適應變更，堆疊中的相依性複雜度很快就會變得明顯。

## Headless 的頭部 {#the-head}

任何系統的頭部通常是該系統的輸出呈現器，通常採 GUI 或其他圖形輸出的形式。

當我們談論 Headless CMS 時，CMS 管理內容並繼續將其傳遞給取用者。然而，透過僅將&#x200B;**內容**&#x200B;以標準方式傳遞，Headless CMS 會省略最後輸出呈現作業，將內容的&#x200B;**展示**&#x200B;作業留給取用內容的服務執行。

![ Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

取用內容的服務，無論是 AR 體驗、網路商店、行動體驗、漸進式網頁應用程式 (PWA) 等，都從 Headless CMS 取用內容並提供自己的呈現操作。它們負責為您的內容提供自己的頭。

省略頭可消除複雜性來簡化 CMS。這樣做也會將呈現內容的責任轉移到實際需要內容並且通常更適合執行呈現的服務。

## 內容模型 {#content-modeling}

內容模型 (也稱為資料模型) 是您的專長，那麼在建立無周邊模型時需要考慮什麼？

要讓無周邊應用程式能夠存取內容並對內容進行一些處理，內容確實需要具有預先定義的結構。您的內容可以採用自由格式，但會使應用程式&#x200B;*十分*&#x200B;不便。

對於 AEM，作為內容架構師，您將執行內容模型以設計一系列&#x200B;**內容片段模型**。這些定義了內容作者建立保留內容的&#x200B;**內容片段**&#x200B;時使用的結構。

### 存取內容 {#access-content}

這更像是一個開發細節 - 但它可能會讓您感興趣，只是為了完成這個故事。

一旦您建立了內容片段模型，並且您的作者已使用它們產生內容，無周邊應用程式將需要存取此內容。

Adobe Experience Manager (AEM) as a Cloud Service 可以使用 AEM GraphQL API 選擇性地存取內容片段，以僅傳回所需的內容。使用 API，開發人員可以制定選取特定內容的查詢。此選取流程是根據&#x200B;*您的*&#x200B;內容片段模型進行的。

這表示您的專案可以實現結構化內容的無周邊傳遞，以便用於您的應用程式中。

## 下一步 {#whats-next}

現在您已經了解了概念和術語，下一步是[了解使用內容片段模型建立模型的基本知識](basics.md)。

## 其他資源 {#additional-resources}

* AEM Headless 開發人員歷程
   * [了解 CMS Headless 開發](/help/journey-headless/developer/learn-about.md)
   * [了解如何建立內容模型](/help/journey-headless/developer/model-your-content.md)
