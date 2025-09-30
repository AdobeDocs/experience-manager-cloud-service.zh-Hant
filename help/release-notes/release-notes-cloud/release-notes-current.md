---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: f5510d83ed2ff52496fd7e83ba29010684731938
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 46%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2025.9.0)的發行日期是2025年9月25日。 下一個功能版本(2025.10.0)計畫於2025年10月30日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites發行前版本的新功能 {#prerelease-sites}

AEM內容片段的內容模型編輯器已經過現代化，以與AEM中的其他React頻譜型介面保持一致。 其使用者介面實作和擴充性模型現在與內容片段編輯器和通用編輯器一致。 現在，從新的內容模型管理員UI開啟新模型編輯器時，預設會使用它。 在觸控式UI中開啟內容模型會開啟觸控式UI編輯器，並提供選項供您試用新編輯器。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets檢視中的新功能 {#new-features-assets-view}

**Dynamic Media範本中含子字串的增強文字格式**

您現在可以套用格式至Dynamic Media範本文字圖層中的子字串。 選取的文字或片語會被視為單獨的圖層，讓您可調整其字型、字型大小、顏色等。 子字串層已引數化，因此您可以使用範本的傳遞URL即時更新

### 具有 OpenAPI 功能的 Dynamic Media 新功能 {#new-features-dynamic-media-with-openapi}

**帶有 OpenAPI URL 的 SEO 友善 DM**

在 DM 中使用 OpenAPI 為資產傳遞建立自訂虛名 URL，以簡短易讀的識別碼取代系統產生的冗長 UUID。這讓連結更為 SEO 友善，而且更符合您的品牌或活動。虛名 URL 會在執行階段自動解析為原始資產 UUID，而不會中斷原有的工作流程。

>[!NOTE]
>
>此功能是以「有限可用性」功能提供。 您可以[建立並提交 Adobe 客戶支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)，以針對您的部署將其啟用。

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Experience Manager Forms 的新功能 {#new-features-forms}

**呼叫SharePoint清單附件的表單資料模型工作流程步驟**

「叫用表單資料模型」工作流程步驟現在支援在SharePoint清單型表單資料模型中處理Base64編碼附件陣列的工作流程端中繼資料。 透過此增強功能，工作流程步驟可以傳遞、儲存及擷取每個附件的中繼資料，例如檔案名稱、MIME型別和自訂屬性。 此功能可讓您進行更全面的資料管理，並有助於順暢的下游整合。 如需詳細資訊，請參閱SharePoint清單附件的叫用表單資料模型工作流程步驟中的[增強支援](/help/forms/aem-forms-workflow-step-reference.md#invoke-form-data-model-fdm-service-step)。

### AEM Forms 的預發行功能

**規則編輯器增強功能**

規則編輯器現在支援增強型導覽，並允許在輸入引數中使用函式和數學運算式。

**事件承載支援的增強型導覽**

Invoke Service處理常式中的`Navigate To`動作現在支援`EVENT_PAYLOAD`，可讓表單作者根據事件回應設定後續動作。 此增強功能提供在設計提交後工作流程時更大的彈性，確保更順暢的轉換和更個人化的使用者體驗。 如需詳細資訊，請參閱[支援事件承載的增強型導覽](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service)。

輸入引數中的&#x200B;**函式和數學運算式支援**

輸入引數現在支援函式呼叫和數學運算式，讓表單作者可直接傳遞動態計算的值。 此增強功能可簡化規則設定、免除額外欄位的需求，並讓表單更能適應複雜的邏輯和計算驅動案例。 如需詳細資訊，請參閱輸入引數[中的](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters)函式與數學運算式支援。

### 全新 AEM Forms 搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗方案為您提供獨一無二的機會，享有尖端創新功能的獨家存取權，並協助引導這些功能的發展。

這些發行說明列出的是目前版本提供的創新功能。如需搶先體驗方案提供的創新功能之完整清單，請參閱 [AEM Forms 搶先體驗方案文件](/help/forms/early-access-ea-features.md)。

**互動式通訊編輯器中的PDF預覽**

使用者可以預覽沒有資料的Interactive Communications PDF、本機JSON資料檔案或資料模型中的資料，啟用彈性的資料導向測試。 如需詳細資訊，請參閱[互動式通訊編輯器中的PDF預覽](/help/forms/interactive-communication/pdf-preview-in-interactive-communication-editor-with-different-data-options.md)。

**互動式通訊支援自訂字型**

「自訂字型」功能可讓使用者在互動式通訊中嵌入自訂或組織核准的字型，以確保跨裝置和平台呈現一致且品牌化的PDF。 如需詳細資訊，請參閱[互動式通訊支援自訂字型](/help/forms/interactive-communication/add-custom-fonts-to-interactive-communication-editor.md)。

**匯入和匯出互動式通訊**

此功能可讓您在不同環境中移轉及重複使用互動式通訊。 您現在可以從一個環境匯出互動式通訊及其相關片段和資料模型，並將其匯入另一個環境。 如需詳細資訊，請參閱[匯入和匯出互動式通訊](/help/forms/interactive-communication/import-and-export-interactive-communications.md)。

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

上線日、直播活動、銷售高峰 — 這些時刻無法中斷。 [我們新的自助服務功能](/help/implementing/deploying/quiet-hours-update-free-periods.md)會在重要時停止自動維護更新，讓您的團隊保持專注。

* 安靜時間：封鎖每天在設定時間進行的自動維護。 適合工作時間、夜間跑步或早上切換。
* 免更新期間：封鎖整週的自動維護。 將其用於啟動、促銷活動或每年凍結。

>[!NOTE]
>
>9月25日以有限可用性功能提供。
>&#x200B;>請傳送電子郵件給[aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com)，讓它在您的程式中啟動。

### 適用於Eclipse的AEM開發人員工具新版本 {#aem-develeper-tools-for-eclipse}

適用於Eclipse的AEM開發人員工具1.4.0版已發行。 此版本新增對Eclipse IDE 2022-12或更新版本的支援，且已透過目前版本(2025-09)驗證。 此工具現在可搭配新版AEM Project Archetype使用，並整合了Sling IDE Tooling 1.3.0的改良功能。

從[Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse)安裝，並參閱[AEM開發人員工具頁面](https://eclipse.adobe.com)以取得詳細資訊。

### Java API 即將淘汰 {#java-api-deprecation}

8月31日，有數個過時的API標示為要移除，因此不應再加以參照。 如果在程式碼中偵測到已棄用的API使用方式，您將會收到動作中心通知，11月13日後，Cloud Manager建置期間將會出現通知，強調移除使用方式的重要性。 請參閱[棄用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整的詳細資訊，但為了方便起見，這些 API 條列如下：

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

### Java 11 執行階段棄用 {#java11-runtime-deprecation}

已棄用&#x200B;*Java 11執行階段*，且大部分環境已升級至效能較高的&#x200B;**Java 21執行階段**。

如果因為不受支援的相依性而無法升級您的環境（請參閱[Java 21執行階段需求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)），您應該已經收到來自Adobe的電子郵件，其中包含後續步驟。 如該處所述，Adobe已於2025年9月18日&#x200B;**升級**&#x200B;開發&#x200B;**和** RDE **環境**，以便您驗證網站和程式並解決任何問題。 **階段**&#x200B;和&#x200B;**生產**&#x200B;的升級將於&#x200B;**2025年10月14日**&#x200B;進行。

>[!NOTE]
>
>執行階段版本與您的程式碼組建版本不同。 雖然我們建議您使用Java 21建置，但目前仍接受Java 11建置。 未來會另行公告 Java 11 版本的棄用通知。

### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

如 4 月的發行說明中所述，AEM Java 記錄必須遵循標準格式，以確保在所有客戶環境中皆進行可靠的監視。不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

從&#x200B;**10月30日**&#x200B;開始，將忽略任何不支援的自訂記錄覆寫。 根據我們的分析，大多數客戶將不會受影響，而 Adobe 會直接聯絡其目前設定可能受影響的客戶。

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

### 適用於Edge Delivery Services的Edge驗證(Beta計畫) {#edge-authentication}

Edge驗證可讓您將存取Edge Delivery Services頁面的許可權限製為僅供已透過您的身分提供者(IdP)驗證的使用者存取。 這是透過部署OpenID Connect (OIDC)組態YAML檔案來達成。

如有需要，請傳送電子郵件給[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，提供使用案例的簡短說明，以及您可能會有的任何問題。

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### Canary生產部署，以便在接受即時流量之前測試程式碼(Beta計畫) {#canary-beta}

在將生產組建公開給使用者之前，先使用僅限內部的測試流量來驗證它。 送貨至生產環境、僅路由Canary流量（使用特殊標題）、監控行為，然後升級至即時流量或回覆，而不會影響客戶。

將您的程式碼發行部署到生產環境，但在決定是否接受即時流量和復原之前，請將其限製為僅內部測試流量。

電子郵件[aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com)以要求存取權並分享意見。

### RDE 快照 (Alpha 方案) {#rde-snapshot-program}

在 Alpha 版本中，快速開發環境 (RDE) 現在支援對程式碼和內容的目前狀態進行快照的功能，這些快照可以在之後還原。在同步可能需要復原的程式碼，或在不同功能的開發之間切換時，此功能很實用。您也可以僅還原可變內容做為測試的已知起點。

如果您有興趣對此功能提供意見，請寄送電子郵件至 [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### AEM 記錄轉送至更多目標 (Beta 版計劃) {#log-forwarding-beta}

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM 已支援將 AEM 和 CDN 記錄轉送至 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。此功能是以自助方式設定，並透過設定管道進行部署。

此功能現在處於測試階段，您可以將 AEM 記錄轉寄至 Amazon S3、Sumo Logic、Dynatrace 和您自己的 New Relic 帳戶 (非 Adobe 提供的帳戶)。請注意，這些記錄目標支援 AEM 記錄 (包括 Apache/Dispatcher)，但不支援 CDN 記錄。傳送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，獲得存取權。

如欲了解更多相關資訊，請參閱[記錄轉送文件](/help/implementing/developing/introduction/log-forwarding.md)。

### 擴充應用程式效能監控(APM) (Alpha程式) {#apm-alpha}

為方便觀察，AEM Cloud Service目前支援Adobe提供的[New Relic One](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic)和客戶管理的[Dynatrace](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace)。 在我們探索其他APM選項的支援時，請透過電子郵件寄給我們：[aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com)，請連絡您偏好的廠商或技術，並提供使用案例。


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
