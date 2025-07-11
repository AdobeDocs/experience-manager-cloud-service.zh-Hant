---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: c8391e09b7e2888423187f48360423c52b18fe0a
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 90%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.6.0) 的發行日期為 2025 年 6 月 26 日。下一個功能版本 (2025.7.0) 預計於 2025 年 7 月 31 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**資產檢視中強化的後設資料表單管理**

現在您可以將後設資料表單從管理檢視直接匯入資產檢視。在資產檢視中這些表單進行的任何更新皆會自動反映在管理檢視中，從而確保兩種體驗的一致性。此功能支援順暢轉換至新的資產檢視，同時保持與現有後設資料設定的連貫性。

![AI 產生的後設資料](/help/assets/assets/import-metadata-forms-page.png)

### 全新的 Content Hub 功能 {#new-features-content-hub}

**集合治理**

您現在能透過 Content Hub [於建立期間控制對於集合的存取權，確保唯有授權使用者可以檢視或管理分組的資產](/help/assets/collections-content-hub.md##create-collections)。這樣可以確保提高安全性、改善協作、組織資產管理，以及簡化治理。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* [最適化Forms和表單片段的通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)：該通用編輯器現在支援建立最適化Forms和可重複使用的表單片段。 作者能以視覺化方式建立表單、設定提交動作及新增reCAPTCHA驗證，這一切都可在簡化的WYSIWYG製作環境中完成。 此功能可加快表單建立、增強一致性，並改善防範垃圾郵件和自動濫用的防護功能。

### 搶鮮版功能

* [從Adaptive Forms產生並同步AFP轉譯](/help/forms/document-generation-afp-api.md)： AFP Output Sync API可讓管理員和使用者從Adaptive Forms產生AFP （進階功能簡報）輸出，並將輸出與外部系統或儲存位置同步。 AFP是專為列印而最佳化的高效能檔案格式，通常用於大型企業環境。

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

* [整合AEM Forms與Adobe Experience Platform](/help/forms/aem-forms-aep-connector.md)： AEM Forms到Adobe Experience Platform聯結器可讓您順暢整合最適化Forms和Adobe Experience Platform。 此功能可將表單資料對應至XDM結構描述，並即時直接提交至AEP。 它可簡化跨Adobe Experience Cloud解決方案個人化和啟用使用案例的資料擷取。

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

若您的環境因相依性不支援而無法升級 (請參閱 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements))，您應已收到一封 Adobe 傳送的電子郵件，其中包含具體的後續步驟。請確保在 **2025 年 8 月 28 日**&#x200B;前完成所有必要的更新，您的環境方能無中斷地進行升級。

備註：執行階段版本與程式碼的建置版本兩者為各自獨立的。雖然我們建議使用 Java 21 進行建置，但目前仍然支援 Java 11 版本。未來會另行公告 Java 11 版本的棄用通知。

### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

如 4 月的發行說明中所述，AEM Java 記錄必須遵循標準格式，以確保在所有客戶環境中皆進行可靠的監視。不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

自 **8 月下旬**&#x200B;開始，所有不支援的自訂記錄覆寫皆會被忽略。根據我們的分析，大多數客戶將不會受影響，而 Adobe 會直接聯絡其目前設定可能受影響的客戶。

請審閱所有取決於自訂記錄行為的下游流程，並將其更新。例如：

* 若您的記錄轉送系統需要自訂的記錄格式，則可能需要調整攝取規則。
* 若您先前已透過變更記錄等級降低記錄的詳細程度，請注意，恢復至預設等級可能會增加記錄量。

### 預設清除舊版本和稽核記錄 {#mt-defaults}

目前，內容版本和稽核日誌皆將其相關的&#x200B;*清除維護任務*&#x200B;預設為停用，因此除非明確地進行設定，否則不會移除任何資料。

不過，為了將存放庫的效能最佳化，自 **2025 年 7 月上旬**&#x200B;開始，會根據下列準則將清除預設為啟用：

#### 內容版本 {#mt-content}

* **新的環境** (建立於即將到來的日期 (稍後通知) 之後)
   * 已存在超過 **30 天**&#x200B;的版本會定期被刪除。
   * 保留過去 30 天內的五個最新版本，以及最新版本和目前版本，無論其已存在多久。

* **現有環境** (建立於此即將到來的日期之前)：
   * 已存在超過 **7 年**&#x200B;的版本會定期被刪除。
   * 保留過去 7 年內的所有版本。
   * 此較高的預設臨界值能防止意外移除最近的資料。然而，若要讓存放庫效能最佳化，建議設定較低的值。

* 您可以透過 YAML 設定來修改這些預設值，並透過設定管道部署。

#### 稽核記錄 {#mt-auditlogs}

* **新的環境** (建立於即將到來的日期之後，該日期將另行通知)：
   * 已存在超過 **7 天**&#x200B;的複寫、DAM 和頁面稽核記錄會定期被刪除。
   * 預設情況下會記錄所有事件。

* **現有環境** (建立於此即將到來的日期之前)：
   * 已存在超過 **7 年**&#x200B;的複寫、DAM 和頁面稽核記錄會定期被刪除。
   * 預設情況下會記錄所有事件。
   * 此較高的預設臨界值能防止意外移除最近的資料。然而，若要讓存放庫效能最佳化，建議設定較低的值。

* 您可以透過 YAML 設定來修改這些預設值，並透過設定管道部署。

如需更多詳細資訊，請參閱[維護任務文章](/help/operations/maintenance.md#defaults)。

### 邊緣運算 (Alpha 版計劃) {#edge-computing}

邊緣運算讓您能夠在 CDN 層執行 JavaScript，使資料處理更為接近一般使用者。因此而減少延遲並達到邊緣的回應式動態體驗。

常見使用案例包含：

* 授予內容存取權之前，透過身分識別提供者對使用者進行身分驗證
* 根據地理位置、裝置類型或使用者屬性，將內容個人化
* 做為 CDN 和您來源之間的中介軟體
* 將第三方 API 的回應傳送至瀏覽器之前，先對其進行重新格式化 (且可能彙總多個 API 的回應)
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
