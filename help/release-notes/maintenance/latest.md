---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: b83d8736d47778ed133e0cc07207e02e581bbc69
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 34%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 24893 版 {#release-24893}

以下摘要說明維護版本24893數的持續改善，該版本於2026年3月17日公開發佈。 前一個維護版本是版本 24678。

2026.3.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-24893}

* CNTBF-613：修正存取遭拒(JCR-101) — 無法登入節點型別。
* GRANITE-53957：將適用於oak-blob-azure的Azure SDK V8升級至V12。
* GRANITE-57035：使用Bouncy Castle作為預設的安全性提供者。
* GRANITE-59249：避免在JVM中註冊安全性提供者。
* GRANITE-61564： `/security/users.html`上的檢視設定無法開啟給管理員。
* GRANITE-64748： OIDC：可設定的`sling.oauth-request-key` Cookie到期日。
* SITES-39767：透過請求屬性(CSP)支援Nonce值。
* SKYOPS-129301：將API jar javadoc規範層級設為17。
* GRANITE-64962：將Apache Jackrabbit Oak更新至1.92.0。
* GRANITE-64963：將Apache Jackrabbit Filevault更新至4.2.0。
* GRANITE-64764：將Apache Commons文字更新至1.15.0版。
* SKYOPS-131412：將Apache Commons Exec更新至1.6.0。
* SKYOPS-131432：將Felix SCR更新至2.2.14。
* SKYOPS-131907：將Sling API區域更新為1.1.10。
* SKYOPS-131938：將GSON更新至2.13.2。
* SKYOPS-132173：將Apache Commons轉碼器更新至1.21.0。
* SKYOPS-132182：將Sling租使用者更新至1.1.8。
* SKYOPS-132267：將org.osgi.service.component更新至1.5.1。
* SKYOPS-132272：將Sling功能模型更新為2.0.4。
* SKYOPS-133689：更新Dispatcher以使用Apache httpd 2.4.66。

### 已修正的問題 {#fixed-issues-24893}

* GRANITE-64443： `workflow.core`移除`log4j`已棄用的匯出專案。
* GRANITE-64543：許可權限制回應應符合API合約。

#### AEM Guides {#guides-24893}

* GUIDES-38412 ：在編輯Schematron `(*.sch)`檔案並使用尋找和取代功能時，尋找和取代面板會在底部部分地顯示在畫面外，阻止存取其輸入欄位和控制項。
* GUIDES-37806：使用不同條件預設集的多個地圖重複使用相同主題時，將最新地圖發佈至Salesforce會覆寫主題內容，導致向先前發佈地圖的使用者顯示不正確的資料。
* GUIDES-39394：當最初受管理為具有特定版本（例如，在`/en/`下）的語言特定資產的影像移至具有更新版本的全域資料夾並執行基準匯出時，新基準會繼續參考該影像的過時語言特定版本，導致基準匯出失敗。
* GUIDES-39054：建立動態基準線時，編輯器有時會因為多個並行的API請求而停止回應，導致所有其他作業暫停。
* GUIDES-37781：將使用者指派給稽核任務時，下拉式清單會列出所有使用者，而非僅列出與所選專案關聯的使用者，導致無效的使用者選項。
* GUIDES-39385：開啟地圖的報表時，「篩選器」面板的載入有所延遲。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-24893}

無。

### 已過時的功能和 API {#deprecated-24893}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-24893}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 9 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-24893}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.92.0 | [Oak 1.92.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.92.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.66 | [Apache Httpd 2.4.66](https://apache.googlesource.com/httpd/+/refs/tags/2.4.66/CHANGES) |
| AEM 核心元件 | 2.30.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
