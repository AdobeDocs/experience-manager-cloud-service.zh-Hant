---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 4353f2a9f6cd649a4377adb9891e0873a51d6ab2
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 85%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術發行說明。

## 11873 版 {#release-11873}

下面是 11873 維護版本的持續改善內容，該版本於 2023 年 5 月 3 日公開發佈。此維護版本是針對先前 11835 維護版本的更新。

此維護版本的功能啟用將為您提供完整的功能集。如需完整詳情，請參閱[最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 增強功能 {#enhancements}

- SITES-1200 - 透過標記型篩選增強搜尋 API 功能
- GRANITE-42939 - 向 oauth 伺服器程式碼新增汰除註解和警告

### 已知問題 {#known-issues-11873}

- SITES-13253 — 核心元件v2.22.6中的RecursionTooDeepException
- SITES-13256 — 使用特殊URL設定的核心WCM預告會中斷頁面呈現
- GRANITE-45462 — 傳訊用戶端多地區設定
- GRANITE-45562 — 影像組合傳回200而非404的問題

### 已修正的問題 {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745 - 修復 PublishPageRenderingErrorsHigh 的問題
- GRANITE-4388 - 修復了在 Mongo 上寫入大量 DAM 資產後輸送量下降的問題
- SITES-11922 - 修復了從未刪除同步狀態的預覽中取消發佈的問題
- ASSETS-21648 - 修復了資產相關功能的權限問題

### 嵌入式技術 {#embedded-tech-11873}

| 科技 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.22.6 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
