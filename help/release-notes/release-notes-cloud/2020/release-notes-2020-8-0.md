---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.8.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 作為2020.8.0的Cloud Service發行說明。'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
translation-type: tm+mt
source-git-commit: 33e92b9cd19dd49dcdb6a8c8f30feccb755f615f
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager as a Cloud Service 2020.8.0 版的一般發行說明。


## [!DNL Adobe Experience Manager Sites] Cloud Service  {#sites}

### [!DNL Sites] {#what-is-new-sites}的新增功能

* 能夠[將頁面和子頁面（頁面樹狀結構）還原為舊版](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)。

* [在[編輯器中建AEM立啟動SPA](/help/sites-cloud/authoring/launches/overview.md)。](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] Cloud Service  {#assets}

### [!DNL Assets] {#what-is-new-assets}的新增功能

* 資產微型服務現在支援視訊轉碼。 [!UICONTROL 處理描述檔]組態中的新區段可讓您設定視訊位元速率和尺寸。 輸出格式為MP4，採用H.264編碼器。 如需詳細資訊，請參閱[管理視訊資產](/help/assets/manage-video-assets.md#transcode-video)。 如需更多轉碼選項和視訊傳送，請使用[!DNL Dynamic Media]附加元件。

* 在新的[!DNL Experience Manager Assets]部署中，現在預設會設定智慧標籤功能。 不需要手動與[!DNL Adobe Developer Console]整合。 在現有部署中，管理員會像以前一樣設定智慧標籤整合。

* 新的[資產下載體驗](/help/assets/download-assets-from-aem.md)允許，

   * 非同步下載以進行大量下載，讓使用者不必等待。
   * 開發人員擴充性的全新模組化API。

* 資產微服務的中繼資料擷取已改善效能。 它可提高整體資產擷取吞吐量。

* 使用處理設定檔，使用「計算服務」產生自訂中繼資料。 請參閱「使用處理設定檔](/help/assets/manage-metadata.md#metadata-compute-service)自訂中繼資料」。[

* 為品牌入口網站使用者提供更簡單的下載體驗，管理員可加以設定。 請參閱[下載體驗概觀](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)。

* 品牌入口網站現在提供原生和高精確PDF檔案預覽。 請參閱[檔案檢視器概觀](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)。

* 您現在可以將CDN（內容傳送網路）快取直接從[!DNL Dynamic Media]作為Cloud Service（與使用[!DNL Dynamic Media Classic]不同）AEM失效。 它可確保在數分鐘內提供最新資產，而非數小時。 請參閱[透過Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)使CDN快取失效。

* 在[!DNL Assets]中，使用者介面控制項、導覽、瀏覽和搜尋體驗新增了增強的協助工具支援。

   * 如果在選擇[!UICONTROL Add Rendition]選項後按Escape鍵，焦點將返回工具欄。<!-- via CQ-4293594-->
   * 使用「電子郵件」組合方塊時，鍵盤焦點可正常運作。<!-- via CQ-4286215 -->
   * 搜索過濾器部分中的收合元素被解釋為標準可展開收合元。<!-- via CQ-4273103 -->
   * 將標籤套用至資產時，對話方塊會將標籤顯示為樹狀元素。 ARIA屬性會適當套用至樹狀元素，讓這些元素現在可存取。<!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版現已推出。它改善了與[!DNL Experience Manager] 6.5.5 Service Pack的相容性，並具有更新的客戶端作業系統相容性清單。 [!DNL Windows] 不支 [!DNL macOS] 援7和10.14之前的版本。

### [!DNL Assets] {#bugs-fixed}中修正的錯誤

* 首次點按時，「建立關聯」和「取消關聯」選項不會回應。 (CQ-4299022)
* 下載資產時，如果您選取透過電子郵件接收資產的選項，則不會傳送電子郵件。 (CQ-4299146)

## Adobe Experience Manager商務Cloud Service{#cloud-services-commerce}

### 新功能 {#what-is-new-commerce}

* 產品主控台功能現已推出。 這可讓行銷人員／作AEM者檢視並導覽儲存在商務後端的類別和產品。 另外也支援產品主控台中的類別和產品屬性。

* 產品和類別挑選器已改進，可讓行銷人員透過SKU選擇產品，或透過類別ID選擇類別。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

[!UICONTROL Cloud Manager]版本2020.8.0的發行日期為2020年8月06日。

### 新功能 {#what-is-new-cloud-manager}

* 「內容審核」是在Cloud Manager Sites生產管道上啟用的功能。 具有Sites的程式的Production Pipeline配置現在包含名為&#x200B;**Content Audit**&#x200B;的第三個頁籤。 每當生產管道執行時，在自訂功能測試後，管道中就會包含新的「內容稽核」步驟，以根據多項維度評估網站，包括效能、搜尋引擎最佳化(SEO)、協助功能、最佳實務和PWA（漸進式Web應用程式）。


   >[!NOTE]
   >「內容審核」已重新命名為「體驗審核」。

   如需詳細資訊，請參閱[體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md)。

* 「資產」程式中新建立的環境現在會自動設定Smart Content Services。

* 高眠環境可以從Cloud Manager的&#x200B;**概述**&#x200B;頁面中解除高眠。

* 能夠在Google Lighthouse支援的頁面上執行Experience Checks。 作為Cloud Manager管道的一部分，最多可以根據體驗KPI檢查和驗證25頁，並在Cloud Manager UI中顯示分數。

### 錯誤修正 {#bug-fixes-cm}

* 在程式碼品質掃描中，會執行一些不必要和不需要的SonarQube外掛程式。

* 在管線執行頁面上，分支名稱格式不正確。

* 在某些情況下，未完成的管線執行未成功記錄為已完成，從而防止了管線的新執行。

* 由於內部通訊問題，管道執行偶爾會出現&#x200B;*卡住*。

* 在布建新組織時，系統管理員以外的其他管理角色的部分使用者會錯誤地獲得Cloud Manager的存取權。

* 在特定條件下，更新索引作業並行啟動多次，導致部署失敗。

* 程式卡上的工具提示不一致正確。

* 在刪除環境中嘗試操作時，用戶介面錯誤地允許該操作。

* Cloud Manager的&#x200B;**概述**&#x200B;頁面上有顏色不符。

### 已知問題 {#known-issues-cm}

* 包含無效頁面，使「內容審核平均分數」低於應有的分數。

* 「內容稽核」標籤會使用作者網域而非發佈網域，錯誤地顯示基本URL。

* 若要啟動「內容稽核」步驟，使用者必須編輯管線，並可選擇新增頁面。 如果未新增任何頁面，則會檢查首頁。

## 內容轉移工具 {#content-transfer-tool}

請依照本節內容，瞭解內容傳輸工具版本v1.0.4的新增功能和更新。

### 新功能 {#what-is-new-ctt}

* 內容傳輸工具現在支援共用S3 DataStore。

### 錯誤修正 {#ctt-bug-fixes}

* 為工具完成動作增加其他逾時。

* 即使記錄顯示錯誤，舊版UI有時仍顯示成功擷取。

## 程式碼重構工具 {#code-refactoring-tools}

請依照本節內容，瞭解程式碼重構工具的新增功能和更新。

### 新功能 {#what-is-new-refactoring}

* AIO-CLI增效模組已推出，以統一程式碼重構工具，讓開發人員可從單一位置叫用並執行程式碼重構工具。 請參閱[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)以取得詳細資訊。

* Dispatcher AEM Converter已擴展，支援將內部部署和Adobe Managed Services Dispatcher配置轉換為與Cloud Service相容AEM的Dispatcher配置。 請參閱[Git資源：Dispatcher AEM Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)以瞭解詳細資訊。

* Dispatcher AEM Converter重新寫入` node.js `並與AIO-CLI插件整合。
