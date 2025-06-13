---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.1.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.1.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: 085629bf-fb24-4511-af6c-bbbeedcb6b98
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 92%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.1.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2025.1.0 版的功能發行說明。

>[!NOTE]
>
>您可以從這裡瀏覽至先前版本 (例如 2023 或 2024 版) 的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.1.0) 的發行日期為 2025 年 1 月 30 日。下一個功能版本 (2025.2.0) 規劃於 2025 年 3 月 4 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2025 年 1 月發行概觀影片，了解 2025.1.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3456072?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**內容片段編輯器評論功能現已正式推出**

使用 AEM 內容片段編輯器中全新的現代化評論服務，在製作 AEM 內容片段時輕鬆地與同事協同合作。
[閱讀更多](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment)。

**內容片段編輯器和管理員使用者介面，已更新 AEM as a Cloud Service 版本支援**

支援新內容片段管理員與編輯器使用者介面的 AEM as a Cloud Service 最低版本現為 2023.8.13099。不再支援新使用者介面正式推出以前的早期版本

### 早期採用者方案 {#sites-early-adopter}

**增強的內容片段**

增強[以唯一識別碼為參照基礎的內容片段參照](/help/headless/graphql-api/uuid-reference-upgrade.md)，有助於確保即使片段移動到另一個位置，個別內容片段的 GraphQL 查詢仍能保持穩定。您現在可以透過「ByID」查詢來實現此功能。雖然路徑可能會改變，並可能因此破壞「ByPath」查詢，但 UUID 是穩定不變的。在任何查詢或其他適用 API 請求中，新的 ID 也可以作為屬性回傳。目前限制 (2025.1)：唯一識別碼尚未支援頁面參照。如果內容片段中有參照頁面，則不應使用此功能。計劃於下一個 AEM as a Cloud Service 版本中移除此限制。

**用於內容片段傳遞的 AEM REST OpenAPI**

[用於內容片段傳遞的 AEM REST OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) 現已可用於 AEM as a Cloud Service。

### 過時的功能 {#sites-deprecated}

#### SPA 編輯器 {#spa-editor}

自 2025.1.0 版本開始，新專案已汰除 [SPA 編輯器](/help/implementing/developing/hybrid/introduction.md)。現有專案仍支援 SPA 編輯器，但新專案不應使用。

目前，AEM 中用於管理 Headless 內容的首選編輯器為：

* [通用編輯器](/help/edge/wysiwyg-authoring/authoring.md)，用於視覺化編輯。
* [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)，用於表單型編輯。

#### PWA 功能 {#pwa-features}

