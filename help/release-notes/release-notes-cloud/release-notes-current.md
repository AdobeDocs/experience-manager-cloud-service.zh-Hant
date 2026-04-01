---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service目前的發行說明'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 最新發行說明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 9820b642af32960c532b238e00267cb4d880535f
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 28%

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

[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]目前功能版本(2026.3.0)的發行日期是2026年3月26日。 下一個功能版本(2026.4.0)計畫於2026年4月30日發行。

## 維護版本發行說明 {#maintenance}

您可以在[這裡](/help/release-notes/maintenance/latest.md)找到最新的維護版本發行說明。

&lt;##發行影片{#release-video}

請觀看 2026 年 3 月發行概觀影片，以了解 2026.3.0 版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)

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

### 內容片段簽出/簽入 {#cf-checkout-in}

為了改善與AEM觸控式UI的平等性，現在也可以使用新的內容片段管理UI來簽出及簽回內容片段。 出庫功能未變更，因此可有效鎖定出庫的內容片段，並防止其他使用者在內容片段編輯器中編輯該片段。 擁有內容片段的使用者與管理員可以簽出片段並重新存入。 將片段簽出對引用的子片段或資產沒有影響。

### 內容片段啟動工作面板 {#cf-launches-jobs}

現在，您可以在內容片段啟動管理UI的屬性面板中檢視內容片段啟動的非同步作業，以觀察其狀態 — 如果作業仍在執行、已完成或中止，以及作業的相關詳細資訊。

### 內容片段編輯器的RTE更新 {#cf-rte-update}

內容片段編輯器的RTF編輯器(RTE)已從TinyMCE移轉至TipTap。 這項變更會帶來許多好處。

* 通用編輯器和內容片段編輯器現在使用相同的RTE技術棧疊。
   * 這表示兩個編輯器現在會產生相同的HTML。
   * 擴充功能現在可重複使用。
   * 現在，使用兩個編輯器（在Headless使用案例中）可以使用相同的函式和方法。
   * 最終目標是兩個編輯器中的一項設定都能帶來統一的體驗。
* 內容編輯器現在擁有Spectrum 2樣式的新外觀。
* 內容片段編輯器中提供的新功能包括尋找和取代，以及隨時提供內容建議程式。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

AEM Sites中的&#x200B;**內容顧問**

AEM Sites現在提供內容建議程式，直接從AEM Assets匯入智慧型資產探索功能。 它可讓使用者輕鬆地直接在其工作流程中探索、瀏覽及重複使用最相關的資產，而不需要切換內容。

內容警告器提供資產的智慧型功能，例如行銷活動簡介型建議、情境式建議、存取Dynamic Media轉譯和詳細的資產中繼資料。

即將推出 — Content Advisor對Adobe Workfront和AJO B2C應用程式的支援，包括探索內容片段的功能

### Dynamic Media 中的新功能 {#dynamic-media-new-features}

#### Dynamic Media範本編輯器更新 {#dynamic-media-template-editor-updates}

**圖層管理增強功能**

* 拖放圖層重新排序：現在可以直接在「圖層」面板中透過拖曳來重新排序圖層，提供更快速、更直覺的方式來組織圖層棧疊順序，而不只是現有的「上移一層」或「下移一層」動作。
* 複製、貼上及複製：完全支援使用鍵盤快速鍵(Cmd/Ctrl+C、V、D)或內容功能表來複製、貼上及復製圖層，並支援多層選取範圍。
* 獨立圖層屬性按鈕：新增專用的圖層屬性按鈕，可更輕鬆導覽至圖層設定，並在圖層上按兩下支援以快速存取。

**文字格式功能**

* 行距控制：新的行距滑桿可精確控制文字圖層中的行高，並具備完整的端對端支援，包括還原/重做以及範本儲存/載入。
* 全大寫格式：文字圖層現在支援「字型樣式」工具列中的「全大寫格式」選項，以及「粗體」、「斜體」和「底線」。
* 垂直對齊選項：新增文字圖層的垂直對齊控制項，在文字方塊內提供更精確的文字定位。

**大小與Dimension控制項**

