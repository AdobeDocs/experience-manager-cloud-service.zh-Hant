---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.4.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.4.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: 48e09824-5c67-49d8-8896-358d679649fc
source-git-commit: c1ff27a76309628f1fb7b816092172aca7c6a738
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.4.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2025.4.0 版的功能發行說明。

>[!NOTE]
>
>您可以從這裡瀏覽至先前版本 (例如 2023 或 2024 版) 的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前功能版本 (2025.4.0) 的發行日期是 2025 年 4 月 24 日。下一個功能版本 (2025.5.0) 預計於 2025 年 6 月 5 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

## 發行影片 {#release-video}

請觀看 2025 年 4 月發行概觀影片，以了解 2025.4.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3464013?quality=12&captions=chi_hant)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新功能 {#enhancements-sites}

**新的內容片段模型管理員使用者介面**

在使用 AEM 內容片段時，為了進一步完善新的用戶端使用者介面清單，現在已針對內容片段模型提供新的管理 UI。新的使用者介面具有簡潔、現代的清單視圖，能使用篩選器搜尋模型，並顯示模型標記和以特定模型為基礎的內容片段。相關文件請參閱[此處](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media (Scene7) {#dynamic-media-scene7}

**增強式安全性環境不支援 Dynamic Media (Scene7)**

AEM as a Cloud Service 上的 Dynamic Media (Scene7) 不符合 HIPAA 標準，因此無法在啟用增強式安全性的 AEM 環境中使用。

自 2025 年 4 月的 AEM as a Cloud Service 版本開始，會設有技術限制以防止在具有增強式安全性的環境中設定 Dynamic Media (Scene7)。因此，在這些環境中，於「**工具** > **雲端服務**」下不會再出現 **Dynamic Media 設定**&#x200B;卡片。

此外，使用 AEM 6.5 的客戶應注意 Dynamic Media (Scene7) 堆疊不符合 HIPAA 標準。

### Dynamic Media Classic {#dynamic-media-classic}

**報告**

自 2025 年 4 月起，不再支援 Dynamic Media Classic 報告儀表板中的「頻寬」索引標籤。

請參閱[頻寬和儲存、報告類型](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports)。

## 資產視圖的新功能 {#new-features-assets-view}

**資產關係**

資產視圖現在支援在簡化的資產詳細資料面板中檢視和編輯資產關係。輕鬆地將來源和衍生等關係加入內容中，讓使用者能更有效地找到相關的主要內容。

![資產關係範例](/help/assets/assets/asset-relations-example.png)

**比較資產的不同版本**

您現在可以使用資產視圖快速選取資產的任何版本，並與其最新版本進行比較。

![比較資產的不同版本](/help/assets/assets/version-compare2.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 搶鮮版功能

* [通用編輯器：表單片段](/help/edge/docs/forms/universal-editor/creating-form-fragments.md)：您現在可以透過通用編輯器為自適應表單建立表單片段並重複使用。這些片段是可重複使用的表單區段 (例如，聯絡資訊、同意欄位)，僅需建置一次即可套用於多個表單。此功能可以簡化表單建立過程、確保一致性，並且提高製作效率。

* [SharePoint 文件庫：以原始檔案名稱儲存附件](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：您現在將表單附件儲存於 SharePoint 文件庫中時，可以選擇使用其原始檔案名稱。此增強功能可以簡化上傳之檔案的識別和管理。

* **規則編輯器**：
   * [「When」子句中點擊事件的二元條件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：規則編輯器現在可以將按鈕點擊事件 (_Is Clicked_) 與「When」子句中的其他條件結合。因此可以根據使用者互動和其他因素，對規則執行進行更精確的控制。備註：使用多個條件時，點擊事件必須是列出的第一個條件。
   * [欄位和面板的驗證條件](/help/forms/rule-editor-core-components-usecases.md)：規則編輯器現在包含 _IsValid_ 和 _IsNotValid_ 條件。因此您可以查看特定欄位或整個面板 (包括水平標籤、垂直標籤、摺疊式面板和精靈等版面) 的驗證狀態，進而根據驗證結果改善表單導覽和使用者體驗。
* **改進 SharePoint 清單的範圍管理**：SharePoint 網站現在支援所有受管理的路徑，例如 /sites 和 /teams。此增強功能讓跨各種 SharePoint 網站結構的整合範圍更為寬廣，在連結組織內容方面提供更大的靈活度。
* **支援將記錄文件儲存至 SharePoint 清單**：使用 SharePoint 清單式表單資料模型 (FDM) 所建立的表單，現在可以透過設定記錄文件繫結參考欄位屬性，將記錄文件 (DoR) 儲存至 SharePoint 清單。此增強功能可以將支援的表單資料和文件與 SharePoint 儲存空間緊密整合。

### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### Adobe Experience Platform (AEP) 與 Forms 的整合

早期採用者現在可以使用 Forms 和 AEP 之間的整合功能。

## CIF 附加元件 {#cloud-services-cif}

### 增強功能 {#enhancements-cif}

* 新增 CIF 產品參考資料類型的產品變體選擇
* **實驗性**： PDP中CIF核心元件的[JSON+LD](/help/commerce-cloud/customizing/json-ld.md)
* **實驗性**： [CIF清除快取的能力](/help/commerce-cloud/configuring/clear-cache.md)

### 錯誤修正 {#bug-fixes-cif}

* 修正產品欄位的搜尋問題
* #variant_sku 的產品 URL 格式未如預期運作
* 無法在產品清單元件上新增超過 20 個 SKU

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 以 OpenAPI 為基礎之 API {#open-apis}

開發人員可以將 AEM as Cloud Service 功能深度整合到自己的應用程式和工具中。新的 AEM as a Cloud Service API 將會遵循 OpenAPI 規範，目標是維持一致性、妥善記錄且簡單易用。需要驗證的端點憑證可藉由建立 Adobe Developer Console 專案產生，並支援 OAuth Server-to-Server、網頁應用程式，及單一頁面應用程式 (SPA)。

查看以 OpenAPI 為基礎之 API 的[完整清單](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis)，[了解更多](/help/implementing/developing/open-api-based-apis.md)，並嘗試一堂說明設定和使用方法的[端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)。

觀看此影片，了解如何設定經驗證的 API 供稍後使用：

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### CDN 設定相關的增強功能 {#cdn-enhancements}

Adobe 管理之 CDN 提供靈活的設定選項，如[設定管道文章](/help/operations/config-pipeline.md#configurations)中所述。以下為一些最新功能：

#### 在 CDN 記錄中納入其他屬性 {#props-in-cdnlogs}

您可以設定[要求和回應轉換](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)中的 `logProperty` 動作，在 CDN 記錄中納入預設屬性之外的更多資訊，這對於包括偵錯和資料分析的情境來說很有用。

#### 區域、洲別和組織屬性作為比對條件 {#matching-conditions}

CDN 規則現在可以針對包括封鎖流量和重新導向在內的使用案例，根據區域、洲別和組織進行比對。`clientRegion` 和 `clientContinent` 能增強已支援的 `clientCountry`，根據地理位置進行比對，而 `clientAsName` 和 `clientAsNumber` 能與自治系統比對，用於識別大型 ISP、公司或雲端提供者。了解更多關於這些[新公開之要求屬性](/help/security/traffic-filter-rules-including-waf.md#condition-structure)的資訊。

#### 設定 Cookie 值 {#cookie-attributes}

您可以在[回應轉換](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations)中設定 Cookie 屬性。

### 支援 Java 21 {#java21}

自 1 月份的版本開始，您可以使用 Java 21 和 Java 17 建置程式碼。您可以存取模式比對、密封類別和各種效能改善等新功能。若要了解設定步驟 (包括更新 Maven 專案和資料庫版本)，請參閱文章「[建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)」。

當偵測到 Java 17 或 21 版本時，會自動部署效能較佳的 Java 21 **執行階段**。但是，對於建置在 Java 11 上的環境，Adobe 也建議選擇使用 Java 21 執行階段，請寄送電子郵件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **執行階段**&#x200B;已於 2 月份部署到您的 dev/RDE 環境，並將於 **4 月 28 日和 29 日**&#x200B;套用至您的中繼/生產環境。請注意，使用 Java 21 (或 Java 17) **建置程式碼** 與 Java 21 執行階段無關，您必須明確地採取步驟，使用 Java 21 (或 Java 17) 建置程式碼。

### 執行 AEM 的記錄設定原則 {#logconfig-policy}

為確保能有效監視客戶環境，AEM Java 記錄必須維持一致的格式，且不應被自訂設定覆寫。記錄輸出必須維持導向預設檔案。針對 AEM 產品程式碼，必須保留預設記錄等級。不過，可以針對客戶開發的程式碼調整記錄等級。

為此，不應變更以下 OSGi 屬性：
* **Apache Sling 記錄設定** (PID: `org.apache.sling.commons.log.LogManager`)：*所有屬性*
* **Apache Sling 記錄記錄器設定** (工廠 PID: `org.apache.sling.commons.log.LogManager.factory.config`)：
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

5 月中旬，AEM 將強制執行一項原則，屆時會忽略對這些屬性的任何自訂修改。請檢閱並從而調整您的下游流程。舉例來說，若您使用記錄轉送功能：
* 如果您的記錄目標需要自訂 (非預設) 記錄格式，則可能需要更新您的攝取規則。
* 若記錄等級的變更會使記錄的詳細程度降低，請注意預設的記錄等級可能會導致記錄量顯著增加。

### AEM 記錄轉送至更多目標：Beta 版方案 {#log-forwarding-earlyadopter}

現在提供 Beta 版，您可以將 AEM 記錄轉送至 New Relic (使用 HTTPS)、Amazon S3 和 Sumo Logic。請注意，支援 AEM 記錄 (包括 Apache/Dispatcher)，但不支援 CDN 記錄。發送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) 以獲得存取權。

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM 已經支援將 (GA) AEM 和 CDN 記錄轉送到 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。此功能是以自助方式設定，並透過設定管道進行部署。

如需了解更多，請參閱[記錄轉送文件](/help/implementing/developing/introduction/log-forwarding.md)。

### 邊緣運算 - 請求意見回饋！ {#edge-computing-feedback}

邊緣運算可讓資料處理更接近瀏覽器，其優點包括減少延遲。Adobe 想要知道，您覺得這項技術對於 AEM Publish Delivery 和 Edge Delivery Services 專案來說是否實用。此外，我們也想知道您預計會如何使用它，以作為我們擬定產品路徑圖的參考。

一些可能的使用案例：

* 使用 IdP 進行驗證以控制內容存取
* 根據地理位置、裝置類型、使用者屬性等轉譯動態內容以進行個人化。
* 進階影像處理
* CDN 與來源之間的中介軟體
* 瀏覽器和第三方 API 之間的一層，可能用於重新設定 API 回應的格式
* 彙總來自多個來源的資料，讓用戶端瀏覽器更容易轉譯它

請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並附上您的問題和評論！

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
