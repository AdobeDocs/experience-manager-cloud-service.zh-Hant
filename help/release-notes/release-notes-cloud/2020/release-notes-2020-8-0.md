---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.8.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2020.8.0版發行說明。」'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 版發行說明  {#release-notes}

以下章節概述 Experience Manager as a Cloud Service 2020.8.0 版的一般發行說明。


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* 能 [將頁面和子頁面（頁面樹）還原為舊版](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* 能 [建立啟動](/help/sites-cloud/authoring/launches/overview.md) 在AEM中 [SPA編輯器。](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

* 現支援透過資產微服務將影片轉碼。 中的新區段 [!UICONTROL 處理設定檔] 設定可讓您設定視訊位元速率和維度。 輸出格式為MP4，採用H.264編解碼器。 如需詳細資訊，請參閱 [管理視訊資產](/help/assets/manage-video-assets.md#transcode-video). 如需更多轉碼選項和視訊傳送，請使用 [!DNL Dynamic Media] 附加元件。

* 新 [!DNL Experience Manager Assets] 部署時，現在預設會設定智慧標籤功能。 無需手動整合 [!DNL Adobe Developer Console]. 在現有部署上，管理員會像之前一樣設定智慧標籤整合。

* 新 [資產下載體驗](/help/assets/download-assets-from-aem.md) 允許，

   * 非同步下載大量內容，使用者不需等待。
   * 開發人員擴充性的全新模組化API。

* 資產微服務的中繼資料擷取效能有所改善。 這可提高整體資產擷取總處理能力。

* 使用處理設定檔，使用計算服務產生自訂中繼資料。 請參閱 [使用處理設定檔的自訂中繼資料](/help/assets/manage-metadata.md#metadata-compute-service).

* 更簡單的下載體驗，供Brand Portal使用者使用，供管理員進行設定。 請參閱 [下載體驗概觀](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Brand Portal現在提供原生和高保真PDF檔案預覽。 請參閱 [檔案檢視器概述](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* 您現在可以直接從 [!DNL Dynamic Media] 在AEMas a Cloud Service中(與使用 [!DNL Dynamic Media Classic])。 這可確保在數分鐘內提供最新資產，而非數小時。 請參閱 [透過Dynamic Media使CDN快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* 在中，使用者介面控制項、導覽、瀏覽和搜尋體驗都新增增強的協助工具支援 [!DNL Assets].

   * 如果您在選取 [!UICONTROL 新增轉譯] 選項，焦點將返回工具欄。 <!-- via CQ-4293594-->
   * 使用「電子郵件」組合框時，鍵盤焦點可正常工作。 <!-- via CQ-4286215 -->
   * 將搜索過濾器部分中的折疊線元素解釋為標準可展開折疊線。 <!-- via CQ-4273103 -->
   * 將標籤套用至資產時，對話方塊會將標籤顯示為樹狀元素。 ARIA屬性會適當套用至樹狀元素，以便現在存取。 <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版現已推出。 它提高了與 [!DNL Experience Manager] 6.5.5 service pack，且有更新的用戶端作業系統相容性清單。 [!DNL Windows] 7和 [!DNL macOS] 不支援10.14之前的版本。

### 修正在[!DNL Assets]中的錯誤 {#bugs-fixed}

* 首次按一下「關聯」和「不關聯」選項時沒有回應。 (CQ-4299022)
* 下載資產時，如果您選取透過電子郵件接收資產的選項，則不會傳送電子郵件。 (CQ-4299146)

## Adobe Experience Manager商務as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品主控台功能現已可用。 這可讓AEM中的行銷人員/作者檢視及導覽儲存於商務後端的類別和產品。 此外，產品主控台也支援類別和產品屬性。

* 產品和類別選擇器經過改良，可讓行銷人員透過SKU選取產品，或透過類別ID選取類別。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

的發行日期 [!UICONTROL Cloud Manager] 2020.8.0版是2020年8月6日。

### 新增功能 {#what-is-new-cloud-manager}

* 內容稽核是在Cloud Manager Sites生產管道中啟用的功能。 使用Sites的程式的生產管道設定現在包含第三個索引標籤，名為 **內容稽核**. 生產管道執行期間，只要自訂功能完成測試，管道中就會增加新的內容稽核步驟，以根據多項維度評估網站，包括效能、SEO（搜尋引擎最佳化）、協助工具、最佳作法和PWA（漸進式網頁應用程式）。


   >[!NOTE]
   >「內容稽核」後來已重新命名為「體驗稽核」。

   請參閱 [體驗稽核測試](/help/implementing/cloud-manager/experience-audit-testing.md) 以取得更多詳細資訊。

* Assets程式中新建立的環境現在會自動透過智慧內容服務進行設定。

* 您可以從Cloud Manager的 **概述** 頁面。

* 能在頁面上執行Experience Check(由Google Lighthouse提供技術支援)。 在Cloud Manager管道中，最多可根據體驗KPI檢查及驗證25個頁面，分數會顯示在Cloud Manager UI中。

### 錯誤修正 {#bug-fixes-cm}

* 在程式碼品質掃描中，會執行一些不必要的SonarQube外掛程式。

* 在管道執行頁面上，分支名稱的格式不正確。

* 在某些情況下，完成的管道執行未被成功記錄為已完成，從而防止了管道的新執行。

* 管道執行偶爾會 *卡住* 因內部通訊問題。

* 布建新組織時，系統管理員以外的其他管理角色的某些使用者會錯誤地獲得Cloud Manager的存取權。

* 在某些情況下，更新索引作業同時啟動多次，導致部署失敗。

* 程式卡上的工具提示不一致。

* 在刪除某個環境時，用戶介面錯誤地允許在該環境中嘗試操作。

* Cloud Manager的 **概述** 頁面。

### 已知問題 {#known-issues-cm}

* 包含的頁面無效，使得「內容稽核平均分數」低於應有的分數。

* 「內容稽核」索引標籤使用作者網域（而非發佈網域），錯誤地顯示基本URL。

* 若要啟用「內容稽核」步驟，使用者必須編輯管道，並選擇性地新增頁面。 如果未新增任何頁面，則會稽核首頁。

## 內容轉移工具 {#content-transfer-tool}

請詳閱本節，了解內容轉移工具1.0.4版的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 「內容轉移工具」現在支援共用S3 DataStore。

### 錯誤修正 {#ctt-bug-fixes}

* 工具完成動作時會新增其他逾時。

* 即使記錄顯示錯誤，舊版UI有時仍會顯示成功擷取。

## 程式碼重構工具 {#code-refactoring-tools}

請詳閱本節，了解程式碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* 推出AIO-CLI增效模組，整合程式碼重構工具，讓開發人員可從單一位置叫用及執行程式碼重構工具。 請參閱 [Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 以取得更多詳細資訊。

* AEM Dispatcher Converter擴充後，可支援將內部部署和Adobe Managed Services Dispatcher設定轉換為與AEMas a Cloud Service相容的Dispatcher設定。 請參閱 [Git資源：AEM Cloud Service Dispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 以取得更多詳細資訊。

* AEM Dispatcher轉換工具重新寫入 ` node.js ` 與AIO-CLI增效模組整合。
