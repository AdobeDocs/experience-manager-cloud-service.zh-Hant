---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 75a011ed952e1801f0988942d4501a52d348bb3f
workflow-type: tm+mt
source-wordcount: '1759'
ht-degree: 44%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>從這裡，您可以導覽至先前版本的發行說明，例如 2023 或 2024。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2025.1.0)的發行日期是2025年1月30日。 下一個功能版本(2025.2.0)計畫於2025年2月27日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**評論內容片段編輯器現已普遍可用**

在編寫AEM內容片段時，透過在AEM內容片段編輯器中使用新的現代化註解服務來輕鬆與同事共同作業。
[閱讀更多](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment)。

**內容片段編輯器和管理員使用者介面，更新AEM as a Cloud Service版本支援**

新內容片段管理員和編輯器使用者介面支援的最低AEM as a Cloud Service版本現在是2023.8.13099。不再支援新使用者介面正式發行前較舊的版本

### 早期採用者方案 {#sites-early-adopter}

**增強的內容片段**

使用不重複ID型參考資料增強[內容片段參考](/help/headless/graphql-api/uuid-reference-upgrade.md)，確保即使移動資產或片段，也能保持有效的穩定連結，不需要更新或重新發佈。 目前限制：唯一 ID 尚未支援頁面參考。如果內容片段中已參考頁面，則不應使用此功能。

**用於內容片段傳送的 AEM REST OpenAPI**

