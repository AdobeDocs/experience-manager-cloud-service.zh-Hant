---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e035c1c27f652af231034588eb1359354182dcb0
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 57%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 25194 版 {#25194}

以下摘要說明維護版本25194數的持續改善，該版本於2026年4月1日公開發佈。 前一個維護版本是版本 24678。

2026.4.0 功能啟用會提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>發行說24893已設為私人。

### 增強功能 {#enhancements-25194}

* Assets-65127：事件自訂中繼資料：改善中繼資料名稱的處理。
* Assets-63313：根據C2PA資訊清單，自動建立匯出資產和父項的相關連結。
* Assets-10995：限制下載zip檔中的資產數量。

### 已修正的問題 {#fixed-issues-25194}

* Assets-62882：管理員檢視：上傳多個無效檔案名稱時資訊工具提示中斷。
* Assets-63642：共用連結無法在某些開發環境(SLA3)上轉譯資產。
* Assets-59267：載入傳遞裝載的應用程式中繼資料時出現NPE。
* Assets-59227：中繼資料匯出：由於regex相符，不再包含未選取的屬性。
* Assets-65187：當欄資料包含逸出逗號時，在雲端中進行CSV預覽。
* Assets-63441：確保所有使用者都有權讀取Assets Omnisearch設定。
* SITES-40095：中繼資料編輯器：本機內容片段參考超過10個專案。

### 已知問題 {#known-issues-25194}

無。

### 已過時的功能和 API {#deprecated-25194}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-25194}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 9 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-25194}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
