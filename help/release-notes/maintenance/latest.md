---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ea7e027b5247b64e78da1d14e4e602f39a37e4bd
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 27%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 18099 {#release-18099}

以下摘要說明維護版本18099數的持續改善，該版本於2024年10月9日公開發佈。 前一個維護版本是版本 17964。

2024.10.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/tw/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-18099}

* Assets-43015：更新至最新的auth.ims套件組合。
* Assets-41684：更新src/main/features/docker/ethos/base-ims-oauth.json。
* Assets-38322：啟用AEM的http要求事件。
* Assets-41684：新增OOB OSGI設定，以定義Assets、Foundation、Sites和Forms的FI與群組對應。
* Assets-41448：更新auth.ims套件組合以支援FI對群組的對應。
* CQ-4356633：在「僅限內容」工具提示中新增額外字元。
* SITES-23584：基礎元件測試在Java 17上失敗。
* GUIDES-19069：新增guidesPeerLinkIndex for aem guides add on.
* GRANITE-54300：更新 Oak 至最新的公開版本 (1.70.0)。
* GRANITE-54274：接受FireflyIMS使用者端。
* GRANITE-36205：將內部 Oak 發行版本更新到最新版。
* GRANITE-45298：低許可權使用者可以不使用簡訊服務但採用XSS方式製作惡意表單，以取得RCE。
* GRANITE-54266：生產SDK缺少搜尋建議程式服務。
* GRANITE-50948 — 將存放庫服務整合到AEM新增替代存放庫服務以進行本機開發。
* GRANITE-53966：對內容分發使用單獨的對話串池。
* GRANITE-53514： Treeactivation 1.0.26。
* GRANITE-54054： com.adobe.granite.repository.impl.SystemUserValidation warnOnly的環境變數。
* GRANITE-50948：將存放庫服務整合到存放庫服務的AEM支援中。
* GRANITE-52454：新增支援協助程式0.1.2。
* GRANITE-53514： Treeactivation 1.0.26。
* GRANITE-54038：將Creative Cloud企業IMS使用者端新增至AEM IMS使用者端允許清單。
* GRANITE-36205：將內部 Oak 發行版本更新到最新版。
* GRANITE-53485：復寫Azure Blob儲存體的支援服務主要驗證。
* GRANITE-54006：將Jackson更新為2.17.2。
* GRANITE-53287：正在更新安全性許可權整合測試版本。
* GRANITE-53914：使用Java 17更新模組版本的平台測試失敗。
* GRANITE-53870：建立內部機制，以略過快速入門的最大JVM版本檢查。
* GRANITE-52454：升級支援協助程式GRANITE-52454升級支援協助程式以使用AEMaaCS的最新版本。
* SKYOPS-85335：將org.apache.sling.jcr.repoinit更新至1.1.52。
* SKYOPS-85336：將Sling Commons Threads更新至3.3.0。
* SKYOPS-76378：改善i18n中ResourceBundle註冊/取消註冊的對話串安全性。
* SKYOPS-84951：可變內容總和檢查碼產生代碼不正確。
* SKYOPS-82383：在命令執行描述項中公開「helm-values」convert-merge-analyze結果。
* SKYOPS-86329：更新平台測試模組版本，以支援java 21 sdk。
* SKYOPS-69768： SlingModels不會將ResourceResolvers還原序列化。
* SKYOPS-84810：在RDE啟動時略過「40-initialize-publish.sh」執行。
* SKYOPS-79285：將Sling XSS更新至2.4.2

### 已修正的問題 {#fixed-issues-18099}

* CNTBF-298：從CC匯出的套件中移除jcr：uuid。
* SKYOPS-83910：修正SKYOPS-82371中發現的並行問題。
* GRANITE-52876：更新至com.adobe.granite.ui.content 0.8.1448。
* GRANITE-53088：由SITES-11992的修正所引入的回歸。
* GUIDES-14445：原生PDF產生失敗，並出現與取得Node.js的相依性相關的錯誤。
* GUIDES-16961：網頁編輯器的基準線和轉譯控制面板中無法解析含有`<conref>`的標題。
* GUIDES-17283：選取&#x200B;**使用新增至topicmeta**&#x200B;選項的中繼資料時，中繼資料屬性不會傳播至原生PDF輸出的檔案屬性。
* GUIDES-17793：在大量啟用已發佈內容期間，參考的PDF沒有從&#x200B;**大量Publish儀表板**&#x200B;啟用。

如需版本中修正之全新和增強型指南功能與問題的詳細資訊，請檢視[Experience Manager Guides發行藍圖](https://experienceleague.adobe.com/tw/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-18099}

* FORMS - 15818：元件描述項條目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在伺服器記錄中找不到陳述式。這些是無害的記錄陳述式。

### 已過時的功能和 API {#deprecated-18099}

 [已過時和移除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文件中詳細介紹了 AEM as a Cloud Service 已過時和移除的功能和 API。

以下是最近已棄用的功能或即將棄用的功能的摘要。

#### JavaScript使用API {#javascript-use-api}

[JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api)已正式淘汰，因為使用者需要偵錯和維護運用API的程式碼，而且與Java替代方案相比，存在效能限制。

您應該轉換至[Java Use API，](https://experienceleague.adobe.com/en/docs/experience-manager-htl/content/java-use-api)，提供更優異的效能、更輕鬆的偵錯，以及更優異的長期支援。

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

請注意，Adobe正在更新`com.day.cq.wcm.api`。 其某些方法和類別在目前版本中已標示為`@Deprecated`。 這些功能將在未來版本中移除。 請考慮改用他們建議的替代方案。

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165：棄用公用API中的org.apache.jackrabbit.oak.plugins.blob。

### 安全性修正 {#security-18099}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 2 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-18099}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
