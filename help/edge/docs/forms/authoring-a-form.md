---
title: 如何在AEM中編寫表單？
description: 瞭解Adobe Experience Manager (AEM)提供的各種表單撰寫平台，以及如何根據您的需求選擇正確的平台。
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
source-git-commit: ec5d15d6ca0e4dc75d1f8abbbd6f794534d8bed7
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 7%

---


# 如何在Adobe Experience Manager (AEM)中撰寫Forms？

Adobe Experience Manager (AEM)提供彈性的平台，可讓您建立吸引人、回應式、動態且最適化的表單。 它提供直覺式使用者介面和一組豐富的現成元件，用於建置和管理Adaptive Forms。 視您的需求而定，無論是否使用表單模型或結構描述，都可以編寫Forms。

## 選擇撰寫平台時的主要考量事項

AEM提供多種表單製作選項，可建立互動且吸引人的表單。 選取表單製作環境時，請考慮下列因素：

| ??**考量** | ??**要問的問題** |
|----------------------|--------------------|
| **使用者專業知識** | 誰將編寫表單 — 開發人員、業務使用者或內容作者？ |
| **表單複雜性** | 表單是否需要進階規則、動態區段或整合？ |
| **重複使用需求** | 表單的部分是否會跨不同的表單或專案重複使用？ |
| **設計彈性** | 您是否需要完整控制版面、主題和樣式？ |
| **整合需求** | 表單是否需要連線到資料模型、工作流程或外部系統？ |
| **易用性** | 平台是否可直覺地反映您團隊的技術技能水準？ |
| **效能與擴充性** | 表單會大規模使用還是在高流量環境中使用？ |
| **全通路傳遞** | 此表單是否會用於網站、行動應用程式、資訊站或多個管道？ |
| **發佈彈性** | 表單將在AEM、Edge Delivery或自訂應用程式上發佈到何處？ |

## AEM中的表單製作方法概觀

AEM支援多種編寫方法，每種方法都適合不同的使用者需求、技術技能水準和發佈目的地。

* [基礎元件](/help/forms/create-adaptive-form-tutorial.md)：使用基礎元件來建置傳統的互動式表單。 最適合整合舊有系統或依賴長期工作流程的表單。 以Foundation元件撰寫的Forms只能在AEM上發佈，而且與Edge Delivery Services不相容。

* [核心元件](/help/forms/creating-adaptive-form-core-components.md)：使用核心元件建立現代、回應式且可擴充的表單。 支援可重複使用、協助工具及更出色的效能。 使用核心元件撰寫的Forms可發佈在AEM和Edge Delivery Services上，提供跨平台的彈性。

