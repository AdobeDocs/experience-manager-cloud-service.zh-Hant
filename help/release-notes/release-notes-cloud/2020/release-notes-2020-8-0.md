---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.8.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0版發行說明。'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
feature: Release Information
role: Admin
source-git-commit: 2aea79d42ef9627a8fc758077a7ee012592888d7
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 35%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0版發行說明 {#release-notes}

以下章節概述 Experience Manager as a Cloud Service 2020.8.0 版的一般發行說明。


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 能夠[將頁面和子頁面（頁面樹狀結構）還原為舊版](/help/sites-cloud/authoring/sites-console/page-versions.md#reinstating-versions)。

* 能夠在AEM [SPA編輯器](/help/sites-cloud/authoring/launches/overview.md)中[建立啟動](/help/implementing/developing/hybrid/introduction.md)。


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 現在資產微服務可支援視訊轉碼。 [!UICONTROL 處理設定檔]組態的新區段可讓您設定視訊位元速率和維度。 輸出格式為使用H.264轉碼器的MP4。 如需詳細資訊，請參閱[管理視訊資產](/help/assets/manage-video-assets.md#transcode-video)。 如需更多轉碼選項及視訊傳送，請使用[!DNL Dynamic Media]附加元件。

* 在新的[!DNL Experience Manager Assets]部署中，現在預設會設定智慧標籤功能。 不需要手動與[!DNL Adobe Developer Console]整合。 在現有部署中，管理員會像之前一樣設定智慧標籤整合。

* 新的[資產下載體驗](/help/assets/download-assets-from-aem.md)允許、

   * 非同步下載大量內容，以免使用者久候。
   * 適用於開發人員擴充性的新模組化API。

* 資產微服務的中繼資料擷取已改善效能。 這可增加整體資產擷取輸送量。

* 使用處理設定檔，以使用計算服務產生自訂中繼資料。 檢視使用處理設定檔[的](/help/assets/manage-metadata.md#metadata-compute-service)自訂中繼資料。

* 給Brand Portal使用者更簡單的下載體驗，管理員可加以設定。 請參閱[下載體驗總覽](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hant#download-configurations)。

* Brand Portal現在提供原生和高解析度PDF檔案預覽。 請參閱[檔案檢視器概觀](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hant#doc-viewer)。

* 您現在可以直接從AEM as a Cloud Service中的[!DNL Dynamic Media]使CDN （內容傳遞網路）快取失效（不必使用[!DNL Dynamic Media Classic]）。 這可確保在幾分鐘內提供最新資產，而非幾小時。 請參閱[透過Dynamic Media使CDN快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)。

* 已在[!DNL Assets]中為使用者介面控制項、導覽、瀏覽及搜尋體驗新增增強的協助工具支援。

   * 如果您在選取[!UICONTROL 新增轉譯]選項後按下Esc鍵，焦點會回到工具列。<!-- via CQ-4293594-->
   * 使用電子郵件下拉式方塊時，鍵盤焦點會如預期運作。<!-- via CQ-4286215 -->
   * 搜尋篩選器區段中的摺疊式功能表元素會解譯為標準可展開的摺疊式功能表。<!-- via CQ-4273103 -->
   * 將標籤套用至資產時，對話方塊會將標籤顯示為樹狀元素。 ARIA屬性已適當套用至樹狀元素，以便現在可加以存取。<!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版現已推出。 它改善了與[!DNL Experience Manager] 6.5.5 Service Pack的相容性，並擁有更新的使用者端作業系統相容性清單。 不支援10.14之前的[!DNL Windows] 7和[!DNL macOS]版本。

### 修正在 [!DNL Assets] 中的錯誤 {#bugs-fixed}

* 第一次按一下「建立關聯及取消關聯」選項時，該選項沒有回應。 (CQ-4299022)
* 下載資產時，如果您選取透過電子郵件接收資產的選項，則不會傳送電子郵件。 (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品主控台功能現已推出。 這可讓AEM中的行銷人員/作者檢視及導覽儲存於商務後端的類別和產品。 此外，產品主控台也支援類別和產品屬性。

* 產品和類別選擇器經過改良，行銷人員可透過SKU選取產品，或透過類別ID選取類別。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

[!UICONTROL Cloud Manager] 2020.8.0版的發行日期為2020年8月06日。

### 新增功能 {#what-is-new-cloud-manager}

* 內容稽核是 Cloud Manager Sites Production Pipelines 上啟用的一項功能。具有 Sites 的計畫的生產管道配置現在包括名為的第三個索引標籤&#x200B;**內容稽核**。生產管道執行期間，只要自訂功能完成測試，管道中就會增加新的內容稽核步驟，以根據多項維度評估網站，包括效能、SEO （搜尋引擎最佳化）、協助工具、最佳作法和PWA （漸進式網頁應用程式）。


  >[!NOTE]
  >此後，內容稽核已重命名為體驗稽核。

  如需更多詳細資訊，請參閱[體驗稽核測試](/help/implementing/cloud-manager/reports/report-experience-audit.md)。

* Assets 計畫中新建立的環境現在將自動設定智慧內容服務。

* 休眠的環境可以從 Cloud Manager 的&#x200B;**概觀**&#x200B;頁。

* 能夠在頁面上執行經驗檢查，由 Google Lighthouse 提供支援。作為 Cloud Manager 管道的一部分，最多可以根據體驗 KPI 檢查和驗證 25 個頁面，並且分數會顯示在 Cloud Manager UI 中。

### 錯誤修正 {#bug-fixes-cm}

* 作為程式碼品質掃描的一部分，正在執行一些不必要和不受歡迎的 SonarQube 插件。

* 在管道執行頁面上，分支名稱的格式不正確。

* 在某些情況下，已完成的管道執行未成功記錄為已完成，從而阻止了管道的新執行。

* 管道執行偶爾會得到&#x200B;*卡住*&#x200B;由於內部溝通問題。

* 在配置新組織時，某些具有系統管理員以外的管理角色的使用者被錯誤地授予對 Cloud Manager 的存取權限。

* 在某些情況下，更新索引作業會並行啟動多次，從而導致部署失敗。

* 計畫卡上的工具提示並非始終正確。

* 在刪除環境時，使用者界面錯誤地允許在環境中嘗試操作。

* Cloud Manager 的顏色不匹配&#x200B;**概觀**&#x200B;頁。

### 已知問題 {#known-issues-cm}

* 包含無效頁面，使內容稽核平均分數低於應有的水平。

* 內容稽核索引標籤使用作者域而不是發布域錯誤地顯示了 BASE URL。

* 若要啟動內容稽核步驟，使用者必須編輯管道並 (可選) 新增頁面。如果沒有新增任何頁面，則會稽核首頁。

## 內容轉移工具 {#content-transfer-tool}

請詳閱本節，瞭解「內容轉移工具」版本1.0.4的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 「內容轉移工具」現在支援共用的S3資料存放區。

### 錯誤修正 {#ctt-bug-fixes}

* 工具完成動作已新增其他逾時。

* 即使紀錄顯示錯誤，舊版UI有時仍會顯示成功擷取。

## 程式碼重構工具 {#code-refactoring-tools}

請詳閱本節，瞭解程式碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* 推出AIO-CLI增效模組，整合了程式碼重構工具，讓開發人員得以從單一位置叫用及執行程式碼重構工具。 如需詳細資訊，請參閱[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)。

* AEM Dispatcher Converter擴充後，可支援將內部部署和Adobe Managed Services Dispatcher設定轉換為與AEM as a Cloud Service相容的Dispatcher設定。 如需詳細資訊，請參閱[Git資源：AEM雲端服務Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)。

* AEM Dispatcher Converter重新寫入` node.js `，並與AIO-CLI外掛程式整合。
