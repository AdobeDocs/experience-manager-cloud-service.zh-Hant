---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.7.0 版發行說明。'
description: "[!DNL Adobe Experience Manager]個2020.7.0as a Cloud Service發行說明。"
exl-id: 75d354a3-6987-4de0-aec8-24043461c516
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 72%

---

# [!DNL Adobe Experience Manager]as a Cloud Service2020.7.0版發行說明 {#release-notes}

以下章節概述 Experience Manager as a Cloud Service 2020.7.0 版的一般發行說明。

## 發行日期 {#release-date}

[!DNL Experience Manager] as a Cloud Service 2020.7.0 版的發行日期為 2020 年 7 月 30 日。

## Adobe Experience Manager Sitesas a Cloud Service {#cloud-services-sites}

### 新增功能 {#what-is-new-sites}

適用於 [!DNL Adobe Target] 和 [!DNL Adobe Analytics] 的 [!DNL Experience Manager] as a Cloud Service 連接器已完成以下強化：

* 新版使用者介面實作會取代以傳統版 UI 為基礎的實作。

* 簡化使用者介面對話方塊，將變數對應的框架建立作業和其他設定保留給 [!DNL Adobe Launch]。請參閱[整合 Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html?lang=zh-Hant) 和[整合 Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html?lang=zh-Hant)。

* 設定現在會儲存在 Experience Manager 存放庫的 `/conf`，而非 `/etc/cloudsettings`。

## [!DNL Adobe Experience Manager Assets]個as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* [!DNL Asset Compute Service] 是可擴充的資產處理服務。管理員可以設定[!DNL Experience Manager]以叫用使用[!DNL Asset Compute Service]建立的自訂應用程式。 開發人員可使用此服務建立專門的自訂應用程式，以配合複雜的使用案例。 此網站服務可針對不同的檔案型別產生縮圖、以Adobe檔案格式產生高品質的影像轉譯、影片編碼（未來功能）、擷取中繼資料、擷取全文作為索引的前導，以及透過所有可用的[!DNL Sensei]服務執行資產。 請參閱[使用資產微服務及處理設定檔](/help/assets/asset-microservices-configure-and-use.md)。

* [!DNL Experience Manager] as a Cloud Service 中 [!DNL Dynamic Media] 的初始設定經過改良，更加健全。現在可為管理員提供處理程序的進度。

* 將資產發佈至 [!DNL Dynamic Media] 的程序已簡化，且功能更健全。現在這是整體資產處理管道的重要環節，不僅使用資產微服務，並改善批次發佈後端。

* 若工作流程步驟與雲端服務部署不相容，系統會在[!UICONTROL 工作流程模型]編輯器中標示警告。此外，在Cloud Service環境中執行現有工作流程時，系統會略過不相容的工作流程步驟。

* 在與[!DNL Cloud Manager]中的環境相關聯的Git專案中，由客戶建立且部署至`/conf/global`的工作流程模型會自動部署至`/var`，因此可在[!DNL Experience Manager]中使用。 `/libs` 底下經客戶變更的產品工作流程模型則不會自動部署至 `/var`。

### 已修正的錯誤 {#assets-bugs-fixed}

* 「移動資產」精靈無法如預期為「集合」中所包含資產載入。 (CQ-4296756)
* `dam:size`和`dam:sha1`的值已從XMP回寫中排除。 (CQ-4237355)
* 大量取消發佈資產時，[!DNL Brand Portal]會產生錯誤，指出請求URI太長。 (CQ-4299474)

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

AEM Commerce現在可在Cloud Service上使用。

如需詳細資訊，請參閱[AEM Commerce快速入門as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/getting-started.html?lang=zh-Hant)。

## 核心元件 {#core-components}

### 新增功能 {#what-is-new-core-components}

[AEM 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 2.11.0 版現在隨附於 AEM Sites，其中包含：

* 導入最新 [PDF 檢視器元件](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/pdf-viewer.html)。

* 提供核心元件的 Accelerated Mobile Pages (AMP) 支援。從 Google 行動搜尋結果進入網站時，系統會即時轉換頁面，有助於提供更快速的客戶體驗，進而改善使用者參與和 SEO。
如需詳細資訊，請參閱核心元件的[AMP支援](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html?lang=zh-Hant)。

* 與 [Adobe 用戶端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=zh-Hant) 1.0.2 版相容。

* 錯誤修正並提升程式碼品質。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

[!UICONTROL Cloud Manager] 2020.7.0 版於 2020 年 7 月 9 日正式發佈。

### 新增功能 {#what-is-new-cloud-manager}

* 環境頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* 每個環境的環境變數數量提高至 200 個。

* Cloud Manager 管道現在支援客戶設定變數和機密。

  如需更多詳細資訊，請參閱管道變數。

* 現在支援身份驗證綁定的私有 Maven 存放庫。

* Cloud Manager 建置容器現可支援 Java 8 和 Java 11。如需更多詳細資訊，請參閱使用 Java 11 支援。

### 錯誤修正 {#bug-fixes-cm}

* 環境完全建立前，從 Cloud Manager 到 Developer Console 的連結未正確啟用。

* 直接從 Cloud Manager 連結至 Developer Console 時，系統未顯示將沙箱計畫的環境解除休眠/休眠的選項。

* 非生產管道編輯頁面有時未顯示&#x200B;**取消**&#x200B;和&#x200B;**儲存**&#x200B;選項。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容的情況下，顯示發佈和發送器區段。

### 已知問題 {#known-issues}

* 由於程式碼涵蓋範圍的計算方式有所變更，Jacoco 外掛程式的&#x200B;*最低*&#x200B;版本現在是 0.7.5.201505241946 (2015 年 5 月發佈)。若客戶明確參考較舊版本，會在程式碼品質處理程序中收到錯誤訊息。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-foundation}

### 新增功能 {#what-is-new-foundations}

* [記錄檔可轉送至Splunk帳戶](/help/implementing/developing/introduction/logging.md#splunk-logs)，讓組織能夠使用其Splunk投資。

* 可為以 Java 程式碼編寫的傳出流量指派[靜態的專屬輸出 IP 位址](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address)，這對某些整合功能可能會相當實用。

* 將 AEM Analytics 雲端服務 UI 從傳統版 UI 移植到新版 AEM UI。另外，Analytics 雲端服務在 AEM 存放庫中的位置也已從 `/etc` 移至 `/conf`，與其他 AEM 雲端服務一致。

* 將 AEM Target 雲端服務 UI 從傳統版 UI 移植到新版 AEM UI。另外，Target 雲端服務在 AEM 存放庫中的位置也已從 `/etc` 移至 `/conf`，與其他 AEM 雲端服務一致。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請參照本節，了解 Cloud Readiness Analyzer v1.0.2 版的新增功能和更新。

### 錯誤修正 {#cra-bug-fixes}

* CRA 較早版本無法在 Adobe Experience Manager (AEM) 6.1 上執行。新增明確支援，讓管理員群組中的使用者使用。

  如需詳細資訊，請參閱[在AEM 6.1](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html?lang=zh-Hant#installing-on-aem61)上安裝CRA 。

* 摘要報告顯示的到期時間戳記不正確。

* CRA 偵測到重複的自訂元件。

* AEM 6.1 中，內容檢查在完整檢查完成前結束。新增例外狀況處理程序，在完整檢查完成前，讓檢查人員可以選擇略過及繼續。
