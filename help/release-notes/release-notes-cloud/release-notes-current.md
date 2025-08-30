---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 0d2164920ca44ee6c872fdfe2090760a1506215d
workflow-type: tm+mt
source-wordcount: '1961'
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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2025.8.0)的發行日期是2025年8月28日。 下一個功能版本(2025.9.0)計畫於2025年9月25日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md)是您存取所有AEM功能的集中式起點。 它會根據您的使用者角色和您可用的授權進行個人化，讓每位使用者都能有效完成其成果。

## AEM中的AI助理 {#AI-assistant}

適用於AEM的[AI助理](/help/implementing/cloud-manager/ai-assistant-in-aem.md)提供對話式介面，可讓您即時回答AEM產品相關問題（*可供所有使用者使用*），並自動建立支援票證（*可供支援管理員使用*）。 此視覺效果直接內嵌於AEM中，並可從AEM Experience Hub、Cloud Manager及作者UI存取。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新功能 {#enhancements-sites}

* 現在，在內容片段管理員 UI 中，您可以檢視內容片段的工作流程狀態，其中包含所選取片段過去和目前正在執行之工作流程的詳細資訊。
* 在常見情況下，透過UUID而不是透過路徑開啟片段，在新內容片段編輯器中開啟內容片段的效能提高25%。
* 現在，在複製包含參考片段的內容片段時，參考片段的副本會儲存在與父片段副本相同的位置。
* 您現在可以在資料夾設定中設定自訂工作區，以將內容片段匯出至Adobe Target中已設定的工作區。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 全新的 Content Hub 功能 {#new-features-content-hub}

**透過篩選器屬性進行大量搜尋**

Content Hub現在讓您更快找到所需的資產。 使用新的大量搜尋功能，您可以為任何篩選器屬性輸入多個值(以分隔字元（例如，多個SKU ID）分隔)，並使用單一搜尋立即擷取所有相符的資產。

### 具有 OpenAPI 功能的 Dynamic Media 之新功能 {#new-features-dynamic-media-with-openapi}

**SEO友善的DM搭配OpenAPI URL**

使用OpenAPI在DM中建立資產傳送的虛名URL，並以可讀取的短識別碼取代系統產生的長型UUID。 如此可讓連結更符合SEO需求，且更能與您的品牌或行銷活動保持一致。 虛名URL會在執行階段自動解析為原始資產UUID，而不會中斷現有的工作流程。

>[!NOTE]
>
>此功能將在9月10日以有限可用功能的形式提供。 您可以[建立並提交Adobe客戶支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)，以便為您的部署啟用。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Experience Manager Forms中的新功能 {#new-features-forms}

**日期與時間輸入元件**

[日期與時間元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component)現已可用，可讓使用者使用行事曆和時鐘介面，或是以支援的格式手動輸入值，來選取日期與時間。

**加強檔案上傳的錯誤處理**

[檔案附件元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)現在會根據允許清單自動驗證上傳的檔案型別。 如果使用者以不支援的格式上傳檔案，表單會在提交期間顯示錯誤。 元件也會檢查檔案內容以驗證其型別，增強表單的整體安全性。

自訂提交動作的&#x200B;**指定錯誤回應**

當[自訂提交動作](/help/forms/custom-submit-action-troubleshooting.md)發生未處理的錯誤時，系統傳回錯誤代碼502。 這有助於識別問題與自訂提交動作相關，讓您更輕鬆進行偵錯。

**從記錄檔案排除隱藏欄位**

新屬性允許從[記錄檔案](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings)中排除隱藏欄位。 依預設，此選項未選取且適用於所有表單欄位。


### AEM Forms中的搶鮮版功能

**產生並同步AFP轉譯**

您現在可以使用[AEM Forms Communication API](/help/forms/document-generation-afp-api.md)將XDP檔案轉換為AFP格式。 AFP是一種高效能格式，廣泛應用於大型企業印刷。

規則編輯器中的&#x200B;**增強功能**

* [函式清單中的驗證方法](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list)：驗證和重設方法現在支援在面板、欄位和表單層級執行。 之前，系統僅支援表單層級。
* [現代JavaScript支援](/help/forms/rule-editor-core-components-difference-tables.md)：已新增自訂函式的ECMAScript 2019及更新版本功能支援，讓您撰寫更有效率、模組化且可重複使用的程式碼。
* [規則編輯器中的下載DoR選項](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor)：下載記錄檔案(DoR)的函式已在規則編輯器中新增為現成可用的(OOTB)選項。

  ![記錄檔案](/help/forms/assets/document-of-record-rn.gif)

* [規則編輯器中的動態變數](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules)：您現在可以在規則編輯器中使用動態（暫時）變數，以更靈活地定義條件和動作。 儲存暫時值不再需要隱藏欄位。
* [自訂事件型規則支援](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support)：您現在可以定義自訂事件，並根據這些事件觸發規則。
* [內容感知可重複面板規則](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels)：在可重複面板中，規則現在會根據內容執行，而非僅套用至最後一個面板執行個體。
* [由引數觸發的規則](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms)：規則編輯器現在支援根據查詢引數、UTM引數或瀏覽器引數執行規則。
* [表單特定自訂函式](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms)： Edge Delivery Services Forms現在支援表單特定自訂函式指令碼，在管理可重複使用的邏輯方面提供更大的彈性。
* [自訂函式的靜態匯入](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions)： Universal Editor中的規則編輯器現在支援靜態匯入，可讓開發人員組織、共用及重複使用多個表單中的函式。

### 全新 AEM Forms 搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗方案為您提供獨一無二的機會，享有尖端創新功能的獨家存取權，並協助引導這些功能的發展。

這些發行說明列出的是目前版本提供的創新功能。如需搶先體驗方案提供的創新功能之完整清單，請參閱 [AEM Forms 搶先體驗方案文件](/help/forms/early-access-ea-features.md)。

**手寫簽名元件**

您現在可以使用[手寫簽名元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature)來協助使用者將他們的簽名新增至表單，例如在合約表單中。 元件可讓使用者使用滑鼠、手寫筆或觸控熒幕，直接在表單中繪製簽名。

在規則編輯器中&#x200B;**直接API整合**

最適化Forms現在支援在視覺規則編輯器中[直接API整合](/help/forms/api-integration-in-rule-editor.md)，不需要表單資料模型。 作者可使用URL或cURL匯入來設定API、對應輸入/輸出引數，以及使用驗證的安全呼叫。

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

### JavaScript編譯更新 {#javascript-compilation}

預設的使用者端程式庫(clientlibs) JavaScript編譯現在會以ECMASCRIPT_2018為目標，而非ECMASCRIPT5。 雖然此更新在過去可覆寫，但依預設會啟用效能改善、現代JavaScript語法和功能。

### 即將棄用Java API {#java-api-deprecation}

數個已棄用的API將於8月31日目標移除，因此將不再參考。 在9月初，如果偵測到API使用情形，系統會傳送Actions Center通知，9月25日後，在Cloud Manager建置期間會顯示通知，強調移除使用情形的重要性。 如需完整詳細資訊，請參閱[淘汰文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，但為了方便起見，下列API如下：

<details>
  <summary>展開以檢視Java API淘汰</summary>

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

### Java 11 執行階段棄用 {#java11-runtime-deprecation}

*Java 11 執行階段*&#x200B;現已棄用，且大多數環境已升級至效能更佳的 **Java 21 執行階段**。

若您的環境因相依性不支援而無法升級 (請參閱 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements))，您應已收到一封 Adobe 傳送的電子郵件，其中包含具體的後續步驟。請確定所有必要的更新已在&#x200B;**2025年10月1日**&#x200B;前完成，因此您的環境可以升級而不會中斷。

備註：執行階段版本與程式碼的建置版本兩者為各自獨立的。雖然我們建議使用 Java 21 進行建置，但目前仍然支援 Java 11 版本。未來會另行公告 Java 11 版本的棄用通知。

### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

如 4 月的發行說明中所述，AEM Java 記錄必須遵循標準格式，以確保在所有客戶環境中皆進行可靠的監視。不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

從&#x200B;**9月25日**&#x200B;開始，任何不支援的自訂記錄覆寫都會被忽略。 根據我們的分析，大多數客戶將不會受影響，而 Adobe 會直接聯絡其目前設定可能受影響的客戶。

請審閱所有取決於自訂記錄行為的下游流程，並將其更新。例如：

* 若您的記錄轉送系統需要自訂的記錄格式，則可能需要調整攝取規則。
* 若您先前已透過變更記錄等級降低記錄的詳細程度，請注意，恢復至預設等級可能會增加記錄量。

### Edge運算(Beta計畫) {#edge-computing}

邊緣運算讓您能夠在 CDN 層執行 JavaScript，使資料處理更為接近一般使用者。因此而減少延遲並達到邊緣的回應式動態體驗。

常見使用案例包含：

* 授予內容存取權之前，透過身分識別提供者對使用者進行身分驗證
* 根據地理位置、裝置類型或使用者屬性，將內容個人化
* 做為 CDN 和您來源之間的中介軟體
* 將來自協力廠商API的回應重新格式化（並可能彙總多個API回應），然後再傳送給瀏覽器
* 使用從各個後端拼接而成的內容，在邊緣編寫及提供伺服器轉譯的 HTML
* 開放 MCP 伺服器供 ChatGPT 和 Claude 等 LLM 存取自訂工具

我們針對正式生產網站提供數量有限的 AEM Publish Delivery 或 Edge Delivery Services 專案機會。若您有興趣參與，或想了解更多相關資訊，請傳送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並簡要描述您的使用案例。

### Edge Delivery Services 的 CDN 設定 (Beta 版計劃) {#cdn-eds-beta}

Adobe 管理之 CDN 提供靈活的設定選項，如[設定管道文章](/help/operations/config-pipeline.md#configurations)中所述。

現在在Beta版中，您可以為功能部署設定管道，包括CDN來源選擇器、回應和請求轉換、CDN記錄轉送等。 請聯絡 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 並提供您使用案例的詳細資訊。

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
