---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: dbdc63db9a9ac954ce6359d3643231d6e195fd53
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 87%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15575 版 {#release-15575}

以下摘要說明維護版本15575數的持續改善，該版本於2024年3月19日公開發佈。 之前的維護版本是版本 15262。

2024.3.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-15575}

無。

### 已修正的問題 {#fixed-issues-15575}

* ASSETS-36358：無法轉譯上傳報告。
* GRANITE-50774：GraniteContent 應在初始化時使用屬性值的確定性順序。

### 已知問題 {#known-issues-15575}

無。

### 變更通知 {#change-notice-15575}

**必要採取的行動**

#### 將 CM Java 版本設定為 11 {#set-java-version-11}

新版本 aem-sdk-api 包含使用 Java 11 Target 編譯的類別，該應用程式與 Cloud Manager 組建環境預設 JDK 版本 1.8 不相容。此更新要求使用 JDK 11 執行 Maven。

建議客戶將 `.cloudmanager/java-version` 檔案加入其 git 存放庫的根目錄中，其內容為： `11`。另請參閱 [建置環境/設定Maven JDK版本](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).

#### 將 aem-cloud-testing-clients 更新至 1.2.1 {#update-aem-cloud-testing-clients}

未來變更將要求自訂功能測試中使用的 [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) 資料庫至少要更新到版本 **1.2.1**

確保 `it.tests/pom.xml` 中的相依性已更新。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

此變更必須在2024年4月6日之前執行。

無法更新相依性資料庫將造成「自訂功能測試」步驟中的管道失敗。

### 內嵌技術 {#embedded-tech-15575}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
