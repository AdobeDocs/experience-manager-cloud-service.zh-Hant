---
title: 作為無AEM頭CMS的創作 — 簡介
description: 介紹使用Adobe Experience Manager as a Cloud Service的功能作為無頭CMS為項目編寫內容。
exl-id: 065b00cb-a82d-4bcb-b2c9-44542cee6303
source-git-commit: 00ec09f327bc2f382d263970e690ed067aaa1355
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# 作為無AEM頭CMS的創作 — 簡介 {#author-headless-introduction}

在 [無AEM頭內容作者之旅](overview.md)，您可以學習在將Adobe Experience Manager()as a Cloud Service用作無頭CMS時理解創作內容所必AEM要的（基本）概念和術語。 這涉及構建和建立您的內容，以便無頭內容交付。

## 目標 {#objective}

* **觀眾**:初學者
* **目標**:介紹與無頭創作相關的概念和術語。

## 內容管理系統(CMS) {#content-management-system}

什麼是內容管理系統？

內容管理系統(CMS)就是它所說的 — 一個用於管理內容的電腦系統。 這有點籠統，因此更準確地說，它（通常）用於管理您希望在您的網站上提供的內容。

## 無頭CMS {#headless-cms}

「無頭」一詞用於描述將內容與在Web上顯示內容的方式有效分離的系統。

傳統上，您會在CMS中管理內容，而同一CMS將負責在您的網頁上呈現該內容。

現在，無頭意味著可以在CMS中管理您的內容集，然後由一個或多個（獨立）應用程式訪問。

這意味著您的內容可以以多種格式傳送到任何設備。 這使整個過程更加靈活，也意味著您無需擔心佈局和格式設定。

>[!NOTE]
>
>如果您想瞭解有關無頭CMS的技術詳細資訊，可以在瞭解CMS無頭開發時閱讀更多資訊。

## Adobe Experience Manager as a Cloud Service  {#aem-cloud-service}

那是什AEM麼？

首先，也是AEM最重要的，是一個內容管理系統，它具有多種功能，也可以定制以滿足您的需求。

這意味著它可以用作：

* 無頭CMS
   * 對於無頭，您的內容可以創作為 **內容片段**。
這些是可由一系列應用程式直接訪問的自包含內容項，因為它們具有基於的預定義結構 **內容片段模型**。
這意味著您的內容可以以多種格式和多種功能訪問各種設備。
(而且，如果你願意，這些片段也可以用AEM於構建網頁。)

* 「傳統」CMS
   * 內容是為網頁創作的，使用一系列元件來定義內容將如何在您的網站上呈現。 即使在這AEM里，您的項目團隊也可以開發定製的元件，因此非常靈活。

## 內容建模 {#content-modeling}

因此，內容建模（也稱為資料建模）是另一個技術術語 — 作為作者，它為什麼會引起您的興趣？

為了讓無頭應用程式能夠訪問您的內容並對其執行某些操作，您的內容確實需要有一個預定義的結構。 你的內容可以自由格式，但它會讓生活 *非常* 應用程式複雜。

基本上，定義內容所遵循的結構的過程包括設計一個模型 — 這稱為資料建模。

對於AEMContent Architect角色（通常是另一個人），將執行資料建模以設計一系列 **內容片段模型**  — 然後，您使用 **內容片段**。

>[!NOTE]
>
>如果您想瞭解有關資料建模的更多資訊，可以在「無頭內容架構AEM師旅程」下閱讀更多內容。

## 下一步是什麼 {#whats-next}

現在您已經掌握了概念和術語，下一步是 [瞭解創作內容片段的基本知識](basics.md)。 這將介紹Content Fragments的基AEM本處理，以及如何編寫內容片段。

## 其他資源 {#additional-resources}

* 無AEM頭開發者之旅
   * [瞭解CMS無頭開發](/help/journey-headless/developer/learn-about.md)
   * [瞭解如何對內容建模](/help/journey-headless/developer/model-your-content.md)

* 無AEM頭內容架構師旅程

* 無AEM頭內容翻譯歷程
