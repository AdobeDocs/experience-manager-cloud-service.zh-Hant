---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service目前的發行說明'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: d389f158ddd71f90b5ee9b707050f5b593ec595a
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 31%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2026.4.0)的發行日期是2026年4月30日。 下一個功能版本(2026.5.0)計畫於2026年5月28日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

<!-- 
## Release Video {#release-video}

Have a look at the April 2026 Release Overview video for a summary of the features added in the 2026.4.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)
-->

## AEM Beta計畫 {#aem-beta-programs}

Adobe Experience Manager (AEM)測試版計畫是讓客戶存取發行前功能和程式碼、提供意見回饋，以及指引AEM未來發展的方法。

>[!IMPORTANT]
>
>Beta發行版本可能包含瑕疵，並依「現況」提供，並無任何保固。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援（透過Adobe支援服務或其他方式）測試版。 Adobe建議客戶謹慎行事，不要依賴Beta版正確運作或效能，或依賴任何隨附的檔案或資料。 Beta版中的功能和API可能會有所變更，恕不另行通知。 因此，使用測試版完全由客戶自行承擔風險。

**參與的優點**

客戶與合作夥伴可提早存取Adobe正在開發的功能，以提供意見並影響產品開發。 此外，也能協助客戶在功能全面推出前做好採用新功能的準備。

**目前的Beta版計畫**

以下小節列出作用中的Beta版計畫。

### AEM中的代理程式 {#agents-in-aem}

