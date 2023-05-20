---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.9.0 版發行說明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service2020.9.0發行說明。」'
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 19%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 版發行說明  {#release-notes}

以下部分概述了有關 [!DNL Experience Manager] as a Cloud Service2020.9.0。

## 發行日期 {#release-date}

發放日期 [!DNL Adobe Experience Manager] as a Cloud Service2020.9.0是2020年9月24日。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* 單次頁面應用程式 (SPA) 編輯器 JavaScript SDK [現在是開放原始碼。](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets]的新增功能 {#what-is-new-assets}

* 使用資產微服務生成的格式副本支援加水印影像檔案。 它可以配置為「處理配置檔案」，並使用PNG檔案作為水印。 請參閱 [水印您的資產](/help/assets/watermark-assets.md)。

* 在 [!DNL Dynamic Media]

   * 選擇性發佈 — 現在市場營銷團隊可以訪問 [!DNL Dynamic Media] 智慧裁剪影像和同步到的動態格式副本 [!DNL Dynamic Media] 這樣他們就可以製作宣傳材料，而不需要將這些資產發佈到 [!DNL Dynamic Media] 全球交付。 [!DNL Experience Manager] 和 [!DNL Dynamic Media] 發佈是獨立的，可以單獨進行，以實現這一點。 請參閱 [選擇性發佈](/help/assets/dynamic-media/selective-publishing.md)。
   * 管理員現在可以重置 [!DNL Dynamic Media] Cloud Service設定時收到的密碼。 可以在 [!DNL Experience Manager] 用戶介面，無需使用 [!DNL Dynamic Media Classic] 案頭應用。

* 要瞭解以下增強功能，請參見 [Brand Portal的新聞嗎](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html)。

   * 通過Adobe Document Cloud視圖SDK整合增強PDF預覽。
   * 按一下下載功能。
   * 下載體驗的新管理配置。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager商業as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已發佈CIF核心元件v1.3.0。請參閱 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) 的子菜單。

* 現在提供產品/類別模板的預覽功能。 這允許業務用戶/營AEM銷人員查看具有真實資料的產品/類別模板。

* 添加到產品和類別的屬性頁面，使業務用戶能夠查看與產品SKU/類別ID相關的詳細資訊。

* 添加到產品控制台的排序功能允許按名稱或價格屬性對產品/類別進行排序。

* 產品搜索功能已添加到產品控制台。

### 錯誤修正 {#bug-fixes-commerce}

* Commerce Cloud配置不尊重繼承。 已修復此問題以確保配置繼承值。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

發放日期 [!UICONTROL 雲管理器] 版本2020.9.0為2020年9月3日。

### 新增功能 {#what-is-new-cloud-manager}

* 內容稽核已重新標記為體驗稽核。
* 構建過程被分成三個獨立的 Maven 命令。
* 如果 Git Repository 克隆失敗，最多會重新嘗試 3 次。

### 錯誤修正 {#bug-fixes-cm}

* 內容稽核索引標籤使用作者域而不是發布域錯誤地顯示了 BASE URL。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

請參照本節，了解 Cloud Readiness Analyzer v1.1.0 版的新增功能和更新。

### 新增功能 {#what-is-new-cra}

* 雲就緒性分析器(CRA)有一個啟動狀態控制台，該控制台顯示 **生成報告** 按鈕以執行CRA。

* CRA UI在運行時顯示進度。 它顯示正在分析的項目和在執行期間找到的查找結果。

* CRA報告以表格格式顯示按查找類型和重要性級別組織的摘要和查找結果數。 按一下該查找結果的數量將自動滾動到該查找結果在報告中的位置。

### 錯誤修正 {#cra-bug-fixes}

* 在某些情況下，強制更新後CRA報告未得到更新。 此版本已修復。

## 內容轉移工具 {#content-transfer-tool}

請按照本部分瞭解內容傳輸工具1.1.10版的新增內容和更新。

### 新增功能 {#what-is-new-ctt}

* 內容傳輸工具(CTT)支援Azure Blob儲存資料儲存。

* CTT用戶介面具有自動重新載入功能，每30秒重新載入一次概述頁。

* 添加到CTT用戶介面以檢索的按鈕 *訪問令牌* 容易。

* 為添加的描述性驗證消息 *URL* 和 *遷移集名稱*。

## 程式碼重構工具 {#code-refactoring}

請按照本部分瞭解代碼重構工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* AIO-CLI插件支援Repository Modernizer，允許用戶使用該插件執行該工具。

   請參閱 [Git資源：aio-cli-plugin-aem — 雲服務 — 遷移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 的子菜單。

* Repository Modernizer實用程式可用於將現有項目包重構為與為AEMas a Cloud Service定義的項目結構相容的包。

   請參閱 [Git資源：儲存庫現代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 的子菜單。
