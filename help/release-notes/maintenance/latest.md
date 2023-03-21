---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service. 的最新維護版本注意事項。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service. 的最新維護版本注意事項。'
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 100%

---


# 維護版本注意事項 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 最新維護版本的技術版本注意事項。

## 11289 版 {#release-11289}

下面是 11289 維護版本的持續改善內容，該版本於 2023 年 3 月 7 日公開發布。 此維護版本是針對先前 10912 維護版本的更新。

此維護版本的功能啟用將為您提供完整的功能集。 如需完整詳情，請參閱[最新版本注意事項](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 已知問題 {#known-issues}

如果您使用的是 CORS，請不要升級。 此版本發現會影響 GraphQL 內容交付功能的問題。 關於 GraphQL 持續性查詢如何快取的預設 AEM Dispatcher 設定變更可能會破壞這類查詢的 GraphQL 內容交付。我們下一個維護版本將修復這個問題。

### 已修正的問題 {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584 已解決無法為帶有註解的頁面建立 Live Copy 的問題
- SITES-11683 已停用 MSM Live Copy 及部分破壞的繼承

#### 資產 {#assets-issues}

- ASSETS-20879 已修復阻止資產報告 UI 正常工作並導致產生報告結果不正確的回歸問題。
- ASSETS-21020 已解決資產下載損壞的問題 - 移動資產後影像設定檔不存在
- ASSETS-21023 已解決 Dynamic Media 中影像轉譯而阻止透過 API 存取的問題

#### Forms {#forms-issues}

- 無

#### 平台 {#platform-issues}

- GRANITE-44467 - 已修復導致匯入失敗的問題 (更新現有節點時)。某些執行個體下的 Filevault 不保留混合類型和子節點

### 嵌入式技術 {#embedded-tech}

| 科技 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.21.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
