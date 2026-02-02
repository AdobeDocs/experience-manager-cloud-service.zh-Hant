---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service目前的發行說明'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 6dfc3fe7e939794a7881a5c24c51ccc43f9af348
workflow-type: tm+mt
source-wordcount: '2126'
ht-degree: 36%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2026.1.0)的發行日期是2026年1月29日。 下一個功能版本(2026.2.0)計畫於2026年2月26日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440931?captions=chi_hant&quality=12)

-->

## AEM Beta計畫 {#aem-beta-programs}

Adobe Experience Manager (AEM)測試版計畫是讓客戶存取發行前功能和程式碼、提供意見回饋，以及指引AEM未來發展的方法。

>[!IMPORTANT]
>
>Beta發行版本可能包含瑕疵，並依「現況」提供，並無任何保固。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援(透過Adobe支援服務或其他方式)測試版。 Adobe建議客戶謹慎行事，不要依賴Beta版正確運作或效能，或依賴任何隨附的檔案或資料。 Beta版中的功能和API可能會有所變更，恕不另行通知。 因此，使用測試版完全由客戶自行承擔風險。

**參與的優點**
客戶與合作夥伴可提早存取Adobe正在開發的功能，以提供意見並影響產品開發。 此外，也能協助客戶在功能全面推出前做好採用新功能的準備。

**目前的Beta版計畫**
以下小節列出作用中的Beta版計畫。

### AEM (Beta程式)中的代理程式 {#agents-in-aem-beta-program}

搶先使用強大的全新AEM代理功能，涵蓋生產、治理、最佳化、探索和開發。 您的意見直接影響Adobe的發展藍圖和最終功能。 如需瞭解詳細資訊，請參閱[AEM代理程式概觀](/help/ai-in-aem/agents/overview.md)。

此計畫通常持續4至6週，但可針對您的主動參與能力進行靈活調整。

若要選擇加入此計畫，請傳送電子郵件至[aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com)，並儘可能加入下列詳細資料：

* 將主動使用代理的團隊成員的名稱和Adobe ID。
* 列出您或您的團隊要使用的特定代理程式。 或者說「所有代理程式」。

選取要參與的客戶會由Adobe直接通知。 參與取決於資格考量因素，包括客戶授權和有限的方案容量。 雖然並非所有要求一開始都能獲得滿足，但未來測試版波段可能會考慮其他客戶。

### AEM Foundation (Beta計畫) {#aem-foundation-beta-programs}

