---
title: 如何在 AEM 中編寫表單？
description: 了解 Adobe Experience Manager (AEM) 中提供的各種表單編寫平台，以及如何根據您的要求選擇適合的平台。
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
exl-id: bd9cb623-c272-4cdf-ad39-f97043f781a6
hide: true
hidefromToC: true
source-git-commit: 1662d1c9458f05c2e511514ce8a04247da90eaf3
workflow-type: ht
source-wordcount: '1075'
ht-degree: 100%

---

# 如何在 Adobe Experience Manager (AEM) 中編寫表單？

Adobe Experience Manager (AEM) 提供一個彈性的平台，用於建立能夠吸引人的動態回應式自適應表單。此平台提供直覺易用的使用者介面以及多種立即可用的元件，可用於建立和管理自適應表單。編寫表單時，可以根據您的要求使用或不使用表單模型或結構描述。

## 選擇編寫平台時的重要考量

AEM 提供多種表單編寫選項，可用來建立具吸引力的互動式表單。在選取表單編寫環境時，請考慮以下因素：

| 📝 **考量事項** | 💡 **要提出的問題** |
|----------------------|--------------------|
| **使用者專業知識** | 誰負責編寫表單，是開發人員、業務使用者或是內容作者？ |
| **表單複雜性** | 表單是否需要進階規則、動態區段或整合？ |
| **可重複使用之需求** | 是否會在不同的表單或專案中重複使用表單的某些部分？ |
| **設計靈活性** | 您是否需要完全掌控版面、主題和樣式？ |
| **整合要求** | 表單是否需要連接到資料模型、工作流程或外部系統？ |
| **使用便利性** | 就您團隊的技術技能程度而言，平台是否簡單易用？ |
| **效能與擴充性** | 表單是否會大規模使用，或在高流量環境中使用？ |
| **全管道傳遞** | 是否會在網站、行動應用程式、資訊站或多個管道上使用表單？ |
| **發佈靈活性** | 表單會在 AEM、Edge Delivery 或自訂應用程式中的哪些位置發佈？ |

## AEM 中表單編寫方法概觀

AEM 支援多種編寫方法，分別適合不同的使用者需求、技術技能程度和發佈目的地。

* [Foundation 元件](/help/forms/create-adaptive-form-tutorial.md)：使用 Foundation 元件建置傳統的互動式表單。最適合整合舊版系統或依賴沿用已久之工作流程的表單。使用 Foundation 元件編寫的表單只能在 AEM 上發佈，且與 Edge Delivery Services 不相容。

* [核心元件](/help/forms/creating-adaptive-form-core-components.md)：使用核心元件建立現代化的可擴充回應式表單。這些元件可以重覆使用、方便存取而且效能更好。使用核心元件編寫的表單可以在 AEM 和 Edge Delivery Services 上發佈，可以橫跨不同平台靈活使用。