如果您想要探索生產、治理、最佳化、探索和開發等強大且新的AEM代理功能，[請在此瞭解如何存取這些功能。](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM Foundation （Beta計畫） {#aem-foundation-beta-programs}

請參閱[AEM Foundation測試版計畫](#foundation-early-adopter)。

### Cloud Manager （Beta計畫） {#cloud-manager-beta-programs}

請參閱[Cloud Manager測試版計畫](/help/implementing/cloud-manager/release-notes/current.md)。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AI翻譯整合 {#ai-translation-integration}

AEM使用者現在可以利用大型語言模型(LLM)進行內容翻譯，以機器翻譯的速度提供人力翻譯品質。 與傳統第三方翻譯服務類似，Azure OpenAI可設定為AEM中的翻譯提供者，並支援未來版本預計提供的其他LLM。 客戶使用自己的LLM授權來實現此功能。 此外，企業翻譯風格指南可上傳至AEM，讓您擷取翻譯規則，確保品牌和風格的一致性。 如需詳細資訊，請參閱[設定AI翻譯整合](/help/sites-cloud/administering/translation/ai-translation-integration.md)。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**內容顧問現在可用於Adobe Workfront和非Adobe應用程式**

Content Advisor現在可供Adobe Workfront和非Adobe （協力廠商）應用程式使用，將智慧型資產探索和內容重複使用擴充到Adobe Express和AEM Sites之外。 此版本提供完整的「內容顧問」體驗，包括AI支援的搜尋、內容感知建議、行銷活動簡訊式探索、動態媒體轉譯存取、內容片段探索、篩選器，以及Adobe Workfront工作流程和外部應用程式的資產中繼資料。

您現在可以直接在您的偏好應用程式中探索、評估及重複使用AEM Assets的已核准資產，實現一致的資產使用、提高效率，以及簡化Adobe和非Adobe應用程式的內容建立。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的搶先體驗功能 {#forms-early-access-features}

**在提交PDF中顯示多選下拉式清單的標籤**
最適化Forms中的多選下拉式元件現在會在[產生的提交PDF](/help/forms/generate-document-of-record-core-components.md)中轉譯其選取的顯示標籤，以確保檔案準確地反映使用者在表單上看到的內容。

**核取方塊、選項按鈕和面板元件的增強協助工具**
最適化Forms核心元件為[核取方塊群組(v2)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group)、[選項按鈕群組(v2)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button)和[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)引入符合WCAG 2.2的語意標籤。 這些元件運用`<fieldset>`和`<legend>` HTML元素，在群組標籤與其選項之間建立有意義的關係，讓熒幕助讀程式和其他輔助技術能夠精確解讀。

Forms Manager中的&#x200B;**版本設定支援**
Forms Manager現在[支援最適化Forms （核心元件和基本元件）](/help/forms/manage-form-versions-forms-manager.md)、表單片段、主題、XDP範本和二進位資產的版本設定。 直接從Forms和檔案主控台建立版本、檢視完整的版本記錄，以及還原表單資產的舊版狀態。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation新功能 {#foundation-new}

#### 適用於AEM Java和Dispatcher開發的IDE AI工具 {#ai-dev}

Java棧疊團隊越來越多地在Cursor、Claude Code、Visual Studio和IntelliJ等工具中使用AI輔助開發，以加快功能交付並提高計畫碼品質。

編碼代理程式可以使用IDE工具來產生和偵錯AEM程式碼和Dispatcher設定。 例如，下列影片逐步解說會示範如何使用「代理程式技能」建立AEM元件。

深入瞭解[使用AI工具進行本機開發](/help/ai-in-aem/local-development-with-ai-tools.md)，您可以隨時傳送電子郵件至[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)，提出問題或意見反應。


>[!VIDEO](https://video.tv.adobe.com/v/3484978/?learn=on&enablevpops)

#### Experience Governance MCP伺服器 {#gov-mcp-server}

Experience Governance MCP Server現已正式推出(GA)。 它與支援「模型內容通訊協定」(MCP)的AI開發人員工具和聊天機器人整合，可讓您在聊天機器人或IDE中使用自然語言提示來維護品牌完整性和法規遵循。 您可以根據品牌治理規則評估內容（文字、影像、頁面），並擷取品牌設定和可用的治理檢查。

深入瞭解[AEM MCP伺服器](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)和[治理代理程式](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview)。

#### 克勞德聯結器 {#aem-claude-connector}

Claude使用者可以瀏覽Anthropic的[Connector Marketplace](https://claude.ai/settings/connectors)，按一下即可安裝[Adobe Experience Manager Connector](/help/ai-in-aem/mcp-support/setup-claude.md#aem-claude-connector)。 這部MCP伺服器會公開一組與AEM互動的成長工具，包括透過提示編輯內容。

#### AEM OIDC發佈新功能報告 {#aem-oidc-on-publish-new-features}

* 修正：驗證後，原始請求的查詢引數會遺失
* 在OIDC驗證[檔案](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md#custom-redirect-after-authentication)中進行驗證後自訂重新導向

#### Microsoft Graph API的郵件服務支援 {#mail-service-graph-api}

AEM的郵件服務現在透過Microsoft Graph API支援Microsoft® Outlook （透過Microsoft 365）。 這對於不允許SMTP （郵件服務已支援）的組織特別有用。 驗證是透過OAuth 2.0進行。 [瞭解如何設定](/help/security/oauth2-support-for-mail-service.md#microsoft-graph-api)。

#### CDN記錄檔可轉送至Sumo Logic {#sumo-cdn-logforwarding}

[記錄檔轉送功能](/help/implementing/developing/introduction/log-forwarding.md#sumologic)現在支援將CDN記錄檔傳送至Sumo Logic。 之前，記錄轉送至Sumo Logic僅限於使用AEM記錄。

### [!DNL Experience Manager]為[!DNL Cloud Service]個Foundation重要通知 {#foundation-notices}

#### IMS驗證Rich錯誤 {#ims-auth-rich-errors}

為協助疑難排解IMS整合，`imsauth`已新增對&#x200B;*rich errors*&#x200B;的支援。

這些錯誤不會只傳回HTTP狀態代碼，而是會提供額外的內容，以協助診斷和解決可能封鎖驗證和存取的問題。

#### Java API淘汰 {#java-api-deprecation}

移除使用過時的API是很重要的事。

自&#x200B;**4月14日**&#x200B;起，包含使用2026年2月26日移除&#x200B;**的API之程式碼的Cloud Manager管道，會在程式碼品質步驟**&#x200B;中失敗。 在移除過時的API使用方式之前，部署將會遭到封鎖。 *這可能會阻止您發佈時效性更新資料，並可能影響您的業務運作。*

自&#x200B;**2026年6月11日起**，仍在使用這些已棄用API的環境&#x200B;**將不會收到重要的Adobe版本更新**，而且不會受到Adobe有關效能和可用性的標準承諾所約束。 因此，您將不會收到新功能或錯誤修正、應用程式穩定性和運作時間可能會受到負面影響，且安全性風險暴露可能會進一步增加。

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
* `org.apache.jackrabbit.oak.plugins.memory`

+++

### [!DNL Experience Manager]作為[!DNL Cloud Service] Foundation早期採用者功能 {#foundation-early-adopter}

#### AEM Edge功能（Beta程式） {#edge-functions}

[AEM Edge功能](/help/implementing/developing/introduction/edge-functions.md)可讓您在CDN層執行JavaScript，讓資料處理更接近一般使用者。 因此而減少延遲並達到邊緣的回應式動態體驗。

常見使用案例包含：

* 根據地理位置、裝置類型或使用者屬性，將內容個人化
* 做為 CDN 和您來源之間的中介軟體
* 將第三方 API 的回應傳送至瀏覽器之前，先對其進行重新格式化 (且可能彙總多個 API 的回應)
* 使用從各個後端拼接而成的內容，在邊緣編寫及提供伺服器轉譯的 HTML
* 為ChatGPT和Claude等AI助理公開MCP伺服器，以存取自訂工具

我們針對正式生產網站提供數量有限的 AEM Publish Delivery 或 Edge Delivery Services 專案機會。 若您有興趣參與，或想了解更多相關資訊，請傳送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並簡要描述您的使用案例。

#### Web層設定管道疑難排解（Beta程式） {#devagent-webtier}

開發代理程式的[管線疑難排解](/help/ai-in-aem/agents/brand-experience/development/development.md)功能可協助開發人員有效診斷和解決AEM as a Cloud Service部署中的問題。 除了支援完整棧疊管道（部署和程式碼品質）之外，開發代理程式現在也支援&#x200B;**網頁層設定管道**&#x200B;的疑難排解，作為Beta程式的一部分。

若要要求存取Beta版，請傳送電子郵件至[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)。 需要預先存取AEM中的代理程式。

#### 復寫AI疑難排解（Alpha計畫） {#replication-ai-troubleshooting-alpha}

在AEM Author和其他介面中使用AI Assistant，您可以疑難排解復寫相關問題，例如封鎖的佇列。 若要加入Alpha計畫，請傳送電子郵件至[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)，說明您的興趣。

#### 適用於AEM 6.5的IDE AI工具移轉至AEM Cloud Service （Beta程式） {#cm-ide-migration}

使用IDE AI工具來執行[Best Practices Analyzer報告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)的建議，加速從AEM 6.5移轉至AEM as a Cloud Service （Java棧疊）。

請傳送電子郵件至[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)，以取得詳細資訊及要求存取功能。

#### Edge Delivery Services 的 Edge 驗證 (Beta 版方案) {#edge-authentication}

透過 Edge 驗證，您可以限制 Edge Delivery Services 頁面的存取權，僅允許通過您的身分提供者 (IdP) 驗證的使用者存取。 部署 OpenID Connect (OIDC) 設定 YAML 檔案即可做到上述動作。

若有興趣，請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，簡短說明您的使用案例以及任何問題。

#### Canary 生產部署，以便在接受即時流量之前測試程式碼 (Beta 版方案) {#canary-beta}

向一般使用者公開之前，先使用僅限內部的測試流量驗證生產建置版本。 運送至生產環境、僅路由 Canary 流量 (使用特殊標頭)、監視行為，然後升級至即時流量或復原，而不會影響客戶。

寄送電子郵件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) 來請求存取權及提供意見回饋。

#### RDE快照（Beta計畫） {#rde-snapshot-program}

在Beta版中，快速開發環境(RDE)現在支援功能[，以取得程式碼和內容目前狀態的快照](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots)，稍後可加以還原。 在同步可能需要復原的程式碼，或在不同功能的開發之間切換時，此功能很實用。 您也可以僅還原可變內容做為測試的已知起點。

若您有興趣使用此功能並提供意見反應，請寄電子郵件給[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

#### 擴充應用程式效能監視 (APM) (Alpha 版方案) {#apm-alpha}

為便於觀察，AEM Cloud Service 目前支援 Adobe 提供的 [New Relic One](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) 和客戶管理的 [Dynatrace](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace)。 由於我們仍在探索其他 APM 選項支援，請寄送電子郵件至 [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) 與我們聯絡，告知您偏好的供應商或技術，並提供使用案例。

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
