---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本注意事項。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本注意事項。'
source-git-commit: ea71ca9fe259fbbf497a35930a10450bd4e26ce8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 維護版本注意事項 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本注意事項。

## 11382 版 {#release-11382}

下面是 11382 維護版本的持續改善內容，該版本於 2023 年 3 月 28 日公開發布。此維護版本是針對先前 11289 維護版本的更新。

此維護版本的功能啟用將為您提供完整的功能集。 如需完整詳情，請參閱[最新版本注意事項](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 已知問題 {#known-issues-11382}

- SITES-12573 - 如果有一個變數未指定，在篩選條件中使用變數的 GraphQL 查詢將會失敗。如果您搭配 AEM as a Cloud Service 使用 GraphQL，請勿更新到這個版本。
- SKYOPS-51970 — 識別buildImage步驟中使用的FACT版本回歸，導致使用者對應不相符。
- GRANITE-44542 — 針對未為封裝篩選器中包含的資料夾指定封裝nodetype（透過提供.content.xml與jcr:primaryType）的客戶，回報問題。 這會將這些資料夾視為nt:folder，在各種情況下會造成問題。

### 已修正的問題 {#fixed-issues-11382}

- ASSETS-21023 - 修復了智慧型裁切轉譯，當客戶嘗試透過 API 存取這些轉譯時可能會觀察到所有 AEM 環境的發佈者執行個體有 Null 指標例外狀況。
- SKYOPS-49280 - 使用 RDE 安裝設定或套件更新到 Publish 時，可能無法觀察到結果，因為 Publish Dispatcher 快取未失效

#### Sites {#sites-issues-11382}

- SITES-7796 - 內容作者能夠在匯出到目標時發佈主內容片段及其各自的變體
- SITES-97 - GraphQL：分頁和排序、混合篩選

>[!NOTE]
>
> 在 SITES-97 中，對 GraphQL 實作進行了一些改進，這些改進可能會導致未預期的行為。如需詳細資訊，請參閱[關於處理 Null 值的 AEM GraphQL 變更](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html)。

#### Assets {#assets-issues-11382}

- ASSETS-20076 - 新增對影片浮水印的支援，其符合目前影像浮水印支援
- ASSETS-21428 - 新增 CSS 變更的排除項目

#### Forms {#forms-issues-11382}

- CQ-4351502 - 更新服務使用者對應以允許在 Sites 中的讀取權限

#### Platform {#platform-issues-11382}

- SITES-11040 - 在 Dispatcher 中有條件地啟用 GraphQL 持續性查詢快取

### 嵌入式技術 {#embedded-tech-11382}

| 科技 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.21.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
