---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 39b2afda66e3bcb7db8ae63a2d0dcd27014ce377
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 77%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 12790 版 {#release-12790}

以下摘要說明2023年7月21日公開發佈的維護版本資12790的持續改善。 此維護版本是先前 12697 維護版本的更新。

2023.7.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-12790}

無。

### 已修正的問題 {#fixed-issues-112790}

- SLING-11974 — 修正SlingHttpServletRequest#getUserPrincipal中未經驗證要求的回歸。 此修正可確保針對未驗證的請求傳回主體。

### 已知問題 {#known-issues-12790}

無。

### 內嵌技術 {#embedded-tech-12790}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.0 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
