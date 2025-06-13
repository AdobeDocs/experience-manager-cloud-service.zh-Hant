---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.3.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.3.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: b9353092-88a0-477c-85f4-f916a4b8ba8f
source-git-commit: 81e5cfd699fee811fc2b072e3b65e9d463a338b2
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.3.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2025.3.0 版的功能發行說明。

>[!NOTE]
>
>您可以從這裡瀏覽至先前版本 (例如 2023 或 2024 版) 的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.3.0) 的發行日期為 2025 年 3 月 27 日。下一個功能版本 (2025.4.0) 已規劃於 2025 年 4 月 24 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2025 年 3 月發行概觀影片，以了解 2025.3.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3463860?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media 中的新功能 {#new-features-dynamic-media}

**支援使用具有 Open API 功能的 Dynamic Media 傳送的長格式影片**

具有 OpenAPI 功能的 Dynamic Media 現在支援長格式影片。長格式影片可支援高達 50GB 和 2 小時。

### Dynamic Media Classic {#dmc}

<!-- CARRY OVER TO APRIL 2025 RELEASE NOTES -->

自 2025 年 4 月起，不再支援 Dynamic Media Classic 報告儀表板中的「頻寬」索引標籤。

請參閱[頻寬和儲存、報告類型](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports)。


## Assets 檢視的新功能 {#new-features-assets-view}


**支援根標記**

AEM Assets 現在支援將後設資料表單的標記屬性對應到自訂中繼資料。此外，身為管理員，您可以限制對特定根標記及其下存在的標記之存取，藉此限制使用者可以使用哪些標記。

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

自 1 月份的版本開始，您可以使用 Java 21 和 Java 17 建置程式碼。您可以存取模式比對、密封類別和各種效能改善等新功能。若要了解設定步驟 (包括更新 Maven 專案和資料庫版本)，請參閱文章「[建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)」。

當偵測到 Java 17 或 21 版本時，會自動部署效能較佳的 Java 21 **執行階段**。但是，對於建置在 Java 11 上的環境，Adobe 也建議選擇使用 Java 21 執行階段，請寄送電子郵件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **執行階段**&#x200B;已於 2 月份部署到您的 dev/RDE 環境，並將於 **4 月 28 日和 29 日**&#x200B;套用至您的中繼/生產環境。請注意，使用 Java 21 (或 Java 17) **建置程式碼** 與 Java 21 執行階段無關，您必須明確地採取步驟，使用 Java 21 (或 Java 17) 建置程式碼。

### AEM 記錄轉送至更多目標 - Beta 版方案 {#log-forwarding-earlyadopter}

現在提供 Beta 版，您可以將 AEM 記錄轉送至 New Relic (使用 HTTPS)、Amazon S3 和 Sumo Logic。請注意，支援 AEM 記錄 (包括 Apache/Dispatcher)，但不支援 CDN 記錄。發送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) 以獲得存取權。

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM 已經支援將 (GA) AEM 和 CDN 記錄轉送到 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。此功能是以自助方式設定，並透過設定管道進行部署。

如需了解更多，請參閱[記錄轉送文件](/help/implementing/developing/introduction/log-forwarding.md)。

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

了解更多有關 [基於 OpenAPI 的 AEM API](/help/implementing/developing/open-api-based-apis.md) 的資訊，並試用一堂說明設定和使用方法的[端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)。

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
