---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.8.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2020.8.0發行說明。」'
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

* 能夠 [將頁面和子頁（頁面樹）還原到早期版本](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)。

* 能夠 [建立啟動](/help/sites-cloud/authoring/launches/overview.md) AEM [編SPA輯器。](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

* 現在資產微服務支援視頻轉碼。 中的新節 [!UICONTROL 處理配置檔案] 配置允許您設定視頻比特率和尺寸。 輸出格式為MP4,H.264編解碼器。 有關詳細資訊，請參閱 [管理視頻資產](/help/assets/manage-video-assets.md#transcode-video)。 要獲得更多轉碼選項和視頻交付，請使用 [!DNL Dynamic Media] 附件。

* 新建 [!DNL Experience Manager Assets] 部署時，現在預設配置了智慧標籤功能。 無需手動整合 [!DNL Adobe Developer Console]。 在現有部署中，管理員會像以前一樣配置智慧標籤整合。

* 新 [資產下載體驗](/help/assets/download-assets-from-aem.md) 允許，

   * 非同步下載用於大型下載，因此用戶不必等待。
   * 一種新的模組化API，用於開發人員擴展性。

* 用於資產微服務的元資料提取具有改進的效能。 它提高了總的資產攝取吞吐量。

* 使用處理配置檔案使用計算服務生成自定義元資料。 請參閱 [使用處理配置檔案的自定義元資料](/help/assets/manage-metadata.md#metadata-compute-service)。

* 管理員可以配置的更簡單的Brand Portal用戶下載體驗。 請參閱 [下載體驗概述](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)。

* 本機和高保真PDF文檔預覽現已在Brand Portal提供。 請參閱 [文檔查看器概述](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)。

* 現在，您可以直接從中使CDN（內容分發網路）快取失效 [!DNL Dynamic Media] 在AEMas a Cloud Service [!DNL Dynamic Media Classic])。 它確保在幾分鐘內而不是幾小時內就能提供最新的資產。 請參閱 [通過Dynamic Media使CDN快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)。

* 增強的輔助功能支援將添加到中的用戶介面控制項、導航、瀏覽和搜索體驗 [!DNL Assets]。

   * 如果在選擇 [!UICONTROL 添加格式副本] 選項。 <!-- via CQ-4293594-->
   * 使用「電子郵件」組合框時，鍵盤焦點按預期工作。 <!-- via CQ-4286215 -->
   * 搜索濾波器部分中的accordions元素被解釋為標準可擴展的accordion。 <!-- via CQ-4273103 -->
   * 將標籤應用於資產時，對話框將標籤顯示為樹元素。 ARIA屬性適當應用於樹元素，以便現在可訪問這些元素。 <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版本現已提供。 它提高了與 [!DNL Experience Manager] 6.5.5 service pack ，並且具有更新的客戶端作業系統相容性清單。 [!DNL Windows] 7和 [!DNL macOS] 不支援10.14以前的版本。

### 修正在[!DNL Assets]中的錯誤 {#bugs-fixed}

* 首次按一下「相關」和「取消關聯」選項時，不會響應。 (CQ-4299022)
* 下載資產時，如果您選擇通過電子郵件接收該資產的選項，則不會發送電子郵件。 (CQ-4299146)

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 產品控制台功能現在可用。 這允許中的營銷商/作AEM者查看和導航儲存在商業後端中的類別和產品。 還提供了對產品控制台中類別和產品屬性的支援。

* 產品和類別選擇器經過改進，使營銷商能夠通過SKU選擇產品或通過類別ID選擇類別。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

發放日期 [!UICONTROL 雲管理器] 版本2020.8.0為2020年8月6日。

### 新增功能 {#what-is-new-cloud-manager}

* 內容審核是在Cloud Manager站點生產管道上啟用的功能。 現在，具有站點的程式的生產管道配置包含名為 **內容審核**。 每當生產管道運行時，在自定義功能測試後，管道中將包括新的內容審核步驟，該步驟將根據包括效能、 SEO（搜索引擎優化）、可訪問性、最佳實踐和PWA(Progressive Web App)在內的多個維度評估站點。


   >[!NOTE]
   >此後，「內容審核」已更名為「體驗審核」。

   請參閱 [體驗審計測試](/help/implementing/cloud-manager/experience-audit-testing.md) 的子菜單。

* Assets程式中新建立的環境現在將自動配置為Smart Content Services。

* 休眠的環境可以從雲管理器的 **概述** 的子菜單。

* 能夠在頁面上執行體驗檢查，由Google燈塔提供支援。 作為Cloud Manager管道的一部分，最多可以根據體驗KPI檢查和驗證25頁，並且分數顯示在Cloud Manager UI中。

### 錯誤修正 {#bug-fixes-cm}

* 正在執行一些不必要的和不需要的SonarQube插件，作為代碼質量掃描的一部分。

* 在管道執行頁上，分支名稱的格式不正確。

* 在某些情況下，未完成的管道執行未成功記錄為已完成，從而防止了管道的新執行。

* 管道執行偶爾會 *卡住* 內部通信問題。

* 在設定新組織時，系統管理員以外的一些具有管理角色的用戶被錯誤地授予了對Cloud Manager的訪問權限。

* 在某些情況下，更新索引作業被並行多次啟動，導致部署失敗。

* 程式卡上的工具提示不一致。

* 用戶介面錯誤地允許在刪除環境時嘗試操作。

* 雲管理器的 **概述** 的子菜單。

### 已知問題 {#known-issues-cm}

* 包含的無效頁面使內容審核平均分數低於應該的分數。

* 「內容審核」頁籤使用作者域而不是發佈域錯誤地顯示基本URL。

* 要激活「內容審核」步驟，用戶必須編輯管道，並（可選）添加頁面。 如果未添加任何頁面，將審核首頁。

## 內容轉移工具 {#content-transfer-tool}

請按照本部分瞭解內容傳輸工具1.0.4版的新增內容和更新。

### 新增功能 {#what-is-new-ctt}

* 內容傳輸工具現在支援共用S3資料儲存。

### 錯誤修正 {#ctt-bug-fixes}

* 為工具添加了完成操作的額外超時。

* 早期版本的UI有時顯示成功的提取，即使日誌顯示錯誤。

## 程式碼重構工具 {#code-refactoring-tools}

請按照本部分瞭解代碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI插件已發佈，用於統一代碼重構工具，使開發人員能夠從一個位置調用和執行代碼重構工具。 請參閱 [Git資源：aio-cli-plugin-aem — 雲服務 — 遷移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 的子菜單。

* AEM Dispatcher Converter擴展為支援將內部和Adobe Managed Services Dispatcher配置轉換為as a Cloud Service兼AEM容的Dispatcher配置。 請參閱 [Git資源：AEM Cloud Service調度器轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 的子菜單。

* 重新AEM寫入的Dispatcher Converter ` node.js ` 與AIO-CLI插件整合。
