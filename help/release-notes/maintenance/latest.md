---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: f15b42e4012385c461b5440b92f53c4e58fb8ac2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 71%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15977 版本 {#release-15977}

以下摘要說明維護版本15977數的持續改善，該版本於2024年4月19日公開發佈。 上一個維護版本是版本 15939。

2024.4.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant)。

### 增強功能 {#enhancements-15977}

* GRANITE-51335：最佳化AEM健康情況檢查，以提高執行個體穩定性。

### 已修正的問題 {#fixed-issues-15977}

* CQ-4357226：修正OAuth憑證之IMS設定支援中的回歸。
* GRANITE-51335： Ratelimit升級至5.0.4已修正Felix健康情況檢查登入。

### 已知問題 {#known-issues-15977}

無。

### 已過時的功能和 API {#deprecated-15977}

* [Adobe Developer Console 中的 JWT 憑證已被取代](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」，了解 AEM as a Cloud Service 中已過時或已移除的功能。

### 內嵌技術 {#embedded-tech-15977}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20 - 1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.24.6 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
