---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.9.0 版發行說明。'
description: "[!DNL Adobe Experience Manager]個2020.9.0as a Cloud Service發行說明。"
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager]as a Cloud Service2020.9.0版發行說明 {#release-notes}

以下章節概述[!DNL Experience Manager]as a Cloud Service2020.9.0版的一般發行說明。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2020.9.0版的發行日期為2020年9月24日。

## [!DNL Adobe Experience Manager Sites]個as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 單頁應用程式(SPA)編輯器JavaScript SDK [現在是開放原始碼](/help/implementing/developing/hybrid/reference-materials.md)。

## [!DNL Adobe Experience Manager Assets]個as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 使用資產微服務產生的轉譯支援浮水印影像檔案。 它可以設定為處理設定檔，並使用PNG檔案作為浮水印。 請參閱[為您的資產加上浮水印](/help/assets/watermark-assets.md)。

* [!DNL Dynamic Media]中的增強功能

   * 選擇性Publish — 現在，行銷團隊可以存取同步到[!DNL Dynamic Media]的[!DNL Dynamic Media]智慧型裁切影像和動態轉譯，以便建立促銷文宣，而完全無須將這些資產發佈至[!DNL Dynamic Media]以進行全域傳送。 [!DNL Experience Manager]和[!DNL Dynamic Media]發佈是分離的，可個別執行以達成此目的。 請參閱[選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)。
   * 管理員現在可以重設布建時收到的[!DNL Dynamic Media]Cloud Service密碼。 重設可在[!DNL Experience Manager]使用者介面中完成，而不需要使用[!DNL Dynamic Media Classic]案頭應用程式。

* 若要瞭解下列增強功能，請參閱[&#x200B; Brand Portal的新功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hant)。

   * 透過Adobe Document Cloud檢視SDK整合強化PDF預覽。
   * 按一下即可下載的功能。
   * 下載體驗有新的管理設定。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發行CIF Core Components v1.3.0。如需詳細資訊，請參閱[CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0)。

* 現已提供產品和類別範本的產品/類別預覽功能。 這可讓AEM中的業務使用者/行銷人員檢視具有真實資料的產品/類別範本。

* 產品和類別新增了屬性頁面，可讓業務使用者檢視與產品SKU/類別ID相關聯的詳細資料。

* 「產品控制檯」新增了排序功能，可依名稱或價格屬性排序產品/類別。

* 產品控制檯新增了產品搜尋功能。

### 錯誤修正 {#bug-fixes-commerce}

* Commerce Cloud設定未遵循繼承。 此問題已修正，以確保設定會繼承值。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

[!UICONTROL Cloud Manager] 2020.9.0版的發行日期為2020年9月3日。

### 新增功能 {#what-is-new-cloud-manager}

* 內容稽核已重新標記為體驗稽核。
* 構建過程被分成三個獨立的 Maven 命令。
* 如果 Git 存放庫複製失敗，最多會重新嘗試 3 次。

### 錯誤修正 {#bug-fixes-cm}

* 內容稽核索引標籤使用作者域而不是發布域錯誤地顯示了 BASE URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請詳閱本節，瞭解Cloud Readiness Analyzer v1.1.0版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* Cloud Readiness Analyzer (CRA)有一個啟動狀態主控台，會顯示一個明確的&#x200B;**產生報表**&#x200B;按鈕，供使用者按一下以執行CRA。

* CRA UI在執行時會顯示進度。 它會顯示正在分析的專案，以及在執行期間找到的結果。

* CRA報表會以表格形式顯示結果的摘要和數目，並依結果型別和重要性層級加以整理。 按一下某個結果的數目，就會自動捲動至該結果在報表中的位置。

### 錯誤修正 {#cra-bug-fixes}

* 在某些情況下，強制重新整理後CRA報表沒有更新。 此版本已修正此問題。

## 內容轉移工具 {#content-transfer-tool}

請詳閱本節，瞭解「內容轉移工具」版本1.1.10的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 內容轉移工具(CTT)支援Azure Blob存放區資料存放區。

* CTT使用者介面具有自動重新載入功能，每30秒會重新載入一次概觀頁面。

* CTT使用者介面新增了按鈕，可輕鬆擷取&#x200B;*存取Token*。

* 已為&#x200B;*URL*&#x200B;和&#x200B;*移轉集名稱*&#x200B;新增描述性驗證訊息。

## 程式碼重構工具 {#code-refactoring}

請詳閱本節，瞭解程式碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI外掛程式支援Repository Modernizer，可讓使用者透過外掛程式執行工具。

  如需詳細資訊，請參閱[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)。

* Repository Modernizer公用程式可用來將現有的專案套件重新建構為與針對AEM as a Cloud Service定義的專案結構相容的套件。

  如需詳細資訊，請參閱[Git資源：儲存庫現代化工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
