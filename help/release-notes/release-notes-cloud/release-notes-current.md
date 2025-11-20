---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 33655e7d58f19a5637ad120d8df537015f2f0aec
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 67%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2025.11.0)的發行日期是2025年11月20日。 下一個功能版本(2025.12.0)計畫於2025年12月11日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440931?captions=chi_hant&quality=12)

-->

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

<!-- ### Pre-Release features in AEM Forms 

**Rule Editor Enhancements**

The Rule Editor now supports enhanced navigation and allows use of function and mathematical expressions in input parameters.

**Enhanced Navigation with Event Payload Support**
 
The `Navigate To` action in the Invoke Service handlers now supports `EVENT_PAYLOAD`, enabling form authors to configure follow-up actions based on event responses. This enhancement offers greater flexibility in designing post-submission workflows, ensuring smoother transitions and more personalized user experiences. For more information, see [Enhanced Navigation with Event Payload Support](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Function and Mathematical Expression Support in Input Parameters**
 
Input parameters now support both function calls and mathematical expressions, enabling form authors to pass dynamically computed values directly. This enhancement streamlines rule configurations, eliminates the need for extra fields, and makes forms more adaptable to complex logic and calculation-driven scenarios. For more information, see [Function and Mathematical Expression Support in Input Parameters](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters). -->

### 全新 AEM Forms 搶先體驗功能 {#forms-new-early-access-features}

AEM Forms 搶先體驗方案為您提供獨一無二的機會，享有尖端創新功能的獨家存取權，並協助引導這些功能的發展。

這些發行說明列出的是目前版本提供的創新功能。如需搶先體驗方案提供的創新功能之完整清單，請參閱 [AEM Forms 搶先體驗方案文件](/help/forms/early-access-ea-features.md)。

#### 互動式通訊增強功能

##### 範本鎖定

鎖定範本中的內容和版面配置元素，以維持品牌完整性並防止未經授權的修改。 這可確保所有通訊的設計一致性。

##### 內容溢位支援

針對流程版面引入「允許在內容內分頁」選項。 此增強功能可讓您順暢地編輯多頁，以及更出色的複雜檔案文字管理。

##### XDP檔案編輯

互動式通訊編輯器現在支援XDP編輯，包括片段整合。 您現在可以在瀏覽器中編輯XDP檔案，而不是只在Forms Windows案頭上執行的Microsoft Designer。

##### 動態頁面編號

在主版頁面上自動顯示「第#頁，共#頁」，以在多頁檔案中進行清晰、一致的分頁。

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

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation新功能 {#foundation-new}

#### Java API 即將棄用 {#java-api-deprecation}

數個已棄用的 API 已標記要於 8 月 31 日移除，因此不應再參照。如果在程式碼中偵測到過時的API使用方式，您將會收到動作中心通知，12月3日後，Cloud Manager建置期間將會顯示通知，強調移除使用方式的重要性。 請參閱[棄用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整的詳細資訊，但為了方便起見，這些 API 條列如下：

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

#### 棄用 Java 11 執行階段 {#java11-runtime-deprecation}

Adobe已於2025年10月14日將&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;環境升級為效能較高的&#x200B;**Java 21執行階段**。 自&#x200B;**1月**&#x200B;下旬開始，AEM Cloud Service SDK或任何雲端環境都不會搭配Java 11執行階段使用。

>[!NOTE]
>
> 若要利用最新的效能最佳化和語言增強功能，建議使用Java 17或Java 21 （偏好設定）建置。 目前仍支援使用Java 8和Java 11進行建置，但即將發行的版本將棄用。 在棄用之前，將會發出單獨的通訊。 請參閱&#x200B;*本文章*&#x200B;的[建置時間需求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)區段。
>

#### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

如 4 月的發行說明中所述，AEM Java 記錄必須遵循標準格式，以確保在所有客戶環境中皆進行可靠的監視。不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

從&#x200B;**12月10日**&#x200B;開始，將忽略任何不支援的自訂記錄覆寫。 根據我們的分析，大多數客戶將不會受影響，而 Adobe 會直接聯絡其目前設定可能受影響的客戶。

請審閱所有取決於自訂記錄行為的下游流程，並將其更新。例如：

* 若您的記錄轉送系統需要自訂的記錄格式，則可能需要調整攝取規則。
* 若您先前已透過變更記錄等級降低記錄的詳細程度，請注意，恢復至預設等級可能會增加記錄量。

### [!DNL Experience Manager]作為[!DNL Cloud Service] Foundation早期採用者功能 {#foundation-early-adopter}

#### 暫停自動維護更新 {#pause-updates}

上線日、現場活動、銷售高峰，這些時刻無法中斷。[我們新的自助服務功能](/help/implementing/deploying/quiet-hours-update-free-periods.md)會在重要時刻停止自動維護更新，讓您的團隊保持專注。

* 暫停更新時段：在每天固定的時段內停止自動維護。適合在工作時間、夜間執行或早晨切換時使用。
* 暫停更新期間：一整週皆停止自動維護。在發佈期間、促銷活動或年度凍結時使用。

>[!NOTE]
>
>於 9 月 25 日以「有限開放」功能的形式提供。
>寄送電子郵件至 [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com)，以便在您的方案中啟動此功能。
>

#### Edge 運算 (Beta 版方案) {#edge-computing}

邊緣運算讓您能夠在 CDN 層執行 JavaScript，使資料處理更為接近一般使用者。因此而減少延遲並達到邊緣的回應式動態體驗。

常見使用案例包含：

* 根據地理位置、裝置類型或使用者屬性，將內容個人化
* 做為 CDN 和您來源之間的中介軟體
* 將第三方 API 的回應傳送至瀏覽器之前，先對其進行重新格式化 (且可能彙總多個 API 的回應)
* 使用從各個後端拼接而成的內容，在邊緣編寫及提供伺服器轉譯的 HTML
* 開放 MCP 伺服器供 ChatGPT 和 Claude 等 LLM 存取自訂工具

我們針對正式生產網站提供數量有限的 AEM Publish Delivery 或 Edge Delivery Services 專案機會。若您有興趣參與，或想了解更多相關資訊，請傳送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並簡要描述您的使用案例。

#### Edge Delivery Services 的 Edge 驗證 (Beta 版方案) {#edge-authentication}

透過 Edge 驗證，您可以限制 Edge Delivery Services 頁面的存取權，僅允許通過您的身分提供者 (IdP) 驗證的使用者存取。部署 OpenID Connect (OIDC) 設定 YAML 檔案即可做到上述動作。

若有興趣，請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，簡短說明您的使用案例以及任何問題。

<!--
#### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

#### Canary 生產部署，以便在接受即時流量之前測試程式碼 (Beta 版方案) {#canary-beta}

向一般使用者公開之前，先使用僅限內部的測試流量驗證生產建置版本。運送至生產環境、僅路由 Canary 流量 (使用特殊標頭)、監視行為，然後升級至即時流量或復原，而不會影響客戶。

將您的程式碼版本部署至生產環境，但在決定要接受即時流量或復原之前，將其限制為僅限內部測試流量。

寄送電子郵件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) 來請求存取權及提供意見回饋。


#### AI回答 — 適用於AEM Sites (Beta計畫)的更聰明、內容感知的回應 {#ai-answers-beta}

AI解答為訪客引進了一種與您的內容互動的新方式。 透過擷取增強型產生(RAG)技術，使用AEM管理的資料，直接在數位體驗中提供準確、品牌一致的答案。

我們正準備啟動AI Answers Beta計畫，目前正邀請客戶註冊其興趣。 由於Beta版的容量非常有限，提早註冊將獲得優先考量。 參與Beta版可讓您在AEM Cloud Service環境中探索AI答案、驗證效能和準確性，並在未來體驗正式推出之前協助打造體驗。

若要要求參與或接收更新，請連絡[feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com)。

#### 使用AI加速AEM開發(Alpha計畫)  {#ai-dev-alpha}

AEM Java棧疊團隊越來越多地在Cursor、Claude Code、Visual Studio和IntelliJ等工具中使用AI輔助開發，以加快功能交付並提高計畫碼品質。 我們正在收集真實世界的體驗，以協助塑造未來Adobe支援的AI功能。

透過傳送電子郵件至[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)，分享您團隊的工作成果，以及您希望Adobe提供的成果。

#### RDE 快照 (Alpha 方案) {#rde-snapshot-program}

在 Alpha 版本中，快速開發環境 (RDE) 現在支援對程式碼和內容的目前狀態進行快照的功能，這些快照可以在之後還原。在同步可能需要復原的程式碼，或在不同功能的開發之間切換時，此功能很實用。您也可以僅還原可變內容做為測試的已知起點。

如果您有興趣對此功能提供意見，請寄送電子郵件至 [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

#### 擴充應用程式效能監視 (APM) (Alpha 版方案) {#apm-alpha}

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
