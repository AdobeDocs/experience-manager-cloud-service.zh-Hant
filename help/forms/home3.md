---
title: AEM Forms as a Cloud Service — 數位表單平台
description: 使用模組化元件建置、整合及最佳化數位表格。 從最適化表單、Data Connectors、工作流程自動化、分析和管理工具中選擇，建立強大的表單體驗。
landing-page-description: 模組化數位表格平台，具備獨立的元件，用於表格建立、資料整合、流程自動化、分析和治理。
keywords: AEM Forms，數位表單，表單產生器，調適型表單，表單整合，工作流程自動化，表單分析，檔案服務
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
source-git-commit: 51d9fed937ea5f12544ed476974d2812843fb457
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 1%

---


# AEM Forms as a Cloud Service {#aem-forms-platform}

使用模組化元件建置、整合及最佳化數位表格。 AEM Forms提供獨立產品，這些產品可搭配使用或獨立運作，根據任何業務需求建立強大的表單體驗。

選擇您需要的元件 — 從簡單的表單建立到複雜的檔案工作流程、資料整合和進階分析。

## 新增功能 {#whats-new}

**最新發行亮點：**

- **日期與時間輸入元件** — 具有行事曆與時鐘介面的增強型使用者輸入
- **增強型檔案上傳安全性** — 自動驗證和內容型別檢查
- **改善錯誤處理** — 使用自訂提交動作的特定錯誤碼進行更好的偵錯
- **記錄檔案增強功能** — 用於排除隱藏欄位的選項，以產生更乾淨的檔案

**發行前功能：**

- **AFP格式支援** — 具有通訊API的企業級列印功能
- **規則編輯器增強功能** — 現代JavaScript支援和動態變數
- **增強的驗證方法** — 面板、欄位和表單層級的驗證改善

