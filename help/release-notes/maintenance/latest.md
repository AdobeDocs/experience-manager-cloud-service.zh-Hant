---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e1fa4b3bcb04ab3e834b34f507f1350fb536b513
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 50%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 21005 版 {#21005}

以下摘要說明維護版本21005數的持續改善，該版本於2025年5月27日公開發佈。 前一個維護版本為 20626 版。

啟用 2025.5.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-21005}

* GRANITE-58927：語意搜尋切換改善。
* GRANITE-58800：將Apache Commons集合更新至4.5.0版。
* GRANITE-58866： Oak更新至1.80.0。
* SKYOPS-106509：透過Java 21中的反射式存取增強GSON相容性。
* SKYOPS-107761： Sling Model Jackson Exporter更新至1.1.6。
* SKYOPS-107813：更新至 Sling ResourceResolver 1.12.8。

### 已修正的問題 {#fixed-issues-21005}

* CNTBF-443：修正SearchSlingJob `EVENT_JOB_TOPIC`屬性。
* GRANITE-57853：修正UI中的下拉式清單對齊問題。
* GRANITE-58107：在OAuth處理常式中停用以使用者為基礎的Pod相似性，修正Publish上的404錯誤。
* GRANITE-58276、SLING-12755：修正可能導致HTL Script Engine Factory無法正確啟動的OSGi相依性週期，造成間歇性伺服器端轉譯錯誤。
* SKYOPS-105151：修正存取套件組合清單時的NPE。
* SKYOPS-83910、SKYOPS-82371 — 修正JSP編譯的並行問題。

#### AEM 指南 {#guides}

* GUIDES-26919 ：在啟用Unified Shell的情況下開啟DITA Map時，編輯器會間歇性地重新整理。
* GUIDES-26282：在更新或建立主題時無法關閉JCR工作階段連線，會導致記憶體流失和服務停機時間。
* GUIDES-26434：如果DITA內容有Weblink，但範圍不是`external`，則原生PDF發佈會無限期繼續。
* GUIDES-26516：當內容發生錯誤時，原生PDF和AEM網站的發佈會停止並排入佇列。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-21005}

無。

### 已過時的功能和 API {#deprecated-21005}

* GRANITE-54164：已從公用API中移除`org.apache.jackrabbit.oak.plugins.blob`。
* GRANITE-54280：已從公用API中移除`org.apache.jackrabbit.oak.cache`。
* GRANITE-58332：公用API已棄用`org.apache.jackrabbit.oak.plugins.memory`。
* 已棄用[Experience Cloud Setup Automation](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md)功能。

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21005}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 5 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 變更通知 {#change-notice-21005}

* 此版本包含以下新產品索引版本：
   * **damAssetLucene-12**

先前索引版本的自訂版本將自動與新產品索引版本合併。請對合併版本套用進一步的自訂更新。

#### 更新aem-cloud-testing-clients {#update-aem-cloud-testing-clients-21005}

即將進行的變更將要求自訂功能測試中使用的資料庫[aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients)至少更新為&#x200B;**1.2.1**&#x200B;版本（建議：最新版本1.2.9）

確保 `it.tests/pom.xml` 中的相依性已更新。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.9</version>
</dependency>
```

此變更必須在2025年6月15日之前執行。
無法更新相依性資料庫將造成「自訂功能測試」步驟中的管道失敗。

### 嵌入技術 {#embedded-tech-21005}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28 - 1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
