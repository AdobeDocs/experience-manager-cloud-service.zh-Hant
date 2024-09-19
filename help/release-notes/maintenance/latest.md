---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: ht
source-wordcount: '572'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17689 {#release-17689}

以下摘要說明維護版本 17689 的持續改善內容，該版本於 2024 年 9 月 10 日公開發行。前一個維護版本是版本 17569。

2024.9.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17689}

* ASSETS-41404：支援 DRM 改善的變更。
* ASSETS-41621：已更新非同步資產複製工作。
* ASSETS-32166：已更新非同步資產移動工作。
* ASSETS-41429：DM OpenAPI 中的影像預設支援。
* ASSETS-38968：改善內容片段參考的展現方案。
* ASSETS-41787、ASSETS-41183：資產批次操作框架的改善。
* GRANITE-52917：改善內容複製套件安裝時間的最佳化內容。
* SCRNS-3980：偵測播放器在未有任何資產排程的子序列中出現的灰色畫面。

### 已修正的問題 {#fixed-issues-17689}

* ASSETS-40875：由 AssetDeleteHandler 記錄的虛假 NPE。
* ASSETS-42422：避免因為單一資產移動觸發非同步工作。
* ASSETS-41234：Unified Shell - 如果在搜尋欄開啟時開啟全球導航系統，可能無法運作。
* ASSETS-42256：Unified Shell - 表示環境只能間歇性運作的標記/徽章。
* ASSETS-41271：防止在移動操作期間不必要地重新發佈資產。
* ASSETS-38894：透過處理監控程式限制重試次數。
* ASSETS-40815：使用預覽 PDF 轉譯以便在「連結共用使用者介面」中顯示 PPT 檔案。
* ASSETS-37123：無法在「連結共用對話框」中載入資產預覽。
* CQ-4358156：更新已刪除標記的反向連結。
* SCRNS-4495：修正在不同使用者群組無法正確運作的「貼上」按鈕。
* SCRNS-4512：從 AEMaaCS 畫面移除與裝置相關的元件。
* SCRNS-4466：在管道儀表板上，隱藏 - 檢視資訊清單、產生離線內容、更新資訊清單快取和顯示面板。
* SCRNS-4513：在以清單檢視的搜尋結果頁面新增欄標題。

### 已知問題 {#known-issues-17689}

* FORMS-14340：FormsAndDocumentOmniSearchHandler 和 CloudStorageSubmitActionInserter 實例化時發生錯誤。這些是無害的記錄陳述式。
* FORMS-15818：元件描述項的項目「OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml」在伺服器記錄中找不到陳述式。這些是無害的記錄陳述式。
* SITES-23662：無法從伺服器記錄的 JCR 記錄陳述式內擷取觸發發佈的使用者。這是針對一項正在開發的功能，可能會導致記錄中出現間歇性且無害的「無法在 OSGI 事件的批次中找到有效的使用者 ID」錯誤。

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
