---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6fa6fc9015624bec9113a198285531a3bdd7e29c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 97%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 18175 {#release-18175}

以下摘要說明維護版本18175數的持續改善，該版本於2024年10月10日公開發佈。 之前的維護版本是版本 17964。由於問題，版本 18099 已設為私人版本。

2024.10.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-18175}

* ASSETS-38322：為 AEM 啟用 http 請求事件。
* ASSETS-41448：更新 auth.ims 套件組合以支援 FI 到群組對應。
* ASSETS-41684：新增 OOB OSGI 設定以定義 FI 到 Assets、Foundation、Sites 和 Forms 的群組對應。
* ASSETS-43015：更新到最新的 auth.ims 套件組合。
* CQ-4356633：在「僅內容」工具提示中新增額外字元。
* GRANITE-50948：將存放庫服務整合到存放庫服務的 AEM 支援中。
* GRANITE-52454：新增支援協助程式 0.1.2。
* GRANITE-52454：升級 Support Helper GRANITE-52454 升級支援協助程式以使用最新版 AEMaaCS。
* GRANITE-53287：更新安全權限整合測試版本。
* GRANITE-53485：支援複製 Azure Blob 儲存體的服務主體驗證。
* GRANITE-53514：Treeactivation 更新至版本 1.0.26。
* GRANITE-53870：建立內部機制以跳過快速入門的最大 JVM 版本檢查。
* GRANITE-53914：修復使用 Java 17 更新模組版本後的平台測試失敗問題。
* GRANITE-53966：使用單獨的執行緒池進行內容分發。
* GRANITE-54006：更新 Jackson 至 2.17.2。
* GRANITE-54038：將 Creative Cloud Enterprise IMS 用戶端新增至 AEM IMS 用戶端允許清單。
* GRANITE-54054：com.adobe.granite.repository.impl.SystemUserValidation warnOnly 的環境變數。
* GRANITE-54266：生產 SDK 缺少搜尋建議服務。
* GRANITE-54274：接受 Firefly IMS 用戶端。
* GRANITE-54300：更新 Oak 至最新的公開版本 (1.70.0)。
* GUIDES-19069：為 AEM Guides 附加元件新增 guidesPeerLinkIndex。
* SITES-23584：修正 Java 17 上 Foundation 元件測試失敗的問題。
* SKYOPS-69768：SlingModel 無法還原序列化 ResourceResolvers。
* SKYOPS-76378：改善 i18n 中 ResourceBundle 註冊/取消註冊的執行緒安全性。
* SKYOPS-79285：更新 Sling XSS 至 2.4.2。
* SKYOPS-82383：在命令執行描述項中公開「helm-values」轉換 - 合併 - 分析結果。
* SKYOPS-84810：RDE 啟動時跳過「40-initialize-publish.sh」執行。
* SKYOPS-84951：修復可變內容總和檢查碼產生程式碼。
* SKYOPS-85335：將 org.apache.sling.jcr.repoinit 更新至 1.1.52。
* SKYOPS-85336：將 Sling Commons 執行緒更新到 3.3.0。
* SKYOPS-86329：更新平台測試模組的版本以支援 Java 21 SDK。

### 已修正的問題 {#fixed-issues-18175}

* CNTBF-298：從 CC 匯出的封裝中移除 jcr:uuid。
* SKYOPS-83910：修復在 SKYOPS-82371 中發現的並行性問題。
* GRANITE-52876：更新到 com.adobe.granite.ui.content 0.8.1448。
* GUIDES-14445：原生 PDF 產生失敗，出現與取得 Node.js 相依性相關的錯誤。
* GUIDES-16961：標題中帶有 `<conref>` 的不會在 Web 編輯器的基線和翻譯儀表板中解析。
* GUIDES-17283：選取「**使用在 topicmeta 中新增的中繼資料**」選項時，中繼資料屬性不會在原生 PDF 輸出的文件屬性中傳播。
* GUIDES-17793：在大量啟動已發佈內容期間，不會從&#x200B;**大量發佈儀表板**&#x200B;啟動參考的 PDF。

如需更多有關該版本中 Guides 新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-18175}

* FORMS-15818：元件描述項條目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在伺服器記錄中找不到陳述式。這些是無害的記錄陳述式。

### 已過時的功能和 API {#deprecated-18175}

 [已過時和移除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文件中詳細介紹了 AEM as a Cloud Service 已過時和移除的功能和 API。

以下是最近汰除或正在汰除的功能摘要。

#### JavaScript Use API {#javascript-use-api}

[JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) 已正式汰除，因為使用者在偵錯和維護利用 API 的程式碼時面臨挑戰，以及與 Java 替代方案相比存在效能限制。

您應該轉換到 [Java Use API](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-htl/content/java-use-api)，它提供更好的性能、更輕鬆的偵錯和更強大的長期支援。

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

請注意，Adobe 正在更新 `com.day.cq.wcm.api`。它的一些方法和類別在目前版本中已被標記為 `@Deprecated`。這些將在未來版本中刪除。請考慮改用建議的替代方案。

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165：在公共 API 中汰除 org.apache.jackrabbit.oak.plugins.blob。

### 安全性修正 {#security-18175}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 2 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-18175}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
