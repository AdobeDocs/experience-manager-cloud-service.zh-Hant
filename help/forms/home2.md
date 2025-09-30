---
title: AEM Forms as a Cloud Service 簡介
description: 探索建立最適化表單、自動化工作流程和管理數位檔案的AEM Forms功能。 完整的表單式業務流程平台。
landing-page-description: 瞭解如何使用AEM Forms as a Cloud Service建立最適化表單、處理檔案和自動化業務工作流程。
keywords: AEM Forms，調適型表單，表單產生器，數位表單，工作流程自動化，檔案服務，表單資料模型
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
exl-id: 50d7ce19-7d76-4ea1-a54c-8ca0e5379982
source-git-commit: eca09e1bf2ba4466f54e915e01218cc89cf5b116
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# AEM Forms as a Cloud Service 簡介 {#introduction}



Adobe Experience Manager Forms as a Cloud Service提供全方位的平台，可建立、管理和最佳化數位表格體驗。 組織可使用AEM Forms將紙面流程數位化、建立回應式網頁表單、自動化檔案工作流程，並大規模提供個人化通訊。

此平台結合表單製作功能與強大的後端服務，可讓您建立從簡單連絡表單到複雜多步驟業務應用程式的所有內容。 使用雲端原生架構，您無需管理基礎建設，即可取得自動更新、彈性擴充及企業級安全性。

本指南會介紹圍繞完整表單生命週期（從初始設計到持續最佳化）組織的核心功能。

## AEM Forms的新增功能 {#whats-new}

**最新發行亮點：**

- **日期與時間輸入元件** — 透過日曆和時鐘介面增強使用者輸入，以精確選擇日期與時間
- **增強型檔案上傳安全性** — 自動驗證和內容型別檢查，以防止不支援的檔案格式
- **改善錯誤處理** — 使用自訂提交動作的特定錯誤碼進行更好的偵錯
- **記錄檔案增強功能** — 用於排除隱藏欄位的選項，以產生更乾淨的檔案

**發行前功能：**

- **AFP格式支援** — 具有通訊API的企業級列印功能
- **規則編輯器增強功能** — 現代JavaScript支援、動態變數和內容感知面板規則
- **增強型驗證方法** — 面板、欄位和表單層級驗證，具有更優異的彈性

