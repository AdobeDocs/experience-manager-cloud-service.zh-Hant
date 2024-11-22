---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 83bc4e09cc7b6c420eee64091fab773ee1dcbd85
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 39%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2022 或 2023。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2024.11.0)的發行日期是2024年11月21日。 下一個功能版本(2024.12.0)計畫於2024年12月12日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- ## Release Video {#release-video}

Have a look at the November 2024 Release Overview video for a summary of the features added in the 2024.11.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

使用通用編輯器編寫的&#x200B;**[!DNL Edge Delivery Services]頁面範本**

快速將任何Edge Delivery頁面轉換為頁面範本。 這可讓您以預先定義的結構和內容啟動新頁面，而不是空白頁面。 [瞭解詳情](/help/sites-cloud/authoring/universal-editor/templates.md)。

**[!DNL Edge Delivery Services]CSV匯入工具，用於透過AEM執行個體發佈**

使用您最愛的試算表工具，有效管理Edge Delivery試算表資料（例如重新導向），並透過新的CSV匯入工具將其上傳至AEM。 [瞭解詳情](/help/edge/wysiwyg-authoring/tabular-data.md#importing)。

### AEM Sites中的發行前功能

使用不重複ID型參考資料增強[內容片段參考](/help/headless/graphql-api/uuid-reference-upgrade.md)，確保即使移動資產或片段時仍可保持有效的穩定連結，無需更新或重新發佈。 目前的限制：不支援使用唯一ID的頁面參考。 如果頁面在內容片段中參照，則不應使用此功能。

### 早期採用者計劃 {#sites-early-adopter}

**用於內容片段傳送的 AEM REST OpenAPI**

[用於內容片段傳送的 AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) 現在已可用於 AEM as a Cloud Service。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media中的搶先使用功能 {#dm-early-access}

**以 AI 產生的影片字幕**

Adobe Dynamic Media 中以 AI 產生的影片字幕，是使用人工智慧來自動產生影片內容的字幕。此功能旨在透過提供準確的即時字幕來改善可存取性並增強使用者體驗。AI 分析影片的音軌以轉錄語音並建立針對準確性或自訂可進行編輯的字幕。這些字幕有助於滿足可存取性的要求，並改善依賴或偏好文字式影片支援之客群的影片參與度。

若要在您的 Dynamic Media 帳戶搶先體驗 AI 產生的字幕支援，請[建立並提交 Adobe 客戶支援案例](/help/assets/dynamic-media/video.md##enable-dash)。

**Dynamic Media傳遞報告**

透過Dynamic Media取得資產傳送的深入分析，包括資產層級傳送計數、反向連結資訊、AEM Assets中的資產路徑及唯一資產ID。 您可以針對AEM Assets存放庫透過Dynamic Media傳送的所有資產，或針對AEM Assets中的特定資料夾階層產生報表。 深入分析有助於評估已交付資產的ROI、評估管道績效，並幫助進行明智的資產管理工作。

若要搶先使用您Dynamic Media帳戶的Dynamic Media傳遞報告，請[建立並提交Adobe客戶支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。

### 資產檢視的新功能 {#assets-view-new-features}

**Dynamic Media面板**

Assets檢視現在可讓您從另一個可供使用的面板，使用OpenAPI轉譯存取Dynamic Media和Dynamic Media。 您可以選擇複製傳送URL，或根據資產和轉譯型別下載轉譯。 如需詳細資訊，請參閱[Dynamic Media轉譯](/help/assets/renditions.md#dynamic-media-renditions)和具有OpenAPI功能的[Dynamic Media](/help/assets/renditions.md#dm-with-openapi-renditions)。

![動態轉譯](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的新功能 {#forms-new-features}

* **[輕鬆更新 Adobe Sign 範圍](/help/forms/adobe-sign-integration-adaptive-forms.md)**：您可以直接從 AEM Cloud 設定頁面修改 Adobe Sign 設定的範圍，讓您更新現有設定更快速、更輕鬆。

* **[最適化表單的非同步函數支援](/help/forms/using-async-funct-in-rule-editor.md)**：當最適化表單需要非同步操作 (例如等待外部流程或資料擷取) 時，您可以使用自訂函數來執行這些操作並在規則編輯器中進行設定。

### AEM Forms中的搶鮮版功能 {#forms-new-prerelease-features}

* **管理發布**：您可以使用管理發布工作流程來發佈或取消發佈跨環境的表單，通常從製作執行個體到發佈和預覽執行個體。 它可讓使用者透過簡化的方式發佈、取消發佈或排程內容發佈。

* **[自動儲存基於核心元件的最適化表單草稿](/help/forms/save-core-component-based-form-as-draft.md)**：使用者現在可以享受自動儲存的好處，此功能會將部分完成的表單自動儲存為草稿。使用者可以稍後再使用同一部裝置或其他裝置完成填寫。此功能可改善組織的轉換率，因為使用者不需要從頭開始填寫表單，因此能減少放棄表單的情況。

* **[規則編輯器增強功能](/help/forms/invoke-service-enhancements-rule-editor.md)**：針對以核心元件為基礎的最適化Forms，您現在可以使用Invoke Service的輸出填入下拉式清單選項、使用Invoke Service的輸出設定可重複的面板、使用Invoke Service的輸出設定個別面板，以及使用Invoke Service的輸出引數來驗證其他欄位。

* **[使用面板版面的導覽按鈕增強使用者體驗](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：您現在可以在面板版面新增導覽按鈕，例如水平標籤、垂直標籤、摺疊式面板或精靈。這些按鈕簡化轉換不同面板的操作，專注於所選取的面板，藉此增強使用者體驗。


### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### 整合

* **[整合最適化Forms與Adobe Marketo Engage](/help/forms/integrate-form-to-marketo-engage.md)**： AEM Formsas a Cloud Service現在包含一個易於使用的選項，以將最適化Forms與Adobe Marketo Engage連線。 此整合可讓您直接使用Marketo Engage的銷售機會擷取及相關自訂物件來建立最適化Forms。 您現在可以使用Marketo Engage中的資料預先填寫表單欄位，並將資料提交回以自動化工作流程，例如智慧行銷活動和電子郵件自動化。 您也可以將最適化表單與Munchkin資料庫連結，以追蹤造訪次數、點按次數和表單提交次數。

#### 最適化Forms和HTML5 Forms

* **[根據現有XFA範本建立最適化Forms](/help/forms/create-adaptive-form-using-xfa-templates.md)**：您現在可以使用XFA表單範本（*.XDP檔案）建立核心元件型最適化Forms。 此功能有助於AEM Forms On-Premise客戶（已投資使用XFA技術）採用AEM Formsas a Cloud Service。

* **HTML5 Forms （以XFA為基礎的網路表單）**：現在，使用XFA技術的AEM Forms內部部署客戶可以輕鬆轉換至AEM Formsas a Cloud Service，同時保留他們現有的使用HTML5 Forms （以XFA為基礎的網路表單）的使用者體驗。 此功能可轉譯HTML5格式的XFA表單範本，使得表單在不支援XFAPDF forms的裝置上可供存取。

  ![HTMLForms （以XFA為基礎的網路表單）](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[檔案附件的Base64編碼字串支援](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：根據核心元件的最適化Forms中的檔案附件元件現在包含將附加檔案提交為Base64編碼字串的選項。

#### 互動式通訊與通訊API

* **互動式通訊編輯器**：互動式通訊編輯器是使用者易用的圖形式通訊設計工具，可簡化個人化、資料導向式通訊的建立，並在任何現代瀏覽器中執行。 它支援順暢的資料整合、複雜的邏輯定義以及多媒體整合，確保專業且合規的檔案、通訊及範本產生能滿足各種業務需求。

  ![互動式通訊編輯器](/help/forms/assets/ic-editor.png)


* **[PDF/A相容性增強功能](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**：您現在可以使用通訊API將PDF檔案轉換為PDF/A格式(1a、2a、3a)以進行封存，同時確保可存取性並驗證是否符合這些標準。


* **[簽章API (檔案Assurance)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**：通訊API中的新RESTful API可讓您輕鬆管理PDF簽章。 它支援的作業如下：
   * 清除簽章：從指定欄位移除簽章。
   * 移除簽名欄位：刪除指定的簽名欄位。


<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## 自動化表單轉換服務

* **[將PDF forms轉換為以核心元件為基礎的最適化Forms](https://experienceleague.adobe.com/en/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**：您現在可以使用Automated forms conversion服務，將PDF forms、AcroForms或XFA型表單轉換為以核心元件為基礎的最適化Forms。


>[!IMPORTANT]
>
> 有興趣加入任何 Forms 創新的搶先體驗計劃？從您的官方地址發送電子郵件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，並附上您感興趣的功能清單。## CIF附加元件{#cloud-services-cif}

## CIF 附加元件 {#cif}

### 錯誤修正 {#bug-fixes-cif}

* 修正使用者介面測試，以便與核心 CIF 元件正常搭配運作。
* 解決類別 URL 格式在雲端執行個體中未如預期運作的問題。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 改善樹狀結構復寫效能(以及淘汰Publish內容樹狀工作流程) {#tree-replication-performance}

[樹狀啟動工作流程步驟](/help/operations/replication.md#tree-activation)是復寫深層內容階層時建議的新工作流程模型步驟。 請注意，它允許獨立複製（例如，透過快速發佈或管理出版物）與進行中的樹狀結構複製工作流程並行進行。 如果您需要在大量復寫仍在進行時發佈一些時效性強的內容，這會特別有用。 樹狀結構復寫步驟會取代Publish內容樹狀工作流程及其相關工作流程步驟，這些步驟現已棄用。

### OpenAPI型API — 早期採用者計畫 {#open-apis-earlyadopter}

開發人員可將AEM作為Cloud Service功能深入整合到他們自己的應用計畫和工具中。 新的AEM as a Cloud Service API將遵循OpenAPI規格，目標是保持一致、詳細記錄且方便使用。 需要驗證的端點的憑證將由建立Adobe Developer Console專案產生。

深入瞭解[以OpenAPI為基礎的AEM API](/help/implementing/developing/open-api-based-apis.md)，並嘗試使用[端對端教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)來說明設定和使用方式。

具體來說，底下列出的API端點屬於率先採用者計畫的一部分。 如有興趣，請傳送電子郵件至[aem-apis@adobe.com](mailto:aem-apis@adobe.com)，說明您打算如何使用這些工具。
* [網站內容片段API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [網站與Assets資料夾API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge運算 — 要求回饋意見！ {#edge-computing-feedback}

Edge運算讓資料處理更靠近瀏覽器，而且可減少延遲等多項優點。 作為藍圖中的輸入內容，我們很樂意聽您覺得此技術對AEM Publish交付和Edge Delivery Services專案是否有用，以及您將其用於何種設想。 傳送電子郵件給[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，其中包含問題與意見！

### 全新 AEM Developer Console (公共 Beta 版) {#aem-developer-console-beta}

試用經改善的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，可為雲端環境內的偵錯程式碼提供更具互動式體驗。

任何人都可以在有效的 AEM Developer Console 中，按一下「*全新適用的控制台*」按鈕以存取公共 Beta 版。Adobe歡迎您提供意見回饋，您可以透過電子郵件寄至[aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] Guides {#guides}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0)找到最新版 Adobe Experience Manager Guides 的新功能和增強功能完整清單。

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
