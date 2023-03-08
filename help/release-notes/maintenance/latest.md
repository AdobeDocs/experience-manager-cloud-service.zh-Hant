---
title: 的最新維護髮行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新維護髮行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 6%

---


# 維護髮行說明 {#maintenance-release-notes}

以下章節概述Experience Manageras a Cloud Service最新維護版本的技術發行說明。

## 版本11289 {#release-11289}

以下摘要為2023年3月7日公開發行之11289版維護的持續改善。 此維護版本是先前維護版本10912的更新。

本維護版本的啟用功能將提供完整的功能集。 請參閱 [最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md) 以取得完整詳細資訊。

### 已知問題 {#known-issues}

如果您使用CORS，請勿升級。 在此版本中發現影響GraphQL內容傳送功能的問題。 若變更預設AEM Dispatcher設定中關於快取GraphQL持續查詢的方式，可能會中斷這類查詢的GraphQL內容傳送。 此問題將在我們的下一個維護髮行中修正。

### 已修正的問題 {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584修正無法為具有註解的頁面建立即時副本的問題
- SITES-11683停用繼承部分中斷的MSM Live Copy

#### 資產 {#assets-issues}

- ASSETS-20879修正回歸，使資產報表UI無法正常運作，並導致產生的報表結果不正確。
- ASSETS-21020修正資產下載中斷的問題 — 移動資產後，影像設定檔不存在
- ASSETS-21023修正Dynamic Media中影像轉譯無法透過API存取的問題

#### Forms {#forms-issues}

- 無

#### 平台 {#platform-issues}

- GRANITE-44467 — 修正更新現有節點時，某些情況下的Filevault不會保留mixin類型和子節點時，造成匯入失敗的問題

### 內嵌技術 {#embedded-tech}

| 科技 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 2.27.0版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本1.4.20-1.4.0 | [HTML模板語言規範](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.21.2版 | [AEM WCM核心元件](https://github.com/adobe/aem-core-wcm-components) |
