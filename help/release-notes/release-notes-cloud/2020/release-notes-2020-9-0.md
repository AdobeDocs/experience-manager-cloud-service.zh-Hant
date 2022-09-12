---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.9.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2020.9.0版發行說明。」'
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 12%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版發行說明  {#release-notes}

以下章節概述的一般發行說明 [!DNL Experience Manager] as a Cloud Service2020.9.0。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a Cloud Service的2020.9.0是2020年9月24日。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* 單次頁面應用程式 (SPA) 編輯器 JavaScript SDK [現在是開放原始碼。](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

* 透過資產微服務產生的轉譯支援浮水印影像檔案。 它可設定為「處理設定檔」，並使用PNG檔案作為浮水印。 請參閱 [為您的資產加上浮水印](/help/assets/watermark-assets.md).

* 中的增強功能 [!DNL Dynamic Media]

   * 選擇性發佈 — 行銷團隊現在可以存取 [!DNL Dynamic Media] 同步至的智慧型裁切影像和動態轉譯 [!DNL Dynamic Media] 這樣他們就能製作宣傳材料，而完全不需要將這些資產發佈到 [!DNL Dynamic Media] 全域傳送。 [!DNL Experience Manager] 和 [!DNL Dynamic Media] 發佈是分離的，可個別執行以達成此目的。 請參閱 [選擇性發佈](/help/assets/dynamic-media/selective-publishing.md).
   * 管理員現在可重設 [!DNL Dynamic Media] Cloud Service設定時收到的密碼。 重設可在 [!DNL Experience Manager] 使用者介面，不需使用 [!DNL Dynamic Media Classic] 案頭應用程式。

* 若要了解下列增強功能，請參閱 [Brand Portal的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

   * 整合Adobe Document Cloud檢視SDK，增強PDF預覽。
   * 按一下即可下載功能。
   * 下載體驗的新管理設定。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager商務as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* CIF核心元件1.3.0版已發行。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) 以取得更多詳細資訊。

* 現在提供產品和類別範本的產品/類別預覽功能。 這可讓AEM中的商務使用者/行銷人員檢視包含真實資料的產品/類別範本。

* 產品和類別新增了屬性頁面，可讓商務使用者檢視與產品SKU/類別ID相關聯的詳細資訊。

* 新增至產品控制台的排序功能，可依名稱或價格屬性排序產品/類別。

* 產品控制台新增了產品搜尋功能。

### 錯誤修正 {#bug-fixes-commerce}

* Commerce Cloud設定不遵守繼承。 此問題已修正，以確保設定會繼承值。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

的發行日期 [!UICONTROL Cloud Manager] 2020.9.0版是2020年9月3日。

### 新增功能 {#what-is-new-cloud-manager}

* 內容稽核已重新標示為體驗稽核。
* 建置程式已分為三個不同的Maven命令。
* 如果Git存放庫複製失敗，則最多會重新嘗試三次。

### 錯誤修正 {#bug-fixes-cm}

* 「內容稽核」索引標籤使用作者網域（而非發佈網域）錯誤顯示基本URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請參照本節，了解 Cloud Readiness Analyzer v1.1.0 版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* Cloud Readiness Analyzer(CRA)有一個啟動狀態控制台，顯示一個明確的 **產生報表** 按鈕，讓使用者按一下以執行CRA。

* CRA UI執行時會顯示進度。 它會顯示正在分析的項目以及在執行期間發現的結果。

* CRA報表會以表格格式顯示結果的摘要和數目，並依結果類型和重要性層級組織。 按一下該結果的數目，會自動捲動至該結果在報表中的位置。

### 錯誤修正 {#cra-bug-fixes}

* 在某些情況下，強制重新整理後，CRA報表沒有更新。 此問題已在此版本中修正。

## 內容轉移工具 {#content-transfer-tool}

請詳閱本節，了解內容轉移工具1.1.10版的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 內容轉移工具(CTT)支援Azure Blob存放區資料存放區。

* CTT使用者介面具有自動重新載入功能，每30秒重新載入一次概觀頁面。

* CTT使用者介面中新增的按鈕以擷取 *存取權杖* 容易。

* 為新增描述性驗證訊息 *URL* 和 *移轉集名稱*.

## 程式碼重構工具 {#code-refactoring}

請詳閱本節，了解程式碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI增效模組支援Repository Modernizer，並可讓使用者使用外掛程式執行工具。

   請參閱 [Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 以取得更多詳細資訊。

* Repository Modernizer公用程式可用來將現有的專案套件重新建構為與針對AEM as a Cloud Service定義的專案結構相容的套件。

   請參閱 [Git資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 以取得更多詳細資訊。
