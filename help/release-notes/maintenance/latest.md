---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 33468de99a3e77539f4bdc9435324c9f52a45d9f
workflow-type: ht
source-wordcount: '350'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 22171 {#22171}

以下摘要說明維護版本 22171 的持續改善內容，此版本已於 2025 年 9 月 2 日公開發佈。前一個維護版本是版本 21994。

啟用 2025.9.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行路徑圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新功能  {#new-features-22171}

* ASSETS-53136：使用 OpenAPI 在 Dynamic Media 中支援虛名 ID。

### 增強功能 {#enhancements-22171}

無。

### 已修正的問題 {#fixed-issues-22171}

* ASSETS-52510：包含 Unicode `U+202F` 的檔案名稱無法執行重複檔案名稱偵測。
* ASSETS-53489：在資產視圖 UI 中刪除資料夾，不會取消核准所有包含的資產。
* ASSETS-54821：Asset Link 中出現間歇性「伺服器錯誤」。
* ASSETS-55024：AEM Assets「透過電子郵件下載」範本中有損壞的影像。
* ASSETS-55325：資產重新命名後，Dynamic Media 靜態 URL 省略檔案副檔名。
* ASSETS-55334：此「連結共用」對話框短暫閃爍後消失或是從未顯示。
* ASSETS-55382：重新啟動的非同步資產工作會建立重複的目標資料夾。
* ASSETS-55472：管理發佈選項「僅包含已發佈的頁面」被忽略。
* SITES-31600：Contexthub js 錯誤中斷個人化。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-22171}

無。

### 已過時的功能和 API {#deprecated-22171}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-22171}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 7 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-22171}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
