---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a1baa7f29c6e15af11347debdd341f9972c06e83
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17258 {#release-17258}

以下摘要說明 17258 維護版本的持續改善內容，該版本於 2024 年 7 月 30 日公開發佈。上一個維護版本是版本 17098。

2024.8.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17258}

* ASSETS-31445 - 初始 Dynamic Media 範本功能
* ASSETS-40399 - 已更新 DM 自動轉錄佇列設定
* ASSETS-40873 - 允許透過 OSGI 設定進行中繼資料匯出最大行數設定

### 已修正的問題 {#fixed-issues-17258}

* ASSETS-30613 - 替換資產不會在新的傳遞層中刪除和新增資產
* ASSETS-31882 - 禁止存取作者中的串流資訊清單檔案
* ASSETS-39598 - 大量匯入無法從 S3 後端刪除名稱中含有特殊字元的資產
* CNTBF-209 - 回流作業取消改進
* SCRNS-3762 - 改進序列通道中的 playerLogger，以便在瀏覽器上預覽通道時將記錄放在控制台上
* SCRNS-4455 - 通道內容提供者中的非管理員使用者缺少「管理發佈」和「快速發佈」按鈕
* SITES-22940 - 無法將內容片段視為工作流程承載

### 已知問題 {#known-issues-17258}

無

### 變更通知 {#change-notice-17258}

* 從 2024 年 9 月開始，AEM as a Cloud Service 將透過 Sling 模型匯出工具框架，停用 Resource Resolver 的序列化。如需詳細資訊，請參閱[文件](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)。

### 已過時的功能和 API {#deprecated-17258}

 [已過時和移除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文件中詳細介紹了 AEM as a Cloud Service 已過時和移除的功能和 API。

### 內嵌技術 {#embedded-tech-17258}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
