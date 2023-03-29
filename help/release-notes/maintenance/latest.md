---
title: 的最新維護髮行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新維護髮行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: c6acdd922c052d0db5bf1f05bc03329fbc44ca33
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 34%

---


# 維護版本注意事項 {#maintenance-release-notes}

以下章節概述目前維護版本的Experience Manageras a Cloud Service技術發行說明。

## 11382 版 {#release-11382}

以下概述於2023年3月28日公開發行的維護版本11382的持續改善。 此維護版本是針對先前 11289 維護版本的更新。

此維護版本的功能啟用將為您提供完整的功能集。 如需完整詳情，請參閱[最新版本注意事項](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 已修正的問題 {#fixed-issues}

- ASSETS-21023 — 修正智慧型裁切轉譯，當客戶嘗試透過API存取這些轉譯時，可在所有AEM環境的Publisher例項上看到Null指標例外狀況。
- SKYOPS-49280 — 使用RDE安裝設定或套件組合更新至Publish時，結果可能無法觀察，因為Publish Dispatcher快取未失效

#### Sites {#sites-issues}

- SITES-7796 — 內容作者在匯出至目標時可發佈主內容片段及其個別變化
- SITES-97 - GraphQL:分頁與排序，混合篩選

>[!NOTE]
>
> 在SITES-97中，GraphQL實作已進行一些改善，可能會造成非預期的行為。 請參閱 [AEM GraphQL處理null值的相關變更](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html?lang=zh-Hant) 以取得更多資訊。

#### 資產 {#assets-issues}

- ASSETS-20076 — 新增支援符合目前影像浮水印支援的視訊浮水印
- ASSETS-21428 — 新增CSS變更的排除項目

#### Forms {#forms-issues}

- CQ-4351502 — 更新服務使用者對應以允許在Sites中進行讀取存取

#### 平台 {#platform-issues}

- SITES-11040 — 在Dispatcher中有條件啟用GraphQL持續查詢快取

### 嵌入式技術 {#embedded-tech}

| 科技 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.21.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