* 長寬比解除鎖定：使用者現在可在調整大小屬性時，解除鎖定長寬比，獨立調整寬度和高度，以更靈活地調整圖層大小。
* 組排文字的線條組態：新增文字組排屬性中`copyfitlines`和`copyfitmaxlines`設定的支援，提供更精細的控制文字組排行為。

**視覺波蘭文**

* 更新了「計時器」和「形狀」圖層的圖示，並改良Spectrum 2 (S2)設計系統圖示。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms 的搶先體驗功能 {#forms-early-access-features}

**在提交PDF中顯示多選下拉式清單的標籤**
最適化Forms中的多選下拉式元件現在會在[產生的提交PDF](/help/forms/generate-document-of-record-core-components.md)中轉譯其選取的顯示標籤，以確保檔案準確地反映使用者在表單上看到的內容。

**核取方塊、選項按鈕和面板元件的增強協助工具**
最適化Forms核心元件為[核取方塊群組(v2)](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group)、[選項按鈕群組(v2)](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button)和[面板元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)引入符合WCAG 2.2的語意標籤。 這些元件運用`<fieldset>`和`<legend>` HTML元素，在群組標籤與其選項之間建立有意義的關係，讓熒幕助讀程式和其他輔助技術能夠精確解讀。

Forms Manager中的&#x200B;**版本設定支援**
Forms Manager現在[支援最適化Forms （核心元件和基本元件）](/help/forms/manage-form-versions-forms-manager.md)、表單片段、主題、XDP範本和二進位資產的版本設定。 直接從Forms和檔案主控台建立版本、檢視完整的版本記錄，以及還原表單資產的舊版狀態。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎 {#foundation}

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation新功能 {#foundation-new}

#### 簡化的索引管理 {#simplified-index-management}

[簡化的索引管理](https://oak-indexing.github.io/oakTools/simplified.html)提供更簡單的方式來定義自訂索引，並使用一個JSON檔案自訂現成可用的(OOTB)索引，而不需複製完整定義或手動管理版本。 自訂會與最新的OOTB索引合併，並在需要時建立新的索引版本。

#### Cloud Manager MCP伺服器 {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480340/?quality=12)

現代IDE使用模型內容通訊協定(MCP)來啟用大型語言模型(LLM)，以叫用MCP伺服器公開的工具。 開發人員不必直接與低階API規格整合，只需以自然語言描述其意圖即可。

Cloud Manager MCP伺服器可讓您使用提示，直接從IDE與Cloud Manager API互動。 支援的情況包括執行管道、檢查環境狀態等。

深入瞭解[AEM MCP伺服器](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)。

### [!DNL Experience Manager]為[!DNL Cloud Service]個Foundation重要通知 {#foundation-notices}

#### Java API淘汰 {#java-api-deprecation}

2026年2月26日移除的已棄用API不應再用於程式碼中。 若要防止部署區塊，請在&#x200B;**2026年3月30日**&#x200B;之前移除API使用量。 重要日期：

* **自2026年1月26日起**：會傳送動作中心通知電子郵件，提醒您移除使用這些API。
* **2026年2月26日**：包含使用這些API之程式碼的Cloud Manager管道將在&#x200B;**程式碼品質**&#x200B;步驟期間&#x200B;**暫停**。 部署管理員、專案管理員或企業所有者可以覆寫此問題，以允許管道繼續。 *這可能會降低您驗證和發行程式碼變更的能力。*
* **2026年3月30日**：包含使用這些API之程式碼的Cloud Manager管道將在&#x200B;**程式碼品質**&#x200B;步驟中&#x200B;**失敗**。 在移除過時的API使用方式之前，部署將會遭到封鎖。 *這可能會阻止您發佈時效性更新資料，並可能影響您的業務運作。*
* **2026年5月4日**：仍在使用已棄用API的環境&#x200B;**將不會收到重要的Adobe版本更新**，且不會受到Adobe有關效能和可用性的標準承諾所約束。 因此，您將不會收到新功能或錯誤修正、應用程式穩定性和運作時間可能會受到負面影響，且安全性風險暴露可能會進一步增加。

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

#### 適用於AEM Java和Dispatcher開發的IDE AI工具（公用Beta程式） {#ai-dev-beta}

Java棧疊團隊越來越多地在Cursor、Claude Code、Visual Studio和IntelliJ等工具中使用AI輔助開發，以加快功能交付並提高計畫碼品質。

參與公開測試版（無需註冊）以試用可由編碼代理程式用來產生和偵錯AEM程式碼和Dispatcher設定的IDE工具。

在[使用AI工具的本機開發](/help/ai-in-aem/local-development-with-ai-tools.md) Beta版檔案中瞭解更多，並透過電子郵件[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)提出問題或回饋。

#### AEM Edge功能（Beta程式） {#edge-functions}

AEM Edge功能可讓您在CDN層執行JavaScript，讓資料處理距離一般使用者更近。 因此而減少延遲並達到邊緣的回應式動態體驗。

常見使用案例包含：

* 根據地理位置、裝置類型或使用者屬性，將內容個人化
* 做為 CDN 和您來源之間的中介軟體
* 將第三方 API 的回應傳送至瀏覽器之前，先對其進行重新格式化 (且可能彙總多個 API 的回應)
* 使用從各個後端拼接而成的內容，在邊緣編寫及提供伺服器轉譯的 HTML
* 開放 MCP 伺服器供 ChatGPT 和 Claude 等 LLM 存取自訂工具

我們針對正式生產網站提供數量有限的 AEM Publish Delivery 或 Edge Delivery Services 專案機會。若您有興趣參與，或想了解更多相關資訊，請傳送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，並簡要描述您的使用案例。

#### 使用開發代理程式（Beta程式）進行網頁層設定管道疑難排解 {#devagent-webtier}

開發代理程式的[管線疑難排解](/help/ai-in-aem/agents/brand-experience/development/development.md)功能可協助開發人員有效診斷和解決AEM as a Cloud Service部署中的問題。 除了支援完整棧疊管道（部署和程式碼品質）之外，開發代理程式現在也支援&#x200B;**網頁層設定管道**&#x200B;的疑難排解，作為Beta程式的一部分。

若要要求存取Beta版，請傳送電子郵件至[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)。 需要預先存取AEM中的代理程式。

#### 適用於AEM 6.5的IDE AI工具移轉至AEM Cloud Service （Alpha程式） {#cm-ide-migration}

使用IDE AI工具來執行[Best Practices Analyzer報告](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)的建議，加速從AEM 6.5移轉至AEM as a Cloud Service （Java棧疊）。

請傳送電子郵件至[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)，以取得詳細資訊。

#### Edge Delivery Services 的 Edge 驗證 (Beta 版方案) {#edge-authentication}

透過 Edge 驗證，您可以限制 Edge Delivery Services 頁面的存取權，僅允許通過您的身分提供者 (IdP) 驗證的使用者存取。部署 OpenID Connect (OIDC) 設定 YAML 檔案即可做到上述動作。

若有興趣，請寄送電子郵件至 [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)，簡短說明您的使用案例以及任何問題。

#### Canary 生產部署，以便在接受即時流量之前測試程式碼 (Beta 版方案) {#canary-beta}

向一般使用者公開之前，先使用僅限內部的測試流量驗證生產建置版本。運送至生產環境、僅路由 Canary 流量 (使用特殊標頭)、監視行為，然後升級至即時流量或復原，而不會影響客戶。

將您的程式碼版本部署至生產環境，但在決定要接受即時流量或復原之前，將其限制為僅限內部測試流量。

寄送電子郵件至 [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) 來請求存取權及提供意見回饋。

#### RDE快照（Beta計畫） {#rde-snapshot-program}

在Beta版中，快速開發環境(RDE)現在支援對程式碼和內容的目前狀態建立快照的功能，以便稍後復原。 在同步可能需要復原的程式碼，或在不同功能的開發之間切換時，此功能很實用。您也可以僅還原可變內容做為測試的已知起點。

若您有興趣使用此功能並提供意見反應，請寄電子郵件給[aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com)。

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
