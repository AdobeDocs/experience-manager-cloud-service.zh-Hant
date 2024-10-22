---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 35%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 18311 {#18311}

以下摘要說明維護版本18311數的持續改善，該版本於2024年10月22日公開發佈。 前一個維護版本是版本 18175。

2024.10.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-18311}

* Assets-41820 ：改善處理監視工具的索引編制。
* Assets-43720 ：改善處理監視程式的功能。
* Assets-42554 ：改善大型資料夾的效能。
* SKYOPS-77603 ：依業務使用者管理重新導向。

### 已修正的問題 {#fixed-issues-18311}

* Assets-37534 ：搜尋變更，不會公開用於核准目標的屬性。
* Assets-38322 ：移除發佈條件提供者設定移除發佈事件功能。
* Assets-40482 ：Scene7視訊播放器中的播放/暫停和靜音/取消靜音按鈕的協助工具問題。
* Assets-40593 ：按一下「Assets >檔案」中的「屬性」按鈕後發生錯誤頁面。
* Assets-40598 ：將未同步的資產移至已啟用同步的資料夾時，同步智慧型裁切。
* Assets-40743 ：檔案名稱中存在某些字元時，觸發取代資產對話方塊會發生問題。
* Assets-40825 ：Assets搜尋Facet在編輯搜尋表單後消失。
* Assets-41007 ：在AEM上刪除有時會在傳送時留下孤立的Assets。
* Assets-41172 ：名稱中不允許使用Dynamic Media範本特殊字元。
* Assets-41896 ：資料夾的cq：discarded屬性中提到的Assets不應發佈至Brand Portal。
* Assets-42067 ： Dynamic Media範本 — 下載發生錯誤。
* Assets-42070 ： Dynamic Media範本 — 非管理員使用者應具有範本建立/編輯存取權。
* Assets-42344 ：連線的Assets同步已中斷連線 — 重新連線並提供客戶建議。
* Assets-42620 ：資產版本的預覽選項問題 — 開啟資產時顯示空白預覽。
* Assets-42701 ：網頁最佳化的影像傳送和裁切問題。
* Assets-42966 ：如果多個作業共用相同的路徑，非同步封鎖可能會因錯誤而解除封鎖。
* Assets-43072 ： Dynamic Media範本 — 範本參考查閱中斷了無效的參考。
* Assets-43212 ：中繼資料結構編輯器中的國際化問題。
* Assets-43202 ：修正從時間軸選取要列印的註解的問題。
* Assets-43502 ： AEM CS現有的影像預設集名稱未顯示在編輯頁面上。
* Assets-43538 ：非同步複製資產作業使用不正確的屬性作為來源路徑。
* Assets-43798 ：在複製資產之前，請先檢查目的地路徑。
* Assets-43945 ：將非同步資產工作佇列的重試延遲增加到20分鐘。
* Assets-44025 ：非同步刪除資產作業在選取個別資產時失敗。
* SITES-26128 ：CreateLiveCopyStep中的類別轉換例外狀況。
* SCRNS-4551 ： [SG集區]包含視訊元件的Screens頻道在瀏覽器預覽和播放器上顯示「一般頁面錯誤」

### 已知問題 {#known-issues-18311}

* FORMS-15818：元件描述項條目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在伺服器記錄中找不到陳述式。這些是無害的記錄陳述式。

### 已過時的功能和 API {#deprecated-18311}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-18311}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 3 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-18311}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
