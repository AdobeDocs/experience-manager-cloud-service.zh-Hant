---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 896a2927c0f5733ab23ca9f6c9e975f8388daff9
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 47%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 最新發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 目前 (最新) 版本的功能發行說明。

>[!NOTE]
>
>您可以從這裡瀏覽至先前版本 (例如 2023 或 2024 版) 的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2025.2.0)的發行日期是2025年3月4日。 下一個功能版本(2025.3.0)計畫於2025年3月27日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AEM Sites中的新功能 {#new-features-sites}

**內容片段自動標籤**

建立內容片段時，現在可以自動繼承指派給內容模型的標籤。 如此一來，即可對內容片段中儲存的內容進行強大的自動分類。

**內容片段UUID支援**

內容片段UUID支援現已正式推出。 新功能不會改變AEM中作業以路徑為基礎的行為（例如移動、重新命名、轉出，路徑會自動調整），但可讓內容片段的外部使用更輕鬆且更穩定，尤其是使用以ByPath查詢直接鎖定個別片段的GraphQL查詢時。 如果片段路徑變更，此類查詢可能會中斷。 使用新的ById查詢型別時，查詢現在會保持穩定，因為路徑這樣做時，片段的UUID不會變更。

**在內容片段編輯器和GraphQL中支援OpenAPI的Dynamic Media**

儲存在與內容片段不同AEM as a Cloud Service程式中的Assets，以及通過新的Dynamic Media （具有OpenAPI功能）啟用的，現在可用於內容片段。 新內容片段編輯器中的影像選擇器現在允許選取「遠端」存放庫作為片段中要參考的影像資產的來源。 在使用AEM GraphQL傳送此類內容片段時，JSON回應現在包含遠端資產(assetId、repositoryId)的必要屬性，讓使用者端應用程式能夠使用OpenAPI URL建立各自的動態媒體以擷取影像。

**翻譯HTTP API**

已處於早期採用者模式一段時間的AEM Translation HTTP REST API現在為GA。 檔案可在[這裡](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/)找到。 此API允許在AEM中自動執行內容翻譯管理流程中的必要步驟。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets 中的新功能 {#new-features-assets}

**Dynamic Media新封裝結構**

更新的Dynamic Media封裝結構現在已推出，以便更符合市場預期和支援追蹤。 新的封裝結構包含：

* Dynamic Media Prime包含具有OpenAPI的Dynamic Media以及可增強傳送的視訊。

* Dynamic Media Ultimate新增傳送和轉換功能，以符合更嚴苛的使用需求。

您必須安裝Assets as a Cloud Service Prime或Ultimate，才能從新的封裝結構中獲益。

**AI 生成影片字幕**

Adobe Dynamic Media 中的 AI 生成影片字幕功能會使用人工智慧，為影片內容自動生成字幕。此功能旨在改善協助工具，並提供精確字幕以改善使用者體驗。 註解產生自原始音訊、任何其他音軌或視訊屬性頁面的「註解和音訊」索引標籤中提供額外的註解。 支援超過 60 種語言，可以在影片發佈之前審閱及預覽字幕。

**自訂搜尋篩選器**

自訂搜尋篩選器可提升尋找相關資訊的精確度和效率。 它允許更量身打造的搜尋，並根據特定屬性（例如品牌、產品、類別或其他關鍵識別碼）篩選資料。 這可改善組織、減少花在篩選無關結果上的時間，並可加快決策過程。 它還支援擴充性，因為大型資料集更容易導覽和分析。

![自訂搜尋篩選器](/help/assets/assets/custom-search-filters.png)


### Content Hub中的搶先使用功能 {#early-access-content-hub}

除了現有的靜態轉譯外，Content Hub現在可讓您檢視及下載動態和智慧型裁切轉譯。 身為Content Hub管理員，您也可以使用「設定使用者介面」來設定這些轉譯對使用者的可用性。

![動態轉譯](/help/assets/assets/download-single-asset-renditions-dynamic.png)



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### 最適化Forms中的HTML電子郵件範本

最適化Forms可讓您使用[HTML電子郵件範本](/help/forms/html-email-templates-in-adaptive-forms.md)。 HTML 電子郵件範本讓您能夠在提交表單時發送內容豐富又有視覺吸引力的個人化電子郵件。這些電子郵件可以使用表單資料進行自訂，並運用各種電子郵件標籤 (例如影像和連結) 加強內容。透過最適化表單，您可以上傳包含 HTML 範本的檔案，或使用純文字編輯器來建立這些範本。

![HTML 電子郵件範本](/help/forms/assets/html-email.png)

#### 增強雲端儲存空間支援：將 PDF 直接上傳至 Azure Blob 儲存體

AEM Forms Document Generation API現在可讓您[直接將產生的PDF檔案](/help/forms/early-access-ea-features.md#doc-generation-api)上傳到Azure Blob儲存體。 此增強功能簡化了儲存和檢索過程，進而提高效率並改善與雲端工作流程的整合。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 支援 Java 21 {#java21}

如1月發行說明中所述，您現在可以使用Java 21建置計畫碼，其中包括新功能（例如切換陳述式的模式比對、密封類別）和效能改善；Java 17建置也是最新支援。 若要了解設定步驟 (包括更新 Maven 專案和資料庫版本)，請參閱「[建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)」文章。

當偵測到 Java 17 或 21 版本時，效能較佳的 Java 21 **執行階段**&#x200B;會自動部署。但是，對於建置在 Java 11 上的環境，我們也建議選擇使用 Java 21 執行階段，請寄送電子郵件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> 2月，Java 21 **執行階段**&#x200B;已部署至開發/RDE環境（除了已使用Java 17或21建置的之外，這些環境已具有Java 21執行階段）。 Java 21將於4月套用至中繼/生產環境。

### 邊緣運算 - 請求意見回饋！ {#edge-computing-feedback}

邊緣運算可讓資料處理更接近瀏覽器，其優點包括減少延遲。Adobe很想知道您是否發現這項技術對AEM Publish Delivery和Edge Delivery Services專案很有用。 此外，讓我們知道您將其用作產品藍圖輸入內容的設想。

部分可能的使用案例：
* 使用IdP進行驗證以閘道內容存取權
* 根據地理位置、裝置型別、使用者屬性等呈現動態（個人化、本地化）內容。
* 進階影像操作
* CDN與來源之間的中介軟體
* 瀏覽器和第三方API之間的圖層，可能會重新格式化API回應
* 彙總來自多個來源的資料，讓使用者端瀏覽器更容易呈現

請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並附上您的疑問和註解！

### 基於 OpenAPI 的 API - 早期採用者方案 {#open-apis-earlyadopter}

開發人員可以將 AEM as Cloud Service 功能深度整合到自己的應用程式和工具中。新的 AEM as a Cloud Service API 將會遵循 OpenAPI 規範，目標是維持一致性、妥善記錄且簡單易用。建立 Adobe Developer Console 專案，便會產生需要驗證之端點的憑證。

了解更多有關 [基於 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md) 的資訊，並試用一堂說明設定和使用方法的[端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)。

具體來說，以下列出的 API 端點可做為早期採用者方案的一部分。如果有興趣，請寄電子郵件至 [aem-apis@adobe.com](mailto:aem-apis@adobe.com)，並說明您預計如何使用它們。

* [Sites 內容片段 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites 和資產資料夾 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

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