內容片段傳送](/help/headless/aem-rest-openapi-content-fragment-delivery.md)的[AEM REST OpenAPI現在可用於AEM as a Cloud Service。

### 過時的功能 {#sites-deprecated}

#### SPA編輯器 {#spa-editor}

[自2025.1.0版開始的新專案已棄用SPA編輯器](/help/implementing/developing/hybrid/introduction.md)。SPA編輯器仍支援現有專案，但不應用於新專案。

在AEM中管理Headless內容的首選編輯器現在是：

* [用於視覺化編輯的通用編輯器](/help/edge/wysiwyg-authoring/authoring.md)。
* [用於表單式編輯的內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)。

#### PWA功能 {#pwa-features}

[自2025.1.0版開始的新專案現已棄用AEM Sites的漸進式網頁應用程式(PWA)功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md)。此功能仍受現有專案支援，但不應用於新專案

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets中的新功能 {#new-features-assets}

**Dynamic Media範本**

透過簡單易用的WYSIWYG Dynamic Media範本編輯器，將URL內嵌於任何第一方或第三方應用程式，即時個人化影像和文字橫幅，透過即時橫幅內容更新提供高度吸引人的體驗。

![動態轉譯](/help/assets/assets/dm-templates-smart-text-resize.png)

**Dynamic Media傳遞報告**

獲得透過Dynamic Media傳送之資產的傳送深入分析，包括資產層級傳送計數、反向連結詳細資料、AEM Assets中的資產路徑及不重複資產ID。 為AEM Assets存放庫或特定資料夾階層中的所有資產產生報表。 這些見解可讓您評估已傳遞資產的ROI、評估管道績效，並為資產管理做出明智的決策。

![動態轉譯](/help/assets/assets/referrer.png)

**Dynamic Media多重音訊和標題**

[在Dynamic Media中支援視訊的多重註解與多重音軌功能](/help/assets/dynamic-media/video.md#about-msma) — 您現在可以輕鬆將多重註解與多重音軌新增至主要視訊。 此功能表示您的視訊可供全球對象存取。 您可以以多種語言向全球客群自訂單一已發佈的主要影片，並遵守不同地理區域的輔助功能指南。此外，作者還可以在使用者介面的單一標籤管理字幕和音軌。

**透過HTTP支援的動態自我調整資料流**

為 Dynamic Media 影片傳遞 (啟用 CMAF) 中的自適應串流推出新的通訊協定支援 (DASH - 基於 HTTP 的動態自適應串流)：

* 最適化串流(DASH/HLS)可確保視訊獲得更佳的使用者觀看體驗。

* DASH 是自適應影片串流的國際標準通訊協定，在業界被廣泛採用

**資產關係**

Assets檢視現在支援在簡化的資產詳細資訊面板中檢視和編輯資產關係。 輕鬆將Source和衍生工具等關係新增至內容，讓使用者可以更有效地尋找相關主圖內容。

**重新處理資產**

Assets檢視現在支援重新處理檔案夾中可用的資產。 您可以選擇使用&#x200B;**完整程式**&#x200B;選項，或使用進階選項，例如，預設預覽轉譯、中繼資料、後處理工作流程和處理設定檔。

### AEM Assets中的搶先使用功能 {#early-access-features-assets}

**以 AI 產生的影片字幕**

Adobe Dynamic Media 中以 AI 產生的影片字幕，是使用人工智慧來自動產生影片內容的字幕。此功能旨在透過提供準確的即時字幕來改善可存取性並增強使用者體驗。註解產生自原始音訊、任何其他音軌或視訊屬性頁面上「註解和音訊」標籤中提供的額外註解。 支援60多種語言，您可以在發佈視訊前檢閱和預覽字幕。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的新功能 {#forms-new-features}

* **管理發布**：您可以使用「管理發布」工作流程來發佈或取消發佈跨環境的表單，通常從作者執行個體到發佈和預覽執行個體。 它可讓使用者以簡化的方式發佈、取消發佈或排程內容發佈。

* **[自動儲存基於核心元件的最適化表單草稿](/help/forms/save-core-component-based-form-as-draft.md)**：使用者現在可以享受自動儲存的好處，此功能會將部分完成的表單自動儲存為草稿。使用者可以稍後再使用同一部裝置或其他裝置完成填寫。此功能可改善組織的轉換率，因為使用者不需要從頭開始填寫表單，因此能減少放棄表單的情況。

* **[規則編輯器增強功能](/help/forms/invoke-service-enhancements-rule-editor.md)**：針對以核心元件為基礎的最適化Forms，您可以使用Invoke Service的輸出來填入下拉式選項，並設定可重複或個別面板。 此外，此輸出可用於驗證其他欄位。

* **[使用面板版面的導覽按鈕增強使用者體驗](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：您現在可以在面板版面新增導覽按鈕，例如水平標籤、垂直標籤、摺疊式面板或精靈。這些按鈕簡化轉換不同面板的操作，專注於所選取的面板，藉此增強使用者體驗。


### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### 在最適化Forms中[HTML電子郵件範本](/help/forms/html-email-templates-in-adaptive-forms.md)

最適化Forms可讓您使用HTML電子郵件範本。 HTML電子郵件範本可讓您在提交表單時，傳送豐富、個人化且吸引目光的電子郵件。 這些電子郵件可使用表單資料自訂，並使用各種電子郵件標籤（例如影像和連結）進行強化。 透過Adaptive Forms，您可以上傳包含HTML範本的檔案，或使用純文字編輯器來建立這些範本。

![HTML電子郵件範本](/help/forms/assets/html-email.png)

#### 增強型雲端儲存空間支援：直接PDF上傳至Azure Blob儲存空間

AEM Forms Document Generation API現在支援直接將產生的PDF檔案上傳到Azure Blob儲存體。 此增強功能可簡化儲存和擷取，提高效率並與雲端工作流程整合。

* **[檔案附件的 Base64 編碼字串支援](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：以核心元件為基礎之最適化表單中的檔案附件元件，現在包含一個將附件作為 Base64 編碼字串提交的選項。

>[!IMPORTANT]
>
> 有興趣加入任何 Forms 創新的搶先體驗計劃？從您的官方地址發送電子郵件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，並附上您感興趣的功能清單。## CIF 附加元件 {#cloud-services-cif}

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Java 21支援 {#java21}

您現在可以使用Java 21建置程式碼，其中包括新功能（例如切換陳述式的模式比對、密封類別）和效能改善；Java 17建置也是最新支援。 如需設定步驟，包括更新您的Maven專案和程式庫版本，請參閱[組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)文章。

偵測到Java 17或21組建時，會自動部署效能較高的Java 21 **執行階段**。 不過，我們也建議選擇使用Java 11建置環境的Java 21執行階段，方法是傳送電子郵件至[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。 瞭解[Java 21執行階段需求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **執行階段**&#x200B;將逐步部署到&#x200B;**所有**&#x200B;環境（除了已使用Java 17或21建置的環境，這些環境已具有Java 21執行階段），從2月的沙箱和dev/RDE開始，然後在4月的階段/生產環境。

### 沙箱程式支援設定管道 {#sandbox-config-pipelines}

沙箱程式現在支援設定管道，可以在Cloud Manager中設定這些管道，以部署儲存在git中的yaml檔案。

[深入瞭解](/help/operations/config-pipeline.md)設定管道，其可設定CDN、記錄轉送及版本清除/稽核記錄清除維護任務。

### 基於 OpenAPI 的 API - 早期採用者方案 {#open-apis-earlyadopter}

開發人員可以將 AEM as Cloud Service 功能深度整合到自己的應用程式和工具中。新的AEM as a Cloud Service API遵循OpenAPI規格，目標是保持一致、詳細記錄且方便使用。 需要驗證的端點的憑證會透過建立Adobe Developer Console專案產生。

了解更多有關 [基於 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md) 的資訊，並試用一堂說明設定和使用方法的[端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)。

具體來說，以下列出的 API 端點可做為早期採用者方案的一部分。如果有興趣，請寄電子郵件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，並說明您預計如何使用它們。

* [Sites 內容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites 和資產資料夾 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### 邊緣運算 - 請求意見回饋！ {#edge-computing-feedback}

邊緣運算可讓資料處理更接近瀏覽器，其優點包括減少延遲。如果您覺得此技術對AEM Publish交付和Edge Delivery Services專案很有用，Adobe很樂意聽到。 此外，讓我們知道您將其用作產品藍圖輸入內容的設想。 請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並附上您的疑問和註解！

### 全新 AEM Developer Console (公共 Beta 版) {#aem-developer-console-beta}

試用經改善的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，可為雲端環境內的偵錯程式碼提供更具互動式體驗。

任何人都可以在有效的 AEM Developer Console 中，按一下「*全新適用的控制台*」按鈕以存取公共 Beta 版。Adobe 樂於接受意見回饋，因此您可以寄送電子郵件至 [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

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
