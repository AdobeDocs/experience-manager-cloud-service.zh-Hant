---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 26178edc3308801e0273aca67b7cd82180131483
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 37%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 12255 版 {#release-12255}

以下摘要說明2023年6月13日公開發佈的維護版本資12255的持續改善。 此維護版是先前 12142 維護版的更新。

此維護版本的功能啟用將為您提供完整的功能集。如需完整詳情，請參閱[最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 增強功能 {#enhancements-12255}

無。

### 已知問題 {#known-issues-12255}

- ASSETS-25729 — 檢視切換器功能表被切斷
- ASSETS-25728 — 重新處理資產選項在搜尋檢視中無法使用
- ASSETS-22603 — 某些下載型別的資產報表欄在UI中顯示「null」值。 可下載的CSV不受影響。

### 已修正的問題 {#fixed-issues-12255}

- 各種協助工具相關更新
- ASSETS-15116 — 資產搜尋檢視中提供的「前往位置」選項
- ASSETS-17453 - (Dynamic Media)無法選取視訊的自訂縮圖
- ASSETS-19279 — 大型檔案的資產下載封存
- ASSETS-19544 — 使用者上次修改以更新資產
- ASSETS-20146 - （觸控式UI）資產下載報表因驗證錯誤而失敗報表一律會顯示在報表清單頁面的頂端
- ASSETS-21056 — 最佳化資產參考效能以將寫入作業最小化
- ASSETS-21909 — 當vtt無法下載時無法看到智慧型裁切視訊
- ASSETS-22261 — 連結共用下載資料夾結構與資產UI下載內容不一致
- ASSETS-22550 — 搜尋篩選面板現在預設為開啟
- ASSETS-22920 — 從Brand Portal取消發佈資料夾並不會將中的資產標籤為已取消發佈
- ASSETS-22922 — 停用的檢視器預設集會顯示在Dynamic Media元件中
- ASSETS-23461 — 從「資產」搜尋檢視快速發佈Brand Portal
- ASSETS-23466 -InDesign Server無法存取的連結處理無法解析包含空格的AAL連結
- ASSETS-23469 — 預設資產篩選器與自訂篩選器衝突
- ASSETS-23981 — 標題排序功能在集合連結中無法運作
- ASSETS-24723 — 已發佈的資產再次重新處理，使用者無需干預
- GRANITE-45385 — 移轉樹狀結構啟動以使用Sling工作而非工作流程

### 內嵌技術 {#embedded-tech-12255}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.0 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