* [Edge Delivery Services Forms](/help/edge/docs/forms/overview.md)： Edge Delivery Services Forms可轉換表單的製作、執行及處理方式。 利用 Edge Delivery Services，組織即可建立快速、安全且高度可用的數位表單，並透過快速的開發環境增強使用者體驗和作業效率。您可以透過兩種方式撰寫Edge Delivery Services Forms：
   * [WYSIWYG製作](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：使用通用編輯器以視覺化方式建立拖放式表單，非常適合技術知識有限的內容作者。 使用Universal Editor編寫的Forms會使用Edge Delivery Services提供，以進行快速、輕量化的呈現。
   * [檔案式撰寫](/help/edge/docs/forms/tutorial.md)：使用Microsoft Excel或Google Sheets之類的工具來定義表單結構和內容。 對於偏好以試算表為導向的輸入之業務使用者，此方法相當實用。 這些表單通常會透過Edge Delivery Services發佈，並適用於輕量且大量量的使用案例。
* [Headless製作](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)：使用API在任何前端(例如React、Angular、行動應用程式或資訊站)將表單轉譯為JSON，而不依賴AEM。 目前，只有核心元件支援Headless傳送。 Headless表單適用於全通路使用案例，且在AEM的頁面轉譯之外單獨使用，使其可彈性用於自訂前端部署。

### AEM表單製作方法的比較分析

下&#x200B;表提供各種AEM表單製作方法的簡短比較，重點說明方法、功能、發佈選項和理想的使用案例，以協助您選取最符合需求的方法。

| **考量** | **基礎元件** | **核心元件** | **通用編輯器(WYSIWYG)** | **文件型編寫** | **Headless製作** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **適合** | 在AEM中維護舊版表單和工作流程 | 具備複雜工作流程與整合功能的可擴充現代化表單 | 為具有複雜需求的Edge Delivery服務網站建立表單 | 快速建立原型或基本表單，無進階提交服務 | 跨平台（網路、行動裝置、資訊站等）的全通路體驗 |
| **使用者專業知識** | 開發人員、內容作者 | 開發人員、進階作者 | 商務使用者、內容作者 | 業務使用者 | 開發人員 |
| **表單複雜性** | 基本表單 | 具有動態區段的複雜表單 | 具有自訂動作的複雜表單 | 簡單表單 | 高度複雜的API驅動表單 |
| **設計彈性** | 有限 | 高（CSS/JS自訂） | 稽核（根據範本） | 有限 | 高（前端框架控制） |
| **整合功能** | 基本AEM工作流程 | 進階（資料模型、工作流程） | 與外部系統整合 | 基本(Google工作表、Excel) | 透過API完全控制 |
| **發佈方法** | 僅限AEM | AEM 和 Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | 透過API的任何前端 |
| **效能與SEO** | 標準 | 基礎元件的改良功能 | Google Lighthouse分數較高，可加快轉譯速度並改善SEO | Google Lighthouse分數較高，可加快轉譯速度並改善SEO | 取決於實作 |
| **全通路傳遞** | 有限 | 中等 | 中等 | 有限 | 高 |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### AEM表單製作方法的功能比較

下表提供不同AEM表單製作方法的主要功能詳細比較，協助您選取最符合需求的方法&#x200B;。

| **功能** | **基礎元件** | **核心元件** | **通用編輯器(WYSIWYG)** | **文件型編寫** | **Headless製作** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **與站台整合的組合** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **內嵌表單支援** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **規則（動態行為）** | 具有自訂函式的進階規則編輯器 | 具有自訂函式的進階規則編輯器 | 具有自訂函式的進階規則編輯器 | 有限：顯示/隱藏、計算值、自訂函式 | 有限：需要自訂實作 |
| **附件支援** | ✅ | ✅ | ✅ | ℹ️ （搶先使用） | ❌ |
| **驗證碼支援** | reCAPTCHA v2/Enterprise、hCaptcha (EA)、Turnstile (EA) | reCAPTCHA v2/Enterprise、hCaptcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 需要自訂整合 |
| **提交功能** | REST端點、電子郵件、表單資料模型(FDM)、叫用AEM工作流程、SharePoint、OneDrive、Azure Blob儲存、Power Automate、Workfront Fusion (EA) | REST端點、電子郵件、表單資料模型(FDM)、叫用AEM工作流程、SharePoint、OneDrive、Azure Blob儲存、Power Automate、Workfront Fusion (EA) | REST端點、電子郵件、表單資料模型(FDM)、叫用AEM工作流程、SharePoint、OneDrive、Azure Blob儲存、Power Automate、Workfront Fusion (EA) | 僅限試算表 | 自訂API端點 |
| **資料結構描述** | FDM，自訂 | FDM，自訂 | FDM，自訂 | 自訂 | 自訂 |
| **預填** | ✅ | ✅ | ??（透過精靈） | ✅ | 自訂實施 |
| **片段** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **視覺規則編輯器** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **本地化** | ✅ | ✅ | ??（透過網站） | ℹ️ (Excel — 手動，Google Sheets功能) | 自訂實施 |
| **資料結構描述（資料樹狀結構）** | ✅ | ✅ | ??（透過UI擴充功能） | ❌ | 自訂實施 |
| **範本支援** | ✅ | ✅ | 僅限初始內容，無原則 | ❌ | 自訂實施 |
| **入口網站** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **DoR製作** | ✅ | ✅ | ??（經德里納） | ❌ | ❌ |
| **DoR產生** | ✅ | ✅ | ??(FORMS-2475新增) | ❌ | ❌ |
| **佈景主題** | ✅ | ✅ | ℹ️ （專案層級） | ℹ️ （專案層級） | 自訂實施 |
| **自訂元件** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OOTB和自訂函式** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **片段參考** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **簽署整合** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **RTL支援** | ❌ | ✅ | ?? | ?? | 自訂實施 |
| **實驗** | ❌ | ❌ | ✅ | ✅ | 自訂實施 |
| 透過Workfront進行&#x200B;**工作管理** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Personalization擴充功能** | ❌ | ❌ | ?? | ❌ | 自訂實施 |
| **編輯器自訂** | ❌ | ❌ | ✅ （透過UI擴充功能） | ❌ | 自訂實施 |
| **提交動作** | ✅ | ✅ | ✅ | 僅限試算表 | 自訂實施 |


## 相關文章

* [使用 Microsoft Excel 或 Google Sheets 的文件型編寫](/help/edge/docs/forms/create-forms.md)
* [通用編輯器或 WYSIWYG 編寫](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [建立最適化表單 (基礎元件)](/help/forms/creating-adaptive-form.md)
* [建立最適化表單 (核心元件)](/help/forms/create-an-adaptive-form.md)
