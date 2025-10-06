---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: f5510d83ed2ff52496fd7e83ba29010684731938
workflow-type: ht
source-wordcount: '1957'
ht-degree: 100%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.9.0) 的發行日期為 2025 年 9 月 25 日。下一個功能版本 (2025.10.0) 規劃於 2025 年 10 月 30 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 預發行的新功能 {#prerelease-sites}

AEM 內容片段的內容模型編輯器經過現代化，與 AEM 中其他 React Spectrum 型介面保持一致。其使用者介面實施方式和擴充性模型，現在與內容片段編輯器及通用編輯器一致。現在，從新的內容模型管理員使用者介面開啟時，預設會使用新的模型編輯器。在觸控式使用者介面中開啟內容模型，會開啟觸控式使用者介面編輯器，並建議您試用新的編輯器。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 資產視圖的新功能 {#new-features-assets-view}

**增強 Dynamic Media 範本中子字串的文字格式**

您現在可以將格式套用至 Dynamic Media 範本文字圖層中的子字串。所選取的單字或片語會視為獨立的圖層，您可以調整其字型、字體大小、顏色等。子字串圖層已參數化，因此您可以使用範本的傳遞 URL 進行即時更新

### 具有 OpenAPI 功能的 Dynamic Media 新功能 {#new-features-dynamic-media-with-openapi}

**帶有 OpenAPI URL 的 SEO 友善 DM**

在 DM 中使用 OpenAPI 為資產傳遞建立自訂虛名 URL，以簡短易讀的識別碼取代系統產生的冗長 UUID。這讓連結更為 SEO 友善，而且更符合您的品牌或活動。虛名 URL 會在執行階段自動解析為原始資產 UUID，而不會中斷原有的工作流程。

>[!NOTE]
>
>此功能目前以「有限開放」的形式提供。您可以[建立並提交 Adobe 客戶支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)，以針對您的部署將其啟用。

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Experience Manager Forms 的新功能 {#new-features-forms}

**SharePoint 清單附件的叫用表單資料模型工作流程步驟**

現在，「叫用表單資料模型」工作流程步驟支援處理 SharePoint 清單型表單資料模型中 Base64 編碼附件陣列的工作流程端後設資料。透過此增強功能，工作流程步驟可以傳遞、儲存及檢索每個附件的後設資料，例如檔案名稱、MIME 類型和自訂屬性。此功能讓您能夠進行更全面的資料管理，並有助於順暢的下游整合。如需詳細資訊，請參閱[增強支援 SharePoint 清單附件的叫用表單資料模型工作流程步驟](/help/forms/aem-forms-workflow-step-reference.md#invoke-form-data-model-fdm-service-step)。

### AEM Forms 的預發行功能

**規則編輯器增強功能**

規則編輯器現在支援增強型導覽，並允許在輸入參數中使用函數和數學運算式。

**支援事件承載的增強型導覽**

叫用服務處理常式中的 `Navigate To` 動作現在支援 `EVENT_PAYLOAD`，讓表單作者能夠根據事件回應設定後續動作。此增強功能讓提交後工作流程之設計擁有更大的彈性，確保轉變過程更加順暢，並提供更加個人化的使用者體驗。如需詳細資訊，請參閱[支援事件承載的增強型導覽](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service)。

**支援在輸入參數中使用函數和數學運算式**

輸入參數現在支援函數呼叫和數學運算式，讓表單作者能夠直接傳遞動態運算所得出的值。此增強功能可以簡化規則設定，不需要增加額外的欄位，並讓表單更能適應需要複雜邏輯判斷以及由複雜計算驅動的情境。如需詳細資訊，請參閱[支援在輸入參數中使用函數和數學運算式](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters)。

### 全新 AEM Forms 搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗方案為您提供獨一無二的機會，享有尖端創新功能的獨家存取權，並協助引導這些功能的發展。

這些發行說明列出的是目前版本提供的創新功能。如需搶先體驗方案提供的創新功能之完整清單，請參閱 [AEM Forms 搶先體驗方案文件](/help/forms/early-access-ea-features.md)。

**互動式通訊編輯器中的 PDF 預覽**

使用者可以預覽不包含資料、包含本機 JSON 資料檔案，或包含來自資料模型之資料的互動式通訊 PDF，藉此彈性地進行資料驅動測試。如需詳細資訊，請參閱[互動式通訊編輯器中的 PDF 預覽](/help/forms/interactive-communication/pdf-preview-in-interactive-communication-editor-with-different-data-options.md)。

**互動式通訊支援自訂字型**

透過自訂字型功能，使用者能夠在互動式通訊中嵌入自訂或組織核准的字型，確保在各種裝置和平台上呈現一致的品牌化 PDF 渲染。如需詳細資訊，請參閱[互動式通訊支援自訂字型](/help/forms/interactive-communication/add-custom-fonts-to-interactive-communication-editor.md)。

**匯入與匯出互動式通訊**

透過這項功能，可以在不同的環境之間移轉及重複使用互動式通訊。您現在可以從一個環境中匯出互動式通訊及其相關片段和資料模型，然後將這些匯入另一個環境中。如需詳細資訊，請參閱[匯入與匯出互動式通訊](/help/forms/interactive-communication/import-and-export-interactive-communications.md)。

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### 發行管理中的新功能 {#new-features-release-management}

**暫停自動維護更新**

上線日、現場活動、銷售高峰，這些時刻無法中斷。[我們新的自助服務功能](/help/implementing/deploying/quiet-hours-update-free-periods.md)會在重要時刻停止自動維護更新，讓您的團隊保持專注。

* 暫停更新時段：在每天固定的時段內停止自動維護。適合在工作時間、夜間執行或早晨切換時使用。
* 暫停更新期間：一整週皆停止自動維護。在發佈期間、促銷活動或年度凍結時使用。

>[!NOTE]
>
>於 9 月 25 日以「有限開放」功能的形式提供。
>>寄送電子郵件至 [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com)，以便在您的方案中啟動此功能。

### Eclipse 適用的 AEM 開發人員工具新版本 {#aem-develeper-tools-for-eclipse}

Eclipse 適用的 AEM 開發人員工具 1.4.0 版已發行。此版本新增對 Eclipse IDE 2022-12 或以上版本的支援，且已通過最新版本 (2025-09) 的驗證。此工具現在可以搭配新版 AEM 專案原型使用，並整合 Sling IDE Tooling 1.3.0 的改良功能。

從 [Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse) 進行安裝，並參閱 [AEM 開發人員工具頁面](https://eclipse.adobe.com)了解詳細資訊。

### Java API 即將棄用 {#java-api-deprecation}

數個已棄用的 API 已標記要於 8 月 31 日移除，因此不應再參照。若在您的程式碼中偵測到使用已棄用 API 的情形，您會收到行動中心通知，而在 11 月 13 日之後，Cloud Manager 建置期間會顯示相關通知，強調不再使用此類 API 的重要性。請參閱[棄用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整的詳細資訊，但為了方便起見，這些 API 條列如下：

+++ 展開以查看 Java API 淘汰內容

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

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### 棄用 Java 11 執行階段 {#java11-runtime-deprecation}

*Java 11 執行階段*&#x200B;已棄用，且大多數環境已升級至效能更佳的 **Java 21 執行階段**。

若您的環境因不支援相依性而無法升級 (請參閱 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements))，您應該已收到 Adobe 寄送的電子郵件，向您說明後續步驟。如該內容所述，Adobe 已於 **2025 年 9 月 18 日**&#x200B;升級 **Dev** 和 **RDE** 環境，因此您可以驗證您的網站和程序，並解決任何遇到的問題。**中繼**&#x200B;和&#x200B;**生產**&#x200B;將於 **2025 年 10 月 14 日**&#x200B;進行升級。

>[!NOTE]
>
>執行階段版本與您的程式碼建置版本是各自獨立的。雖然我們建議使用 Java 21 進行建置，但目前仍然接受 Java 11 的建置版本。未來會另行公告 Java 11 版本的棄用通知。

### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

如 4 月的發行說明中所述，AEM Java 記錄必須遵循標準格式，以確保在所有客戶環境中皆進行可靠的監視。不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

從 **10 月 30 日**&#x200B;開始，將忽略所有不受支援的自訂記錄覆寫。根據我們的分析，大多數客戶將不會受影響，而 Adobe 會直接聯絡其目前設定可能受影響的客戶。

請審閱所有取決於自訂記錄行為的下游流程，並將其更新。例如：

* 若您的記錄轉送系統需要自訂的記錄格式，則可能需要調整攝取規則。
* 若您先前已透過變更記錄等級降低記錄的詳細程度，請注意，恢復至預設等級可能會增加記錄量。

### Edge 運算 (Beta 版方案) {#edge-computing}

邊緣運算讓您能夠在 CDN 層執行 JavaScript，使資料處理更為接近一般使用者。因此而減少延遲並達到邊緣的回應式動態體驗。

常見使用案例包含：

* 根據地理位置、裝置類型或使用者屬性，將內容個人化
* 做為 CDN 和您來源之間的中介軟體
* 將第三方 API 的回應傳送至瀏覽器之前，先對其進行重新格式化 (且可能彙總多個 API 的回應)
* 使用從各個後端拼接而成的內容，在邊緣編寫及提供伺服器轉譯的 HTML
* 開放 MCP 伺服器供 ChatGPT 和 Claude 等 LLM 存取自訂工具

我們針對正式生產網站提供數量有限的 AEM Publish Delivery 或 Edge Delivery Services 專案機會。若您有興趣參與，或想了解更多相關資訊，請傳送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並簡要描述您的使用案例。

### Edge Delivery Services 的 Edge 驗證 (Beta 版方案) {#edge-authentication}

透過 Edge 驗證，您可以限制 Edge Delivery Services 頁面的存取權，僅允許通過您的身分提供者 (IdP) 驗證的使用者存取。部署 OpenID Connect (OIDC) 設定 YAML 檔案即可做到上述動作。

若有興趣，請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，簡短說明您的使用案例以及任何問題。

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### Canary 生產部署，以便在接受即時流量之前測試程式碼 (Beta 版方案) {#canary-beta}

向一般使用者公開之前，先使用僅限內部的測試流量驗證生產建置版本。運送至生產環境、僅路由 Canary 流量 (使用特殊標頭)、監視行為，然後升級至即時流量或復原，而不會影響客戶。

將您的程式碼版本部署至生產環境，但在決定要接受即時流量或復原之前，將其限制為僅限內部測試流量。

寄送電子郵件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) 來請求存取權及提供意見回饋。

### RDE 快照 (Alpha 方案) {#rde-snapshot-program}

在 Alpha 版本中，快速開發環境 (RDE) 現在支援對程式碼和內容的目前狀態進行快照的功能，這些快照可以在之後還原。在同步可能需要復原的程式碼，或在不同功能的開發之間切換時，此功能很實用。您也可以僅還原可變內容做為測試的已知起點。

如果您有興趣對此功能提供意見，請寄送電子郵件至 [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### AEM 記錄轉送至更多目標 (Beta 版計劃) {#log-forwarding-beta}

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM 已支援將 AEM 和 CDN 記錄轉送至 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。此功能是以自助方式設定，並透過設定管道進行部署。

此功能現在處於測試階段，您可以將 AEM 記錄轉寄至 Amazon S3、Sumo Logic、Dynatrace 和您自己的 New Relic 帳戶 (非 Adobe 提供的帳戶)。請注意，這些記錄目標支援 AEM 記錄 (包括 Apache/Dispatcher)，但不支援 CDN 記錄。傳送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，獲得存取權。

如欲了解更多相關資訊，請參閱[記錄轉送文件](/help/implementing/developing/introduction/log-forwarding.md)。

### 擴充應用程式效能監視 (APM) (Alpha 版方案) {#apm-alpha}

為便於觀察，AEM Cloud Service 目前支援 Adobe 提供的 [New Relic One](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) 和客戶管理的 [Dynatrace](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace)。由於我們仍在探索其他 APM 選項支援，請寄送電子郵件至 [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) 與我們聯絡，告知您偏好的供應商或技術，並提供使用案例。


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
