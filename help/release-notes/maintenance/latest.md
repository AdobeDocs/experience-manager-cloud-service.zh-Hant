---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b7e7bc7546b836667fff9db0ea5419e751f492cb
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 78%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15977 版本 {#release-15977}

下面是 15977 維護版本持續改善內容的摘要；該版本於 2024 年 4 月 19 日公開發行。上一個維護版本是版本 15939。

2024.4.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hant)。

### 增強功能 {#enhancements-15977}

* GRANITE-51335：最佳化 AEM 健康情況檢查以提高執行個體穩定性。

### 已修正的問題 {#fixed-issues-15977}

* CQ-4357226：已修正 IMS 設定對 OAuth 憑證的支援迴歸問題。
* GRANITE-51335：速率限制升級到 5.0.4 已修正 Felix 健康情況檢查註冊。

### 已知問題 {#known-issues-15977}

* **(僅適用於AEM Forms)** 安裝AEM Cloud Foundation維護發行說15977後，在表單製作期間和針對發佈的表單，最適化表單欄位的呈現順序不正確。 如果您使用AEM Forms，為避免任何不便，建議在即將推出的維護版本中解決問題前不要升級至15977版本。


### 已過時的功能和 API {#deprecated-15977}

* [Adobe Developer Console 中的 JWT 憑證已被取代](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」，了解 AEM as a Cloud Service 中已過時或已移除的功能。

### 內嵌技術 {#embedded-tech-15977}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.24.6 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
