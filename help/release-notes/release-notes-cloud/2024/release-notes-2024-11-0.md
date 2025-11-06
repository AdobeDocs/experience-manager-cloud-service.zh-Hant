---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.11.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.11.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: 3fd6482e-66f0-48ee-983c-4cb6b7742dcd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 97%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.11.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2024.11.0 版的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2022 或 2023。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本 (2024.11.0) 的發行日期是 2024 年 11 月 21 日。下一個功能版本(2025.1.0)計畫於2025年1月30日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2024 年 11 月發行概觀影片，了解 2024.11.0 版本的新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3440931?captions=chi_hant&quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**[!DNL Edge Delivery Services]頁面範本搭配通用編輯器製作**

快速將任何 Edge Delivery 頁面轉變為頁面範本。這可讓您使用預先定義的結構和內容開始使用新頁面，而非從空白的頁面開始。[閱讀更多](/help/sites-cloud/authoring/universal-editor/templates.md)。

**[!DNL Edge Delivery Services]CSV 匯入器透過 AEM 執行個體進行發佈**

在您喜愛的試算表工具中有效管理您的 Edge Delivery 試算表資料 (例如重新導向)，並透過新的 CSV 匯入器將其上傳至 AEM。[閱讀更多](https://www.aem.live/docs/authoring-tabular-data)。

### AEM Sites 中的預發行功能

使用不重複ID型參考資料增強[內容片段參考](/help/headless/graphql-api/uuid-reference-upgrade.md)，確保即使移動資產或片段，也能保持有效的穩定連結，不需要更新或重新發佈。 目前限制：唯一 ID 尚未支援頁面參考。如果內容片段中已參考頁面，則不應使用此功能。

### 早期採用者方案 {#sites-early-adopter}

**用於內容片段傳送的 AEM REST OpenAPI**

[用於內容片段傳送的 AEM REST OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) 現在已可用於 AEM as a Cloud Service。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 的搶先體驗功能 {#dm-early-access}

**AI 生成影片字幕**

Adobe Dynamic Media 中的 AI 生成影片字幕功能會使用人工智慧，為影片內容自動生成字幕。透過提供準確的即時字幕，這項功能可改善可存取性並增強使用者體驗。AI 分析影片的音軌以轉錄語音並建立針對準確性或自訂可進行編輯的字幕。這些字幕有助於滿足可存取性的要求，並改善依賴或偏好文字式影片支援之客群的影片參與度。

若要在您的 Dynamic Media 帳戶搶先體驗 AI 產生的字幕支援，請[建立並提交 Adobe 客戶支援案例](/help/assets/dynamic-media/video.md##enable-dash)。

**Dynamic Media 傳遞報告**

取得透過 Dynamic Media 傳遞之資產的傳遞深入分析，以及資產層級傳遞計數、反向連結資訊、AEM Assets 中的資產路徑和唯一資產 ID。可以針對 AEM Assets 存放庫或 AEM Assets 中特定的資料夾階層，為透過 Dynamic Media 傳遞的所有資產產生報告。深入分析有助於測量所傳遞資產的 ROI、測量管道效能，且有助於為資產執行明智的資產管理任務。

若要在您的 Dynamic Media 帳戶搶先體驗 Dynamic Media 傳遞報告，請[建立並提交 Adobe 客戶支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。

### Assets 檢視的新功能 {#assets-view-new-features}

**Dynamic Media 面板**

Assets 檢視現在能夠讓您從個別面板存取 Dynamic Media 和具有 OpenAPI 功能的 Dynamic Media 轉譯。您可以根據資產和轉譯類型選擇複製傳遞 URL 或下載轉譯。如需更多資訊，請參閱 [Dynamic Media 轉譯](/help/assets/renditions.md#dynamic-media-renditions)和[具有 OpenAPI 功能的 Dynamic Media 轉譯](/help/assets/renditions.md#dm-with-openapi-renditions)。

![動態轉譯](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的新功能 {#forms-new-features}

* **[輕鬆更新 Adobe Sign 範圍](/help/forms/adobe-sign-integration-adaptive-forms.md)**：您可以直接從 AEM Cloud 設定頁面修改 Adobe Sign 設定的範圍，讓您更新現有設定更快速、更輕鬆。

* **[最適化表單的非同步函數支援](/help/forms/using-async-funct-in-rule-editor.md)**：當最適化表單需要非同步操作 (例如等待外部流程或資料擷取) 時，您可以使用自訂函數來執行這些操作並在規則編輯器中進行設定。

### AEM Forms 的預發行功能 {#forms-new-prerelease-features}

* **管理發佈**：您可以使用管理發佈工作流程跨環境發佈或取消發佈表單，通常是從作者實例到發佈和預覽實例。它可讓使用者以簡化的方式發佈、取消發佈或排程內容發佈。

* **[自動儲存基於核心元件的最適化表單草稿](/help/forms/save-core-component-based-form-as-draft.md)**：使用者現在可以享受自動儲存的好處，此功能會將部分完成的表單自動儲存為草稿。使用者可以稍後再使用同一部裝置或其他裝置完成填寫。此功能可改善組織的轉換率，因為使用者不需要從頭開始填寫表單，因此能減少放棄表單的情況。

* **[規則編輯器增強功能](/help/forms/invoke-service-enhancements-rule-editor.md)**：對於以核心元件為基礎的最適化表單，您現在可以使用調用服務的輸出填入下拉式選項、使用調用服務的輸出來設定可重複面板、使用調用服務的輸出來設定個別面板，以及使用調用服務的輸出參數來驗證其他欄位。

* **[使用面板版面的導覽按鈕增強使用者體驗](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：您現在可以在面板版面新增導覽按鈕，例如水平標籤、垂直標籤、摺疊式面板或精靈。這些按鈕簡化轉換不同面板的操作，專注於所選取的面板，藉此增強使用者體驗。


### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### 整合

* **[將最適化表單與 Adobe Marketo Engage 整合](/help/forms/integrate-form-to-marketo-engage.md)**：AEM Forms as a Cloud Service 現在包含一個易於使用的選項，可將最適化表單與 Adobe Marketo Engage 連結。此整合可讓您直接使用 Marketo Engage 的商機捕獲和相關自訂物件來建立最適化表單。您現在可以使用 Marketo Engage 中的資料預先填入表單欄位，並將資料提交回自動化工作流程，例如智慧行銷活動和電子郵件自動化。您還可以將最適化表單與 Munchkin 程式庫連結，以追蹤造訪次數、點按次數和表單提交次數。

#### 最適化表單和 HTML5 表單

* **[根據現有的 XFA 範本建立最適化表單](/help/forms/create-adaptive-form-using-xfa-templates.md)**：您現在可以使用 XFA 表單範本 (*.XDP 檔案) 建立以核心元件為基礎的最適化表單。此功能有助於已投資於 XFA 技術的 AEM Forms 內部部署客戶採用 AEM Forms as a Cloud Service。

* **HTML5 表單 (XFA 型網頁表單)**：現在，使用 XFA 技術的 AEM Forms 內部部署客戶可以輕鬆轉變到 AEM Forms as a Cloud Service，同時保留其現有的 HTML5 (XFA 型網頁表單) 表單使用者體驗。此功能可讓 XFA 表單範本以 HTML5 格式呈現，進而使表單可以在不支援 XFA 型 PDF 表單的裝置上存取。

  ![HTML 表單 (XFA 型網頁表單)](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[檔案附件的 Base64 編碼字串支援](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：以核心元件為基礎之最適化表單中的檔案附件元件，現在包含一個將附件作為 Base64 編碼字串提交的選項。

#### 互動式通訊和通訊 API

* **互動式通訊編輯器**：互動式通訊編輯器是一種簡單易用的圖形通訊設計工具，可簡化個人化、資料驅動通訊的建立，且可在任何現代瀏覽器中執行。它支援無縫的資料整合、複雜的邏輯定義和豐富媒體整合，從而確保產生專業且合規的文件、通訊和範本，以滿足各種業務需求。

  ![互動式通訊編輯器](/help/forms/assets/ic-editor.png)


* **[PDF/A 合規性增強功能](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**：您現在可以使用通訊 API 將 PDF 文件轉換為 PDF/A 格式 (1a、2a、3a)，以用於存檔目的，同時確保可存取性和驗證是否符合這些標準。


* **[簽章 API (文件保證)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**：通訊 API 中的新 RESTful API 能夠輕鬆管理 PDF 簽章。它支援以下操作：
   * 清除簽名：將簽名從指定欄位中移除。
   * 移除簽名欄位：刪除指定的簽名欄位。

<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## 自動化表單轉換服務

* **[將 PDF 表單轉換為以核心元件為基礎的最適化表單](https://experienceleague.adobe.com/zh-hant/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**：您現在可以使用自動化表單轉換服務，將 PDF 表單、AcroForms 或 XFA 型表單轉換為以核心元件為基礎的最適化表單。

>[!IMPORTANT]
>
> 有興趣加入任何 Forms 創新的搶先體驗計劃？從您的官方地址發送電子郵件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，並附上您感興趣的功能清單。## CIF 附加元件 {#cloud-services-cif}

## CIF 附加元件 {#cif}

### 錯誤修正 {#bug-fixes-cif}

* 修正使用者介面測試，以便與核心 CIF 元件正常搭配運作。
* 解決類別 URL 格式在雲端執行個體中未如預期運作的問題。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 改善的樹狀複寫效能 (並停用發佈內容樹狀工作流程) {#tree-replication-performance}

[啟用樹狀工作流程步驟](/help/operations/replication.md#tree-activation)是建議用於複製深層內容階層的新工作流程模型步驟。值得注意的是，它可讓獨立複製 (例如透過快速發佈或管理發佈) 能夠與正在進行的樹狀複寫工作流程並行。當您需要在大量複寫仍在進行時發佈一些有時效性的內容，此功能特別實用。樹狀複寫步驟取代了發佈內容樹狀工作流程及其相關的工作流程步驟 (現已停用)。

### 基於 OpenAPI 的 API - 早期採用者方案 {#open-apis-earlyadopter}

開發人員可以將 AEM as Cloud Service 功能深度整合到自己的應用程式和工具中。新的 AEM as a Cloud Service API 將遵循 OpenAPI 規範，目標是一致、完整記錄且簡單易用。需要驗證之端點的憑證將透過建立 Adobe Developer Console 專案來產生。

了解更多有關 [基於 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md) 的資訊，並試用一堂說明設定和使用方法的[端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)。

具體來說，以下列出的 API 端點可做為早期採用者方案的一部分。如果有興趣，請寄電子郵件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，並說明您預計如何使用它們。

* [Sites 內容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* Sites與Assets資料夾API
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### 邊緣運算 - 請求意見回饋！ {#edge-computing-feedback}

邊緣運算可讓資料處理更接近瀏覽器，其優點包括減少延遲。做為對路徑圖的輸入，我們很希望知道您是否認為此技術對 AEM Publish Delivery 和 Edge Delivery Services 專案很實用，以及您設想的用途。請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並附上您的疑問和註解！

### 全新 AEM Developer Console (公共 Beta 版) {#aem-developer-console-beta}

試用經改善的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，可為雲端環境內的偵錯程式碼提供更具互動式體驗。

任何人都可以在有效的 AEM Developer Console 中，按一下「*全新適用的控制台*」按鈕以存取公共 Beta 版。Adobe 樂於接受意見回饋，因此您可以寄送電子郵件至 [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] Guides {#guides}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)找到最新版 Adobe Experience Manager Guides 的新功能和增強功能完整清單。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

## 通用編輯器 {#universal-editor}

您可以在[這裡](/help/release-notes/universal-editor/current.md)找到通用編輯器版本的完整清單。

## 產生變化版本 {#generate-variations}

您可以在[這裡](/help/generative-ai/release-notes-generate-variations.md)找到「產生變化版本」版本的完整清單。

## Experience Cloud 發行說明 {#experience-cloud}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/release-notes/experience-cloud/current)查看其他 Experience Cloud 應用程式版本的相關資訊。
