---
title: 將 Edge Delivery Services 與現有 AEM 專案結合使用
description: 了解如何在現有 AEM 專案中利用 Edge Delivery Services 的優勢
feature: Edge Delivery Services
exl-id: f54aac3a-1d0c-4be0-9aa6-616217e0e458
source-git-commit: b940877abff45e2a9ee046aec74af067007f41c3
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 100%

---


# 將 Edge Delivery Services 與現有 AEM 專案結合使用 {#existing-projects}

您不需要等待新的 AEM 專案，即可取得 Edge Delivery Services 帶來的好處。Edge Delivery Services 可以整合到現有的 AEM 專案中，讓您可立即利用專案提升的效能。

## AEM 頁面編輯器限制 {#page-editor}

在有 Edge Delivery Services 之前，AEM 所管理的內容是使用 AEM 頁面編輯器進行編輯。如果您的專案是在 Edge Delivery Services 推出之前展開，幾乎可確定您目前是使用頁面編輯器。

AEM 頁面編輯器僅適用於 [AEM 元件](/help/implementing/developing/components/overview.md)，例如[核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 這些元件與 Edge Delivery Services 不相容&#x200B;&#x200B;。因此，需要兩個階段才能將 Edge Delivery Services 引入現有的 AEM 專案：

* [第 1 階段 - 取代前端](#replace-front-end)
* [第 2 階段 - 切換至 Universal Editor](#switch-ue)

## 第 1 階段 - 取代前端 {#replace-front-end}

在第一階段，您可以繼續使用現有的 AEM 網站結構、元件和製作工具。網站轉譯將透過使用 JavaScript 和 CSS 的區塊進行重建，並將透過 Edge Delivery Services 進行交付。

請參閱 Edge Delivery Services 文件的[「建置」區段](/help/edge/developer/block-collection.md) ，了解有關區塊以及如何開發 Edge Delivery Services 更多詳細資訊。

應用程式建立工具上的轉換器需要轉換 AEM 轉譯的 HTML 輸出，並將其傳送至 Edge Delivery Services。

![發佈流程中的內容轉換器](assets/content-converter.png)

第二階段會透過消除技術重疊來完成流程：AEM Author 上有 HTL 和 Java 的 AEM 核心元件、Edge Delivery 上以 JS 為主的區塊，還有以 NodeJS 為主的轉換器。

## 第 2 階段 - 切換至 Universal Editor {#switch-ue}

在這個階段中，AEM 頁面編輯器將會由 Universal Editor 取代。由於 Universal Editor 可以直接使用區塊，因此不再需要 AEM 核心元件和轉換器。
