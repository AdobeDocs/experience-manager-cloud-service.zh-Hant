---
title: Current Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service.
description: Current Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service.
translation-type: tm+mt
source-git-commit: 05184bbf507fe84ffb69da90502190b1a2793ee3
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版發行說明 {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service.

## 發行日期 {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 is October 28, 2020.
下列版本(2020.11.0)將於2020年12月1日發行。

## [!DNL Adobe Experience Manager Sites] 雲端服務 {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

<!-- add when release done: * **Core Components 2.12.0**: With Core Components being on auto-update, benefit from the latest improvements contributed by the community. See list of changes since 2.11.1: Release Notes -->

* **原型24**:開始新AEM專案的建議基礎已變得更好，現在包括新的Adobe用戶端資料層、以AMP傳送網站的選項，以及新的擴充點，以新增專案CSS/JS。

* **ContextHub資料夾**:能夠建立觀眾資料夾，以輕鬆組織、尋找和選擇觀眾區隔，以用於ContextHub選件定位功能。

## [!DNL Adobe Experience Manager Assets] 雲端服務 {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* **[!DNL Adobe Sensei]提供動態視訊智慧標籤**:借由運用AI模型來分析物件和特定動作標籤的視訊內容，DAM使用者可以減少新增標籤的時間，而有更多時間運用暴露的豐富資訊，為客戶提供正確的體驗。 請參閱 [智慧型標籤視訊資產](/help/assets/smart-tags-video-assets.md)。

* **品牌入口網站增強功能**:下列新功能和更多功能皆可在中取得 [!DNL Brand Portal]。 如需詳細資訊，請參 [[!DNL Brand Portal] 閱發行說明](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)。

   * [增強下載體驗](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) ，以簡化、快速下載。 管理員可設定其他下載組態，以提供符合使用者和企業需求的體驗。
   * 現在，您只需按一下滑鼠，即可從任 [何頁面導覽至「檔案](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)」、「系列」和「共用連結」。
   * 使用者現 [在可以選取並下載特定轉譯](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) 。 新的轉譯下載選項可在「資產詳細資訊」頁面的「轉譯」面板中使用。
   * 來賓用戶會話超時15分鐘，可確保為所有併發用戶提供更好的體驗。

* **[!DNL Adobe Asset Link]2.1版**:目前提供適 [用於、和的Adobe Asset](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) Link [!DNL Adobe Photoshop]擴充功 [!DNL Adobe Illustrator]能新 [!DNL Adobe InDesign] 版本。 它新增了與2020年10月發行 [!DNL Adobe Creative Cloud] 的2021版最新應用程式的相容性。

* **[!DNL Assets]WebP檔案支援**: [!DNL Assets] 雲端服務現在支援建立WebP影像格式的轉譯。 WebP是Google建立的新興影像格式。 WebP檔案格式的影像在視覺上與JPG或PNG檔案沒有區隔，而且檔案要小得多。 降低資產的檔案大小可縮短頁面載入時間，並協助內容建立者提供更快速的網頁體驗。 請參 [閱建立標準處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發佈CIF Venia參考網站- 2020.10.2，其中包含最新的CIF核心元件1.4.0版。如需詳細 [資訊，請參閱CIF韋尼亞參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) 。

* 已發佈CIF核心元件v1.4.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) ，以取得詳細資訊。

### 錯誤修正 {#bug-fixes-commerce}

* 產品主控台和挑選器中的GraphQL請求是透過HTTP POST完成。 此問題已修正，以確保Apollo GraphQL客戶端遵守GraphQL客戶端OSGi配置中的設定，以支援GET請求（如果已配置）。

* CIF雲端設定UI針對/lib和/apps/中的設定顯示「儲存並關閉」按鈕。 但這些是唯讀的，因此UI已修正為只顯示「關閉」按鈕。


## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

AEM中Cloud Manager作為雲端服務2020.11.0的發行日期為2020年11月12日。

### What is new in [!DNL Cloud Manager] {#what-is-new-cm}

* 現在，「環境」 **卡和「環境** 」摘要頁上的「環境」菜單選項中，用戶可以使用新的「本地登錄 ******** 」菜單選項。
如需詳細 [資訊，請參閱](/help/implementing/cloud-manager/manage-environments.md##login-locally) 「管理環境」。

* Cloud Manager中 **的** 「學習」索引標籤已在UI中以新影像重新整理。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在建立執行前載入的相依性需要下載Maven外掛程式。
* 從Cloud Manager頁尾選取語言的連結現在會導覽至正確的位置。
* 有時在程式碼掃描期間，SonarQube程式不會啟動。 現在會自動偵測到此問題，並嘗試重新啟動。
* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 已新增支援根據「工作流程標題」、「工作流程模型」、「狀態」、「啟動器」、「裝載路徑」和「開始日期」來搜尋工作流程例項。 請參閱 [搜尋工作流程例項](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

## 內容轉移工具 {#content-transfer-tool}

Follow this section to learn about what is new and the updates for [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### 新增功能 {#what-is-new-ctt}

* 改善記錄檔的使用者體驗。 已新增時間戳記至擷取和擷取記錄檔。 新增訊息，指出記錄檔是否空白。

### 錯誤修正 {#ctt-bug-fixes}

* 如果遷移集包含具有部分相似檔案名的路徑，則內容傳輸工具正在跳過內容檔案。 這個問題已經修正。

## 最佳實務分析器 {#best-practices-analyzer}

### 發行日期 {#release-date-bpa}

最佳做法分析器的發行日期是2020年11月13日。

### What is new in [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* Cloud Readiness Analyzer現在是最佳做法分析器(BPA)。 BPA提供您目前AEM實作的最佳實務評估，並協助評估從現有AEM例項移至AEM（雲端服務）的準備程度。

* 新增偵測器以偵測使用情 `java.io.InputStream`況，若在AEM中當做雲端服務使用，可能會造成問題。

### 錯誤修正 {#bpa-bug-fixes}

* 修正導致與textfield foundation元件相 *關的正面* (bug)錯誤。
