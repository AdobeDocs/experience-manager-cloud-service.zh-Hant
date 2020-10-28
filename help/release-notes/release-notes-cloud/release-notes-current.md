---
title: ' [!DNL Adobe Experience Manager]  雲端服務 2020.10.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 作為2020.10.0的雲端服務發行說明。'
translation-type: tm+mt
source-git-commit: 12883e87d4aee796b23c366e77651134dafb8f4c
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 22%

---


# [!DNL Adobe Experience Manager] 雲端服務 2020.10.0 版發行說明 {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## 發行日期 {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 is October 28, 2020.
下列版本(2020.11.0)將於11月26日發行。

## [!DNL Adobe Experience Manager Sites] 雲端服務 {#sitess}

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

* **[!DNL Assets]WebP檔案支援**: [!DNL Assets] 雲端服務現在支援WebP影像格式。 WebP是Google建立的新興影像格式。 WebP檔案格式的影像在視覺上與JPG或PNG檔案沒有區隔，而且檔案要小得多。 降低資產的檔案大小可縮短頁面載入時間，並協助內容建立者提供更快速的網頁體驗。

<!--
### Bugs Fixed {#bugs-fixed-assets}

Content to come
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發佈CIF Venia參考網站- 2020.10.2，其中包含最新的CIF核心元件1.4.0版。如需詳細 [資訊，請參閱CIF韋尼亞參考網站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) 。

* 已發佈CIF核心元件v1.4.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) ，以取得詳細資訊。

### 錯誤修正 {#bug-fixes-commerce}

* 產品主控台和挑選器中的GraphQL請求是透過HTTP POST完成。 此問題已修正，以確保Apollo GraphQL客戶端遵守GraphQL客戶端OSGi配置中的設定，以支援GET請求（如果已配置）。

* CIF雲端設定UI針對/lib和/apps/中的設定顯示「儲存並關閉」按鈕。 但這些是唯讀的，因此UI已修正為只顯示「關閉」按鈕。

## Cloud Manager {#cloud-manager}

* 「環境」頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* Cloud Manager 建置容器現可支援 Java 8 和 Java 11。

* 每個環境的環境變數數量提高至 200 個。

* 「概述」頁面上的「環境」卡現在最多可列出三個環境。 用戶可以選擇「顯 **示全部** 」按鈕，以導航至「環境」摘要頁，以查看包含完整環境清單的表。
有關詳細 [資訊，請參閱](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 「查看環境」。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 環境完全建立前，從 Cloud Manager 到開發人員控制台的連結未正確啟用。

* 直接從 Cloud Manager 連結至開發人員控制台時，系統未顯示將沙箱方案的環境解除休眠/休眠的選項。

* 「非生產管線編輯」(Non-Production Pipeline Edit)頁面上的「取消」(Cancel)和「保存」(Save)按鈕不一律可見。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立新方案時，建議的名稱有時會傳回重複的現有方案名稱。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容的情況下，顯示發佈和發送器區段。


## Adobe Experience Manager 雲端服務基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 新增支援根據「工作流程標題」、「工作流程模型」、「狀態」、「啟動器」、「裝載路徑」和「開始日期」來搜尋工作流程例項。

## 內容轉移工具 {#content-transfer-tool}

Follow this section to learn about what is new and the updates for [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### 新增功能 {#what-is-new-ctt}

* 改善記錄檔的使用者體驗。 已新增時間戳記至擷取和擷取記錄檔。 新增訊息，指出記錄檔是否空白。

### 錯誤修正 {#ctt-bug-fixes}

* 如果遷移集包含具有部分相似檔案名的路徑，則內容傳輸工具正在跳過內容檔案。 這個問題已經修正。