[檢視完整發行說明→](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## 搶先體驗方案 {#early-access}

在尖端的AEM Forms創新技術正式推出之前，先取得這些技術的專屬存取權。

**目前的早期存取功能：**

- **AEM Forms AI助理** — 用於自動化表單建立、面板產生和最佳化建議的Generative AI
- **手寫簽名元件** — 使用滑鼠、手寫筆或觸控熒幕在表單中直接擷取簽名
- **直接API整合** — 無需表單資料模型設定，即可連線至規則編輯器中的API
- **Forms最佳化** - AI支援的效能分析和轉換率改善建議

**加入程式：**
率先存取創新內容，並協助塑造AEM Forms的未來。

[要求存取→](mailto:aem-forms-ea@adobe.com) | [深入瞭解→](/help/forms/early-access-ea-features.md)


## 核心功能 {#core-capabilities}

AEM Forms支援從初始建立到持續最佳化的完整數位表單歷程。 每個階段都建立在上一階段的基礎之上，為表單式業務流程建立完整的平台。

**AEM Forms工作流程歷程：**

    建立→控管→發佈→擷取→程式→整合→追蹤→封存→改善
    ↓        ↓        ↓         ↓         ↓         ↓          ↓       ↓        ↓
    設計   檢閱   部署   收集   控點   連線   監視器存放區   最佳化
    ↑                                                                              ↓
    ←←←←←←←←←←←←←←←持續改善回圈←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←

### 建立：表單設計與開發 {#create}

使用針對不同需求和技術需求量身打造的多種製作方法，建立調適型表單。

**視覺化表單產生器**
使用[核心元件](/help/forms/creating-adaptive-form-core-components.md)、[基礎元件](/help/forms/creating-adaptive-form.md)或[Edge Delivery Services](/help/edge/docs/forms/overview.md)，透過拖放介面設計回應式表單。 視覺化編輯器提供立即的意見反應，同時維持可在各種裝置和輔助技術中使用的簡潔語意標籤。

**檔案式製作**
透過[Edge Delivery Services](/help/edge/docs/forms/overview.md)，使用熟悉的工具(例如Microsoft Excel)建立表單。 此方法可讓內容作者在不具備技術專業知識的情況下建立高效能表單，同時取得優異的Google Lighthouse分數。

**範本和主題**
使用預先建立的[範本](/help/forms/template-editor-core-components.md) （定義結構和初始內容）加速表單建立。 套用一致品牌化與[主題](/help/forms/using-themes-in-core-components.md)，控制多個表單的視覺樣式，確保設計一致並縮短開發時間。

**資料整合**
在設計階段將表單連線到後端系統。 [表單資料模型](/help/forms/create-form-data-models.md)提供可連線多個資料來源的統一介面，啟用[預先填入](/help/forms/prepopulate-adaptive-form-fields.md)、[驗證規則](/help/forms/rule-editor-core-components.md)，以及表單與業務系統之間的順暢資料流。

**驗證和條件邏輯**
實作[條件式邏輯](/help/forms/rule-editor-core-components.md)、漸進式揭露和調適型驗證，以引導使用者完成複雜的程式。 [儲存並繼續功能](/help/forms/save-core-component-based-form-as-draft.md)可讓使用者跨多個工作階段完成表單。

**HTML5 Forms**
針對行動裝置和舊版瀏覽器，將XFA型表單轉譯為[HTML5表單](/help/forms/introductionhtml5.md)。 HTML5 Forms提供原生行動體驗，不含外掛程式，同時維護表單邏輯和原始XDP範本的驗證。

**互動式通訊**
使用視覺化編輯器建立以檔案為中心的通訊，例如宣告、發票和通知。 [互動式通訊](/help/forms/interactive-communication/create-interactive-communication.md)結合靜態內容與動態資料，以產生跨列印與數位通道的個人化通訊。

### 控管：檢閱與法規遵循 {#govern}

建立監督和核准程式，以確保表單符合組織標準和法規要求。

**工作流程型核准**
透過具有角色型指派的多步驟稽核流&#39;b5&#39;7b來遞送表單設計。 利害關係人可以在發佈之前[檢閱](/help/forms/create-reviews-forms.md)、[註解](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)並核准表單，使用[AEM工作流程](/help/forms/aem-forms-workflow.md)維護品質控制和合規性監督。

**版本管理**
追蹤表單版本並維護法規遵循的稽核軌跡。 內建[版本設定](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)可確保您可以復原變更、比較反複專案，以及維護規範稽核的歷史記錄。

**存取控制與許可權**
定義建立、編輯和發佈表單的精細許可權。 [角色型存取](/help/forms/forms-groups-privileges-tasks.md)可確保只有授權的使用者才能修改表單，同時維持敏感業務流程的職責分離。

### 發佈：多管道分佈 {#publish}

跨多個管道和接觸點部署表單，以便聯絡任何位置的使用者。

**全通路發佈**
將表單發佈至[AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)、獨立網頁、行動應用程式，或[內嵌在協力廠商系統](/help/forms/embed-adaptive-form-core-components-external-web-page.md)。 單一來源發佈可確保一致性，同時適應不同的頻道需求。

**本地化與Personalization**
使用[AEM的翻譯工作流程](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md)以多種語言傳遞表單，同時支援[由左至右及由右至左的語言](/help/forms/right-left-languages.md)。 與Adobe Target整合，根據使用者區段、行為或內容資料來個人化表單體驗。

**效能最佳化**
運用Edge Delivery Services實現快如閃電的表單載入和最佳的SEO效能。 內容傳遞網路可確保全域協助工具，並將延遲降至最低。

**Forms入口網站**
建立集中式表單存放庫，讓使用者可以探索、存取和管理表單。 [Forms Portal](/help/forms/configure-forms-portal.md)在統一介面中提供搜尋功能、表單分類、草稿管理和提交追蹤，以增強使用者體驗。

### 擷取：使用者體驗和資料收集 {#capture}

最佳化表單填寫體驗，以最大化完成率和資料品質。

**回應式設計**
Forms會自動適應不同的熒幕大小和輸入方法。 觸控最佳化的控制項、鍵盤導覽及熒幕助讀程式相容性，可確保所有使用者型別都有[協助工具](/help/forms/creating-accessible-adaptive-forms.md)。

**數位簽章**
整合[Adobe Sign](/help/forms/working-with-adobe-sign.md)，以在表單體驗中取得合法繫結的電子簽章。 使用者無需離開表單即可簽署檔案，簡化核准流程並減少放棄情形。

**提交動作**
設定[提交動作](/help/forms/configure-submit-actions-core-components.md)，以定義使用者完成並提交表單時會發生的情況。 將資料路由至電子郵件、資料庫、工作流程或外部系統，同時提供立即的意見回饋和確認給使用者。

### 處理：提交處理與路由 {#process}

利用強大的處理、驗證和路由功能處理表單提交。

**資料驗證與處理**
透過伺服器端驗證和自動化處理規則，確保資料完整性。 為使用者產生回條、確認或後續追蹤資料時，轉換、驗證及遞送提交的資料。

**通訊API**
透過[RESTful API](/help/forms/aem-forms-cloud-service-communications-introduction.md)以程式設計方式產生、操控及保護檔案。 建立PDF、可供列印的格式、組合檔案、套用數位簽章，以及處理企業規模檔案工作流程的大量批次作業[](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)。

**記錄檔案**
自動產生表單提交的PDF記錄，以供遵循和使用者確認。 [記錄檔案](/help/forms/generate-document-of-record-core-components.md)會建立已完成表單的格式化、可列印版本，其中包含提交的資料，提供交易和法規要求的正式檔案。

**工作流程協調流程**
根據表單提交觸發複雜的業務流程。 透過核准鏈路由資料、將任務指派給特定使用者，並自動化例行作業，同時維護稽核軌跡。

**錯誤處理與復原**
內建的重試機制和遞補處理可確保不會遺失任何提交。 完整的記錄功能有助於疑難排解問題，並維護服務等級協定。

### 整合：後端連線 {#integrate}

將表單連線至現有業務系統和資料來源，以順暢地傳輸資訊。

**預先建立的聯結器**
與[Salesforce](/help/forms/configure-salesforce.md)、[Microsoft Dynamics](/help/forms/configure-msdynamics.md)、[SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md)和Adobe Experience Cloud解決方案的原生整合。 預先建立的聯結器可減少開發時間，同時確保可靠的資料同步化。

**RESTful API整合**
透過[提交動作](/help/forms/configure-submit-action-restpoint.md)或[資料整合](/help/forms/data-integration.md)，透過RESTful API連線到任何可由Web存取的服務。 表單資料模型可抽象化整合複雜性，提供一致的介面，無論基礎系統架構為何。

**即時資料交換**
啟用表單與業務系統之間的雙向資料流。 透過全面的[資料整合](/help/forms/data-integration.md)，從現有記錄預先填入表單、針對即時資料進行驗證，以及在提交時同時更新多個系統。

### 追蹤：分析和效能監視 {#track}

透過全面分析和監控，瞭解表單效能和使用者行為。

**表單分析**
透過[Adobe Analytics整合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)追蹤完成率、放棄模式和欄位層級互動。 識別摩擦點、測量轉換漏斗，並瞭解不同區段中的使用者行為。

**效能監視**
監視表單載入時間、提交成功率和系統效能。 即時儀表板可提供技術健全狀態和使用者體驗量度的深入分析。

**Business Intelligence**
產生表單使用量、提交量及程式效率的報告。 Analytics會提供容量規劃、使用者體驗最佳化及業務流程改良的相關資訊。

**交易報告**
監控AEM Forms部署中的API使用情形、檔案產生磁碟區和[可記帳交易](/help/forms/transaction-reports-billable-apis.md)。 追蹤消耗模式、最佳化資源配置，並維持使用授權要求的合規性。

### 封存：檔案管理與法規遵循 {#archive}

安全地儲存和管理表單提交和產生的檔案，以供長期保留和法規遵循。

**檔案儲存空間**
在AEM的數位資產管理系統中儲存產生的檔案和表單提交，或與外部檔案存放庫(例如[SharePoint](/help/forms/configure-submit-action-sharepoint.md)、[OneDrive](/help/forms/configure-submit-action-onedrive.md)或[Azure Blob儲存體](/help/forms/configure-submit-action-azure-blob-storage.md))整合。

**法規遵循與保留**
實施符合法規要求（包括GDPR、CCPA和HIPAA）的資料保留政策。 [自動封存程式](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)確保檔案會保留所需時間，並在適當時安全處置。

**安全性與存取控制**
將加密、數位簽章和[角色型存取控制](/help/forms/forms-groups-privileges-tasks.md)套用至封存的檔案。 稽核追蹤會追蹤檔案存取權及合規性報告和安全性監督的修改。

### 改善：最佳化及增強功能 {#improve}

透過資料導向的深入分析和測試，持續最佳化表單效能和使用者體驗。

**A/B測試整合**
使用Adobe Target測試不同的表單版面配置、欄位排列和使用者流程。 統計分析有助於識別針對不同使用者區段和使用案例的最有效方法。

**Analytics驅動的最佳化**
分析使用者行為資料以找出改善機會。 [檢視並了解熱度對應、欄位互動分析和放棄模式識別的分析報告](/help/forms/view-understand-aem-forms-analytics-reports.md)，以告知反複設計增強功能。

**反複式增強功能**
根據使用者意見、績效指標和業務需求實施持續改進流程。 [版本控制](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)和復原功能可啟用安全的實驗和快速反複專案。

## 快速入門 {#getting-started}

您採取的方法取決於您眼前的需求和長遠目標。

### 快速入門：簡單Forms {#quick-start}

根據您的技術背景和效能需求，選擇您偏好的撰寫方法：

**視覺化表單建置：**

1. **[使用核心元件建立最適化表單](/help/forms/creating-adaptive-form-core-components.md)**，用於新式、回應式表單
2. **[設定提交動作](/help/forms/configure-submit-actions-core-components.md)**&#x200B;以處理表單資料
3. **[在AEM Sites中內嵌表單](/help/forms/embed-adaptive-form-aem-sites.md)**&#x200B;或透過直接連結共用

**檔案式製作：**

1. **[使用Excel建立表單](/help/edge/docs/forms/create-forms.md)**&#x200B;搭配Edge Delivery Services以進行高效能表單
2. **[發佈至Edge Delivery](/help/edge/docs/forms/publish-forms.md)**&#x200B;以獲得最佳載入速度和SEO

**舊版表單支援：**

- 針對行動裝置最佳化的XFA表單轉譯，**[HTML5 Forms](/help/forms/introductionhtml5.md)**

### 進階實作：業務流程 {#advanced-implementation}

對於涉及多個系統、檔案產生和核准工作流程的複雜需求：

**資料整合和工作流程：**

1. **[設定表單資料模型](/help/forms/create-form-data-models.md)**&#x200B;以連線後端系統
2. **[設計工作流程流程](/help/forms/aem-forms-workflow.md)**&#x200B;以進行核准和路由
3. **[設定Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)**&#x200B;以測量效能

**檔案服務與通訊：**

1. **[實作通訊API](/help/forms/aem-forms-cloud-service-communications-introduction.md)**&#x200B;以自動產生檔案
2. **[建立互動式通訊](/help/forms/interactive-communication/create-interactive-communication.md)**&#x200B;以取得個人化的宣告和通知
3. **[設定Forms入口網站](/help/forms/configure-forms-portal.md)**&#x200B;以集中管理表單

### 企業部署：規模與控管 {#enterprise-deployment}

對於需要治理、合規性和監控的組織範圍部署：

**架構與治理：**

1. **[檢閱可擴充部署的架構模式](/help/forms/aem-forms-cloud-service-architecture.md)**
2. **[設定使用者管理](/help/forms/forms-groups-privileges-tasks.md)**&#x200B;和存取控制
3. **[設定團隊共同作業的開發工作流程](/help/forms/setup-local-development-environment.md)**

**移轉與監視：**

1. 從現有系統&#x200B;**[規劃移轉策略](/help/forms/migrate-to-forms-as-a-cloud-service.md)**
2. **[實作交易監視](/help/forms/transaction-reports-billable-apis.md)**&#x200B;以追蹤使用情況和遵循規範

<details>
<summary><strong>❓常見問題</strong></summary>

**什麼是表單產生器？**
表單產生器是一種可讓您在不編碼的情況下建立數位表單的工具。 您可以使用拖放介面設計表單、新增文字方塊和下拉清單等欄位，並線上發佈以收集使用者的資料。

**如何建立線上表單？**
透過AEM Forms，您可以透過視覺拖放編輯器使用核心元件建立調適型表單、使用Edge Delivery Services建立高效能表單，或將基礎元件用於已建立的工作流程。 首先，請選取範本、新增表單欄位、設定資料連線，以及跨多個管道發佈。

**什麼是好的線上表單？**
良好的線上表單可快速載入行動裝置、具備清晰的標籤、使用邏輯欄位排序、包含驗證以防止錯誤，並在提交時立即向使用者提供意見回饋。

**我可以將表單與其他商務系統整合嗎？**
是的，現代表單建置器提供廣泛的整合功能。 您可以將表單連線至CRM系統、電子郵件行銷平台、資料庫、雲端儲存空間和工作流程自動化工具，以簡化您的業務流程。

**線上表單是否安全？**
專業表單建置器包含企業級的安全性功能，例如資料加密、安全資料傳輸、存取控制，以及遵守GDPR、HIPAA和CCPA等法規以保護敏感資訊。

**如何將電子簽章新增至我的表格？**
數位簽名可以使用Adobe Sign或其他電子簽章提供者直接整合到表單中。 這可讓使用者在表單體驗中簽署檔案，而不需要個別的簽名工作流程，並減少表單放棄情形。

**表單能否自動產生PDF檔案？**
可以，現代化的表單平台可在提交表單時自動產生PDF收據、確認或記錄檔案。 這對於遵循法規、儲存記錄和為使用者提供即時確認至關重要。

**如何追蹤表單效能和分析？**
表單分析可協助您瞭解完成率、放棄模式和使用者行為。 與Adobe Analytics等分析平台整合可深入分析哪些欄位會造成摩擦以及如何最佳化轉換率。

**什麼是表單工作流程自動化？**
表單工作流程自動化會透過核准程式遞送提交、指派任務給團隊成員，以及在其他業務系統中觸發動作。 如此可免除手動處理，並確保以一致的方式處理表單資料。

**如何讓殘障人士也能使用表格？**
[可存取的表單](/help/forms/creating-accessible-adaptive-forms.md)包括適當的標籤、鍵盤導覽、熒幕閱讀器相容性，以及符合WCAG准則。 這可確保所有使用者都能完成表單，無論其能力或輔助技術為何。

**表單產生器的費用是多少？**
AEM Forms as a Cloud Service的定價取決於您的特定需求、使用量和功能需求。 如需詳細的定價資訊，以及討論適合您組織的解決方案，請聯絡Adobe銷售人員或您的Adobe代表。

</details>

## 後續步驟 {#next-steps}

探索符合您目前優先順序的功能：

- **[建置您的第一個表單](/help/forms/creating-adaptive-form-core-components.md)**&#x200B;以體驗編寫環境
- **[檢閱架構選項](/help/forms/aem-forms-cloud-service-architecture.md)**&#x200B;以進行部署規劃
- **[設定您的開發環境](/help/forms/setup-local-development-environment.md)**&#x200B;以進行團隊共同作業
- **[探索整合選項](/help/forms/data-integration.md)**&#x200B;以連線現有系統

如需完整的實作指引，請考慮Adobe Professional Services以加快部署，並確保從一開始就使用最佳實務。
