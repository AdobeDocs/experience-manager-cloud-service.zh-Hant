---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] as a 2020.10.0的Cloud Service發行說明。'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: af5eb5aeb34e2f0ead98e0a0acb412b19bcfe517
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 19%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 版發行說明  {#release-notes}

以下章節概述[!DNL Experience Manager]作為Cloud Service2020.10.0的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2020.10.0的發行日期為2020年10月28日。
下列版本(2020.11.0)將於2020年12月1日發行。

## [!DNL Adobe Experience Manager Sites] 作為Cloud Service {#sites}

### [!DNL Sites]中的新增功能 {#what-is-new-sites}

* **[核心元件2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)**:Adobe Experience Manager作為Cloud Service可享受核心元件最新版本自動更新的優勢。2.12.0版包含社群提供的最新改善。 改良功能包括[新的POST表單處理常式；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data)透過內容感知組態包含自訂CSS、JavaScript和中繼資料[標籤的功能；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)和[`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components)公用程式，以簡化自訂元件中的Adobe資料層整合。 請參閱2.12.0中的[變更清單](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)。

* **[專案原型24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**:建議的啟動新Experience Manager專案的基礎更完善。現在包含新的[Adobe用戶端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)、[在AMP中傳送網站的選項、](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html)以及新的[擴充點，以新增專案CSS/JS。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub資料夾](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**:能夠建立受眾資料夾，以輕鬆組織、尋找和選取要用於ContextHub選件鎖定目標功能的對象區段。

## [!DNL Adobe Experience Manager Assets] 作為Cloud Service {#assets}

* **[!DNL Adobe Sensei]支援的視訊智慧標籤**:借由套用AI模型來分析物件和動作專用標籤的視訊內容，DAM使用者可以利用公開的豐富資訊，減少新增標籤的時間，並有更多時間使用。而您又可以向客戶提供合適的體驗。 請參閱[智慧標籤視訊資產](/help/assets/smart-tags-video-assets.md)。

* **Brand Portal增強功能**:提供下列新功能及更多 [!DNL Brand Portal]項。如需詳細資訊，請參閱[[!DNL Brand Portal] 發行說明](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)。

   * [增強的下載](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) 體驗，提供簡化且快速的下載。管理員可設定額外的下載組態，以提供符合使用者和企業需求的體驗。
   * 現在可以從任何頁面按一下即可導覽至檔案、[集合](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)和共用連結。
   * 使用者現在可以[選取並下載特定轉譯](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page)。 可透過「資產」詳細內容頁面的「轉譯」面板新的轉譯下載選項。
   * 來賓使用者工作階段逾時15分鐘，可確保所有同時使用者獲得更佳體驗。

* **[!DNL Adobe Asset Link]版本2.1**:適用於、和 [的Adobe](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) 資產 [!DNL Adobe Photoshop]連結擴 [!DNL Adobe Illustrator]充功能 [!DNL Adobe InDesign] 的新版本已推出。它新增了與2020年10月發行的2021版最新[!DNL Adobe Creative Cloud]應用程式的相容性。

* **[!DNL Assets]WebP檔案支援**: [!DNL Assets] 作為Cloud Service，現在支援WebP影像格式。WebP是Google建立的新興影像格式。 WebP檔案格式的影像在視覺上與JPG或PNG檔案沒有差別，而且檔案要小得多。 降低資產的檔案大小可縮短頁面載入時間，並協助內容建立者提供更快速的網路體驗。 請參閱如何在[建立處理設定檔](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)中使用WebP 。

## Adobe Experience Manager Commerce as aCloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* CIF Venia Reference Site - 2020.10.2版已發行，其中包含最新CIF核心元件1.4.0版。如需詳細資訊，請參閱[CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2)。

* CIF核心元件v1.4.0已發行。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) 。

### 錯誤修正 {#bug-fixes-commerce}

* 產品主控台和選擇器中的GraphQL請求是透過HTTPPOST完成。 此問題已修正，以確保Apollo GraphQL用戶端遵循GraphQL用戶端OSGi設定中的設定，以支援GET請求（若已設定）。

* CIF雲端設定UI針對/lib和/apps/中的設定顯示「儲存並關閉」按鈕。 但這些介面是唯讀的，因此UI已修正為只顯示「關閉」按鈕。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Cloud Manager在Experience Manageras aCloud Service中的發行日期2020.10.0為2020年10月2日。

### [!DNL Cloud Manager]中的新增功能 {#what-is-new-cm}

* 環境頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* Cloud Manager的「建置容器」現在支援使用Java™ 8或Java™ 11來編譯專案。 Maven工具鏈系統支援Java™ 11。

* 每個環境的環境變數數量提高至 200 個。

* 「概述」頁面上的「環境」卡片現在最多會列出三個環境。 用戶可以選擇&#x200B;**全部顯示**按鈕以導航到「環境」摘要頁以查看包含完整環境清單的表。
如需詳細資訊，請參閱[檢視環境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 環境完全建立前，從 Cloud Manager 到開發人員控制台的連結未正確啟用。

* 直接從 Cloud Manager 連結至開發人員控制台時，系統未顯示將沙箱方案的環境解除休眠/休眠的選項。

* 非生產管道編輯頁面上的取消和儲存按鈕不一定會顯示。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立方案時，建議的名稱有時會傳回現有方案名稱的重複項目。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 環境頁面有時會在未顯示任何內容時顯示發佈和Dispatcher區段。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 新增了根據「工作流程標題」、「工作流模型」、「狀態」、「發起人」、「裝載路徑」和「開始日期」搜尋工作流程例項的支援。 請參閱[搜尋工作流程例項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

## 內容轉移工具 {#content-transfer-tool}

進一步了解[內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 記錄檔的使用者體驗已改善。 提取和擷取記錄檔新增時間戳記。 已新增訊息，指出記錄是否空白。

### 錯誤修正 {#ctt-bug-fixes}

* 如果移轉集包含的路徑與檔案名稱部分類似，則「內容轉移工具」會略過內容檔案。
