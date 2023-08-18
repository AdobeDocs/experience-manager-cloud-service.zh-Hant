---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cf8b5d8b11452268b2839053c1e05cc2ec107a91
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 63%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 13173 版 {#release-13173}

以下摘要說明維護版本13173數的持續改善，該版本於2023年8月18日公開發佈。 此維護版本是先前 13099 維護版本的更新。

2023.8.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-13173}

無。

### 已修正的問題 {#fixed-issues-13173}

- SITES-15463：網站範本 — 無法發佈範本。

### 已知問題 {#known-issues-13173}

- SITES-15359：內容片段 — 變數名稱模式無法正確比對具有 ```'_'``` 資源名稱中的。
- Forms-10444：最適化Forms範本 — 無法發佈範本（因應措施：使用發佈主控台）。
- CQ-4354191：工作流程 — 由於nt：unstructured節點上存在復寫中繼資料，自訂啟動器可能會觸發許多次（因應措施：更新啟動器以排除復寫中繼資料屬性以避免重疊）。

### 內嵌技術 {#embedded-tech-13173}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
