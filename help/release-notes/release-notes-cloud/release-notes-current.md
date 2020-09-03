---
title: ' [!DNL Adobe Experience Manager]  雲端服務 2020.8.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 雲端服務 2020.8.0 版發行說明。'
translation-type: tm+mt
source-git-commit: 87d41dc311e96c41be230046f511d2c3301d48f1
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 6%

---


# [!DNL Adobe Experience Manager] 雲端服務 2020.8.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.8.0 版的一般發行說明。

## 發行日期 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.8.0 is August 27, 2020.

## [!DNL Adobe Experience Manager Sites] 雲端服務 {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* 能夠將頁 [面和子頁面（頁面樹狀結構）還原為舊版](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)。

* 可在AEM SPA Editor中建立啟動。

## [!DNL Adobe Experience Manager Assets] 雲端服務 {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* 資產微型服務現在支援視訊轉碼，「處理描述檔」畫面中有新的「視訊」區段支援視訊位元速率和尺寸設定（輸出格式為MP4，含H.264 codec）。  如需詳細資訊，請參 [閱「管理視訊資產](/help/assets/manage-video-assets.md#transcode-video)」。 若需更多轉碼選項， [!DNL Dynamic Media] 可使用視訊傳送附加元件。

* 在新部 [!DNL Experience Manager Assets] 署中，智慧型標籤功能現在預設已設定。 不需要手動與整合 [!DNL Adobe Developer Console]。 在現有部署中，管理員 [會像以前一樣設定智慧標籤](/help/assets/smart-tags-configuration.md#aio-integration) 整合。

* 全新的 [資產下載體驗](/help/assets/download-assets-from-aem.md) ,

   * 非同步下載以進行大量下載，讓使用者不必等待。

   * 開發人員擴充性的全新模組化API。

* [!DNL Experience Manager] 已改善資產微服務的中繼資料擷取效能。 它可提高整體資產擷取吞吐量。

* 使用處理設定檔，使用「計算服務」產生自訂中繼資料。 請參閱使 [用處理設定檔自訂中繼資料](/help/assets/manage-metadata.md#metadata-compute-service)

* 為品牌入口網站使用者提供更簡單的下載體驗，管理員可加以設定。 請參閱 [下載體驗概觀](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)。

* 品牌入口網站現在提供原生和高精確PDF檔案預覽。 請參閱 [檔案檢視器概觀](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)。

* 您現在可以直接在AEM中將CDN（內容傳送網路）快取作為雲端服務(而非使用 [!DNL Dynamic Media][!DNL Dynamic Media Classic])失效，以確保在數分鐘內就能提供最新的資產，而非數小時。 請參閱 [透過動態媒體使CDN快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)

* 在中的使用者介面控制項、導覽、瀏覽和搜尋體驗中新增了增強的協助工具支援 [!DNL Assets]。

   * 如果您在選取「新增轉譯」選項後按 [!UICONTROL Escape鍵] ，焦點會返回工具列。 <!-- via CQ-4293594-->
   * 使用「電子郵件」組合方塊時，鍵盤焦點可正常運作。 <!-- via CQ-4286215 -->
   * 搜索過濾器部分中的收合元素被解釋為標準可展開收合元。 <!-- via CQ-4273103 -->
   * 將標籤套用至資產時，對話方塊會將標籤顯示為樹狀元素。 ARIA屬性會適當套用至樹狀元素，讓這些元素現在可存取。 <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版現已推出，可改善與 [!DNL AEM] 6.5.5的相容性 [!DNL Service Pack] ，並更新用戶端作業系統相容性清單(移除 [!DNL Windows] 7和10.14 [!DNL MacOS] 之前的版本)。

### 修正於 [!DNL Assets] {#bugs-fixed}

* 首次點按時，「建立關聯」和「取消關聯」選項不會回應。 (CQ-4299022)
* 下載資產時，如果您選取透過電子郵件接收資產的選項，則不會傳送電子郵件。 (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新功能 {#what-is-new-commerce}

* 產品主控台功能現已推出。 這可讓AEM中的行銷人員／作者檢視並導覽儲存在商務後端的類別和產品。 另外也支援產品主控台中的類別和產品屬性。

* 產品和類別挑選器已改進，可讓行銷人員透過SKU選擇產品，或透過類別ID選擇類別。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### 新功能 {#what-is-new-cloud-manager}

* 「內容審核」是在Cloud Manager Sites生產管道上啟用的功能。 具有「網站」的程式的「生產管道」設定現在包含名為「內容審核」的第 **三個標籤**。 每當生產管道執行時，在自訂功能測試後，管道中就會包含新的「內容稽核」步驟，以根據多項維度評估網站，包括效能、搜尋引擎最佳化(SEO)、協助工具、最佳實務和PWA（漸進式網頁應用程式）。

   >[!NOTE]
   >「內容審核」現在已重新命名為「體驗審核」。

   如需詳細 [資訊，請參閱Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md) 。

* 「資產」程式中新建立的環境現在會自動設定Smart Content Services。

* 高眠環境可以從Cloud Manager的「概述」頁面中解除高 **眠** 。

* 能夠在Google Lighthouse支援的頁面上執行Experience Checks。 作為Cloud Manager管道的一部分，最多可以根據體驗KPI檢查和驗證25頁，並在Cloud Manager UI中顯示分數。

### 錯誤修正 {#bug-fixes-cm}

* 在程式碼品質掃描中，會執行一些不必要和不需要的SonarQube外掛程式。

* 在管線執行頁面上，分支名稱格式不正確。

* 在某些情況下，未完成的管線執行未成功記錄為已完成，從而防止了管線的新執行。

* 管道執行偶爾會因 *內部* 通訊問題而卡住。

* 在布建新組織時，系統管理員以外的其他管理角色的部分使用者會錯誤地獲得Cloud Manager的存取權。

* 在特定條件下，更新索引作業並行啟動多次，導致部署失敗。

* 程式卡上的工具提示不一致正確。

* 在刪除環境中嘗試操作時，用戶介面錯誤地允許該操作。

* Cloud Manager的「概述」頁面上有顏色不 **符** 。

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

* AIO-CLI增效模組已推出，以統一程式碼重構工具，讓開發人員可從單一位置叫用並執行程式碼重構工具。 請參閱 [Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) ，以取得詳細資訊。

* AEM Dispatcher Converter已擴充，可支援將內部部署和Adobe Managed Services Dispatcher組態轉換為AEM，做為Cloud Service相容的Dispatcher組態。 請參閱 [Git資源：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) ，以取得詳細資訊。

* AEM Dispatcher Converter已重新寫入AIO-CLI ` node.js ` 增效模組並與之整合。
