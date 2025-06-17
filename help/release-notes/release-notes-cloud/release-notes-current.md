---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 75816f35a8bca8356e17b13341c2ddbd850f8eff
workflow-type: tm+mt
source-wordcount: '2077'
ht-degree: 95%

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


[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.5.0) 的發行日期為 2025 年 6 月 5 日。下一個功能版本 (2025.6.0) 規劃於 2025 年 6 月 26 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440931?quality=12&captions=chi_hant)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AI 產生的中繼資料**

AEM Assets 現在使用 [AI 自動產生中繼資料，包括標題、說明和關鍵字](/help/assets/metadata-assets-view.md#ai-smart-tags)。這些 AI 產生的欄位能提升中繼資料準確性，讓資產更易於搜尋、分類和推薦。此方法不僅能藉由除去手動標記過程提升效率，還能確保大量數位內容的一致性和擴充性。

![AI 產生的中繼資料](/help/assets/assets/enhanced-smart-tags.png)

**與 Figma 整合**

AEM Assets 可以和 Figma 原生整合，讓設計者能自 Figma 使用者介面直接存取儲存於 AEM Assets 內的資產。您可以在Figma畫布中置入AEM Assets中管理的內容，然後將新內容或編輯過的內容儲存在AEM Assets存放庫中。 若要存取Figma社群頁面上可用的AEM Assets Connector，請按一下[這裡](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector)。

>[!VIDEO](https://video.tv.adobe.com/v/3463828)


### 全新的 Content Hub 功能 {#new-features-content-hub}

**屬性型存取控制 (ABAC)**

[Content Hub 現在允許您針對資產存取套用規則型限制。](/help/assets/attribute-based-access-control.md)資產權限能確保治理，並確保使用者僅能存取相關的資產。

資產限制規則以中繼資料為基礎，若規則中所定義的條件和資產中繼資料相互符合，該使用者群組便能看見該資產。

屬性型存取控制的一些主要優勢包括：

* 除去對資料夾結構的權限相依性

* 讓管理員能夠上傳資產並回溯性判定權限結構

* 減少重複的數量，提高資產完整性。當相同的資產與不同的群組共用時，資料夾型權限需要進行重複。

**使用者介面品牌化**

管理員現在能透過 Content Hub [使用品牌專屬元素自訂使用者介面](/help/assets/configure-content-hub-ui-options.md##configure-branding-content-hub)，包括橫幅影像、橫幅標題和正文，以及主要和次要顏色。這些增強功能有助於確保品牌一致性、簡化使用者上線流程，並建立信任。

![使用者介面品牌化](/help/assets/assets/content-hub-ui-branding.png)

**公開連結共用**

Content Hub 現在支援[產生共用連結，允許外部使用者](/help/assets/share-assets-content-hub.md##share-assets)在沒有應用程式存取權的情況下檢視資產中繼資料或下載資產。

![使用者介面品牌化](/help/assets/assets/public-and-private-link.png)

**集合治理**

您現在能透過 Content Hub [於建立期間控制對於集合的存取權，確保唯有授權使用者可以檢視或管理分組的資產](/help/assets/collections-content-hub.md##create-collections)。這樣可以確保提高安全性、改善協作、組織資產管理，以及簡化治理。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>集合治理是一項限量開放使用的功能。您可以建立支援服務單來啟用這項功能。

**將多個資產以 ZIP 檔案的形式下載**

您現在還能透過 Content Hub，[以 ZIP 檔案而非個別檔案的形式下載所選取之資產及其轉譯](/help/assets/download-assets-content-hub.md#download-asset-renditions)，簡化檔案管理作業。

**Content Hub 中的 Dynamic Media 轉譯**

直接在 [Content Hub 使用者介面中存取所有 Dynamic Media 轉譯預設集和智慧裁切並進行下載](/help/assets/download-assets-content-hub.md#download-asset-renditions)。

![Dynamic Media 轉譯](/help/assets/assets/dm-renditions-content-hub.png)

### Dynamic Media 中的新功能 {#new-features-dynamic-media}

**Dynamic Media 與 AJO B2C 的原生整合**

[Experience Manager (AEM) Dynamic Media 與 Journey Optimizer (AJO) B2C 的原生整合](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/content-management/combine/aem-dynamic)，讓行銷人員能夠輕鬆地將 AEM Dynamic Media 資產 (轉譯和 DM 範本) 嵌入至 AJO 內容中，並在多個通道之間提供即時更新和極度個人化的體驗。

>[!VIDEO](https://video.tv.adobe.com/v/3463793/?learn=on&enablevpops=&autoplay=true&captions=chi_hant)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 搶鮮版功能

* [通用編輯器：表單片段](/help/edge/docs/forms/universal-editor/creating-form-fragments.md)：您現在可以透過通用編輯器為自適應表單建立表單片段並重複使用。這些片段是可重複使用的表單區段 (例如，聯絡資訊、同意欄位)，僅需建置一次即可套用於多個表單。此功能可以簡化表單建立過程、確保一致性，並且提高製作效率。

* [SharePoint 文件庫：以原始檔案名稱儲存附件](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library)：您現在將表單附件儲存於 SharePoint 文件庫中時，可以選擇使用其原始檔案名稱。此增強功能可以簡化上傳之檔案的識別和管理。

* **規則編輯器**：
   * [「When」子句中點擊事件的二元條件](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor)：規則編輯器現在可以將按鈕點擊事件 (_Is Clicked_) 與「When」子句中的其他條件結合。因此可以根據使用者互動和其他因素，對規則執行進行更精確的控制。備註：使用多個條件時，點擊事件必須是列出的第一個條件。
   * [欄位和面板的驗證條件](/help/forms/rule-editor-core-components-usecases.md)：規則編輯器現在包含 _IsValid_ 和 _IsNotValid_ 條件。因此您可以查看特定欄位或整個面板 (包括水平標籤、垂直標籤、摺疊式面板和精靈等版面) 的驗證狀態，進而根據驗證結果改善表單導覽和使用者體驗。
* [改進 SharePoint 清單的範圍管理](/help/forms/connect-forms-to-sharepoint-list.md)：SharePoint 網站現在支援所有受管理的路徑，例如 /sites 和 /teams。此增強功能讓跨各種 SharePoint 網站結構的整合範圍更為寬廣，在連結組織內容方面提供更大的靈活度。
* [支援將記錄文件儲存至 SharePoint 清單](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields)：使用 SharePoint 清單式表單資料模型 (FDM) 所建立的表單，現在可以透過設定記錄文件繫結參考欄位屬性，將記錄文件 (DoR) 儲存至 SharePoint 清單。此增強功能可以將支援的表單資料和文件與 SharePoint 儲存空間緊密整合。

### AEM Forms 的搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗計劃為您提供獨一無二的機會，獲得先進創新內容的獨家使用權，並協助形塑開發。

本發行說明列出目前版本提供的創新功能。如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。

#### Adobe Experience Platform (AEP) 與 Forms 的整合

早期採用者現在可以使用 Forms 和 AEP 之間的整合功能。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 更新的棄用流程 {#updated-deprecation-process}

Adobe 會定期審查功能、資料庫、API 和設定，確保其符合效能、安全性和價值標準。當功能不再符合這些標準時，會標記為棄用，並且必須在指定的移除日期之前停止使用。於此日期之前，Adobe 會透過電子郵件通知提醒客戶，並告知繼續或部署新版本之前需要在 Cloud Manager 中採取的動作。若未採取必要的動作，可能會導致無法升級至 AEM 的新版本，進而對安全性、效能、可靠性和可用性產生潛在影響。

如欲了解進一步的詳細資訊，請參閱[棄用文章](/help/release-notes/deprecated-removed-features.md)。

#### 接近移除日期的棄用 Java API 和 OSGi 設定 {#deprecated-near-removals}

展開下方清單，檢視不應再使用的棄用 API 和 OSGi 設定。如需完整詳情 (包括移除的時間表)，請參閱棄用文章。

<details>
  <summary>展開以查看棄用內容</summary>

Java API：
* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

OSGi 屬性：

* `org.apache.sling.commons.log.LogManager` (所有屬性)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`、`org.apache.sling.commons.log.pattern`)

</details>

### Java 11 執行階段棄用 {#java11-runtime-deprecation}

**Java 11 執行階段**&#x200B;現已棄用，且大多數環境已升級至效能更佳的 **Java 21 執行階段**。

若您的環境因相依性不支援而無法升級 (請參閱 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements))，您應已收到一封 Adobe 發送的電子郵件，其中包含具體的後續步驟。請確保在 **2025 年 8 月 28 日**&#x200B;前完成所有必要的更新，您的環境方能無中斷地進行升級。

備註：執行階段版本與程式碼的建置版本兩者為各自獨立的。雖然我們建議使用 Java 21 進行建置，但目前仍然支援 Java 11 版本。未來會另行公告 Java 11 版本的棄用通知。

### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

如 4 月的發行說明中所述，AEM Java 記錄必須遵循標準格式，以確保在所有客戶環境中皆進行可靠的監視。不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

自 **8 月下旬**&#x200B;開始，所有不支援的自訂記錄覆寫皆會被忽略。根據我們的分析，大多數客戶不會受到影響，而 Adobe 會直接聯繫其目前設定可能受到影響的客戶。

請審閱所有取決於自訂記錄行為的下游流程，並將其更新。例如：

* 若您的記錄轉送系統需要自訂的記錄格式，則可能需要調整攝取規則。
* 若您先前已透過變更記錄等級降低記錄的詳細程度，請注意，恢復至預設等級可能會增加記錄量。

### 預設清除舊版本和稽核記錄 {#mt-defaults}

目前，內容版本和稽核記錄檔的相關&#x200B;*清除維護工作*&#x200B;預設為停用，因此除非明確設定，否則不會移除任何資料。

不過，為了讓存放庫的效能最佳化，自 **2025 年 6 月下旬**&#x200B;開始，會依循以下準則將清除預設為啟用：

#### 內容版本 {#mt-content}

* **新的環境** (建立於即將到來的日期 (稍後通知) 之後)
   * 已存在超過 **30 天**&#x200B;的版本會定期被刪除。
   * 保留過去 30 天內的五個最新版本，以及最新版本和目前版本，無論其已存在多久。

* **現有環境** (建立於此即將到來的日期之前)：
   * 已存在超過 **7 年**&#x200B;的版本會定期被刪除。
   * 保留過去 7 年內的所有版本。
   * 此較高的預設臨界值能防止意外移除最近的資料。然而，若要讓存放庫效能最佳化，建議設定較低的值。

* 您可以透過使用設定管道部署的YAML設定來修改這些預設值。

#### 稽核記錄 {#mt-auditlogs}

* **新的環境** (建立於即將到來的日期之後，該日期將另行通知)：
   * 已存在超過 **7 天**&#x200B;的複寫、DAM 和頁面稽核記錄會定期被刪除。
   * 預設情況下會記錄所有事件。

* **現有環境** (建立於此即將到來的日期之前)：
   * 已存在超過 **7 年**&#x200B;的複寫、DAM 和頁面稽核記錄會定期被刪除。
   * 預設情況下會記錄所有事件。
   * 此較高的預設臨界值能防止意外移除最近的資料。然而，若要讓存放庫效能最佳化，建議設定較低的值。

* 您可以透過使用設定管道部署的YAML設定來修改這些預設值。

如需更多詳細資訊，請參閱[維護任務文章](/help/operations/maintenance.md#defaults)。

### 邊緣運算 (Alpha 版計劃) {#edge-computing}

邊緣運算讓您能夠在 CDN 層執行 JavaScript，使資料處理更為接近一般使用者。因此而減少延遲並達到邊緣的回應式動態體驗。

常見使用案例包含：

* 授予內容存取權之前，透過身分識別提供者對使用者進行身分驗證
* 根據地理位置、裝置類型或使用者屬性，將內容個人化
* 做為 CDN 和您來源之間的中介軟體
* 將第三方 API 的回應傳遞至瀏覽器之前，先對其進行重新格式化 (且可能整合多個 API 的回應)
* 使用從各個後端拼接的內容，在邊緣編寫並提供伺服器轉譯的 HTML

我們針對正式生產網站提供數量有限的 AEM Publish Delivery 或 Edge Delivery Services 專案機會。若您有興趣參與，或想了解更多相關資訊，請傳送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並簡要描述您的使用案例。

### Edge Delivery Services 的 CDN 設定 (Beta 版計劃) {#cdn-eds-beta}

Adobe 管理之 CDN 提供靈活的設定選項，如[設定管道文章](/help/operations/config-pipeline.md#configurations)中所述。

部署設定管道用於包括 CDN 來源選擇器、回應和請求轉換等功能 (現在處於測試階段)。請聯絡 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 並提供您使用案例的詳細資訊。

### AEM 記錄轉送至更多目標 (Beta 版計劃) {#log-forwarding-beta}

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM 已支援將 AEM 和 CDN 記錄轉送至 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。此功能是以自助方式設定，並透過設定管道進行部署。

您可以將 AEM 記錄轉送至 Amazon S3、Sumo Logic 和您自己的 New Relic 帳戶 (非 Adobe 所提供的帳戶) (現在處於測試階段)。請注意，這些記錄目標支援 AEM 記錄 (包括 Apache/Dispatcher)，但不支援 CDN 記錄。傳送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，獲得存取權。

如欲了解更多相關資訊，請參閱[記錄轉送文件](/help/implementing/developing/introduction/log-forwarding.md)。

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
