---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: ea3a476f7f2d7d97a2428c6facf61b746dba7a23
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 65%

---

# 維護發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術發行說明。

## 11873 版 {#release-11873}

以下概述於2023年5月3日公開發行的11873版維護持續改善項目。 此維護版本是針對先前 11835 維護版本的更新。

此維護版本的功能啟用將為您提供完整的功能集。如需完整詳情，請參閱[最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 增強功能 {#enhancements}

- SITES-1200 — 使用標籤型篩選增強搜尋API功能
- GRANITE-42939 — 將淘汰註解和警告新增至oauth-server程式碼

### 已知問題 {#known-issues-11873}

無.

### 已修正的問題 {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745 — 修正PublishPageRenderingErrorsHigh的問題
- GRANITE-4388 — 修正Mongo上大量DAM資產寫入作業後，輸送量降低的問題
- SITES-11922 — 修正未移除同步狀態的取消發佈預覽問題
- ASSETS-21648 — 修正資產相關功能的權限問題

### 嵌入式技術 {#embedded-tech-11873}

| 科技 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.21.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
