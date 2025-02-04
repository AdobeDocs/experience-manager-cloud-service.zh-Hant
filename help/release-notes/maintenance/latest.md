---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a3c414f9b5e575856a942e02661e8c70a7083495
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 89%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 19149 {#19149}

下面是 19149 維護版本持續改善的內容，該版本於 2025 年 1 月 21 日公開發佈。前一個維護版本是版本 18751。

2025.1.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-19149}

* ASSETS-45286：顯示下載封存同步工作的精細進度。
* ASSETS-46296：資產選擇器中支援動態媒體範本。
* ASSETS-44796：DAM 非同步資產工作的觸發資產事件。

### 已修正的問題 {#fixed-issues-19149}

* GRANITE-55074：確保在錯誤回應上設定 CORS 回應標頭。
* ASSETS-43755：大量資產相關的擴充性改善。
* ASSETS-45399：建立資產即時副本後重新導向至 Assets Console。
* ASSETS-45462：自訂資料夾縮圖的瀏覽器快取問題。
* ASSETS-46398：隱藏 DM 範本的下載和重新處理動作。
* ASSETS-44484：重新儲存所連接資產設定的問題。
* ASSETS-44122：在複製到目前資料夾時，非同步複製資源工作不會重新命名目標資料夾。
* ASSETS-44463：成功匯出中繼資料時，看不到下載 CSV 按鈕。
* ASSETS-45134：移動有目標標題的工作會覆寫所有資料夾標題。
* ASSETS-45137：與透過資產視圖大量上傳發生衝突。
* ASSETS-45758：新增關係後，資產關係會出現無限繁忙/載入動畫。
* ASSETS-44148：AEM 中的 NODE_MOVED 事件可能會導致記錄出現虛假 NPE。
* ASSETS-28607：設定自訂影片縮圖時出現 JS 錯誤。
* GRANITE-55781：改善 Adob&#x200B;&#x200B;e Developer Console 和 AEM 之間的群組同步。「[使用者群組和產品設定檔同步的變更](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)」內的更多詳細資訊。
* GRANITE-55754：確保 SDK 啟動指令碼支援 Java 21。
* GRANITE-54248：無法捲動大型資源資料夾中的所有項目。
* SCRNS-4597：搜尋結果清單視圖改善。


### 已知問題 {#known-issues-19149}

無。

### 已過時的功能和 API {#deprecated-19149}

 [已過時和移除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文件中詳細介紹了 AEM as a Cloud Service 已過時和移除的功能和 API。

#### 使用者群組和產品設定檔同步的變更

使用 Adob&#x200B;&#x200B;e Admin Console 進行權限管理時，不得使用下列群組，因為這些群組將不再同步至 AEM：
* 以 _GROUP_NAME_SUFFIX 結尾的 AEM 群組。
* 來自其他環境、程式或產品的產品設定檔。

若要了解更多詳情，請查看「[使用者群組和產品設定檔同步的變更](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)」。

#### 棄用SPA編輯器 {#deprecate-spa-editor}

[自2025.1.0版開始的新專案已棄用SPA編輯器](/help/implementing/developing/hybrid/introduction.md)。SPA編輯器仍支援現有專案，但不應用於新專案。

在AEM中管理Headless內容的首選編輯器包括：

* [用於視覺化編輯的通用編輯器](/help/edge/wysiwyg-authoring/authoring.md)。
* [用於表單式編輯的內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md)。

### 安全性修正 {#security-19149}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 4 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-19149}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
