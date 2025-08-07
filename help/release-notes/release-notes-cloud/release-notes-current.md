---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 3b6d75b13730e920a10bc623947bc8b2d46dc5a9
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 50%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2025.7.0)的發行日期是2025年8月7日。 下一個功能版本(2025.8.0)計畫於2025年8月28日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440931?quality=12&captions=chi_hant)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites 的新功能 {#enhancements-sites}

**內容片段增強功能**

* 您現在可以複製具有子系的內容片段。
* 您現在可以在資料夾設定中設定自訂工作區，以將內容片段匯出至Adobe Target中已設定的工作區。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**將圖案新增至Dynamic Media範本**

您現在可以在Experience Manager Assets中[將圖案圖層](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas)新增至Dynamic Media範本。 形狀圖層與影像和文字圖層類似，透過範本URL支援即時更新的引數。 您也可以在範本中加入圖案的call-to-action (CTA)連結。

![新增配色至Dynamic Media範本](/help/assets/assets/enable-uniform-radius-shape.png)

**AI產生的中繼資料增強功能**

AEM Assets現在可讓您[設定在「資產瀏覽」頁面的「卡片檢視」或「清單檢視」中顯示資產標題](/help/assets/smart-tags.md#configure-ai-generated-titles)。 您可以選擇顯示您定義的資產標題、使用AI產生的標題，或僅在資產沒有現有標題時才使用AI產生的標題。

![設定AI產生的標題](/help/assets/assets/configure-title-ai-generated.png)

您現在也可以選擇在資料夾層級停用AI產生的中繼資料。


### 全新的 Content Hub 功能 {#new-features-content-hub}

**在Content Hub中增強品牌彈性**

Content Hub以現有的個人化功能為基礎，現在可讓管理員透過新增自訂標誌影像來進一步調整部署。 此外，也新增了橫幅與標誌影像的TIFF檔案格式支援，提供更優異的設計彈性。

**更聰明地共用標題連結**

您現在可以在產生共用連結時新增標題 — 不論是從資產詳細資料檢視中或選取一或多個資產後。 這可協助收件者輕鬆識別每個連結的用途，尤其是在接收多個共用資產時。

![私人與公開連結](/help/assets/assets/shared-link-for-assets.png)

**已改善篩選器導覽**

Content Hub現在於篩選器內包含&#x200B;**全部顯示**&#x200B;選項，可讓使用者檢視所有可用多面向以及資產計數（從目前僅檢視最多10個多面向的限制）。 每個篩選器中的增強搜尋和排序功能可讓您更輕鬆地更高效地發現和管理資產。

### AEM案頭應用程式3.0.0版 {#desktop-app-release-3.0.0}

享受自動上傳新檔案和資料夾、增強的檔案作業、更聰明的資產探索，以及與AEM無縫整合，讓內容管理更快速、更清晰、更直覺。

如需完整的功能清單，請參閱[案頭應用程式發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-desktop-app/using/release-notes)。

### Dynamic Media中的新功能搭配OpenAPI功能 {#new-features-dynamic-media-with-openapi}

**發佈前預覽資產**

[!DNL Dynamic Media with OpenAPI capabilities]現在允許直接在[!DNL AEM Sites]作者頁面中預覽資產，然後再公開使用。 與利害關係人共用預覽頁面，以收集關於視覺品質和情境適應的意見回饋。 在稽核週期中，您可以在最終確定多個資產版本以供發佈之前，建立和管理這些版本。

**OpenAPI影像要求的增強智慧型影像處理**

所有OpenAPI影像要求現在都會善用智慧影像與自動促銷和遞補邏輯。 此增強功能會根據裝置和網路狀況最佳化影像，提供更快的頁面載入速度並降低頻寬使用量，同時維持視覺品質。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的新功能 {#forms-new-features}

最適化Forms和表單片段的&#x200B;**通用編輯器**

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)現在支援建立最適化Forms和可重複使用的表單片段。 作者可以在簡化的所見即所得製作環境中視覺化地建置表單、設定提交動作，並新增 reCAPTCHA 驗證。此功能可加速表單建立、增強一致性，並改善對垃圾郵件和自動化濫用的防護。

![通用編輯器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


適用於Edge Delivery Services Forms的&#x200B;**Forms提交服務**

請參閱[Forms提交服務](/help/forms/forms-submission-service.md)。 可讓您順暢地將最適化表單提交中的資料直接儲存至熱門的試算表平台，例如Google Sheets、Microsoft OneDrive或SharePoint。 此整合可讓您直接將表單資料提交至您選擇的試算表，消除手動資料傳輸並減少錯誤，進而簡化資料管理。

主要優點包括：

* **直接整合：**&#x200B;設定您的表單，將資料直接提交至指定的試算表。
* **自訂資料對應：**&#x200B;將表單欄位對應到有組織的儲存空間中的對應試算表欄。
* **存取控制：**&#x200B;利用現有的試算表許可權來管理誰可以存取或修改提交的資料。

**從最適化Forms產生並同步AFP轉譯**

[AFP Output Sync API](/help/forms/document-generation-afp-api.md)可讓系統管理員和使用者從Adaptive Forms產生AFP （進階函式簡報）輸出，並將輸出與外部系統或儲存位置同步。 AFP 是一種針對列印最佳化的高效能文件格式，常用於大型企業環境。

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

### AEM Forms中的全新搶先存取功能 {#forms-new-early-access-features}

AEM Forms搶先體驗計畫為您提供獨一無二的機會，讓您以獨家方式存取尖端創新技術，並幫助打造其開發藍圖。

以下版本說明列出目前版本中提供的創新內容。 如需搶先體驗計劃提供之創新的完整清單，請參閱 [AEM Forms 搶先體驗計劃文件](/help/forms/early-access-ea-features.md)。


<!-- **Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

互動式通訊編輯器的&#x200B;**規則編輯器**

使用直覺式的點選介面，直接在檔案中建立動態的資料驅動動作。 輕鬆定義條件式邏輯、自動化工作流程，以及個人化內容，無需撰寫程式碼。

自訂元件的&#x200B;**AEM Forms Scaffolder CLI**

>[!VIDEO]&#x200B;(https://video.tv.adobe.com/v/3470514/aem-forms scaffolding-aem-custom component generator-aem-forms cli-aem-forms custom component-aem-forms開發工具)

使用此CLI工具加速AEM Forms Edge Delivery Services開發。 立即產生啟動自訂元件開發所需的程式碼和接線 — 無樣板，輕鬆無礙。

動態表單資料的&#x200B;**API整合工具**

API整合工具可讓表單作者建立動態、智慧型的表單，這些表單會根據使用者互動，自動從外部REST API擷取及填入資料。 此無程式碼整合功能可將靜態表單轉換為回應式資料收集介面。


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

**Java 11執行階段* — 現已棄用，且大部分環境已升級至效能更高的&#x200B;**&#x200B;Java 21執行階段**。

若您的環境因相依性不支援而無法升級 (請參閱 [Java 21 執行階段要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements))，您應已收到一封 Adobe 傳送的電子郵件，其中包含具體的後續步驟。請確保在 **2025 年 8 月 28 日**&#x200B;前完成所有必要的更新，您的環境方能無中斷地進行升級。

備註：執行階段版本與程式碼的建置版本兩者為各自獨立的。雖然我們建議使用 Java 21 進行建置，但目前仍然支援 Java 11 版本。未來會另行公告 Java 11 版本的棄用通知。

### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

如 4 月的發行說明中所述，AEM Java 記錄必須遵循標準格式，以確保在所有客戶環境中皆進行可靠的監視。不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

自 **8 月下旬**&#x200B;開始，所有不支援的自訂記錄覆寫皆會被忽略。根據我們的分析，大多數客戶將不會受影響，而 Adobe 會直接聯絡其目前設定可能受影響的客戶。

請審閱所有取決於自訂記錄行為的下游流程，並將其更新。例如：

* 若您的記錄轉送系統需要自訂的記錄格式，則可能需要調整攝取規則。
* 若您先前已透過變更記錄等級降低記錄的詳細程度，請注意，恢復至預設等級可能會增加記錄量。

### 預設清除舊版本和稽核記錄 {#mt-defaults}

目前，內容版本和稽核記錄有它們相關聯的*清除維護任務 — 預設為停用，因此除非明確設定，否則不會移除任何資料。

不過，為了最佳化存放庫效能，依照下列准則，系統將在未來公佈的日期預設啟用清除：

#### 內容版本 {#mt-content}

* **新環境*- (建立於即將來臨的日期之後（稍後通知）
   * 將定期刪除早於**30天* — 的版本。
   * 保留過去 30 天內的五個最新版本，以及最新版本和目前版本，無論其已存在多久。

* **現有環境*- （在此即將到來的日期之前建立）：
   * 將定期刪除早於**7年* — 的版本。
   * 保留過去 7 年內的所有版本。
   * 此較高的預設臨界值能防止意外移除最近的資料。然而，若要讓存放庫效能最佳化，建議設定較低的值。

* 您可以透過 YAML 設定來修改這些預設值，並透過設定管道部署。

#### 稽核記錄 {#mt-auditlogs}

* **新環境*- （建立於即將來臨的日期之後，將另行通訊）：
   * 將定期刪除早於**7天* — 的復寫、DAM和頁面稽核記錄。
   * 預設情況下會記錄所有事件。

* **現有環境*- （在此即將到來的日期之前建立）：
   * 將定期刪除超過**7年* — 的復寫、DAM和頁面稽核記錄。
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
* 公開ChatGPT和Claude等LLM的MCP伺服器，以存取自訂工具

我們針對正式生產網站提供數量有限的 AEM Publish Delivery 或 Edge Delivery Services 專案機會。若您有興趣參與，或想了解更多相關資訊，請傳送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並簡要描述您的使用案例。

### Edge Delivery Services 的 CDN 設定 (Beta 版計劃) {#cdn-eds-beta}

Adobe 管理之 CDN 提供靈活的設定選項，如[設定管道文章](/help/operations/config-pipeline.md#configurations)中所述。

現在在Beta版中，為功能部署設定管道，包括CDN來源選擇器、回應和請求轉換、CDN記錄轉送等。 請聯絡 [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) 並提供您使用案例的詳細資訊。

### RDE快照(Alpha計畫) {#rde-snapshot-beta}

在Alpha中，快速開發環境(RDE)現在支援一項功能，可拍攝程式碼和內容的目前狀態快照，以便稍後復原。 同步可能需要還原的程式碼時，或在開發不同功能之間切換時，這可能很有用。 也可以只將可變內容還原為已知的測試起點。

如果您有興趣提供此功能的意見回饋，請傳送電子郵件給[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

### AEM 記錄轉送至更多目標 (Beta 版計劃) {#log-forwarding-beta}

雖然可以從 Cloud Manager 下載記錄，但許多組織發現將這些記錄串流至偏好的記錄目標是很有幫助的。AEM 已支援將 AEM 和 CDN 記錄轉送至 Azure Blob 儲存體、Datadog、HTTPS、Elasticsearch (和 OpenSearch) 以及 Splunk。此功能是以自助方式設定，並透過設定管道進行部署。

現在處於Beta版，您可以將AEM記錄轉送至Amazon S3、Sumo Logic、Dynatrace和您自己的New Relic帳戶(非Adobe提供的帳戶)。 請注意，這些記錄目標支援 AEM 記錄 (包括 Apache/Dispatcher)，但不支援 CDN 記錄。傳送電子郵件至 [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)，獲得存取權。

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
