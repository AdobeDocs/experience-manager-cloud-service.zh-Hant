---
title: 什麼是 Headless CMS？
description: 了解 Headless CMS。它們如何運作？有哪些替代選項和差異？為什麼要使用 Headless CMS？
exl-id: 53f24f69-ad49-4b8e-9a91-36cd64c1f2b9
feature: Headless
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 100%

---

# 什麼是 Headless CMS？ {#what-is-a-headless-cms}

Headless 內容管理是當今網頁設計的關鍵發展，它將前端、用戶端應用程式與後端、內容管理系統分離。因此，Headless CMS 會負責 (後端) 內容管理服務以及允許 (前端) 應用程式存取該內容的機制。

但是這個術語的真正含義是什麼？我們在此 (非常快速地) 介紹重要概念。

## 什麼是內容管理系統 (CMS)？ {#content-management-system}

讓我們從基礎開始 - 什麼是內容管理系統？

內容管理系統 (CMS) 會儲存、管理和傳遞用於提供線上體驗的內容。

## 傳統 CMS {#traditional-cms}

傳統上，CMS 即已包括用於儲存和傳遞內容的後端功能，以及用於呈現瀏覽器將顯示的體驗標記的前端技術 (展示層)。

非常強大，讓您可以完全控制內容和格式，但缺少當今快速發展的環境中所需的一些靈活性；例如，與外部應用程式結合。

## Headless CMS {#headless-cms}

使用無周邊內容管理系統，後端和前端現在可分離。

無周邊部分是內容後端，因為無周邊內容管理系統 (CMS) 是僅限後端的內容管理系統，明確設計和建置為內容存放庫，可透過 API 存取內容，以便在任何裝置上顯示。

獨立開發和維護的前端使用內容傳遞 API 通常採用 JSON 格式從無周邊後端擷取內容，通常採用 JSON 格式。例如，這可以作為 React 或 Angular 應用程式 (單頁應用程式 (SPA))。

Headless CMS 後端通常需要內容已根據模型或方案進行結構化。這有助於用戶端應用程式要求正確內容來呈現體驗。一些 CMS 可以公開 JSON 格式的結構化和非結構化內容。

此拓撲的一個關鍵特性是 Headless CMS 以 JSON 格式提供的內容是純內容，沒有設計或版面資訊。在 Headless CMS 實作中，所有格式和版面都由分離的前端應用程式維護。

Headless CMS 拓撲的一個主要好處是能夠跨多個管道重複使用內容，這可能使用不同的用戶端前端實作。這可以提高前端開發流程效率。但這也表示前端體驗開發流程可以變得非常以程式碼和 IT 為中心，IT 基本上擁有體驗。

## 內容傳遞 API {#content-delivery-apis}

Headless CMS 可以提供一種或多種方式將內容公開給用戶端應用程式。最常見的是 HTTP REST API、GraphQL API 或兩者皆有。

雖然 REST API 通常看起來是一種更簡單的要求內容方式 (例如，為符合條件的所有內容提供 JSON)，但它們通常會向用戶端應用程式提供太多內容。這可能導致用戶端必須剖析和篩選掉用於呈現的實際必要內容。

相比之下，GraphQL 是一種更有針對性的機制，允許用戶端應用程式準確查詢用於呈現體驗的必要內容。

## 全堆疊 CMS {#fullstack-cms}

全堆疊 CMS 通常代表用於管理和傳遞內容的傳統拓撲，包括用於呈現體驗的內容後端和前端技術。使用全堆疊 CMS 進行內容傳遞通常發生內部內容傳遞 API 上。前端功能通常特定於全堆疊 CMS。這種前端技術與內容後端的結合讓所見即所得 (WYSIWYG) 體驗編寫成為主要優勢。

## 混合 CMS {#hybrid-cms}

全堆疊 CMS 的現代進化版可以是混合 CMS。這旨在結合兩者的強項：

* 使用現代前端工具跨管道進行高效的前端開發，
* 同時保留 WYSIWYG 體驗編寫讓非技術使用者可使用，並避免 IT 成為跨組織內容和體驗管理的瓶頸。

這是透過採用現代前端框架 (例如 React) 但保持與內容後端的最低結合度來實現的。

## 分離的 CMS {#decoupled-cms}

雖然這個術語「分離的 CMS」有時是獨立使用的，但它本質上是透過強調其與用戶端前端應用程式分離的主要特性來描述 Headless CMS 後端。

## 有周邊 CMS {#headful-cms}

這是傳統 CMS 的另一個術語。

## 延伸閱讀 {#further-reading}

此處提供更多在 Headless CMS 拓撲中使用 AEM 的相關資訊：

* [Adobe Experience Manager as a Headless CMS 簡介](/help/headless/introduction.md)
