---
title: 作為無AEM頭CMS的內容建模 — 簡介
description: 介紹使用Adobe Experience Manager as a Cloud Service的功能作為無頭CMS來為項目的內容建模。
exl-id: 62061d73-6fdb-440b-a7dd-b0d530d49186
source-git-commit: 00ec09f327bc2f382d263970e690ed067aaa1355
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 作為無AEM頭CMS的內容建模 — 簡介 {#architect-headless-introduction}

在 [無AEM頭內容架構師旅程](overview.md)，您可以學習在將Adobe Experience Manager()as a Cloud Service用作無頭CMS時理解內容建模所必AEM要的（基本）概念和術語。

本文檔幫助您瞭解無頭內容的交付、AEM如何支援無頭內容以及如何為無頭內容建模。 閱讀完後，您應：

* 瞭解無頭內容交付的基本概念。
* 熟悉如何支AEM持無頭和內容建模。

## 目標 {#objective}

* **觀眾**:初學者
* **目標**:介紹與無頭內容建模相關的概念和術語。

## 完整堆棧內容交付 {#full-stack}

自從易於使用的大規模內容管理系統(CMS)興起以來，各公司一直利用它們作為管理消息傳遞、品牌推廣和通信的中心位置。 將CMS用作管理經驗的中心點，通過消除在不同系統中重複任務的需要而提高了效率。

![經典的全堆棧CMS](/help/journey-headless/developer/assets/full-stack.png)

在全棧CMS中，用於處理內容的所有功能都在CMS中。 系統的功能構成了CMS堆棧的不同元件。 全棧解決方案具有許多優點。

* 有一個系統要維護。
* 內容集中管理。
* 系統的所有服務都是整合的。
* 內容創作是無縫的。

因此，如果需要添加新的通道或需要支援新類型的體驗，則可以將一個（或多個）新元件插入堆棧中，並且只有一個位置可以進行更改。

![向堆棧添加新通道](/help/journey-headless/developer/assets/adding-channel.png)

但是，堆棧內依賴項的複雜性很快變得明顯，因為堆棧中的其他項需要調整以適應更改。

## 《無頭》 {#the-head}

任何系統的頭通常是該系統的輸出呈現器，通常以GUI或其他圖形輸出的形式。

當我們討論無頭CMS時， CMS會管理內容，並繼續將其提供給消費者。 但是，只通過 **內容** 無頭CMS以標準化方式忽略最終輸出渲染， **演示** 內容到消費服務。

![無頭CMS](/help/journey-headless/developer/assets/headless-cms.png)

消費服務，無論是AR體驗、網店、移動體驗、漸進式Web應用(PWA)等，都會從無頭CMS中獲取內容並提供自己的呈現。 他們會為您的內容提供自己的頭腦。

省去頭部，通過消除複雜性來簡化CMS。 這樣做還會將內容呈現的責任轉移到實際需要內容並且通常更適合此類呈現的服務上。

## 內容建模 {#content-modeling}

內容建模（也稱為資料建模）是您的專長，因此在為無頭對象建模時需要考慮哪些因素？

為了讓無頭應用程式能夠訪問您的內容並對其執行某些操作，內容真正需要有一個預定義的結構。 你的內容可以自由格式，但它會讓生活 *非常* 應用程式複雜。

作AEM為內容架構師，您將執行內容建模以設計 **內容片段模型**。 這些定義內容作者建立 **內容片段** 保存內容。

### 訪問內容 {#access-content}

這更像是一個開發細節 — 但你可能會感興趣，只是為了完成這個故事。

一旦您建立了內容片段模型，並且您的作者使用它們來生成內容，無頭應用程式就需要訪問此內容。

Adobe Experience Manager(AEM)as a Cloud Service，可以使用AEMGraphQL API有選擇地訪問您的內容片段，以僅返回所需的內容。 使用API，開發人員可以制定選擇特定內容的查詢。此選擇過程基於 *你* 內容片段模型。

這意味著您的項目可以實現結構化內容的無頭交付，以便在您的應用程式中使用。

## 下一步是什麼 {#whats-next}

現在您已經掌握了概念和術語，下一步是 [瞭解使用內容片段模型進行建模的基礎知識](basics.md)。

## 其他資源 {#additional-resources}

* 無AEM頭開發者之旅
   * [瞭解CMS無頭開發](/help/journey-headless/developer/learn-about.md)
   * [瞭解如何對內容建模](/help/journey-headless/developer/model-your-content.md)
