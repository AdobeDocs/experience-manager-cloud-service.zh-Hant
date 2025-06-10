---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d3cdc3d69c0002c5b124150050f905123457331c
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 47%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 21193 版 {#21193}

以下摘要說明維護版本21193數的持續改善，該版本於2025年6月10日公開發佈。 前一個維護版本為 21005 版。

啟用 2025.6.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-21193}

* Assets-51245：改善觸控式UI中大型資料夾清單的效能。
* Assets-51686：改善大量作業工作，包括更輕鬆的作業取消、增強記錄、稽核下載以獲得大型結果。
* CQ-4360131：改善OpenAPI端點的錯誤回應，允許API使用者端接收正確的結構化錯誤資訊。

### 已修正的問題 {#fixed-issues-21193}

* Assets-41007：已刪除的資產仍可在Content Hub中顯示。
* Assets-50994： AemRequestEventFilter造成過多Jetty執行緒競爭。
* Assets-50155：觸發重複的中繼資料變更事件。
* Assets-50716：在Assets清單檢視中依標題排序的功能未如預期運作。
* Assets-50820：確保正確拒絕對資產關係API的無效請求，並顯示400錯誤。
* Assets-50562：資產上傳API應根據名稱衝突的預設行為來建立版本。
* Assets-50992： Assets API initiateUpload.json端點應傳回「application/json」內容型別。
* Assets-51322：自動移除並到期的非同步路障，這些路障在失敗工作後會無限期保留。
* Assets-51809：由於瀏覽器快取，CSV編輯器未顯示最近儲存的變更。
* SITES-31678：具有內容感知參考的體驗片段(XF)未解析XF Publishing API中的正確語言根。


### 已知問題 {#known-issues-21193}

無。

### 已過時的功能和 API {#deprecated-21193}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21193}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 2 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-21193}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28 - 1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
