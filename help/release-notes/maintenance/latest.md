---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2e90e40a0fe439653987a23792a4c1ec612aafd6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 57%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 21570 {#21570}

以下摘要說明維護版本21570數的持續改善，該版本於2025年7月15日公開發佈。 前一個維護版本為版本 21484。

>[!NOTE]
>
>[發行版本21484](/help/release-notes/maintenance/2025/2025-7-0.md#21484)已設為私人，並由發行說21570取代。

啟用 2025.7.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-21570}

* 已移轉至Apache Httpd 2.4.63

### 已修正的問題 {#fixed-issues-21570}

* SKYOPS-112722 — 修正造成虛名URL解析失敗的問題

### 已知問題 {#known-issues-21570}

* 相關的AEM SDK具有不同的版本ID (21575)，並可透過軟體發佈入口網站取得。
* Apache HTTP Server 2.4.63版對`mod_rewrite`在URL中處理問號(`?`)的方式進行了重大變更。 已實作此變更以防止使用`UnsafeAllow3F`旗標，這被視為安全性風險。 這會影響任何依賴URL模式中問號偵測的`RewriteRule`指示。

### 已過時的功能和 API {#deprecated-21570}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21570}

無

### 嵌入技術 {#embedded-tech-21570}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
