---
title: ' [!DNL Adobe Experience Manager]  雲端服務 2020.9.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 雲端服務 2020.9.0 版發行說明。'
translation-type: tm+mt
source-git-commit: 9bb087cb0570a1f3bbffb989a9399d3274f9c5e1
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 20%

---


# [!DNL Adobe Experience Manager] 雲端服務 2020.9.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.9.0 版的一般發行說明。

## [!DNL Adobe Experience Manager Sites] 雲端服務 {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* 單頁應用程式(SPA)編輯器Javascript SDK現 [在是開放原始碼。](/help/implementing/developing/spa/reference-materials.md)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新功能 {#what-is-new-commerce}

* 已發佈CIF核心元件v1.3.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) ，以取得詳細資訊。

* 現在提供產品／類別範本的預覽功能。 這可讓AEM中的商業使用者／行銷人員檢視具有真實資料的產品／類別範本。

* 屬性頁面已新增至產品和類別，可讓商業使用者檢視與產品SKU/類別ID相關的詳細資訊。

* 新增至「產品主控台」的排序功能，允許依名稱或價格屬性來排序產品／類別。

* 產品搜尋功能已新增至產品主控台。

### 錯誤修正 {#bug-fixes-commerce}

* Commerce Cloud設定不尊重繼承。 此問題已修正，以確保配置繼承值。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.9.0 is September 03, 2020.

### 新功能 {#what-is-new-cloud-manager}

* 內容審核已重新標示為「體驗審核」。
* 建立程式已分為三個不同的Maven命令。
* 如果Git Repository無法克隆，則最多將重新嘗試三次。

### 錯誤修正 {#bug-fixes-cm}

* 「內容審核」標籤使用作者網域而非發佈網域錯誤顯示基本URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請參照本節，了解 Cloud Readiness Analyzer v1.1.0 版的新增功能和更新。

### 新功能 {#what-is-new-cra}

* Cloud Readiness Analyzer(CRA)有一個啟動狀態控制台，它顯示一個明確的「生成報告 **** 」按鈕，供用戶按一下以執行CRA。

* CRA UI會在執行中顯示進度。 它顯示正在分析的項目和在執行過程中發現的查找結果。

* CRA報告以按查找類型和重要性級別組織的表格形式顯示了調查結果的摘要和數目。 按一下該尋找的數目會自動捲動至該尋找在報表中的位置。

### 錯誤修正 {#cra-bug-fixes}

* 在某些情況下，CRA報告在強制更新後無法更新。 此版本已修正此問題。

