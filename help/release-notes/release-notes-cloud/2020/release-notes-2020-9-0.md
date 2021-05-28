---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.9.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] as a 2020.9.0的Cloud Service發行說明。'
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 11%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager] as a 2020.9.0Cloud Service的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service2020.9.0的發行日期為2020年9月24日。

## [!DNL Adobe Experience Manager Sites] 作為Cloud Service {#sites}

### [!DNL Sites] {#what-is-new-sites}中的新增功能

* 單次頁面應用程式 (SPA) 編輯器 JavaScript SDK [現在是開放原始碼。](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] 作為Cloud Service {#assets}

### [!DNL Assets] {#what-is-new-assets}中的新增功能

* 透過資產微服務產生的轉譯支援浮水印影像檔案。 它可設定為「處理設定檔」，並使用PNG檔案作為浮水印。 請參閱[為您的資產加上浮水印](/help/assets/watermark-assets.md)。

* [!DNL Dynamic Media]中的增強功能

   * 選擇性發佈 — 現在，行銷團隊可以存取同步至[!DNL Dynamic Media]的智慧型裁切影像和動態轉譯，以便建立促銷文宣，而完全無須將這些資產發佈至[!DNL Dynamic Media]以進行全域傳送。 [!DNL Dynamic Media][!DNL Experience Manager] 和發 [!DNL Dynamic Media] 布是分離的，可個別執行以達成此目的。請參閱[選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)。
   * 管理員現在可以重設在布建時收到的[!DNL Dynamic Media]Cloud Service密碼。 重設可在[!DNL Experience Manager]使用者介面中完成，不需使用[!DNL Dynamic Media Classic]案頭應用程式。

* 若要了解下列增強功能，請參閱[Brand Portal中的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html)。

   * 整合Adobe Document Cloud檢視SDK，增強PDF預覽。
   * 按一下即可下載功能。
   * 下載體驗的新管理設定。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* CIF核心元件v1.3.0已發行。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) 。

* 現在提供產品和類別範本的產品/類別預覽功能。 這可讓AEM中的商務使用者/行銷人員檢視包含真實資料的產品/類別範本。

* 產品和類別新增了屬性頁面，可讓商務使用者檢視與產品SKU/類別ID相關聯的詳細資訊。

* 新增至產品控制台的排序功能，可依名稱或價格屬性排序產品/類別。

* 產品控制台新增了產品搜尋功能。

### 錯誤修正 {#bug-fixes-commerce}

* Commerce Cloud設定不遵守繼承。 此問題已修正，以確保設定會繼承值。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

[!UICONTROL Cloud Manager] 2020.9.0版的發行日期為2020年9月3日。

### 新功能 {#what-is-new-cloud-manager}

* 內容稽核已重新標示為體驗稽核。
* 建置程式已分為三個不同的Maven命令。
* 如果Git存放庫複製失敗，則最多會重新嘗試三次。

### 錯誤修正 {#bug-fixes-cm}

* 「內容稽核」索引標籤使用作者網域（而非發佈網域）錯誤顯示基本URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請參照本節，了解 Cloud Readiness Analyzer v1.1.0 版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* Cloud Readiness Analyzer(CRA)有一個啟動狀態控制台，顯示一個明確的&#x200B;**產生報表**&#x200B;按鈕，供使用者點選以執行CRA。

* CRA UI在執行時會顯示進度。 它會顯示正在分析的項目以及在執行期間發現的結果。

* CRA報表會以表格格式顯示結果的摘要和數目，並依結果類型和重要性層級組織。 按一下該結果的數目，會自動捲動至該結果在報表中的位置。

### 錯誤修正 {#cra-bug-fixes}

* 在某些情況下，強制重新整理後，CRA報表沒有更新。 此問題已在此版本中修正。

## 內容轉移工具 {#content-transfer-tool}

請詳閱本節，了解內容轉移工具1.1.10版的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 內容轉移工具(CTT)支援Azure Blob存放區資料存放區。

* CTT使用者介面具有自動重新載入功能，每30秒重新載入一次概觀頁面。

* CTT使用者介面新增了按鈕，可輕鬆擷取&#x200B;*存取Token*。

* 為&#x200B;*URL*&#x200B;和&#x200B;*移轉集名稱*&#x200B;新增描述性驗證訊息。

## 程式碼重構工具 {#code-refactoring}

請詳閱本節，了解程式碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI增效模組支援Repository Modernizer，並可讓使用者使用外掛程式執行工具。

   請參閱[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)以取得詳細資訊。

* Repository Modernizer公用程式可用來將現有的專案套件重新建構為與針對AEM定義為Cloud Service的專案結構相容的套件。

   請參閱[Git資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)以取得詳細資訊。
