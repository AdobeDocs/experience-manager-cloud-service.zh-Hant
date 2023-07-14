---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 241dcc75e9f2c840be85c34800d8145457baa58d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 43%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 12697 版 {#release-12697}

以下摘要說明2023年7月14日公開發佈的維護版本資12697的持續改善。 此維護版本是先前 12549 維護版的更新。維護發行說12697會取代12585以修正一個問題。

2023.7.0 Feature Activation將提供此維護版本的完整功能集。 請參閱 [Experience Manager發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) 以取得詳細資訊。

### 增強功能 {#enhancements-12697}

- 一般RDE穩定性改善(SKYOPS-61133、SKYOPS-55281、SKYOPS-61216和SKYOPS-61401)
- DXML-12327： AEM Guides：支援原生PDF發佈的語言變數
- DXML-11518： AEM Guides：增強原生PDF發佈的中繼資料支援
- DXML-10093： AEM Guides：支援連線至外部資料來源以及將資料插入dita主題
- DXML-10699： AEM Guides：支援翻譯中的XLIFF格式
- DXML-10141： AEM Guides：使用微服務式發佈以進行PDF（原生和DITA-OT）、HTML和自訂預設集型別的選項
- SKYOPS-61385 — 更新Dispatcher以在Apache HTTPD中評估規則運算式時使用libpcre2

### 已修正的問題 {#fixed-issues-12697}

- AEM Guides：各種原生PDF增強功能和穩定性修正
- SKYOPS-53130：改善RDE中的AC工具支援
- SKYOPS-57146：修正AEM啟動時的Sling死結

### 已知問題 {#known-issues-12697}

無。

### 內嵌技術 {#embedded-tech-12697}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.0 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
