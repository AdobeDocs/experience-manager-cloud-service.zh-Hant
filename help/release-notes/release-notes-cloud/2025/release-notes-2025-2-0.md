---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.2.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.2.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: b893663d-35f1-43ae-a029-4c249b117f2d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 96%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.2.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2025.2.0 版的功能發行說明。

>[!NOTE]
>
>您可以從這裡瀏覽至先前版本 (例如 2023 或 2024 版) 的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.2.0) 的發行日期為 2025 年 3 月 4 日。下一個功能版本 (2025.3.0) 預計於 2025 年 3 月 27 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2025 年 2 月發行概觀影片，了解 2025.2.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3458080?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AEM Sites 中的新功能 {#new-features-sites}

**內容片段自動標記**

建立內容片段時，現在可自動繼承指派給內容模型的標記。這樣一來，儲存在內容片段中的內容便可以有效率地完成自動分類。

**內容片段 UUID 支援**

內容片段 UUID 支援現在正式推出。新功能不會改變 AEM 中基於路徑的操作行為，例如移動、重新命名、轉出 (路徑會自動調整)，但它可讓外部使用內容片段的操作變得更輕鬆且更穩定，尤其是在使用 GraphQL 查詢直接針對個別片段進行 ByPath 查詢時。如果變更片段路徑，這類查詢可能無法進行。使用新的 ById 查詢類型時，即使路徑變更，片段的 UUID 也不會改變，所以此查詢現在可保持穩定。

**內容片段編輯器和 GraphQL 中具有 OpenAPI 功能的 Dynamic Media 支援**

儲存在不同的 AEM as a Cloud Service 方案而不是內容片段中的資產，以及具備擁有 OpenAPI 功能的 Dynamic Media 的資產，現在皆可在內容片段中使用。新的內容片段編輯器的影像選擇器，現在允許在片段中引用的影像資產選擇「遠端」存放庫作為其來源。使用 AEM GraphQL 傳遞此類內容片段時，JSON 回應現在包含遠端資產的必要屬性 (assetId、repositoryId)，因此用戶端應用程式可以建立相應的 Dynamic Media 並透過 OpenAPI URL 來擷取影像。

**內容片段編輯器轉出**

我們將繼續使用[Unified Shell](/help/sites-cloud/administering/content-fragments/authoring.md) （使用Spectrum-UI）在AEM as a Cloud Service中啟用新的[內容片段編輯器](/help/overview/aem-cloud-service-on-unified-shell.md)。 繼在 2024 年 11 月成為所有雲端服務開發人員環境的預設選項後，此功能將在 2025 年 4 月 1 日成為所有中繼環境的預設選項，並在 2025 年 5 月 1 日成為所有生產環境的預設選項。在所有情況下，使用者仍然可以選擇恢復使用 AEM Touch UI 中的傳統內容片段編輯器。

**翻譯 HTTP API**

在早期採用者模式中已開放使用一段時間的 AEM 翻譯 HTTP REST API 現在正式推出。您可以在[這裡找到檔案。](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/translation/) API允許在AEM中自動執行翻譯管理流程中內容的必要步驟。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets 中的新功能 {#new-features-assets}

**Dynamic Media 全新封裝結構**

Dynamic Media 全新封裝結構現已推出，更加符合市場預期且支援追蹤。全新封裝結構包括：

* Dynamic Media Prime，其中包括支援 OpenAPI 的 Dynamic Media 和影片，可強化傳遞。

* Dynamic Media Ultimate 新增傳遞和轉換功能，以滿足更高的使用要求。

您必須擁有 Assets as a Cloud Service Prime 或 Ultimate 才能享受全新封裝結構的好處。

**AI 生成影片字幕**

Adobe Dynamic Media 中的 AI 生成影片字幕功能會使用人工智慧，為影片內容自動生成字幕。透過提供準確的字幕，這項功能可改善輔助工具的效能並增強使用者體驗。字幕是根據原始音訊所產生，而在影片屬性頁面的「字幕和音訊」標籤會提供任何其他音軌或額外的字幕。您可以在影片發佈之前審查及預覽字幕，其支援超過 60 種語言。

**自訂搜尋篩選器**

自訂搜尋篩選器可提高搜尋相關資訊的準確性和效率。您可以利用這項功能進行更精確的搜尋，根據特定屬性 (例如品牌、產品、類別或其他關鍵識別碼) 篩選資料。這樣可以改善組織效率，減少篩選無關結果所花費的時間，並可以加快決策過程。自訂搜尋篩選器亦支援擴充性，因為瀏覽和分析大型資料集變得更加簡單。

![自訂搜尋篩選器](/help/assets/assets/custom-search-filters.png)

### Content Hub 的搶先體驗功能 {#early-access-content-hub}

除了現有的靜態轉譯，您現在使用 Content Hub 亦可以檢視和下載動態和智慧裁切轉譯。作為 Content Hub 管理員，您也可以使用「設定」使用者介面來設定使用者是否可使用這些轉譯。

![動態轉譯](/help/assets/assets/download-single-asset-renditions-dynamic.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### 最適化表單中的 HTML 電子郵件範本

最適化表單讓您能夠使用 [HTML 電子郵件範本](/help/forms/html-email-templates-in-adaptive-forms.md)。HTML 電子郵件範本讓您能夠在提交表單時發送內容豐富又有視覺吸引力的個人化電子郵件。這些電子郵件可以使用表單資料進行自訂，並運用各種電子郵件標籤 (例如影像和連結) 加強內容。透過最適化表單，您可以上傳包含 HTML 範本的檔案，或使用純文字編輯器來建立這些範本。

![HTML 電子郵件範本](/help/forms/assets/html-email.png)

#### 增強雲端儲存空間支援：將 PDF 直接上傳至 Azure Blob 儲存體

您現在可以透過 AEM Forms 的文件產生 API，[將產生的 PDF 文件直接上傳](/help/forms/early-access-ea-features.md#doc-generation-api)至 Azure Blob 儲存體。此增強功能簡化了儲存和檢索過程，進而提高效率並改善與雲端工作流程的整合。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 支援 Java 21 {#java21}

如 1 月發行說明中所述，您現在可以使用 Java 21 建置程式碼，其中包括新功能 (例如 switch 陳述式的模式比對、密封類別) 和效能改進；也為 Java 17 版本提供全新支援。若要了解設定步驟 (包括更新 Maven 專案和資料庫版本)，請參閱「[建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)」文章。

當偵測到 Java 17 或 21 版本時，效能較佳的 Java 21 **執行階段**&#x200B;會自動部署。但是，對於建置在 Java 11 上的環境，我們也建議選擇使用 Java 21 執行階段，請寄送電子郵件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> 在 2 月，除了已經使用 Java 17 或 21 建置的環境之外 (這些環境已有 Java 21 執行階段)，Java 21 **執行階段**&#x200B;也已部署到開發/RDE 環境。Java 21 將於 4 月套用至中繼/生產環境。

### 邊緣運算 - 請求意見回饋！ {#edge-computing-feedback}

邊緣運算可讓資料處理更接近瀏覽器，其優點包括減少延遲。Adobe 想要知道，您覺得這項技術對於 AEM Publish Delivery 和 Edge Delivery Services 專案來說是否實用。此外，我們也想知道您預計會如何使用它，以作為我們擬定產品路徑圖的參考。

一些可能的使用案例：

* 使用 IdP 進行驗證以控制內容存取
* 根據地理位置、裝置類型、使用者屬性等，轉譯動態 (個人化、本地化) 內容。
* 進階影像處理
* CDN 與來源之間的中介軟體
* 瀏覽器和第三方 API 之間的一層，可能用於重新設定 API 回應的格式
* 彙總來自多個來源的資料，讓用戶端瀏覽器更容易轉譯它

請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並附上您的問題和評論！

### 基於 OpenAPI 的 API - 早期採用者方案 {#open-apis-earlyadopter}

開發人員可以將 AEM as Cloud Service 功能深度整合到自己的應用程式和工具中。新的 AEM as a Cloud Service API 將會遵循 OpenAPI 規範，目標是維持一致性、妥善記錄且簡單易用。建立 Adobe Developer Console 專案，便會產生需要驗證之端點的憑證。

了解更多有關 [基於 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md) 的資訊，並試用一堂說明設定和使用方法的[端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)。

具體來說，以下列出的 API 端點可做為早期採用者方案的一部分。如果有興趣，請寄電子郵件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，並說明您預計如何使用它們。

* [Sites 內容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* Sites與Assets資料夾API
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### 全新 AEM Developer Console (公共 Beta 版) {#aem-developer-console-beta}

試用經改善的 [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)，可為雲端環境內的偵錯程式碼提供更具互動式體驗。

任何人都可以在有效的 AEM Developer Console 中，按一下「*全新適用的控制台*」按鈕以存取公共 Beta 版。Adobe 樂於接受意見回饋，因此您可以寄送電子郵件至 [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## [!DNL Experience Manager] Guides {#guides}

您可以在[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2025-releases/2502-release/whats-new-2025-02-0)找到最新版 Adobe Experience Manager Guides 的新功能和增強功能完整清單。

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
