---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 47%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17689 {#release-17689}

以下摘要說明維護版本17689數的持續改善，該版本於2024年9月10日公開發佈。 前一個維護版本是版本 17569。

2024.9.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17689}

* Assets-41404：支援DRM改良的變更。
* Assets-41621：已更新非同步資產複製工作。
* Assets-32166：已更新非同步資產移動工作。
* Assets-41429： DM OpenAPI中的影像預設集支援。
* Assets-38968：改善內容片段參考的呈現。
* Assets-41787、ASSETS-41183： Assets大量作業框架的改良。
* GRANITE-52917：最佳化以縮短內容複製套件的安裝時間。
* SCRNS-3980：偵測具有子序列的播放器上的灰色畫面，但未排定資產。

### 已修正的問題 {#fixed-issues-17689}

* Assets-40875： AssetDeleteHandler記錄的虛假NPE。
* Assets-42422：避免觸發單一資產移動的非同步工作。
* Assets-41234：Unified Shell — 如果在搜尋列開啟時開啟，全域導覽可能無法運作。
* Assets-42256： Unified Shell — 指出環境僅間歇運作的標籤/徽章。
* Assets-41271：防止在移動作業期間不必要地重新發佈Assets。
* Assets-38894：限制由處理監視程式重試。
* Assets-40815：使用預覽PDF轉譯，在連結共用UI中顯示PPT檔案。
* Assets-37123：無法在連結共用對話方塊中載入資產預覽。
* CQ-4358156：更新正在刪除之標籤的回溯連結。
* SCRNS-4495：修正不同使用者群組的「貼上」按鈕無法正常運作的問題。
* SCRNS-4512：從AEMaaCS畫面中移除與裝置相關的元件。
* SCRNS-4466：在頻道控制面板上，隱藏 — 檢視資訊清單、產生離線內容、更新資訊清單快取、顯示面板。
* SCRNS-4513：在清單檢視中為搜尋結果頁面新增欄標題。

### 已知問題 {#known-issues-17689}

* Forms-14340：具現化FormsAndDocumentOmniSearchHandler和CloudStorageSubmitActionInserter時發生錯誤。 這些是無害的記錄陳述式。
* Forms-15818：元件描述項專案「OSGI-INF/com.adobe.aemfd.docmanager.impl」。在伺服器記錄檔中找不到*.xml&#39;陳述式。 這些是無害的記錄陳述式。
* SITES-23662：無法從伺服器記錄檔中的JCR記錄陳述式中擷取觸發發佈的使用者。 這是針對正在開發中的功能，可能會在記錄中造成間歇性和無害的「在批次OSGI事件中找不到有效的使用者ID」錯誤。

### 變更通知 {#change-notice-17689}

* 從 2024 年 9 月開始，AEM as a Cloud Service 將透過 Sling 模型匯出工具框架，停用 Resource Resolver 的序列化。如需詳細資訊，請參閱[文件](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)。

### 已過時的功能和 API {#deprecated-17689}

請注意，我們正在更新 `com.day.cq.wcm.api`，並且在目前版本中，我們已將其中某些方法和類別標記為 `@Deprecated`。這些將於未來的版本中刪除，因此若您正在使用其中的任何一個，請考慮改用所建議的替代方案。

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-17689}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 4 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-17689}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.26.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
