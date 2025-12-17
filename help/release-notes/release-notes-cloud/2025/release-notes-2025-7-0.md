---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.7.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.7.0 版發行說明。'
feature: Release Information
role: Admin
exl-id: b1d25db0-d4a8-4663-b7fe-2d7381e12567
source-git-commit: 76ccdf13f56d7020ef266bc54bebbcc6eff1067d
workflow-type: tm+mt
source-wordcount: '2273'
ht-degree: 96%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2025.7.0 版發行說明 {#release-notes}

以下章節概述 [!DNL Experience Manager] as a Cloud Service 2025.7.0 版的功能發行說明。

>[!NOTE]
>
>您可以從這裡瀏覽至先前版本 (例如 2023 或 2024 版) 的發行說明。
>
>查看 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解關於 [!DNL Experience Manager] as a Cloud Service 未來功能的啟用。

>[!NOTE]
>
>若要透過每月電子郵件通知，了解 Experience Cloud 發行說明的最新消息，請訂閱 [Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2025.7.0 版) 的發行日期為 2025 年 8 月 7 日。下一個功能版本 (2025.8.0) 規劃於 2025 年 8 月 28 日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新功能 {#enhancements-sites}

* 您現在只需一次操作，即可複製內容片段及其參考片段 (子系)。這樣可以重新使用現有的內容片段結構來建立新內容。
* 現在，在內容片段管理員 UI 中，您可以檢視內容片段的工作流程狀態，其中包含所選取片段過去和目前正在執行之工作流程的詳細資訊。
* 現在，重新命名或移動 Live Copy 來源頁面會觸發重新發佈相應地重新命名或移動的 Live Copy 頁面。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**將形狀新增至 Dynamic Media 範本**

現在，您可以在 Experience Manager Assets 中[將形狀圖層新增至 Dynamic Media 範本](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas)。與影像和文字圖層類似，形狀圖層支援透過範本 URL 使用參數進行即時更新。您也可以在範本中把行動號召 (CTA) 連結加入各個形狀中。

![將形狀新增至 Dynamic Media 範本](/help/assets/assets/enable-uniform-radius-shape.png)

**增強 AI 產生的後設資料**

AEM Assets 現在可讓您在[資產瀏覽頁面上設定用卡片視圖或清單視圖顯示資產標題](/help/assets/smart-tags.md#configure-ai-generated-titles)。您可以選擇顯示您定義的資產標題、使用 AI 產生的標題，或僅於資產沒有現有標題時使用 AI 產生的標題。

![設定 AI 產生的標題](/help/assets/assets/configure-title-ai-generated.png)

您現在也可以選擇在資料夾層級停用 AI 產生的後設資料。

### 全新的 Content Hub 功能 {#new-features-content-hub}

**增強 Content Hub 內的品牌化彈性**

在現有個人化功能的基礎上，Content Hub 現在讓管理員可藉由新增自訂標誌影像來進一步自訂其部署。橫幅和標誌影像也新增支援 TIFF 檔案格式，提供更高的設計彈性。

**使用有標題的連結，共用更有智慧**

現在，您在產生共用連結時可以新增標題，無論是從資產詳細資料視圖，或是在選取一項或多項資產之後。這樣做可以協助收件者輕鬆識別每個連結的用途，尤其是在接收到多項共用資產時。

![私人與公開連結](/help/assets/assets/shared-link-for-assets.png)

**改善篩選器導覽**

現在，Content Hub 的篩選器也包含「**顯示全部**」選項，讓使用者可以檢視所有可用面向以及資產計數，而不必受限於目前只能檢視最多十個面向的限制。增強各個篩選器的搜尋和排序功能，可以更輕鬆、更有效地探索及管理資產。

### AEM 桌面應用程式版本 3.0.0 {#desktop-app-release-3.0.0}

享受新檔案和資料夾自動上傳的功能、增強的檔案操作、更智慧的資產探索，以及與 AEM 的緊密整合，讓內容管理更快速、更清楚，且更加直覺易用。

如需完整的功能清單，請參閱[桌面應用程式發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-desktop-app/using/release-notes)。

### 具有 OpenAPI 功能的 Dynamic Media 之新功能 {#new-features-dynamic-media-with-openapi}

**發佈前預覽資產**

現在，[!DNL Dynamic Media with OpenAPI capabilities] 允許在資產開放使用之前，直接在 [!DNL AEM Sites] 製作頁面預覽資產。與利害關係人分享預覽頁面，收集關於視覺品質及內容契合度的意見。於審閱週期內，在最終確認發佈內容之前，您可以建立與管理多個資產版本。

**增強智慧型影像處理，用於 OpenAPI 影像要求**

現在，所有 OpenAPI 影像要求都能充分善用具有自動升級功能和備用邏輯的智慧型影像處理。此增強功能可以根據裝置和網路條件將影像最佳化，加快頁面載入速度並減少頻寬使用量，同時保持視覺品質。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的新功能 {#forms-new-features}

**適用於自適應表單和表單片段的通用編輯器**

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)現在支援建立自適應表單和可重複使用的表單片段。作者可以在簡化的所見即所得製作環境中視覺化地建置表單、設定提交動作，並新增 reCAPTCHA 驗證。此功能可加速表單建立、增強一致性，並改善對垃圾郵件和自動化濫用的防護。

![通用編輯器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


**適用於 Edge Delivery Services 表單的表單提交服務**

[表單提交服務](/help/forms/forms-submission-service.md)讓您將自適應表單所提交的資料順暢地直接儲存至常用的試算表平台中，例如 Google Sheets、Microsoft OneDrive 或 SharePoint。這樣的整合可以將表單資料直接提交至您選擇的試算表，免除手動轉移資料的作業並減少錯誤，進而簡化資料管理。

主要優勢包括：

* **直接整合：**&#x200B;設定您的表單，將資料直接提交至指定的試算表。
* **自訂資料對應：**&#x200B;將表單欄位對應至相應的試算表欄中，維持資料儲存的條理。
* **存取控制：**&#x200B;善用現有的試算表權限，管理哪些人可以存取或修改已提交的資料。

**從自適應表單產生並同步 AFP 轉譯**

[AFP 輸出同步 API](/help/forms/document-generation-afp-api.md) 讓管理員和使用者能夠從自適應表單產生 AFP (進階功能呈現) 輸出，並將此輸出與外部系統或儲存位置同步。AFP 是一種針對列印最佳化的高效能文件格式，常用於大型企業環境。

<!-- ### New pre-release features in AEM Forms {#forms-new-pre-release-features}

**Enhancements in Rule Editor**

* The `validate` method in the function list now supports validation at the panel, field, and form levels.
* Client-side custom function parsing now supports ES10+ JavaScript features and static imports.
* The button to download Document of Record (DoR) is now available as an out-of-the-box (OOTB) option in the rule editor.
* Rules now support the use of dynamic variables.
* Custom event-based rules are now supported.
* Repeatable panel rules are now executed based on context, rather than only on the last panel instance.
* Rules can now be triggered based on query parameters, UTM parameters, and browser parameters.
* Form-specific custom function scripts are now supported for Adaptive Forms in Edge Delivery Services.

 -->

### 全新 AEM Forms 搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗方案為您提供獨一無二的機會，享有尖端創新功能的獨家存取權，並協助引導這些功能的發展。

這些發行說明列出的是目前版本提供的創新功能。如需搶先體驗方案提供的創新功能之完整清單，請參閱 [AEM Forms 搶先體驗方案文件](/help/forms/early-access-ea-features.md)。


<!-- **Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

**適用於互動式通訊編輯器的規則編輯器**

透過直覺易用的指向與點按介面，直接在文件中建置動態、資料驅動的動作。輕鬆定義條件式邏輯、自動化工作流程，以及將內容個人化，不需要編寫程式碼。

**適用於自訂元件的 AEM Forms 支架 CLI**

>[!VIDEO](https://video.tv.adobe.com/v/3470514/aem-forms scaffolding-aem-custom component generator-aem-forms cli-aem-forms custom component-aem-forms development tool)

使用此 CLI 工具加速開發 AEM Forms Edge Delivery Services。立即產生啟動自訂元件開發所需的程式碼和線路，不需要範本，也沒有麻煩手續。

**動態表單資料 API 整合工具**

表單作者可以利用 API 整合工具來建立動態、智慧的表單，而此表單會根據使用者互動情形，自動從外部 REST API 擷取及填入資料。這項無程式碼整合功能將靜態表單轉換為回應式資料彙集介面。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### 權限管理的節點視圖 {#node-view}

AEM 引進了節點視圖權限管理。其主要功能與傳統使用者介面相同，但更加簡單易用而且有效率。若要了解更多詳細資訊，請參閱[專門文章](/help/security/touch-ui-principal-view.md)。

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

現已棄用 **Java 11 執行階段*，且大多數環境已升級至效能更好的 &#x200B;** Java 21 執行階段**。

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

不過，為了最佳化存放庫效能，系統將在未來公佈的日期預設啟用清除。

如需更多詳細資訊，請參閱[維護任務文章](/help/operations/maintenance.md#defaults)。

#### 內容版本 {#mt-content}

* **新環境** （建立於即將來臨的日期之後，將於稍後通訊）：
   * 將定期刪除超過30天的版本。
   * 保留過去 30 天內的五個最新版本，以及最新版本和目前版本，無論其已存在多久。

* **現有環境** (建立於此即將到來的日期之前)：
   * 將定期刪除超過7年的版本。
   * 保留過去 7 年內的所有版本。
   * 此較高的預設臨界值能防止意外移除最近的資料。然而，若要讓存放庫效能最佳化，建議設定較低的值。

* 您可以透過 YAML 設定來修改這些預設值，並透過設定管道部署。

#### 稽核記錄 {#mt-auditlogs}

* **新的環境** (建立於即將到來的日期之後，該日期將另行通知)：
   * 將定期刪除超過7天的復寫、DAM和頁面稽核記錄。
   * 預設情況下會記錄所有事件。

* **現有環境** (建立於此即將到來的日期之前)：
   * 將定期刪除超過7年的復寫、DAM和頁面稽核記錄。
   * 預設情況下會記錄所有事件。
   * 此較高的預設臨界值能防止意外移除最近的資料。然而，若要讓存放庫效能最佳化，建議設定較低的值。

* 您可以透過 YAML 設定來修改這些預設值，並透過設定管道部署。

### 邊緣運算 (Alpha 版計劃) {#edge-computing}

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

這是現在處於測試階段的功能，可針對內容傳遞網路來源選擇器、回應和請求轉換、內容傳遞網路記錄轉寄等功能部署設定管道。請聯絡 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 並提供您使用案例的詳細資訊。

### RDE 快照 (Alpha 方案) {#rde-snapshot-beta}

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
