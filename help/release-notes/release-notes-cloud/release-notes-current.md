---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 31fac8e421e58146977222d699bac1c7cf3ee4e5
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 42%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2025.4.0)的發行日期是2025年4月24日。 下一個功能版本(2025.5.0)計畫於2025年6月5日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites中的新功能 {#enhancements-sites}

**新的內容片段模型管理員UI**

使用AEM內容片段時，進一步完成新使用者端使用者介面的清單，內容片段模式現在有新的管理員UI可用。 新的UI提供簡潔而現代的清單檢視，可讓您使用篩選器搜尋模型，並顯示模型標籤以及根據特定模型存在的內容片段。 檔案可在[這裡](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)找到。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media (Scene7) {#dynamic-media-scene7}

增強式安全性環境中不支援&#x200B;**Dynamic Media (Scene7)**

AEM as a Cloud Service上的Dynamic Media (Scene7)尚未符合HIPAA標準，因此無法用於已啟用「增強式安全性」的AEM環境。

從2025年4月AEM as a Cloud Service發行版本開始，技術限制可防止在增強安全性的環境中設定Dynamic Media (Scene7)。 因此，**工具** > **雲端服務**&#x200B;底下的&#x200B;**Dynamic Media設定**&#x200B;卡不再顯示在這些環境中。

此外，使用AEM 6.5的客戶應注意Dynamic Media (Scene7)棧疊尚未準備好使用HIPAA。

### Dynamic Media Classic {#dynamic-media-classic}

**報告**

自 2025 年 4 月起，不再支援 Dynamic Media Classic 報告儀表板中的「頻寬」索引標籤。

請參閱[頻寬和儲存、報告類型](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports)。


## Assets檢視中的新功能 {#new-features-assets-view}

**資產關係**

資產視圖現在支援在簡化的資產詳細資料面板中檢視和編輯資產關係。輕鬆將Source和衍生工具等關係新增至內容，讓使用者更有效地尋找相關主圖內容。

![Assets關係範例](/help/assets/assets/asset-relations-example.png)

**比較資產的版本**

您現在可以使用Assets檢視，快速選取資產的任何版本與其最新版本進行比較。

![比較資產的版本](/help/assets/assets/version-compare2.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 搶鮮版功能

* [通用編輯器 — 表單片段](/help/edge/docs/forms/universal-editor/creating-form-fragments.md)：通用編輯器現在可讓您建立及重複使用最適化Forms的表單片段。 這些片段是可重複使用的表單區段（例如聯絡詳細資訊、同意欄位），可以一次建置並套用至多個表單。 此功能可簡化表單建立、確保一致性並改善編寫效率。

* [SharePoint Document Library — 以原始檔案名稱儲存附件](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：您現在可以選擇在SharePoint Document Library中儲存表單附件時，使用原始檔案名稱儲存表單附件。 此增強功能可簡化已上傳檔案的識別和管理。

* **規則編輯器**：
   * [在「When」子句中有Click事件的二進位條件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：規則編輯器現在允許將按鈕點選事件(_Is Clicked_)與「When」子句中的其他條件結合。 這可讓您根據使用者互動和其他因素，更精確地控制規則執行。 注意：使用多個條件時，點按事件必須是列出的第一個條件。
   * [欄位和面板的驗證條件](/help/forms/rule-editor-core-components-usecases.md)：規則編輯器現在包含&#x200B;_IsValid_&#x200B;和&#x200B;_IsNotValid_&#x200B;條件。 這些功能可讓您檢視特定欄位或整個面板（包括如「水準標籤」、「垂直標籤」、「摺疊式面板」和「精靈」等版面）的驗證狀態，有助於改善表單導覽和基於驗證結果的使用者體驗。
* [已改善SharePoint清單的範圍管理](/help/forms/connect-forms-to-sharepoint-list.md)： SharePoint網站現在支援所有受管理的路徑，例如/sites和/teams。 此增強功能實現了跨各種SharePoint網站結構的更廣泛整合，在連線到組織內容方面提供了更大的靈活性。
* [支援將記錄檔案儲存至SharePoint清單](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields)：使用SharePoint清單型表單資料模型(FDM)建立的Forms現在可以透過設定記錄檔案繫結參考欄位屬性，將記錄檔案(DoR)儲存至SharePoint清單。 此增強功能可讓支援的表單資料和檔案與SharePoint儲存體緊密整合。

### AEM Forms中的搶先使用功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### Adobe Experience Platform (AEP)與Forms整合

Forms與AEP之間的整合功能現已可供早期採用者使用。

## CIF 附加元件 {#cloud-services-cif}

### 增強功能 {#enhancements-cif}

* 新增CIF產品參考資料型別的產品變體選擇
* [實驗性]：PDP中CIF核心元件的JSON+LD
* [實驗性]： CIF清除快取的能力

### 錯誤修正 {#bug-fixes-cif}

* 修正產品欄位中的搜尋問題
* 產品URL格式無法如#variant_sku預期運作
* 無法新增超過20個SKU至產品清單元件

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### OpenAPI型API {#open-apis}

開發人員可以將 AEM as Cloud Service 功能深度整合到自己的應用程式和工具中。新的 AEM as a Cloud Service API 將會遵循 OpenAPI 規範，目標是維持一致性、妥善記錄且簡單易用。需要驗證的端點的憑證會透過建立Adobe Developer Console專案並支援OAuth伺服器對伺服器、Web應用程式和單頁應用程式(SPA)來產生。

[檢視OpenAPI型API的完整清單](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis)，[深入瞭解](/help/implementing/developing/open-api-based-apis.md)，並嘗試使用[端對端教學課程](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)，說明設定和使用方式。

觀看此影片以瞭解如何設定已驗證的API以供稍後使用：

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### CDN設定相關的增強功能 {#cdn-enhancements}

Adobe-Managed CDN提供彈性的設定選項，如[設定管道文章](/help/operations/config-pipeline.md#configurations)所述。 以下是一些近期的功能：

#### 在CDN記錄檔中包含其他屬性 {#props-in-cdnlogs}

對於除錯和資料分析等狀況很有用，您可以在[請求和回應轉換](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)中設定`logProperty`動作，在預設屬性之外的CDN記錄中包含更多資訊。

#### 區域、大陸及組織屬性作為相符條件 {#matching-conditions}

CDN規則現在可以根據地區、大陸和組織來比對使用案例，包括封鎖流量和重新導向。 `clientRegion`和`clientContinent`會根據地理位置增加已支援的`clientCountry`以相符，而`clientAsName`和`clientAsNumber`會比對自治系統以識別大型ISP、公司或雲端提供者。 深入瞭解這些[新公開的請求屬性](/help/security/traffic-filter-rules-including-waf.md#condition-structure)。

#### 設定Cookie值 {#cookie-attributes}

您可以在[回應轉換](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations)中設定Cookie屬性。

### Java 21支援 {#java21}

自 1 月份的版本開始，您可以使用 Java 21 和 Java 17 建置程式碼。您可以存取模式配對、密封類別和各種效能改善等新功能。若要了解設定步驟 (包括更新 Maven 專案和資料庫版本)，請參閱文章「[建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)」。

當偵測到 Java 17 或 21 版本時，會自動部署效能較佳的 Java 21 **執行階段**。但是，對於建置在 Java 11 上的環境，Adobe 也建議選擇使用 Java 21 執行階段，請寄送電子郵件至 [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)。了解 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)。

>[!IMPORTANT]
>
> Java 21 **執行階段**&#x200B;已於 2 月份部署到您的 dev/RDE 環境，並將於 **4 月 28 日和 29 日**&#x200B;套用至您的中繼/生產環境。請注意，使用 Java 21 (或 Java 17) **建置程式碼** 與 Java 21 執行階段無關 - 您必須明確地採取步驟，使用 Java 21 (或 Java 17) 來建置程式碼。

### 實施AEM的記錄設定原則 {#logconfig-policy}

為了確保有效監控客戶環境，AEM Java記錄必須保持一致的格式，並且不應由自訂設定覆寫。 記錄輸出必須保持指向預設檔案。 對於AEM產品程式碼，必須保留預設記錄層級。 不過，調整客戶開發程式碼的記錄層級是可接受的。

為此，不應變更下列OSGi屬性：
* **Apache Sling記錄設定** (PID： `org.apache.sling.commons.log.LogManager`) — *所有屬性*
* **Apache Sling記錄記錄器組態** （工廠PID： `org.apache.sling.commons.log.LogManager.factory.config`）：
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

5月中旬，AEM將強制執行將忽略對這些屬性的任何自訂修改的原則。 請檢閱並據此調整您的下游流程。 例如，如果您使用記錄轉送功能：
* 如果您的記錄目的地需要自訂（非預設）記錄格式，您可能需要更新擷取規則。
* 如果記錄層級的變更降低了記錄詳細程度，請注意，預設記錄層級可能會導致記錄磁碟區顯著增加。

### AEM記錄轉送至更多目的地 — Beta計畫 {#log-forwarding-earlyadopter}

現在提供 Beta 版，您可以將 AEM 記錄轉送至 New Relic (使用 HTTPS)、Amazon S3 和 Sumo Logic。請注意，支援 AEM 記錄 (包括 Apache/Dispatcher)，但不支援 CDN 記錄。發送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) 以獲得存取權。

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM 已經支援將 (GA) AEM 和 CDN 記錄轉送到 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。此功能是以自助方式設定，並透過設定管道進行部署。

如需了解更多，請參閱[記錄轉送文件](/help/implementing/developing/introduction/log-forwarding.md)。

### 邊緣運算 - 請求意見回饋！ {#edge-computing-feedback}

邊緣運算可讓資料處理更接近瀏覽器，其優點包括減少延遲。Adobe 想要知道，您覺得這項技術對於 AEM Publish Delivery 和 Edge Delivery Services 專案來說是否實用。此外，我們也想知道您預計會如何使用它，以作為我們擬定產品路徑圖的參考。

一些可能的使用案例：

* 使用 IdP 進行驗證以控制內容存取
* Personalization：根據地理位置、裝置型別、使用者屬性等呈現動態內容。
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
