---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.9.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 2020.9.0版雲端服務發行說明。'
translation-type: tm+mt
source-git-commit: 701d9ff3c9553c28bce0ef417487facedb22373f
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 9%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]作為雲端服務2020.9.0的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]作為Cloud Service 2020.9.0的發行日期為2020年9月24日。

## [!DNL Adobe Experience Manager Sites] 雲端服務  {#sites}

### [!DNL Sites] {#what-is-new-sites}的新增功能

* 單頁應用程式(SPA)編輯器JavaScript SDK [現在是開放原始碼。](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] 雲端服務  {#assets}

### [!DNL Assets] {#what-is-new-assets}的新增功能

* 使用資產microservices產生的轉譯支援浮水印影像檔案。 它可以設定為「處理設定檔」，並使用PNG檔案做為浮水印。 請參閱[浮水印您的資產](/help/assets/watermark-assets.md)。

* [!DNL Dynamic Media]中的增強功能

   * 選擇性發佈——行銷團隊現在可以存取與[!DNL Dynamic Media]同步的[!DNL Dynamic Media]智慧型裁切影像和動態轉譯，讓他們建立促銷文宣，完全不需要將這些資產發佈至[!DNL Dynamic Media]以進行全域傳送。 [!DNL Experience Manager] 而發 [!DNL Dynamic Media] 布則可獨立進行，以達成此目的。請參閱[選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)。
   * 管理員現在可以重設布建時收到的[!DNL Dynamic Media]雲端服務密碼。 重設可在[!DNL Experience Manager]使用者介面中完成，而不需使用[!DNL Dynamic Media Classic]案頭應用程式。

* 若要瞭解下列增強功能，請參閱[品牌入口網站的新增功能](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html)。

   * 使用Adobe Document Cloud檢視SDK整合增強PDF預覽。
   * 按一下即可下載功能。
   * 下載體驗的新管理設定。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發佈CIF核心元件v1.3.0。有關詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0)。

* 現在提供產品／類別範本的預覽功能。 這可讓AEM中的商業使用者／行銷人員檢視具有真實資料的產品／類別範本。

* 屬性頁面已新增至產品和類別，可讓商業使用者檢視與產品SKU/類別ID相關的詳細資訊。

* 新增至「產品主控台」的排序功能，允許依名稱或價格屬性來排序產品／類別。

* 產品搜尋功能已新增至產品主控台。

### 錯誤修正 {#bug-fixes-commerce}

* Commerce Cloud設定不尊重繼承。 此問題已修正，以確保配置繼承值。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

[!UICONTROL Cloud Manager]版本2020.9.0的發行日期為2020年9月03日。

### 新功能 {#what-is-new-cloud-manager}

* 內容審核已重新標示為「體驗審核」。
* 建立程式已分為三個不同的Maven命令。
* 如果Git Repository無法克隆，則最多將重新嘗試三次。

### 錯誤修正 {#bug-fixes-cm}

* 「內容審核」標籤使用作者網域而非發佈網域錯誤顯示基本URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請參照本節，了解 Cloud Readiness Analyzer v1.1.0 版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* Cloud Readiness Analyzer(CRA)有一個啟動狀態控制台，它顯示一個明確的&#x200B;**生成報告**&#x200B;按鈕，供用戶按一下以執行CRA。

* CRA UI會在執行中顯示進度。 它顯示正在分析的項目和在執行過程中發現的查找結果。

* CRA報告以按查找類型和重要性級別組織的表格形式顯示了調查結果的摘要和數目。 按一下該尋找的數目會自動捲動至該尋找在報表中的位置。

### 錯誤修正 {#cra-bug-fixes}

* 在某些情況下，CRA報告在強制更新後無法更新。 此版本已修正此問題。

## 內容轉移工具 {#content-transfer-tool}

請依照本節內容，瞭解內容傳輸工具版本1.1.10的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 內容傳輸工具(CTT)支援Azure Blob儲存資料儲存。

* CTT使用者介面具有自動重新載入功能，每30秒重新載入一次概述頁面。

* 新增至CTT使用者介面的按鈕，以輕鬆擷取&#x200B;*存取Token*。

* 為&#x200B;*URL*&#x200B;和&#x200B;*遷移集名稱*&#x200B;添加了描述性驗證消息。

## 程式碼重構工具 {#code-refactoring}

請依照本節內容，瞭解程式碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI插件支援Repository Modernizer，並允許用戶使用插件執行工具。

   請參閱[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)以取得詳細資訊。

* Repository Modernizer公用程式可用來將現有的專案套件重新架構為與為AEM定義為雲端服務的專案結構相容的套件。

   請參閱[Git資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)，以瞭解詳細資訊。

