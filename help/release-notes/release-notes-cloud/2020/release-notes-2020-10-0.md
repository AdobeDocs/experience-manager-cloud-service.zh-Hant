---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2020.10.0發行說明。」'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 19%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 版發行說明  {#release-notes}

以下部分概述了有關 [!DNL Experience Manager] as a Cloud Service2020.10.0。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.10.0是2020年10月28日。
以下版本(2020.11.0)將於2020年12月1日發佈。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* **[核心元件2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**:Adobe Experience Manager as a Cloud Service受益於對最新版核心元件的自動更新。 2.12.0版包括社區提供的最新改進。 改進包括 [新的POST表格處理程式；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) 能夠包括自定義CSS、JavaScript和元資料 [標籤通過上下文感知配置；](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) 和 [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) 用於簡化自定義元件中的Adobe資料層整合。 查看 [更改清單](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) 的子2.12.0。

* **[原型24工程](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**:建議的啟動新Experience Manager項目的基礎更好。 現在包括了 [Adobe客戶端資料層](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)，選擇 [在AMP中傳送站點，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) 新建 [添加項目CSS/JS的擴展點。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub資料夾](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**:能夠建立受眾資料夾以便於組織、查找和選擇受眾段，以用於ContextHub提供目標功能。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]帶電視頻智慧標籤**:通過應用AI模型來分析對象和動作特定標籤的視頻內容，DAM用戶可以花費更少的時間添加標籤，而更多的時間使用暴露的豐富資訊。 反過來，您又可以為客戶提供正確的體驗。 請參閱 [智慧標籤視頻資產](/help/assets/smart-tags-video-assets.md)。

* **Brand Portal增強**:以下新功能及更多功能可在 [!DNL Brand Portal]。 有關詳細資訊，請參閱 [[!DNL Brand Portal] 發行說明](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)。

   * [增強的下載體驗](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) 用於簡化、快速下載。 管理員可設定額外的下載組態，以提供符合使用者和企業需求的體驗。
   * 按一下導航至「檔案」， [集合](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)，並且現在可以從任何頁面訪問共用連結。
   * 用戶可以 [選擇並下載特定格式副本](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) 現在。 可透過「資產」詳細內容頁面的「轉譯」面板新的轉譯下載選項。
   * 來賓用戶會話超時15分鐘可確保所有併發用戶獲得更好的體驗。

* **[!DNL Adobe Asset Link]版本2.1**:新版本 [Adobe資產連結](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 擴展 [!DNL Adobe Photoshop]。 [!DNL Adobe Illustrator], [!DNL Adobe InDesign] 的子菜單。 它增加了與最新 [!DNL Adobe Creative Cloud] 2021版的應用程式，於2020年10月發佈。

* **[!DNL Assets]WebP檔案支援**: [!DNL Assets] as a Cloud Service現在支援WebP影像格式。 WebP是Google建立的一種新興的影像格式。 WebP檔案格式的影像在視覺上與JPG或PNG檔案無法區分，而且檔案要小得多。 降低資產的檔案大小可縮短頁面載入時間，並幫助內容建立者提供更快的Web體驗。 請參閱中如何使用WebP [建立處理配置檔案](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)。

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### [!DNL Forms]的新增功能 {#what-is-new-forms-oct-2021}

* **自適應Forms分析**:現在，您可以通過Adobe Analytics為Adaptive Forms捕獲和跟蹤已登錄和未登錄（匿名）的行為，以收集最終用戶的見解。 它幫助企業用戶根據收集到的見解，就自適應表單內容、佈局和樣式做出明智的決策。

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms-oct-2021}

* **將工作AEM流資料外部化以進行安全處理**:您可以將包含敏感個AEM人資料(SPD)元素的在製品工作流變數資料儲存在客戶管理的儲存庫中，以便進行安全處理。 處理工作流時，儲存在工作流變數中的資料不會保留在儲存AEM庫中。 根據需要從客戶管理的儲存庫中取出。

### [!DNL Forms]的 Beta 版功能 {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 幫助您將模板和XML資料組合起來，以生成各種格式的文檔。 該服務允許您以同步和批處理模式生成文檔。

您可以寫信寄到 [!DNL formscsbeta@adobe.com] 來註冊 beta 版計劃。

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發佈CIF Venia參考站點 — 2020.10.2，包括最新的CIF核心元件版本v1.4.0。請參閱 [CIF Venia參考站點](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) 的子菜單。

* 已發佈CIF核心元件v1.4.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) 的子菜單。

### 錯誤修正 {#bug-fixes-commerce}

* GraphQL請求在產品控制台和選擇器中通過HTTPPOST完成。 此問題已修復，以確保Apollo GraphQL客戶端尊重GraphQL客戶端OSGi配置中的設定，以支援已配置的GET請求。

* CIF雲配置UI顯示/lib和/apps/中配置的「保存和關閉」按鈕。 但這些介面是只讀的，因此UI固定為僅顯示「關閉」按鈕。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

Experience Manageras a Cloud Service中的Cloud Manager的發佈日期為2020.10.0 2020年10月2日。

### [!DNL Cloud Manager]的新增功能 {#what-is-new-cm}

* 「環境」頁面已重新設計。

* 休眠環境現在會在 Cloud Manager 休眠時顯示分離狀態。

* Cloud Manager「build container」現在支援使用Java™ 8或Java™ 11編譯項目。 Maven工具鏈系統提供對Java™ 11的支援。

* 每個環境的環境變數數量提高至 200 個。

* 「概述」(Overview)頁面上的「環境」(Environment)卡現在最多列出三個環境。 用戶可以選擇 **全部顯示** 按鈕，來查看包含完整環境清單的表。
請參閱 [查看環境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 的子菜單。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 環境完全建立前，從 Cloud Manager 到開發人員控制台的連結未正確啟用。

* 直接從 Cloud Manager 連結至開發人員控制台時，系統未顯示將沙箱方案的環境解除休眠/休眠的選項。

* 「非生產管道編輯」(Non-Production Pipeline Edit)頁面上的「取消」(Cancel)和「保存」(Save)按鈕並不總是可見。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 建立程式時，建議的名稱有時會返回現有程式名稱的副本。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

* 環境名稱驗證發生差一錯誤。

* 「環境」頁有時會顯示未出現的發佈段和Dispatcher段。

## Adobe Experience Manager as a Cloud Service 基礎 {#cloud-service-foundation}

### 工作流程 {#workflows}

* 已添加支援，用於根據工作流標題、工作流模型、狀態、啟動器、負載路徑和開始日期搜索工作流實例。 請參閱 [搜索工作流實例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

## 內容轉移工具 {#content-transfer-tool}

瞭解有關新增內容和更新的詳細資訊 [內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) 版本1.1.12。

### 新增功能 {#what-is-new-ctt}

* 改進了日誌的用戶體驗。 已添加到提取和接收日誌的時間戳。 添加的消息指示日誌是否為空。

### 錯誤修正 {#ctt-bug-fixes}

* 如果遷移集包含的路徑部分具有相似的檔案名，則內容傳輸工具正在跳過內容檔案。