[從2025.1.0版開始的新專案現已棄用AEM Sites的漸進式網頁應用程式(PWA)功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md)。此功能仍受現有專案支援，但不應用於新專案

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets 中的新功能 {#new-features-assets}

**Dynamic Media 傳遞報告**

取得透過 Dynamic Media 傳遞之資產的傳遞深入分析，包括資產層級傳遞計數、反向連結詳細資訊、AEM Assets 中的資產路徑和唯一資產 ID。為 AEM Assets 存放庫或特定資料夾階層中所有資產產生報告。您可以利用這些深入分析來測量已傳遞資產的 ROI、評估管道效能，並做出明智的資產管理決策。

![動態轉譯](/help/assets/assets/referrer.png)

**Dynamic Media 多語言音訊和字幕**

[Dynamic Media 中的影片支援多語言字幕和多語言音軌](/help/assets/dynamic-media/video.md#about-msma) - 您現在可以輕鬆地為主要影片新增多語言字幕和多語言音軌。擁有此功能代表全球觀眾都可以存取您的影片。您可以著手自訂一部已發佈的主要影片，以多種語言提供給全球觀眾，並遵守不同地理區域的無障礙指南。此外，作者還可以透過使用者介面的單一標籤管理字幕和音軌。

**支援 Dynamic Adaptive Streaming over HTTP**

針對 Dynamic Media 影片傳遞 (啟用 CMAF) 中的自適應串流推出新支援的通訊協定 (DASH - Dynamic Adaptive Streaming over HTTP，即基於 HTTP 的動態自適應串流)：

* 自適應串流 (DASH/HLS) 可確保使用者能擁有更好的影片觀看體驗。

* DASH 是自適應影片串流的國際標準通訊協定，並在業界獲得廣泛使用


**重新處理資產**

資產視圖現在支援重新處理資料夾中的資產。您可以選取&#x200B;**完整處理**&#x200B;選項，也可以使用進階選項，例如預設預覽轉譯、中繼資料、後處理工作流程，以及處理設定檔。

### AEM Assets 的搶先體驗功能 {#early-access-features-assets}

**AI 生成影片字幕**

Adobe Dynamic Media 中的 AI 生成影片字幕功能會使用人工智慧，為影片內容自動生成字幕。透過提供準確的即時字幕，這項功能可改善可存取性並增強使用者體驗。字幕是根據原始音訊、任何附加音軌，或影片屬性頁面上的「字幕和音訊」標籤中所提供之額外字幕所產生的。支援超過 60 種語言，可以在影片發佈之前審閱及預覽字幕。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的新功能 {#forms-new-features}

* **管理出版物**：您可以使用[管理出版物](/help/forms/manage-publication.md#publish-forms-using-the-manage-publication-option))工作流程來跨環境發佈或取消發佈表單，通常是從作者執行個體到發佈和預覽執行個體。 它可讓使用者以簡化的方式發佈、取消發佈或排程內容發佈。

* **[自動儲存基於核心元件的最適化表單草稿](/help/forms/save-core-component-based-form-as-draft.md)**：使用者現在可以享受自動儲存的好處，此功能會將部分完成的表單自動儲存為草稿。使用者可以稍後再使用同一部裝置或其他裝置完成填寫。此功能可改善組織的轉換率，因為使用者不需要從頭開始填寫表單，因此能減少放棄表單的情況。

* **[規則編輯器增強功能](/help/forms/invoke-service-enhancements-rule-editor.md)**：針對以核心元件為基礎的最適化Forms，您可以使用Invoke Service的輸出來填入下拉式選項，並設定可重複或個別面板。 另外，此輸出可用於驗證其他欄位。

* **[使用面板版面的導覽按鈕增強使用者體驗](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：您現在可以在面板版面新增導覽按鈕，例如水平標籤、垂直標籤、摺疊式面板或精靈。這些按鈕簡化轉換不同面板的操作，專注於所選取的面板，藉此增強使用者體驗。


### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### 最適化Forms中的[HTML電子郵件範本](/help/forms/html-email-templates-in-adaptive-forms.md)

最適化Forms可讓您使用HTML電子郵件範本。 HTML 電子郵件範本讓您能夠在提交表單時發送內容豐富又有視覺吸引力的個人化電子郵件。這些電子郵件可以使用表單資料進行自訂，並運用各種電子郵件標籤 (例如影像和連結) 加強內容。透過最適化表單，您可以上傳包含 HTML 範本的檔案，或使用純文字編輯器來建立這些範本。

![HTML 電子郵件範本](/help/forms/assets/html-email.png)

#### 增強雲端儲存空間支援：將 PDF 直接上傳至 Azure Blob 儲存體

AEM Forms Document Generation API現在支援直接將產生的PDF檔案上傳到Azure Blob Storage。 此增強功能簡化了儲存和檢索過程，進而提高效率並改善與雲端工作流程的整合。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 支援 Java 21 {#java21}

您現在可以使用 Java 21 建置程式碼，其中包括新功能 (例如 switch 語句的模式配對、密封類別) 和效能改善；也為 Java 17 版本提供全新支援。若要了解設定步驟 (包括更新 Maven 專案和資料庫版本)，請參閱「[建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)」文章。

當偵測到 Java 17 或 21 版本時，效能較佳的 Java 21 **執行階段**&#x200B;會自動部署。但是，對於建置在 Java 11 上的環境，我們也建議選擇使用 Java 21 執行階段，請寄送電子郵件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **執行階段**&#x200B;會逐步部署至&#x200B;**所有**&#x200B;環境 (已使用 Java 17 或 21 建置的環境除外，因已經具備 Java 21 執行階段)，從二月的沙箱和 dev/RDE 開始，然後是四月的中繼/生產環境。

### 沙箱方案支援設定管道 {#sandbox-config-pipelines}

沙箱方案現在支援設定管道，後者可以在 Cloud Manager 中進行設定，以部署保存在 Git 中的 yaml 檔案。

[了解更多](/help/operations/config-pipeline.md)關於設定管道的資訊，其能設定 CDN、轉送記錄，以及執行版本清除/稽核記錄清除維護任務。

### 基於 OpenAPI 的 API - 早期採用者方案 {#open-apis-earlyadopter}

開發人員可以將 AEM as Cloud Service 功能深度整合到自己的應用程式和工具中。新的 AEM as a Cloud Service API 將會遵循 OpenAPI 規範，目標是維持一致性、妥善記錄且簡單易用。建立 Adobe Developer Console 專案，便會產生需要驗證之端點的憑證。

了解更多有關 [基於 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md) 的資訊，並試用一堂說明設定和使用方法的[端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)。

具體來說，以下列出的 API 端點可做為早期採用者方案的一部分。如果有興趣，請寄電子郵件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，並說明您預計如何使用它們。

* [Sites 內容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* Sites與Assets資料夾API
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### 邊緣運算 - 請求意見回饋！ {#edge-computing-feedback}

邊緣運算可讓資料處理更接近瀏覽器，其優點包括減少延遲。Adobe 很希望知道，您是否認為這項技術對於 AEM Publish Delivery 和 Edge Delivery Services 專案來說很實用。此外，我們也想知道您預計會如何使用它，作為我們擬定產品發展藍圖的參考。請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並附上您的疑問和註解！

### 全新 AEM Developer Console (公共 Beta 版) {#aem-developer-console-beta}

試用經改善的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，可為雲端環境內的偵錯程式碼提供更具互動式體驗。

任何人都可以在有效的 AEM Developer Console 中，按一下「*全新適用的控制台*」按鈕以存取公共 Beta 版。Adobe 樂於接受意見回饋，因此您可以寄送電子郵件至 [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] Guides {#guides}

您可以在[這裡](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2412-release/fixed-issues-2024-12-0)找到最新版 Adobe Experience Manager Guides 的新功能和增強功能完整清單。

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
