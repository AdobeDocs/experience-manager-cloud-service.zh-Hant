---
title: 2020.7.0版雲端服務 [!DNL Adobe Experience Manager] 的發行說明。
description: '[!DNL Adobe Experience Manager]作為2020.7.0版雲端服務發行說明。'
translation-type: tm+mt
source-git-commit: 5103d54bcb71d6c78894a30edafccf288a51368f
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 7%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.7.0 版的一般發行說明。

## 發行日期 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.7.0 is July 30, 2020.

## Adobe Experience Manager Sites雲端服務 {#cloud-services-sites}

### 新功能 {#what-is-new-sites}

[!DNL Experience Manager] 作為雲端服務連接器， [!DNL Adobe Target] 並 [!DNL Adobe Analytics] 透過下列方式加強：

* 新的使用者介面實作會取代以Classic UI為基礎的實作。

* 簡化使用者介面對話方塊，讓變數對應和其他組態的架構建立作業留待 [!DNL Adobe Launch]。

* 配置現在會儲存在 `/conf` Experience Manager資 `/etc/cloudsettings` 料庫中，而非儲存在。

## Adobe Experience Manager Assets 雲端服務 {#assets}

>[!NOTE]
>AEM Assets as a Cloud Service功能將於未來幾天推出。

### 新功能 {#what-is-new-assets}

* [!DNL Asset Compute Service] 是可擴充且可擴充的服務，可處理資產。 管理員可以設定Experience Manager來叫用使用建立的自訂工作 [!DNL Asset Compute Service]器。 開發人員可使用本服務來建立專業的自訂工作者，以配合複雜的使用案例。 此網站服務可針對不同的檔案類型產生縮圖、從Adobe檔案格式產生高品質的影像轉譯、編碼視訊（未來）、擷取中繼資料、擷取全文做為索引的先驅，並透過所有可用的Sensei服務執行資產。 請參 [閱使用資產微服務和處理配置檔案](/help/assets/asset-microservices-configure-and-use.md)。

* 將初始配置 [!DNL Dynamic Media] 改 [!DNL Experience Manager] 進為雲端服務，使其更強穩。 現在，它可為管理員提供流程的進度。

* 將資產發佈至 [!DNL Dynamic Media] 簡化並增強其強穩性，因為它是使用資產微服務的整體資產處理管道的一部分，並改善批次發佈後端。

* 與雲端服務部署不相容的工作流程步驟現在會在工作流程模型編輯器中標示 [!UICONTROL 為警告] 。 此外，在雲端服務環境上執行現有工作流程時，會略過不相容的工作流程步驟。

* 由客戶在與Cloud Manager中的環境相關聯的Git專案中 `/conf/global` 所建立的工作流程模型會自動部署至Experience Manager中， `/var` 並因此可供使用。 客戶所變更的產 `/libs` 品工作流程模型不會自動部署至 `/var`。

## 核心元件 {#core-components}

### 新功能 {#what-is-new-core-components}

[核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 2.11.0 版現已隨附於 AEM Sites，其中包含：

* 新 [PDF檢視器元件簡介](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html)

* [Accelerated Mobile Pages(AMP)支援核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/developing/amp.html) ，透過從Google行動搜尋結果進入網站時即時進行頁面轉換，有助於提高客戶體驗，進而改善使用者參與度和搜尋引擎最佳化(SEO)。

* 與 [Adobe Client資料層1.0.2版相容](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html)

* 錯誤修正和程式碼品質改良

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Cloud Manager  2020.7.0版的發行日期為2020年7月9日。

### 新功能 {#what-is-new-cloud-manager}

* 環境頁面已重新設計。

* 休眠的環境現在在Cloud Manager中，當休眠時會顯示離散狀態。

* 每個環境的環境變數數已增加到200個。

* Cloud Manager管道現在支援客戶集變數和機密。

   如需詳細 [資訊，請參閱](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) 「管線變數」。

### 錯誤修正 {#bug-fixes-cm}

* 從Cloud Manager到Developer Console的連結在完全建立環境之前未正確啟用。

* 直接從Cloud Manager連結至「開發人員主控台」時，不會顯示沙盒程式環境的解除休眠／休眠選項。

* 「非 **生產管線** 」(Non-Production Pipeline)編輯頁面上的「取消」(Cancel)和「保存 **** 」(Save)選項並不總是可見。

* 程式碼品質處理中的某些失敗可能會導致記錄檔無法正確產生。

* 建立新程式時，建議的名稱有時會返回現有程式名稱的副本。

* 有些大型管線步驟記錄無法一貫地透過使用者介面下載。

* 驗證環境名稱時會出現一個逐項錯誤。

* 「環境」頁面有時會在無顯示時顯示發佈和分派器區段。

### 已知問題 {#known-issues}

* 由於程式碼涵蓋範圍的計算方式有所變 *更* ,Jacoco外掛程式的最低版本現在為0.7.5.201505241946（2015年5月發行）。 明確參照舊版的客戶會在程式碼品質程式中收到錯誤訊息。


## Adobe Experience Manager雲端服務基礎 {#cloud-foundation}

### 新功能 {#what-is-new-foundations}

* [日誌可以轉發到Splunk帳戶](/help/implementing/developing/introduction/logging.md#splunk-logs)，這允許組織利用其Splunk投資。

* [可為以Java代碼寫程式的出站通信分配靜態](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) 、專用的出站IP地址，這對某些整合可能非常有用。

* 將AEM Analytics雲端服務UI從Classic UI移植到新的AEM UI。 此外，也將Analytics雲端服務在AEM儲存庫中的位置 `/etc` 從移 `/conf`至，以與其他AEM雲端服務一致。

* 將AEM Target雲端服務UI從Classic UI移植至新的AEM UI。 也將AEM儲存庫中Target雲端服務的位置從移 `/etc` 動到 `/conf`，以與其他AEM雲端服務一致。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請依照本節瞭解Cloud Readiness Analyzer 1.0.2版的新增功能和更新。

### 錯誤修正 {#cra-bug-fixes}

* CRA的舊版無法在Adobe Experience Manager(AEM)6.1上執行。 已新增明確支援，允許管理員群組中的使用者。

   如需詳細 [資訊，請參閱「在AEM 6.1上安裝CRA](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) 」。

* 摘要報表上顯示的到期時間戳記不正確。

* CRA正在檢測重複的定製元件。

* 在AEM 6.1中，內容檢查在完成完整檢查之前即已結束。 已添加異常處理，允許檢查員跳過並繼續，直到完全檢查完成。
