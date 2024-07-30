---
title: AEM Sites與Edge Delivery Services
description: 瞭解Edge Delivery Services如何擴展AEM Sites的製作和發佈可能性，以加速內容建立並以100%效能提供網站。
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: b3497f87446ca4c1c71d48f29aebcaa882feb898
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 5%

---


# AEM Sites與Edge Delivery Services {#sites-and-edge}

瞭解Edge Delivery Services如何擴展AEM Sites的製作和發佈可能性，以加速內容建立並以100%效能提供網站。

## 概觀 {#overview}

除了AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)作為雲端原生AEM as a Cloud Service平台的一部分所提供的所有[功能和特性之外，Edge Delivery Services還提供額外的撰寫和發佈可能性，以加速內容建立並以100%的效能提供網站。

## 什麼是Edge Delivery Services？ {#what-is-edge}

Edge Delivery Services提供卓越的體驗，透過提供快速編寫和開發的高影響力體驗，促進參與和轉換。 這是一組可組合的服務，有助建立快速開發環境；編寫作者可在其中快速更新和發佈，並且能快速推出新網站。在檔案[Edge Delivery Services概觀中進一步瞭解Edge Delivery Services。](/help/edge/overview.md)

搭配AEM Sitesas a Cloud Service使用Edge Delivery Services時，您的專案將受益於以下好處：

* [全新的開發人員體驗](#developer-experience)
* [新的發佈階層](#publish-tier)
* [其他撰寫選項](#authoring-options)

## 全新的開發人員體驗 {#developer-experience}

Edge Delivery Services的核心理念是&#x200B;*速度*。 先從開發人員體驗開始。 如果您的開發人員：

* 瞭解Git基本概念和
* 瞭解HTML、CSS和JavaScript的基本概念

不到30分鐘，他們就可以開始自訂自己的Edge Delivery Services專案和元件。 首先，在GitHub上複製範本專案，然後提交您的變更。 您的自訂功能可立即上線！

請參閱檔案[快速入門 — 開發人員教學課程](https://www.aem.live/developer/tutorial)，瞭解更多有關Edge Delivery Services開發的資訊。

## 新的Publish階層 {#publish-tier}

不僅開發時間大幅縮短，Edge Delivery Services也帶來超快的網站。

## 其他撰寫選項 {#authoring-options}

Edge Delivery Services也能提供新的撰寫選項，加快內容建立速度。

### 通用編輯器 {#universal-editor}

Universal Editor提供順暢的、所見即所得(WYSIWYG)製作體驗，可用來製作任何內容。

請參閱檔案[WYSIWYG Content Authoring for Edge Delivery Services](/help/edge/wysiwyg-authoring/authoring.md)，以進一步瞭解如何使用通用編輯器編寫內容。

### 以文件為主的製作 {#document-authoring}

檔案式製作讓任何人都能運用眾所周知的工具(Word和Google檔案)建立內容，不需接受任何訓練。 使用這些簡單的工具，Edge Delivery Services可以立即將變更轉換為Word檔案，以更新您網站上的內容。

請參閱檔案[製作和發佈內容](https://www.aem.live/docs/authoring)，深入瞭解如何使用檔案式製作。

## Edge適合您嗎？ {#decision}

Adobe已發現其客戶及其參與的利害關係人從各種規模專案的Edge Delivery Services中大量受益。 因此，Adobe建議將Edge Delivery Services作為任何新專案的起點。

也可以在Edge Delivery上部署網站或頁面的子集，同時將其餘專案保留在目前棧疊上。 每當需要改善效能、自然流量、客戶參與度、開發人員或內容速度時，建議採用此做法。

如果您不確定Edge Delivery是否適合您，請洽詢您的Adobe代表。

### Edge Delivery和Headless呢？ (#headless)

Edge Delivery是從後端分離出來的效能優先標題。 如果您有自訂Head，例如React SPA，Adobe會建議AEM Headless整合模式。 如需詳細資訊，請參閱[AEM Headless檔案](/help/headless/introduction.md)。

不過，Adobe通常建議使用Edge Delivery作為預設標題，以受益於其速度和效能，並透過Headless方法(例如React或SPA)整合專案的Headless部分（通常是業務應用程式）。
