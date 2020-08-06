---
title: 2020.7.0版雲端服務 [!DNL Adobe Experience Manager] 的發行說明。
description: '[!DNL Adobe Experience Manager]作為2020.7.0版雲端服務發行說明。'
translation-type: tm+mt
source-git-commit: a2b7ca2ab6ab3c95b07de49a43c8b119a792a7ac
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 37%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.7.0 版的一般發行說明。

## 發行日期 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.7.0 is July 30, 2020.

## Adobe Experience Manager Sites雲端服務 {#cloud-services-sites}

### 新功能 {#what-is-new-sites}

[!DNL Experience Manager] 作為雲端服務連接器， [!DNL Adobe Target] 並 [!DNL Adobe Analytics] 透過下列方式加強：

* 新的使用者介面實作會取代以Classic UI為基礎的實作。

* 簡化使用者介面對話方塊，讓變數對應和其他組態的架構建立作業留待 [!DNL Adobe Launch]。 請參 [閱整合Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html)[與整合Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html)。

* 配置現在會儲存在 `/conf` Experience Manager資 `/etc/cloudsettings` 料庫中，而非儲存在。

## Adobe Experience Manager Assets 雲端服務 {#assets}

### 新功能 {#what-is-new-assets}

* [!DNL Asset Compute Service] 是可擴充且可擴充的服務，可處理資產。 管理員可以設定Experience Manager來叫用使用建立的自訂應用程式 [!DNL Asset Compute Service]。 開發人員可使用本服務來建立專業的自訂應用程式，以配合複雜的使用案例。 此網站服務可針對不同的檔案類型產生縮圖、從Adobe檔案格式產生高品質的影像轉譯、編碼視訊（未來）、擷取中繼資料、擷取全文做為索引的先驅，並透過所有可用的Sensei服務執行資產。 請參 [閱使用資產微服務和處理配置檔案](/help/assets/asset-microservices-configure-and-use.md)。

* 將初始配置 [!DNL Dynamic Media] 改 [!DNL Experience Manager] 進為雲端服務，使其更強穩。 現在，它可為管理員提供流程的進度。

* 將資產發佈至 [!DNL Dynamic Media] 簡化並增強其強穩性，因為它是使用資產微服務的整體資產處理管道的一部分，並改善批次發佈後端。

* 與雲端服務部署不相容的工作流程步驟現在會在工作流程模型編輯器中標示 [!UICONTROL 為警告] 。 此外，在雲端服務環境上執行現有工作流程時，會略過不相容的工作流程步驟。

* 由客戶在與Cloud Manager中的環境相關聯的Git專案中 `/conf/global` 所建立的工作流程模型會自動部署至Experience Manager中， `/var` 並因此可供使用。 客戶所變更的產 `/libs` 品工作流程模型不會自動部署至 `/var`。

## 核心元件 {#core-components}

### 新功能 {#what-is-new-core-components}

Release 2.11.0 of the [AEM Core Components](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) is now available as part of AEM Sites including:

* 新的 [PDF檢視器元件簡介](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html)。

* 現在提供核心元件的加速行動頁面(AMP)支援。 從Google行動搜尋結果進入網站時，透過即時轉換頁面，有助於提高客戶體驗，進而改善使用者參與度和搜尋引擎最佳化(SEO)。
有關詳細 [資訊，請參閱核心元件的AMP](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/amp.html) 支援。

* 與 [Adobe Client資料層1.0.2版相容](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html)。

* 錯誤修正和程式碼品質改良。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

[!UICONTROL Cloud Manager] 2020.7.0 版於 2020 年 7 月 9 日正式發佈。

### 新功能 {#what-is-new-cloud-manager}

* 環境頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* 每個環境的環境變數數量提高至 200 個。

* Cloud Manager 管道現在支援客戶設定變數和機密。

   如需詳細資訊，請參閱[管道變數](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables)。

### 錯誤修正 {#bug-fixes-cm}

* 環境完全建立前，從 Cloud Manager 到開發人員控制台的連結未正確啟用。

* 直接從 Cloud Manager 連結至開發人員控制台時，系統未顯示將沙箱方案的環境解除休眠/休眠的選項。

* 非生產管道編輯頁面有時未顯示&#x200B;**取消**&#x200B;和&#x200B;**儲存**&#x200B;選項。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立新方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容的情況下，顯示發佈和發送器區段。

### 已知問題 {#known-issues}

* 由於程式碼涵蓋範圍的計算方式有所變更，Jacoco 外掛程式的&#x200B;*最低*&#x200B;版本現在是 0.7.5.201505241946 (2015 年 5 月發佈)。明確參照舊版的客戶會在程式碼品質程式中收到錯誤訊息。

## Adobe Experience Manager雲端服務基礎 {#cloud-foundation}

### 新功能 {#what-is-new-foundations}

* [日誌可以轉發到Splunk帳戶](/help/implementing/developing/introduction/logging.md#splunk-logs)，這允許組織利用其Splunk投資。

* [可為以Java代碼寫程式的出站通信分配靜態](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) 、專用的出站IP地址，這對某些整合可能非常有用。

* 將AEM Analytics雲端服務UI從Classic UI移植到新的AEM UI。 此外，也將Analytics雲端服務在AEM儲存庫中的位置 `/etc` 從移 `/conf`至，以與其他AEM雲端服務一致。

* 將AEM Target雲端服務UI從Classic UI移植至新的AEM UI。 也將AEM儲存庫中Target雲端服務的位置從移 `/etc` 動到 `/conf`，以與其他AEM雲端服務一致。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新功能 {#what-is-new-commerce}

AEM Commerce現在可在Cloud Service上使用。

如需詳 [細資訊，請參閱「AEM Commerce as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/getting-started.html) 」快速入門。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請參照本節，了解 Cloud Readiness Analyzer v1.0.2 版的新增功能和更新。

### 錯誤修正 {#cra-bug-fixes}

* CRA 較早版本無法在 Adobe Experience Manager (AEM) 6.1 上執行。新增明確支援，讓管理員群組中的使用者使用。

   如需詳細資訊，請參閱[在 AEM 6.1 上安裝CRA](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61)。

* 摘要報告顯示的到期時間戳記不正確。

* CRA 偵測到重複的自訂元件。

* AEM 6.1 中，內容檢查在完整檢查完成前結束。新增例外狀況處理程序，在完整檢查完成前，讓檢查人員可以選擇略過及繼續。
