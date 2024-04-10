---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1dd2eae9201c86d2cdac78ff99634eff8ca57a05
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 77%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15860 版 {#release-15860}

以下摘要說明維護版本15860數的持續改善，該版本於2024年4月10日公開發佈。 之前的維護版本是版本 15787。

2024.3.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-15860}

無。

### 已修正的問題 {#fixed-issues-15860}

* 修正當啟動參考已刪除或移動的頁面時，顯示啟動主控台的回歸。

### 已知問題 {#known-issues-15860}

無。

### 已棄用的功能和API {#deprecated-15860}

* [Adobe Developer Console 中的 JWT 憑證已被取代](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

請檢視 [過時和移除的功能和API](/help/release-notes/deprecated-removed-features.md) 以瞭解AEMas a Cloud Service中已過時或移除的內容。

### 變更通知 {#change-notice-15860}

**必要採取的行動**

#### 將 CM Java 版本設定為 11 {#set-java-version-11}

新版本 aem-sdk-api 包含使用 Java 11 Target 編譯的類別，該應用程式與 Cloud Manager 組建環境預設 JDK 版本 1.8 不相容。此更新要求使用 JDK 11 執行 Maven。

建議客戶將 `.cloudmanager/java-version` 檔案加入其 git 存放庫的根目錄中，其內容為： `11`。請參閱「[組建環境/設定 Maven JDK 版本](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version)」。


### 內嵌技術 {#embedded-tech-15860}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.24.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