請參閱[AEM Foundation測試版計畫](#foundation-early-adopter)。

### Cloud Manager (Beta計畫) {#cloud-manager-beta-programs}

請參閱[Cloud Manager測試版計畫](/help/implementing/cloud-manager/release-notes/current.md)。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Content MCP Server {#content-MCP}

AEM Cloud Service現在包含&#x200B;**內容MCP伺服器**，提供標準化方式，讓AI支援的體驗可透過MCP相容工具使用AEM內容。

在聊天應用程式和代理程式平台工作的開發人員和進階使用者，可以將AEM連線到自訂的輔助程式和自動化，讓內容工作成為端對端業務工作流程的一部分。

AEM提供兩部伺服器：

1. **唯讀內容MCP伺服器** — 用於安全地擷取內容
1. **讀取/寫入內容MCP伺服器** — 用於變更內容

這些MCP伺服器包含用於處理&#x200B;**頁面**、**內容片段**&#x200B;和&#x200B;**Assets**&#x200B;的工具，並且可以從下列MCP使用者端使用： **ChatGPT**、**Claude**、**Cursor**&#x200B;和&#x200B;**Microsoft Copilot Studio**。

深入瞭解[將MCP與AEM雲端服務](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)搭配使用。 如有疑問或意見，請傳送電子郵件至[aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com)。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**AI 搜尋**

AI 搜尋引進了智慧型內容感知搜尋體驗，其透過瞭解使用者查詢背後的含義和意圖，超越了傳統關鍵字比對。 由AI和機器學習提供技術支援，即使查詢的措辭不同、包含拼字錯誤、使用同義字或以不同語言提交，也能提供更準確的結果，讓使用者更快找到相關內容，事半功倍。

如需詳細資訊，請參閱[Assets檢視](/help/assets/search-assets-view.md#ai-search)和[管理員檢視](/help/assets/search-assets.md#ai-search)中的AI 搜尋。

**案頭應用程式3.0.1版本**

[案頭應用程式3.0.1 （2025年12月20日）](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-desktop-app/using/release-notes)可改善主要工作流程的可靠性、效能和穩定性。 此版本透過修正AEM Author的同步問題來確保一致的資料夾命名，允許在作用中傳輸期間不間斷地使用應用程式，透過非同步處理來增強UI回應能力，最佳化具有分頁的大型檔案傳輸，以及解決穩定性問題，包括在Author伺服器上傳和下載大型資料夾期間重新啟動和當機。

**Adobe Asset Link CEP 2026.01.0版本**

[Adobe Asset Link CEP 2026.01.0](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)在InDesign中推出了新的「重新連結遺漏的連結」選項，會自動從相同的AEM資料夾中重新連結其他遺漏的資產。 此功能根據檔案名稱來比對資產，大幅減少還原中斷連結時的手動工作量。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

**最適化Forms （基礎元件）中註腳預留位置的增強功能**

* 新增[多行支援及分行符號](/help/forms/footnotes-richtextsupport.md)，讓註腳內容呈現得更清晰、更有表現力。
* 現在，無論相關面板的可見度為何，註腳都會持續顯示在註腳預留位置內，確保關鍵資訊的存取方式維持一致。

### 全新 AEM Forms 搶先體驗功能 {#forms-new-early-access-features}

**從JSON陣列擷取值**

擴充自訂函式功能，以從JSON陣列[擷取透過API呼叫收到的值，並直接繫結至調適型表單欄位。 &#x200B;](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array)您現在可以使用最少的手動資料對應來開發商業邏輯和規則。

**在發佈執行個體上執行關聯UI**

您現在可以直接在發佈執行個體上執行[關聯UI](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)。 這可讓您的代理存取關聯UI，並輕鬆為客戶個人化通訊。

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

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager]為[!DNL Cloud Service]個Foundation重要通知 {#foundation-notices}

#### Java API淘汰 {#java-api-deprecation}

2026年2月26日移除的已棄用API不應再用於程式碼中。 若要防止部署封鎖，請在2026年3月26日之前移除API使用方式。 重要日期：

* **自2026年1月26日起**：每個環境&#x200B;**每週都會傳送動作中心通知電子郵件**，以提醒您移除這些API的使用情況。
* **2026年2月26日**：包含使用這些API之程式碼的Cloud Manager管道將在&#x200B;**程式碼品質**&#x200B;步驟期間&#x200B;**暫停**。 部署管理員、專案管理員或企業所有者可以覆寫此問題，以允許管道繼續。
* **2026年3月26日**：包含使用這些API之程式碼的Cloud Manager管道將在&#x200B;**程式碼品質**&#x200B;步驟期間&#x200B;**失敗**，**封鎖新程式碼的部署**，直到移除使用為止。
* **2026年4月30日**：仍在使用這些API的環境可能&#x200B;**不再接收重要的Adobe版本更新**。

請參閱[棄用文章](/help/release-notes/deprecated-removed-features.md#aem-apis)，了解完整的詳細資訊，但為了方便起見，這些 API 條列如下：

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

Adobe已於2025年10月14日將&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;環境升級為效能較高的&#x200B;**Java 21執行階段**。 從&#x200B;**2月9日**&#x200B;開始（逐步推出至2月11日），AEM Cloud Service SDK或任何雲端環境都無法搭配Java 11執行階段使用。

>[!NOTE]
>
> 若要利用最新的效能最佳化和語言增強功能，建議使用Java 17或Java 21 （偏好設定）建置。 目前仍支援使用Java 8和Java 11進行建置，但即將發行的版本將棄用。 在棄用之前，將會發出單獨的通訊。 請參閱&#x200B;*本文章*&#x200B;的[建置時間需求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)區段。
>

#### 執行 AEM Java 記錄設定原則 {#logconfig-policy}

AEM Java記錄必須遵循標準格式，以確保在所有客戶環境中進行可靠的監控。 不再支援自訂記錄設定 (例如變更記錄格式、輸出檔案或預設記錄等級)。記錄必須保持導向預設檔案，並且必須保留 AEM 產品程式碼的預設記錄等級。如需完整詳情，請參閱[記錄文章](/help/implementing/developing/introduction/logging.md#configuration-loggers)。

任何不支援的自訂記錄覆寫&#x200B;*現在都會被忽略*。 大部分客戶均未受到影響，Adobe已聯絡其目前設定可能受影響的客戶。

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

#### AEM Edge功能(Beta程式) {#edge-functions}

AEM Edge Functions (在舊版發行說明中稱為&#x200B;*Edge Computing*)可讓您在CDN層執行JavaScript，讓資料處理更接近一般使用者。 因此而減少延遲並達到邊緣的回應式動態體驗。

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

#### Canary 生產部署，以便在接受即時流量之前測試程式碼 (Beta 版方案) {#canary-beta}

向一般使用者公開之前，先使用僅限內部的測試流量驗證生產建置版本。運送至生產環境、僅路由 Canary 流量 (使用特殊標頭)、監視行為，然後升級至即時流量或復原，而不會影響客戶。

將您的程式碼版本部署至生產環境，但在決定要接受即時流量或復原之前，將其限制為僅限內部測試流量。

寄送電子郵件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) 來請求存取權及提供意見回饋。

#### AI回答 — 適用於AEM Sites (Beta計畫)的更聰明、內容感知的回應 {#ai-answers-beta}

AI解答為訪客引進了一種與您的內容互動的新方式。 透過擷取增強型產生(RAG)技術，使用AEM管理的資料，直接在數位體驗中提供準確、品牌一致的答案。

我們正準備啟動AI Answers Beta計畫，目前正邀請客戶註冊其興趣。 由於Beta版的容量非常有限，提早註冊將獲得優先考量。 參與Beta版可讓您在AEM Cloud Service環境中探索AI答案、驗證效能和準確性，並在未來體驗正式推出之前協助打造體驗。

若要要求參與或接收更新，請連絡[feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com)。

#### RDE快照(Beta計畫) {#rde-snapshot-program}

在Beta版中，快速開發環境(RDE)現在支援對程式碼和內容的目前狀態建立快照的功能，以便稍後復原。 在同步可能需要復原的程式碼，或在不同功能的開發之間切換時，此功能很實用。您也可以僅還原可變內容做為測試的已知起點。

若您有興趣使用此功能並提供意見反應，請寄電子郵件給[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

#### 適用於AEM Java和Dispatcher開發(Beta程式)的IDE人工智慧工具 {#ai-dev-beta}

Java棧疊團隊越來越多地在Cursor、Claude Code、Visual Studio和IntelliJ等工具中使用AI輔助開發，以加快功能交付並提高計畫碼品質。 加入Beta版以：

* 分享真實世界的體驗，以協助打造未來的Adobe支援AI功能
* 嘗試人工智慧代理程式可用於產生和偵錯AEM程式碼和Dispatcher設定的IDE工具

請傳送電子郵件至[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)，以取得詳細資訊。

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
