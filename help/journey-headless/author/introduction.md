---
title: AEM無頭內容製作歷程
description: 介紹Adobe Experience Manager as aCloud Service的強大、彈性、無頭式功能，以及如何為專案製作內容。
hide: true
hidefromtoc: true
source-git-commit: b860493d92e7886513fe08e3eb6c56bf88ca58c0
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---


# 使用AEM製作無頭版 — 簡介 {#author-headless-introduction}

在[AEM無頭內容製作歷程](overview.md)的這部分中，您可以了解以Adobe Experience Manager(AEM)為Cloud Service，了解無頭內容傳送所需的（基本）概念和術語。

## 目標 {#objective}

* **對象**:入門者
* **目標**:介紹與無頭製作相關的概念和術語。

## 內容管理系統(CMS) {#content-management-system}

什麼是內容管理系統？

內容管理系統(CMS)就是它所說的 — 一種用於管理內容的電腦系統。 這有點籠統，所以更確切地說，它通常用於管理您想在網站上提供的內容。

## 無頭式CMS {#headless-cms}

無頭是一種術語，用於描述通過在Web上顯示該內容的方式有效地分離內容的系統。

傳統上，您需要在CMS中管理內容，而同一個CMS則負責在網頁上呈現該內容。

現在，無頭意味著您的內容集可以在CMS中進行管理，然後由一個或多個（獨立）應用程式訪問。

這表示您的內容可以以多種格式傳送至任何裝置。 這可讓整個程式更有彈性，也表示您不需要擔心版面和格式設定。

>[!NOTE]
>
>如果您想進一步了解無頭式CMS的技術詳細資訊，可以在了解CMS無頭式開發中閱讀更多資訊。

## Adobe Experience Manager as a Cloud Service  {#aem-cloud-service}

那什麼是AEM?

首先，AEM是一個內容管理系統，具有多種功能，也可以根據您的需求定制。

這都表示它可作為：

* 無頭式CMS
   * 若為無頭，您的內容可製作為&#x200B;**內容片段**。
這些是可由一系列應用程式直接存取的自包含內容項目，因為它們具有基於**內容片段模型**的預定義結構。
這表示您的內容可觸及到多種裝置、多種格式和多種功能。
(此外，如果您想要，也可以在建立AEM網頁時使用這些片段，這是雙重打擊。)

* 「傳統」CMS
   * 內容是為網頁所製作，使用一系列元件來定義內容在您網站上的呈現方式。 即使在這裡，由於您的專案團隊可以開發自訂元件，AEM也極具彈性。

## 內容模型 {#content-modeling}

因此，內容模型（也稱為資料模型）是另一個技術術語，為何您覺得它是作者？

為了讓無頭應用程式能夠訪問您的內容並執行某些操作，您的內容確實需要有一個預定義的結構。 您的內容可以自由格式，但會使應用程式的生活&#x200B;*非常*&#x200B;變得複雜。

基本上，定義內容要遵循的結構的過程涉及設計模型 — 這稱為資料模型。

對於AEM，內容架構師角色（通常是不同的人員）將執行資料模型以設計&#x200B;**內容片段模型**&#x200B;範圍，然後您使用&#x200B;**內容片段**&#x200B;來作為內容的基礎。

>[!NOTE]
>
>如果您想要進一步了解資料模型，可以在AEM Headless Content Architect Journey下閱讀更多資訊。

## 下一步 {#whats-next}

現在您已了解概念和術語，接下來的步驟是[了解製作內容片段的基本知識](basics.md)。 這將介紹AEM的基本處理方式，以及如何編寫內容片段。

## 其他資源 {#additional-resources}

* AEM Headless Developer Journey
   * [了解CMS無頭開發](/help/journey-headless/developer/learn-about.md)
   * [了解如何建立內容模型](/help/journey-headless/developer/model-your-content.md)

* AEM無頭式內容架構者歷程

* AEM無頭內容翻譯歷程