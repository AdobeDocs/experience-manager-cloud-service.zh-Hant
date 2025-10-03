---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6cf380fd972888fa21f682b0e799cf5ab594e829
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 48%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 22758 版 {#22758}

以下摘要說明維護版本22758數的持續改善，該版本於2025年10月1日公開發佈。 前一個維護版本是 22450 版。

啟用 2025.10.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-22758}

* Assets-56227：重新命名adobe-countdown-timer修飾元。
* CNTBF-493:2.0.28版的凹凸內容 — 回流套件組合版本。
* CQ-4361110： Granite翻譯。
* CQ-4361112：最新的AEM翻譯。
* GRANITE-56026：改善許可權API狀態程式碼回應。
* GRANITE-61015：已新增`org.apache.commons.io.channels`封裝至公開匯出的清單。
* GRANITE-61167： Felix記錄檔已更新至最新的OSGI規格。
* GRANITE-61167：更新許多Apache Felix相依性。
* GRANITE-61169：改善受保護字串的檢查。
* GRANITE-61622：更新許多Apache Sling相依性。
* GRANITE-61663：將`com.adobe.granite.repository.indexdefs-1.0.2`新增到quickstart。
* GRANITE-61811：將`com.adobe.granite.repository-2.0.0`新增到quickstart。
* SITES-32014：接聽外部事件以更新服務註冊。
* SITES-34277：修正頁面翻譯工作流程中的封鎖錯誤。
* SKYOPS-108706：升級版將套件組合切換至最新版本（etag快取）。
* SKYOPS-114210：正在更新至最新版本的aem.pss.service套件組合。
* SKYOPS-116171：更新至 Sling ResourceResolver 1.12.12。
* SKYOPS-119811：已發行dispatcher-publish 2.0.258。

### 已修正的問題 {#fixed-issues-22758}

* GRANITE-61875：修正「無效運算式評估」的觸發器 — 作者無法儲存內容片段且無法下載資產。
* SITES-22059：修正PDF Viewer元件中的JS錯誤。 核心元件網站> PDF檢視器中的未本地化「檔案預覽不可用」字串。
* GRANITE-59704：修正htmllibmanager.debug所導致的編輯模式失敗。
* GRANITE-61042：將FELIX-6796 （ServiceTracker NPE修正）整合至AEM Felix Web Console套件組合。
* GRANITE-61165：Workspace.copy()擲回RepositoryException。
* GRANITE-61875：將ui.commons更新至5.10.50。

### 已知問題 {#known-issues-22758}

無。

### 已過時的功能和 API {#deprecated-22758}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-22758}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決 13 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-22758}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.1 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
