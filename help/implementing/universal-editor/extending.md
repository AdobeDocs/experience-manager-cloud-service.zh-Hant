---
title: 擴充通用編輯器
description: 了解擴充通用編輯器功能的不同選項以便支援內容作者的需求。
feature: Developing
role: Admin, Architect, Developer
exl-id: 2f487fa5-57a7-477a-ad68-590e6cc12f4e
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: ht
source-wordcount: '581'
ht-degree: 100%

---

# 擴充通用編輯器 {#extending}

了解擴充通用編輯器功能的不同選項，以便支援內容作者的需求。

>[!TIP]
>
>通用編輯器也提供多種[自訂選項，](/help/implementing/universal-editor/customizing.md)使您更能符合專案需求。

## 擴充功能 {#extensions}

通用編輯器做為 Adobe Experience Cloud 的一項服務，可以透過 App Builder 和 Experience Manager 擴充其使用者介面。Adobe 透過 [Extension Manager](https://experience.adobe.com/aem/extension-manager) 提供許多現成的擴充功能，方便您在專案中使用。

* **[AEM 多網站管理器 (MSM) 擴充功能](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)**：在元件層級中斷或恢復繼承關係
* **[AEM 頁面屬性擴充功能](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)**：在通用編輯器中存取頁面的頁面屬性視窗
* **[AEM 網站管理員擴充功能](/help/sites-cloud/authoring/universal-editor/authoring.md#sites-console)**：在通用編輯器中頁面的位置開啟 Sites 控制台
* **[AEM 頁面鎖定擴充功能](/help/sites-cloud/authoring/universal-editor/authoring.md#locking-pages)**：從通用編輯器檢視和變更頁面鎖定狀態
* **[AEM 工作流程擴充功能](/help/sites-cloud/authoring/universal-editor/authoring.md#workflows)**：從通用編輯器啟動頁面和頁面內容的工作流程
* **[AEM 通用編輯器開發人員登入擴充功能](/help/sites-cloud/authoring/universal-editor/authoring.md#developer-login)**：執行本機開發時輕鬆完成本機 AEM SDK 的驗證
* **[產生變化版本](/help/generative-ai/generate-variations-integrated-editor.md)**：使用生成式 AI 直接在屬性面板中建立內容的變化版本。
* **[通用編輯器的 AEM 產品選取器](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**：從編輯器中選取或移除產品資料，以便整合 Adobe Commerce 資料。
* **[通用編輯器內容草稿](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**：建立、編輯和管理多個內容草稿。
* **[可設定的資產選取器](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**：可以從所編輯頁面使用的存放庫以外的存放庫來選取資產。
* **表單規則編輯器**：以視覺化的方式新增 AEM Forms 欄位的動態行為，不需要編寫程式碼。
* **[將內容片段匯出至 Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**：將在 Adobe Experience Manager as a Cloud Service 中建立的內容片段匯出至 Adobe Target，做為 Target 活動中的產品建議，以便大規模針對體驗進行測試及個人化。
* **[內容片段工作流程](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**：針對選取的內容片段啟動 AEM 工作流程。

如需如何啟用這些擴充功能的相關資訊，[請參閱 Extension Manager 文件。](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## 擴充使用者介面 {#extending-ui}

通用編輯器的使用者介面擴充功能是使用 Adobe App Builder 建置的 JavaScript 應用程式。您也可以使用這些相同的工具，在標題選單和屬性面板上自行新增按鈕和動作，以及建立自己的通用編輯器事件。

若您想了解自行建立擴充功能的可能性，請參閱以下資源：

1. [使用者介面擴充性](https://developer.adobe.com/uix/docs/) - 這是使用者介面擴充功能的開發人員文件。
1. [使用者介面擴充性指南](https://developer.adobe.com/uix/docs/guides/) - 關於如何自行開發擴充功能的逐步說明
1. [通用編輯器使用者介面擴充點](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - 通用編輯器特定的擴充點文件

>[!TIP]
>
>若您偏好透過範例了解，請參閱 [AEM 使用者介面擴充性教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview)。雖然其內容主要聚焦於擴充內容片段控制台，但在通用編輯器中實施使用者介面擴充功能是相同的概念。

[使用 AEM Sites 中的 Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)，您可以針對每個實例啟用或停用擴充功能、存取 Adobe 的第一方擴充功能 (包括通用編輯器的擴充功能) 等等。

## 擴充點 {#extension-points}

除了使用者介面擴充性以外，通用編輯器還提供許多其他可靈活使用的擴充點，能夠與自訂業務需求緊密整合。

* **[區塊](https://www.aem.live/developer/block-collection)**：採用簡單的 JSON 格式，專案可以調整供建立內容使用的區塊和 UE 功能。
* **[自訂使用者介面](#extending-ui)**：擴充功能可以在側邊面板或模態視窗對話框中顯示所需的使用者介面。
* **[事件](/help/implementing/universal-editor/events.md)**：擴充功能在頁面上接收關於作者動作和選取項目的事件，以便做出適當回應。