* [Edge Delivery Services 表單](/help/edge/docs/forms/overview.md)：Edge Delivery Services 表單改變編寫、執行和處理表單的方式。各組織可以利用 Edge Delivery Services 來建立快速、安全且高度可用的數位表單，並透過快速開發環境增強使用者體驗和操作效率。您可以使用兩種方式編寫 Edge Delivery Services 表單：
   * [WYSIWYG 編寫](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：使用通用編輯器透過視覺化的拖放方式建立表單，非常適合技術知識有限的內容作者。使用通用編輯器編寫的表單透過 Edge Delivery Services 傳遞，可在快速且耗費少量資源的情況下轉譯。
   * [文件型編寫](/help/edge/docs/forms/tutorial.md)：使用 Microsoft Excel 或 Google Sheets 等工具定義表單結構和內容。此方法對於偏好使用試算表控制輸入的商業使用者而言很實用。這些表單通常透過 Edge Delivery Services 發佈，適用於消耗少量資源但數量龐大的使用案例。
* [Headless 編寫](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)：使用 API 將表單轉譯為適用於任何前端 (例如 React、Angular、行動應用程式或資訊站) 的 JSON，而無需依賴 AEM。目前，只有核心元件支援 Headless 傳遞。Headless 表單非常適合全管道使用案例，且其使用不受 AEM 頁面轉譯之影響，可供自訂前端部署靈活使用。

### AEM 表單編寫方法的比較分析

下表用精簡的方式比較各種 AEM 表單編寫方法，並強調其中的方法、功能、發佈選項和理想使用案例，協助您選擇最符合需求的方式。

| **考量事項** | **Foundation 元件** | **核心元件** | **通用編輯器 (WYSIWYG)** | **文件型編寫** | **Headless 編寫** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **最適合** | 維護 AEM 內的舊版表單和工作流程 | 具有複雜工作流程和整合項目的現代化可擴充表單 | 為具有複雜需求的 Edge Delivery Service 網站建立表單 | 在沒有進階提交服務的情況下，快速製作原型或基本表單 | 跨平台 (網頁、行動裝置、資訊站等) 的全管道體驗 |
| **使用者專業知識** | 開發人員、內容作者 | 開發人員、進階作者 | 商業使用者、內容作者 | 商業使用者 | 開發人員 |
| **表單複雜性** | 基本表單 | 具有動態區段的複雜表單 | 具有自訂動作的複雜表單 | 簡易表單 | 高度複雜並由 API 控制的表單 |
| **設計靈活性** | 有限 | 高 (CSS/JS 自訂) | 中等 (以範本為基礎) | 有限 | 高 (前端框架控制) |
| **整合能力** | 基本 AEM 工作流程 | 進階 (資料模型、工作流程) | 與外部系統整合 | 基本 (Google Sheets、Excel) | 透過 API 完整控制 |
| **發佈方法** | 僅限 AEM | AEM 和 Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | 透過 API 發佈至任何前端 |
| **效能與 SEO** | 標準 | 相較於 Foundation 元件有所改善 | Google Lighthouse 分數高，可更快完成轉譯和產生更好的 SEO | Google Lighthouse 分數高，可更快完成轉譯和產生更好的 SEO | 視實施情況而定 |
| **全管道傳遞** | 有限 | 中等 | 中等 | 有限 | 高 |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### AEM 表單編寫方法的功能比較

下表詳細比較不同 AEM 表單編寫方法的重要功能，協助您選擇最符合需求的方式。&#x200B;

| **功能** | **Foundation 元件** | **核心元件** | **通用編輯器 (WYSIWYG)** | **文件型編寫** | **Headless 編寫** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **使用 Sites 統一結構** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **嵌入表單支援** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **規則 (動態行為)** | 具有自訂功能的進階規則編輯器 | 具有自訂功能的進階規則編輯器 | 具有自訂功能的進階規則編輯器 | 受限：顯示/隱藏、運算值、自訂函數 | 受限：必須自訂實施 |
| **附件支援** | ✅ | ✅ | ✅ | ℹ️ (搶先體驗) | ❌ |
| **驗證碼支援** | reCAPTCHA v2/Enterprise、hCaptcha (EA)、Turnstile (EA) | reCAPTCHA v2/Enterprise、hCaptcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | 必須自訂整合 |
| **提交功能** | REST 端點、電子郵件、表單資料模型 (FDM)、叫用 AEM 工作流程、SharePoint、OneDrive、Azure Blob 儲存體、Power Automate、Workfront Fusion (EA) | REST 端點、電子郵件、表單資料模型 (FDM)、叫用 AEM 工作流程、SharePoint、OneDrive、Azure Blob 儲存體、Power Automate、Workfront Fusion (EA) | REST 端點、電子郵件、表單資料模型 (FDM)、叫用 AEM 工作流程、SharePoint、OneDrive、Azure Blob 儲存體、Power Automate、Workfront Fusion (EA) | 僅限試算表 | 自訂 API 端點 |
| **資料結構描述** | FDM、自訂 | FDM、自訂 | FDM、自訂 | 自訂 | 自訂 |
| **預填** | ✅ | ✅ | 💡 (透過精靈) | ✅ | 自訂實施 |
| **片段** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **視覺化規則編輯器** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **本地化** | ✅ | ✅ | 💡 (透過 Sites) | ℹ️ (Excel - 手動、Google Sheet 函數) | 自訂實施 |
| **資料結構描述 (資料樹)** | ✅ | ✅ | 💡 (透過使用者介面擴充功能) | ❌ | 自訂實施 |
| **範本支援** | ✅ | ✅ | 僅限初始內容，無原則 | ❌ | 自訂實施 |
| **入口網站** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **記錄文件製作** | ✅ | ✅ | 💡 (透過 Derlina) | ❌ | ❌ |
| **記錄文件產生** | ✅ | ✅ | 💡 (FORMS-2475 新增) | ❌ | ❌ |
| **主題** | ✅ | ✅ | ℹ️ (在專案層級) | ℹ️ (在專案層級) | 自訂實施 |
| **自訂元件** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OOTB 與自訂函數** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **片段參考** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **簽署整合** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **RTL 支援** | ❌ | ✅ | 💡 | 💡 | 自訂實施 |
| **實驗** | ❌ | ❌ | ✅ | ✅ | 自訂實施 |
| **透過 Workfront 管理任務** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **個人化擴充功能** | ❌ | ❌ | 💡 | ❌ | 自訂實施 |
| **編輯器自訂** | ❌ | ❌ | ✅ (透過使用者介面擴充功能) | ❌ | 自訂實施 |
| **提交動作** | ✅ | ✅ | ✅ | 僅限試算表 | 自訂實施 |


## 相關文章

* [使用 Microsoft Excel 或 Google Sheets 的文件型編寫](/help/edge/docs/forms/create-forms.md)
* [通用編輯器或 WYSIWYG 編寫](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [建立最適化表單 (基礎元件)](/help/forms/creating-adaptive-form.md)
* [建立自適應表單 (核心元件)](/help/forms/create-an-adaptive-form.md)
