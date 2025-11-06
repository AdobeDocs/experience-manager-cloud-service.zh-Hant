---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.8.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.8.0 版發行說明。'
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 96%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.8.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2025.8.0 版的功能發行說明。

>[!NOTE]
>
>您可以從這裡瀏覽至先前版本 (例如 2023 或 2024 版) 的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.8.0 版) 的發行日期為 2025 年 8 月 28 日。下一個功能版本 (2025.9.0 版) 預計於 2025 年 9 月 25 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440931?captions=chi_hant&quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md) 是方便存取集中所有 AEM 功能的起點。可以根據您的使用者角色和可用授權進行個人化，讓每位使用者都能有效率地完成其目標。

## AEM 中的 AI 助理 {#AI-assistant}

AEM 的 [AI 助理](/help/implementing/cloud-manager/ai-assistant-in-aem.md)提供一個對話式介面，其設計目標在於讓您立即取得與 AEM 產品相關問題的答案 (*適用於所有使用者*)，並自動支援票證建立 (*適用於支援管理員)。* AI 助理會直接嵌入 AEM，並且可透過 AEM Experience Hub、Cloud Manager 和 Author UI 存取。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新功能 {#enhancements-sites}

* 現在，在內容片段管理員 UI 中，您可以檢視內容片段的工作流程狀態，其中包含所選取片段過去和目前正在執行之工作流程的詳細資訊。
* 在新的內容片段編輯器中，使用 UUID 而非路徑開啟片段的效能，比一般情況提升 25%。
* 在複製帶有引用片段的內容片段時，現在引用片段的副本儲存在與主版片段副本相同的位置。
* 現在您可以在資料夾設定中設定自訂工作區，將內容片段匯出至 Adobe Target 的設定工作區。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 全新的 Content Hub 功能 {#new-features-content-hub}

**透過篩選器屬性進行批次搜尋**

Content Hub 現在可以更快速地發現您所需的資產。使用新的批次搜尋功能，您可以透過分隔符號隔開，為任何篩選器屬性輸入多個值 (例如，多個 SKU ID)，並使用單一搜尋立即檢索所有相符的資產。

### 具有 OpenAPI 功能的 Dynamic Media 新功能 {#new-features-dynamic-media-with-openapi}

**品牌和可讀取的資產傳遞URL**

運用Dynamic Media中具有OpenAPI的虛名URL，讓具有OpenAPI的Dynamic Media更人性化。 虛名URL允許用簡短的、品牌控制的識別碼取代資產傳送URL中長、系統產生、難以記憶的UUID。 這可讓「虛名」URL變得更短、更易於閱讀和分享，且更能與您的品牌或行銷活動保持一致。 虛名 URL 會在執行階段自動解析為原始資產 UUID，而不會中斷原有的工作流程。

>[!NOTE]
>
>此功能目前以「有限開放」的形式提供。請參閱[此文章](/help/assets/vanity-urls.md)以開始。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* [日期和時間輸入元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component)：現在提供日期和時間元件，讓使用者可以使用行事曆和時鐘介面選取日期和時間，或手動輸入受支援格式的值。
* [檔案上傳的錯誤處理功能強化](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)：檔案附件元件現在會自動根據允許清單驗證上傳的檔案類型。如果使用者以不支援的格式上傳檔案，該表單將在提交過程中顯示錯誤。此元件也檢查檔案內容以驗證其類型，增強表單的整體安全性。
* [自訂提交動作的指定錯誤回應](/help/forms/custom-submit-action-troubleshooting.md)：自訂提交動作遭遇未處理的錯誤時，會傳回錯誤代碼 502。這有助於識別問題是關於自訂提交動作，因此讓除錯更為容易。
* [從記錄文件中排除隱藏欄位](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings)：已新增屬性以允許從記錄文件中排除隱藏欄位。預設情況下，並未選取此選項且適用於所有表單欄位。

### AEM Forms 的預發行功能

* [生成並同步 AFP 轉譯](/help/forms/document-generation-afp-api.md)：您現在可以使用 AEM Forms Communication API 將 XDP 檔案轉換成 AFP 格式。AFP 是一種廣泛應用於大型企業列印的高效能格式。
* **規則編輯器的增強功能**
   * [函數清單中的驗證方法](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list)：現在支援在面板、欄位及表單層級執行驗證和重設方法。之前僅支援在表單層級執行。
   * [現代 JavaScript 支援](/help/forms/rule-editor-core-components-difference-tables.md)：自訂函式現已支援 ECMAScript 2019 及後續版本的功能，讓您可以撰寫更有效率且可重複使用的模組化程式碼。
   * [在規則編輯器中下載 DoR 選項](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor)：在規則編輯器中新增了一項現成可用 (OOTB) 的功能，可用於下載記錄文件 (DoR)。
     ![記錄文件](/help/forms/assets/document-of-record-rn.gif)
   * [規則編輯器中的動態變數](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules)：您現在可以在規則編輯器中使用動態 (臨時) 變數，以更靈活地定義條件和動作。儲存臨時值不再需要隱藏欄位。
   * [自訂事件型規則支援](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support)：您現在可以定義自訂事件並根據那些事件觸發規則。
   * [上下文感知可重複面板規則](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels)：在可重複面板中，現在規則是根據上下文執行，而不是僅套用於最後一個面板實例。
   * [參數觸發的規則](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms)：規則編輯器現在支援根據查詢參數、UTM 參數或瀏覽器參數的規則執行。
   * [表單專用自訂函數](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms)：Edge Delivery Services Forms 現在支援表單專用的自訂函數指令碼，為管理可重複使用的邏輯提供更大的靈活性。
   * [自訂函數的靜態匯入](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions)：通用編輯器中的規則編輯器現在支援靜態匯入，讓開發人員可以跨多個表單整理、共用和重複使用函數。

### AEM Forms 的早期採用者功能

* [手寫簽名元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature)：您現在可以使用手寫簽名元件。協助使用者將其簽名新增至表單中，例如合約表單。該元件讓使用者使用滑鼠、手寫筆或觸控螢幕，直接在表單中書寫其簽名。
* [規則編輯器中的直接 API 整合](/help/forms/api-integration-in-rule-editor.md)：自適應表單現在支援視覺化規則編輯器中的直接 API 整合，而無需表單資料模型。作者可以透過 URL 或 cURL 匯入來設定 API、對應輸入/輸出參數，同時透過驗證保護呼叫的安全。

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### JavaScript 編譯更新 {#javascript-compilation}

預設用戶端程式庫 (clientlibs) JavaScript 編譯現在以 ECMASCRIPT_2018 為目標，而不是 ECMASCRIPT5。雖然過去可以覆寫，但此更新預設啟用效能提升、現代 JavaScript 語法及相關功能。

### Java API 即將淘汰 {#java-api-deprecation}

許多已淘汰的 API 將於 8 月 31 日移除，因此不應再引用。在 9 月初，若偵測到使用 API 的情形，系統將透過動作中心傳送通知；而 9 月 25 日之後，在 Cloud Manager 建置時也會顯示通知，以強調移除使用的重要性。請參閱[棄用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整的詳細資訊，但為了方便起見，這些 API 條列如下：

<details>
  <summary>展開以查看 Java API 淘汰內容</summary>

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

</details>

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### 棄用 Java 11 執行階段 {#java11-runtime-deprecation}

*Java 11 執行階段*&#x200B;現已棄用，且大多數環境已升級至效能更佳的 **Java 21 執行階段**。

若您的環境因相依性不支援而無法升級 (請參閱 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements))，您應已收到一封 Adobe 傳送的電子郵件，其中包含具體的後續步驟。請確保在 **2025 年 10 月 1 日**&#x200B;前完成所有必要的更新，以便您的環境可以無中斷地進行升級。

備註：執行階段版本與程式碼的建置版本兩者為各自獨立的。雖然我們建議使用 Java 21 進行建置，但目前仍然支援 Java 11 版本。未來會另行公告 Java 11 版本的棄用通知。

### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

如 4 月的發行說明中所述，AEM Java 記錄必須遵循標準格式，以確保在所有客戶環境中皆進行可靠的監視。不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

自 **9 月 25 日**&#x200B;開始，將忽略所有不受支援的自訂記錄覆寫。根據我們的分析，大多數客戶將不會受影響，而 Adobe 會直接聯絡其目前設定可能受影響的客戶。

請審閱所有取決於自訂記錄行為的下游流程，並將其更新。例如：

* 若您的記錄轉送系統需要自訂的記錄格式，則可能需要調整攝取規則。
* 若您先前已透過變更記錄等級降低記錄的詳細程度，請注意，恢復至預設等級可能會增加記錄量。

### Edge 運算 (Beta 版方案) {#edge-computing}

邊緣運算讓您能夠在 CDN 層執行 JavaScript，使資料處理更為接近一般使用者。因此而減少延遲並達到邊緣的回應式動態體驗。

常見使用案例包含：

* 授予內容存取權之前，透過身分識別提供者對使用者進行身分驗證
* 根據地理位置、裝置類型或使用者屬性，將內容個人化
* 做為 CDN 和您來源之間的中介軟體
* 將第三方 API 的回應傳送至瀏覽器之前，先對其進行重新格式化 (且可能彙總多個 API 的回應)
* 使用從各個後端拼接而成的內容，在邊緣編寫及提供伺服器轉譯的 HTML
* 開放 MCP 伺服器供 ChatGPT 和 Claude 等 LLM 存取自訂工具

我們針對正式生產網站提供數量有限的 AEM Publish Delivery 或 Edge Delivery Services 專案機會。若您有興趣參與，或想了解更多相關資訊，請傳送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並簡要描述您的使用案例。

### Edge Delivery Services 的 CDN 設定 (Beta 版計劃) {#cdn-eds-beta}

Adobe 管理之 CDN 提供靈活的設定選項，如[設定管道文章](/help/operations/config-pipeline.md#configurations)中所述。

這是現在處於測試階段的功能，您可針對內容傳遞網路來源選擇器、回應和要求轉換、內容傳遞網路記錄轉寄等功能部署設定管道。請聯絡 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 並提供您使用案例的詳細資訊。

### RDE 快照 (Alpha 方案) {#rde-snapshot-program}

在 Alpha 版本中，快速開發環境 (RDE) 現在支援對程式碼和內容的目前狀態進行快照的功能，這些快照可以在之後還原。在同步可能需要復原的程式碼，或在不同功能的開發之間切換時，此功能很實用。您也可以僅還原可變內容做為測試的已知起點。

如果您有興趣對此功能提供意見，請寄送電子郵件至 [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### AEM 記錄轉送至更多目標 (Beta 版計劃) {#log-forwarding-beta}

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM 已支援將 AEM 和 CDN 記錄轉送至 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。此功能是以自助方式設定，並透過設定管道進行部署。

此功能現在處於測試階段，您可以將 AEM 記錄轉寄至 Amazon S3、Sumo Logic、Dynatrace 和您自己的 New Relic 帳戶 (非 Adobe 提供的帳戶)。請注意，這些記錄目標支援 AEM 記錄 (包括 Apache/Dispatcher)，但不支援 CDN 記錄。傳送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，獲得存取權。

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
