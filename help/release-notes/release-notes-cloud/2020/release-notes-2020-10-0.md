---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0版發行說明。'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 24%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager] as a Cloud Service 2020.10.0版的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0版的發行日期為2020年10月28日。
下列版本(2020.11.0)將於2020年12月1日發行。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* **[核心元件2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**： Adobe Experience Manager as a Cloud Service受益於核心元件最新版本的自動更新。 版本2.12.0包含社群貢獻的最新改善。 改良功能包括[新的POST表單處理常式；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data)可透過內容感知組態包含自訂CSS、JavaScript和中繼資料[標籤；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)以及[`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components)公用程式，以簡化自訂元件中的Adobe資料層整合。 檢視2.12.0中的[變更清單](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)。

* **[專案原型24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**：啟動新Experience Manager專案的建議基礎已有所改善。 它現在包含新的[Adobe使用者端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)、[在AMP中傳遞網站的選項](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html)，以及新增專案CSS/JS[的新](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)擴充功能點。

* **[ContextHub資料夾](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**：能夠建立對象資料夾，以輕鬆組織、尋找和選取要用於ContextHub選件鎖定目標功能的對象區段。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe AI]支援的視訊智慧標籤**：透過套用AI模型來分析物件和動作特定標籤的視訊內容，DAM使用者可以花更少的時間新增標籤，而花更多時間使用公開的、豐富的資訊。 反過來，您也能為客戶提供合適的體驗。 請參閱[智慧標籤視訊資產](/help/assets/smart-tags-for-videos.md)。

* **Brand Portal增強功能**： [!DNL Brand Portal]提供下列新功能及其他專案。 如需詳細資訊，請參閱[[!DNL Brand Portal] 發行說明](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)。

   * [改善下載體驗](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)，提供簡化及快速的下載。 管理員可設定額外的下載組態，以提供符合使用者和企業需求的體驗。
   * 現在可以從任何頁面一鍵導覽至檔案、[集合](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)和共用連結。
   * 使用者現在可以[選取並下載特定轉譯](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page)。 可透過「資產」詳細內容頁面的「轉譯」面板新的轉譯下載選項。
   * 訪客使用者作業逾時15分鐘可確保所有同時使用者獲得更理想的體驗。

* **[!DNL Adobe Asset Link]2.1**&#x200B;版： [、](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)和[!DNL Adobe Photoshop]的新版[!DNL Adobe Illustrator]Adobe Asset Link[!DNL Adobe InDesign]擴充功能已推出。 它新增與2020年10月發行之2021版的最新[!DNL Adobe Creative Cloud]應用程式的相容性。

* **[!DNL Assets]WebP檔案支援**： [!DNL Assets] as a Cloud Service現在支援WebP影像格式。 WebP是Google建立的新興影像格式。 WebP檔案格式的影像在視覺上與JPG或PNG檔案沒有區別，且檔案較小。 降低資產的檔案大小可改善頁面載入時間，並幫助內容建立者提供更快速的網頁體驗。 瞭解如何在[建立處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)中使用WebP。

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**：您現在可以透過Adobe Analytics for Adaptive Forms擷取及追蹤已登入和未登入（匿名）的行為，以收集使用者的深入解析。 它可協助業務使用者根據所收集的深入分析，針對最適化表單內容、版面配置和樣式做出明智的決策。

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms-oct-2021}

* **外部化AEM工作流程資料以進行安全處理**：您可以將包含敏感個人資料(SPD)元素的程式內AEM工作流程變數資料儲存在客戶管理的存放庫中，以進行安全處理。 處理工作流程時，儲存在工作流程變數中的資料不會儲存在AEM存放庫中。 系統會隨選從客戶管理的存放庫擷取。

### [!DNL Forms] 的 Beta 版功能  {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**： [通訊API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html)可幫助您合併範本和XML資料，以產生多種格式的檔案。 此服務可讓您以同步和批次模式產生檔案。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Venia參考網站 — 2020.10.2，其中包含最新CIF核心元件1.4.0版。如需詳細資訊，請參閱[CIF Venia參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2)。

* 已發行CIF Core Components v1.4.0。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0)。

### 錯誤修正 {#bug-fixes-commerce}

* 產品主控台和選取器中的GraphQL要求是透過HTTP POST完成。 此問題已修正，以確保Apollo GraphQL使用者端遵守GraphQL使用者端OSGi設定中的設定，以在設定時支援GET請求。

* CIF雲端設定UI針對/lib和/apps/中的設定顯示「儲存並關閉」按鈕。 但由於這些介面是唯讀的，因此UI已修復為僅顯示「關閉」按鈕。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Experience Manager as a Cloud Service 2020.10.0中的Cloud Manager發行日期是2020年10月02日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* 環境頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* Cloud Manager的「建置容器」現在支援使用Java™ 8或Java™ 11編譯專案。 Maven工具鏈系統支援Java™ 11。

* 每個環境的環境變數數量提高至 200 個。

* 總覽頁面上的環境卡現在會列出最多三個環境。 使用者可以選擇&#x200B;**全部顯示**按鈕，瀏覽到「環境摘要」頁面以查看包含完整環境清單的表格。
如需更多詳細資訊，請參閱[檢視環境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 環境完全建立前，從 Cloud Manager 到 Developer Console 的連結未正確啟用。

* 直接從 Cloud Manager 連結至 Developer Console 時，系統未顯示將沙箱計畫的環境解除休眠/休眠的選項。

* 非生產管道編輯頁面有時未顯示取消和儲存按鈕。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容時，顯示發佈和Dispatcher區段。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 已新增根據工作流程標題、工作流程模型、狀態、發起人、裝載路徑和開始日期來搜尋工作流程例項的支援。 請參閱[搜尋工作流程執行個體](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

## 內容轉移工具 {#content-transfer-tool}

深入瞭解[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改善記錄的使用者體驗。 擷取和內嵌記錄檔中新增的時間戳記。 已新增訊息，以指出記錄檔是否為空白。

### 錯誤修正 {#ctt-bug-fixes}

* 如果移轉集包含具有部分類似檔案名稱的路徑，則內容轉移工具會略過內容檔案。