[檢視完整發行說明→](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## 搶先體驗方案 {#early-access}

獨家存取尖端的AEM Forms創新技術：

- **🤖AEM Forms AI Assistant** — 用於自動錶單建立和最佳化的Generative AI
- **✍️草寫簽章元件** — 表單中的直接簽章擷取
- **🔗直接API整合** — 無需設定表單資料模型即可連線至API
- **📊Forms最佳化** - AI支援的效能分析和轉換改善

[要求存取→](mailto:aem-forms-ea@adobe.com) | [深入瞭解→](/help/forms/early-access-ea-features.md)

## 📋表單建立與編寫 {#form-creation}

使用最符合您需求和技術要求的製作方法來建立表單。

### 核心元件Forms {#core-components}

| **核心元件Forms** |
|---|
| 使用最新網頁標準的現代、回應式表單建置。 建立可自動跨裝置運作的調適型表單，並產生Headless表單以供API導向傳送。 |
| **功能：**&#x200B;視覺化的拖放式表單產生器，包含現代化元件、自動回應式設計和內建協助工具功能。 |
| **何時使用：**&#x200B;新專案、新式Web體驗、Headless表單傳遞、行動優先設計。 |
| ✅回應式設計✅協助工具合規性✅無周邊功能✅現代UI元件 |
| [開始使用核心元件→](/help/forms/creating-adaptive-form-core-components.md) |

### 基礎元件Forms {#foundation-components}

| **基礎元件Forms** |
|---|
| 針對現有專案和舊版整合建立的表單建置方法。 具有廣泛自訂選項的成熟元件。 |
| **它的功能：**&#x200B;傳統的最適化表單建置具有完整的元件庫和廣泛的自訂功能。 |
| **何時使用：**&#x200B;現有專案、舊版系統整合、特定的自訂需求、已建立的工作流程。 |
| ✅廣泛的元件庫✅深層自訂✅舊版相容性✅經驗證的穩定性 |
| [開始使用基礎元件→](/help/forms/creating-adaptive-form.md) |

### Edge Delivery Forms {#edge-delivery}

| **Edge Delivery Forms** |
|---|
| 使用熟悉的工具(如Microsoft Excel)建立高效能表單。 獲得卓越的載入速度和SEO效能。 |
| **它的功能：**&#x200B;使用Excel試算表建立表單，以最佳的Google Lighthouse分數發佈到高效能邊緣傳遞網路。 |
| **何時使用：**&#x200B;效能關鍵應用程式、以SEO為中心的專案、內容作者導向的表單建立、全域內容傳遞。 |
| ⚡ Excel式編寫⚡快如閃電的載入⚡最佳化SEO ⚡全域CDN傳遞 |
| [開始使用Edge Delivery →](/help/edge/docs/forms/overview.md) |

### HTML5 表單 {#html5-forms}

| **HTML5 Forms** |
|---|
| 針對行動裝置和舊版瀏覽器，將XFA型表單轉譯為HTML5。 維護表單邏輯，同時提供原生行動體驗。 |
| **功能：**&#x200B;將XFA表單範本轉換為具有原生行動體驗和跨瀏覽器相容性的HTML5表單。 |
| **何時使用：** XFA表單現代化、行動裝置最佳化、舊版瀏覽器支援、現有XDP投資。 |
| 📱 XFA相容性📱行動裝置最佳化📱跨瀏覽器支援📱沒有外掛程式需求 |
| [開始使用HTML5 Forms →](/help/forms/introductionhtml5.md) |

### 互動式通訊 {#interactive-communications}

| **互動式通訊** |
|---|
| 使用具有動態資料整合的視覺化編輯器，建立以檔案為中心的通訊，如宣告、發票和通知。 |
| **功能：**&#x200B;設計個人化通訊，將靜態內容與動態資料結合，以供列印與數位頻道使用。 |
| **何時使用：**&#x200B;客戶對帳單、發票、通知、個人化通訊、檔案繁重的工作流程。 |
| 📄視覺檔案設計📄動態資料整合📄多管道輸出📄 Personalization |
| [開始使用互動式通訊→](/help/forms/introduction-to-interactive-communication.md) |

## 🔗資料與整合 {#data-integration}

將表單連線至後端系統和資料來源，以實現順暢的資訊流程和即時資料交換。

### 表單資料模型 {#form-data-model}

| **表單資料模型** |
|---|
| 具有預先填入、驗證和提交功能的統一介面，可連線多個資料來源。 一致模型背後的抽象整合複雜性。 |
| **功能：**&#x200B;建立統一的資料層，將表單連線至具有一致介面和資料流程管理的多個後端系統。 |
| **何時使用：**&#x200B;多重資料來源整合、複雜的資料關係、預先母體需求、即時資料驗證。 |
| 🔄多來源整合🔄資料模式🔄預先填入🔄驗證規則🔄統一介面 |
| [開始使用表單資料模型→](/help/forms/create-form-data-models.md) |

### RESTful聯結器 {#restful-connectors}

| **RESTful聯結器** |
|---|
| 透過RESTful API與任何可由Web存取的服務直接整合。 連線至自訂API和網站服務。 |
| **功能：**&#x200B;透過提交動作或資料整合，啟用表單中的直接API呼叫，以便即時連線至網路服務。 |
| **何時使用：**&#x200B;自訂API整合、網站服務連線、即時資料交換、協力廠商服務整合。 |
| 🌐直接API呼叫🌐即時連線🌐彈性整合🌐自訂服務支援 |
| [設定REST端點→](/help/forms/configure-submit-action-restpoint.md) \| [資料整合設定→](/help/forms/data-integration.md) |

### Salesforce聯結器 {#salesforce-connector}

| **Salesforce聯結器** |
|---|
| 與Salesforce CRM原生整合，用於銷售機會管理、客戶資料同步和銷售程式自動化。 |
| **它的功能：**&#x200B;預先建立的Salesforce聯結器，包含表單資料同步處理、建立銷售機會及管理客戶記錄。 |
| **何時使用：** Salesforce CRM整合、潛在客戶產生表單、客戶資料管理、銷售程式自動化。 |
| 🏢預先建立的聯結器🏢銷售機會管理🏢資料同步處理🏢銷售自動化 |
| [設定Salesforce整合→](/help/forms/configure-salesforce.md) |

### Microsoft Dynamics聯結器 {#dynamics-connector}

| **Microsoft Dynamics聯結器** |
|---|
| 與Microsoft Dynamics的企業整合，提供ERP和CRM連線能力，以及完整的業務流程支援。 |
| **功能：**&#x200B;將表單連線至Microsoft Dynamics，用於客戶管理、業務流程整合和企業資料流程。 |
| **何時使用：** Microsoft Dynamics整合、企業工作流程、客戶管理、業務流程自動化。 |
| 🏭企業連線能力🏭業務流程整合🏭客戶管理🏭資料同步處理 |
| [設定Dynamics整合→](/help/forms/configure-msdynamics.md) |

### SharePoint聯結器 {#sharepoint-connector}

| **SharePoint聯結器** |
|---|
| 檔案管理與SharePoint整合，用於檔案儲存、共同作業和檔案工作流程自動化。 |
| **它的功能：**&#x200B;在SharePoint中儲存表單提交與產生的檔案，並具有自動化檔案管理與共同作業功能。 |
| **何時使用：**&#x200B;檔案管理、團隊共同作業、檔案儲存、SharePoint工作流程。 |
| 📁檔案儲存📁 Collaboration功能📁自動化工作流程📁 SharePoint整合 |
| [設定SharePoint整合→](/help/forms/connect-forms-to-sharepoint-document-library.md) |

## 流程與工作流程 {#process-workflow}

使用全面的工作流程與處理功能，自動化業務流程、核准及檔案產生。

### AEM 工作流程 {#aem-workflows}

針對複雜的表單驅動工作流程，提供多步驟核准、任務指派及流程協調的業務流程自動化。

**它的功能：**&#x200B;建立具有核准鏈結的自動化業務流程、工作路由及表單提交的流程監視。

**何時使用：**&#x200B;核准程式、業務自動化、工作管理、複雜的工作流程、程式協調。

**主要功能：**&#x200B;程式自動化、核准鏈、工作路由、程式監控、商業規則。

[開始使用AEM工作流程→](/help/forms/aem-forms-workflow.md)

### Adobe Sign整合 {#adobe-sign}

具有法律約束力數位簽名的電子簽章工作流程直接整合到表單體驗中，以實現無縫簽名流程。

**它的功能：**&#x200B;啟用表單中的數位簽章，其中包含合法繫結的電子簽章功能以及自動化簽章工作流程。

**何時使用：**&#x200B;合約簽署、法律檔案、核准工作流程、法規要求、簽名自動化。

**主要功能：**&#x200B;法律電子簽章、簽名工作流程、法規支援、自動化程式。

[設定Adobe Sign →](/help/forms/working-with-adobe-sign.md)

### 提交動作 {#submit-actions}

使用多個處理選項（包括電子郵件、資料庫儲存、工作流程觸發器和自訂處理）來處理表單提交。

**它的功能：**&#x200B;定義使用者提交表單時會發生什麼情況 — 將資料路由到電子郵件、資料庫、工作流程或外部系統。

**何時使用：**&#x200B;表單提交處理、資料路由、通知系統、整合觸發程式。

**主要功能：**&#x200B;多重提交選項、資料路由、通知系統、整合觸發程式。

[設定提交動作→](/help/forms/configure-submit-actions-core-components.md)

### 通訊API {#communication-apis}

使用RESTful API程式化檔案產生、操作和安全性，用於高容量檔案處理和自動化。

**它的功能：**&#x200B;使用API以程式設計方式產生、控制及保護檔案，以建立PDF、檔案組合及批次處理。

**何時使用：**&#x200B;檔案自動化、大量處理、程式化產生、檔案元件、批次作業。

**主要功能：**&#x200B;檔案產生、批次處理、程式控制、檔案安全性、API自動化。

[開始使用通訊API →](/help/forms/aem-forms-cloud-service-communications-introduction.md)

## 分析與最佳化 {#analytics-optimization}

使用全方位的分析和測試功能監控表單效能、瞭解使用者行為並最佳化轉換率。

### Adobe Analytics 整合 {#adobe-analytics}

透過對完成率、放棄模式和資料導向最佳化的使用者行為的詳細分析，進行表單效能追蹤。

**它的功能：**&#x200B;透過全面報告追蹤表單互動、完成率、欄位層級分析和使用者行為模式。

**何時使用：**&#x200B;效能監視、轉換最佳化、使用者行為分析、資料導向改善。

**主要功能：**&#x200B;效能追蹤、使用者行為分析、轉換量度、詳細報告。

[設定Analytics整合→](/help/forms/integrate-aem-forms-with-adobe-analytics.md)

### 交易報告 {#transaction-reports}

使用監控和計費透明度，包含有關整個部署的API呼叫、檔案產生和可計費交易的詳細報告。

**它的功能：**&#x200B;監視API使用量、檔案產生量，以及具有詳細消耗報告和成本追蹤的可計費交易。

**使用時機：**&#x200B;使用監控、成本追蹤、容量規劃、法規遵循報告、資源最佳化。

**主要功能：**&#x200B;使用追蹤、成本監控、容量規劃、法規遵循報告。

[檢視異動報表→](/help/forms/transaction-reports-billable-apis.md)

### A/B測試整合 {#ab-testing}

透過測試不同的版面、欄位安排和使用者流程，使用統計分析來改善轉換，進而實現表單最佳化。

**它的作用：**&#x200B;測試不同的表單變數，以識別不同使用者區段和使用案例的最有效方法。

**何時使用：**&#x200B;轉換最佳化、使用者體驗測試、效能改善、資料導向設計決策。

**主要功能：**&#x200B;表單測試、統計分析、轉換最佳化、效能比較。

[瞭解表單最佳化→](/help/forms/view-understand-aem-forms-analytics-reports.md)

## 管理與治理 {#management-governance}

適用於企業規模表單部署的集中式表單管理、使用者存取控制和治理功能。

### Forms Portal {#forms-portal}

集中式表單存放庫，可在統一介面中搜尋功能、表單分類、草稿管理和提交追蹤。

**功能：**&#x200B;建立集中式表單存放庫，讓使用者可以探索、存取、管理草稿，以及透過搜尋和分類追蹤提交內容。

**何時使用：**&#x200B;表單探索、集中管理、使用者自助服務、草稿管理、提交追蹤。

**主要功能：**&#x200B;表單探索、搜尋功能、草稿管理、提交追蹤、使用者介面。

[設定Forms入口網站→](/help/forms/configure-forms-portal.md)

### 使用者管理 {#user-management}

角色型存取控制，具備組織內表單建立、編輯、發佈及管理的精細許可權。

**它的功能：**&#x200B;定義使用者角色和許可權，用於具有細微存取控制和安全性的表單管理的不同方面。

**何時使用：**&#x200B;存取控制、安全性管理、角色定義、許可權管理、組織治理。

**主要功能：**&#x200B;角色型存取、許可權管理、安全性控制、組織治理。

[設定使用者管理設定→](/help/forms/forms-groups-privileges-tasks.md)

### 版本控制 {#version-control}

表單生命週期管理，包含版本追蹤、變更歷史記錄、復原功能，以及合規性和治理的稽核追蹤。

**它的功能：**&#x200B;追蹤表單版本、維護變更歷史記錄、啟用回覆，以及針對合規性和治理需求提供稽核追蹤。

**何時使用：**&#x200B;變更管理、法規遵循需求、稽核追蹤、版本追蹤、治理程式。

**主要功能：**&#x200B;版本追蹤、變更記錄、復原功能、稽核追蹤、法規遵循支援。

[瞭解版本設定→](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)

## 產品快速入門 {#getting-started}

根據您目前的需求與技術需求，選擇您的起點。

### 表單建立快速入門 {#form-creation-start}

**對於現代專案：**&#x200B;以[核心元件Forms](/help/forms/creating-adaptive-form-core-components.md)開始

**高效能：**&#x200B;從[Edge Delivery Forms](/help/edge/docs/forms/overview.md)開始

**針對現有專案：**&#x200B;以[Foundation元件Forms](/help/forms/creating-adaptive-form.md)開始

針對XFA現代化：**從** HTML5 Forms[開始](/help/forms/introductionhtml5.md)

**檔案通訊：**&#x200B;以[互動式通訊](/help/forms/introduction-to-interactive-communication.md)開始

### 資料整合快速入門 {#integration-start}

**針對多個資料來源：**&#x200B;以[表單資料模型](/help/forms/create-form-data-models.md)開頭

Salesforce CRM的&#x200B;**：**&#x200B;開始於[Salesforce聯結器](/help/forms/configure-salesforce.md)

Microsoft Dynamics的&#x200B;**：**&#x200B;以[Dynamics Connector](/help/forms/configure-msdynamics.md)開始

**自訂API：**&#x200B;以[RESTful聯結器](/help/forms/configure-submit-action-restpoint.md)開始

**檔案儲存：**&#x200B;從[SharePoint Connector](/help/forms/connect-forms-to-sharepoint-document-library.md)開始

### 流程自動化快速入門 {#workflow-start}

**核准程式：**&#x200B;從[AEM工作流程](/help/forms/aem-forms-workflow.md)開始

**對於電子簽章：**&#x200B;開始於[Adobe Sign整合](/help/forms/working-with-adobe-sign.md)

**提交處理：**&#x200B;從[提交動作](/help/forms/configure-submit-actions-core-components.md)開始

**檔案產生：**&#x200B;以[通訊API](/help/forms/aem-forms-cloud-service-communications-introduction.md)開始

### Analytics快速入門 {#analytics-start}

**效能追蹤：**&#x200B;從[Adobe Analytics整合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)開始

**使用狀況監視：**&#x200B;開始於[交易報告](/help/forms/transaction-reports-billable-apis.md)

**最佳化深入分析：**&#x200B;以[Analytics報表](/help/forms/view-understand-aem-forms-analytics-reports.md)開始

### 管理快速入門 {#management-start}

**表單探索：**&#x200B;從[Forms入口網站](/help/forms/configure-forms-portal.md)開始

**存取控制：**&#x200B;從[使用者管理](/help/forms/forms-groups-privileges-tasks.md)開始

**變更追蹤：**&#x200B;以[版本控制](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)開始

## 架構與部署 {#architecture}

如需完整的實作指引：

- **[檢閱可擴充部署的架構模式](/help/forms/aem-forms-cloud-service-architecture.md)**
- **[設定團隊共同作業的開發環境](/help/forms/setup-local-development-environment.md)**
- 從現有系統&#x200B;**[規劃移轉策略](/help/forms/migrate-to-forms-as-a-cloud-service.md)**

## 支援與資源 {#support}

- **說明中心** — 取得實作與疑難排解方面的協助
- **社群論壇** — 與其他AEM Forms使用者和專家交流
- **專業服務** — 適用於企業部署的Adobe諮詢
- **訓練與認證** — 發展AEM Forms功能的專業知識

*選擇建置強大表單體驗所需的元件。 每個產品都可獨立運作，或與其他產品結合，以建立符合您業務需求的完整解決方案。*
