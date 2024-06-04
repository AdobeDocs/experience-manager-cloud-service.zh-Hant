---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 624ba716cb2ec2a45b0ed70516d0b2ad1db94912
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 44%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 16544 {#release-16544}

以下摘要說明維護版本16544數的持續改善，該版本於2024年6月4日公開發佈。 上一個維護版本是版本 16461。

2024.6.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-16544}

* GRANITE-41133：支援Jakarta Servlet API 5和OSGi Servlet Whiteboard API。
* GRANITE-51355：棄用org.slf4j.event。
* GRANITE-51565：從AEM發佈本機群組時，AEM會失去與外部群組的本機群組關係。
* GRANITE-51707：在http重新導向期間設定Cookie saml_request_path以進行驗證。
* GRANITE-52010：將 Jackrabbit 版本更新至 2.20.16。
* GRANITE-52057：將Filevault更新為3.7.3-T20240514105118-694f6aea，以修正JCRVLT-745。
* SKYOPS-35998：更新「Sling RepoInit」相依性：Repoinit Parser 1.9.0、Repoinit JCR 1.1.46。

### 已修正的問題 {#fixed-issues-16544}

* GRANITE-51375：如果未指定中間路徑，idp-sync會擲回NPE。
* GUIDES-17171：超過15KB之主題的複製和貼上作業失敗，出現非預期的錯誤。
* GUIDES-17088：變更檔案狀態的功能 **檔案屬性** 面板無法正常運作，且變更為 *草稿* 州別。
* GUIDES-16931：建立版本後，主題中的連結影像無法顯示在基準線中。
* GUIDES-16896：可重複使用的內容面板在 **使用者偏好設定** 設定為檢視檔案 **檔案名稱**.

如需Experience Manager指南新功能和增強功能以及已修正問題的詳細資訊，請檢視 [Experience Manager指南發行藍圖](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### 已知問題 {#known-issues-16544}

無。

### 已過時的功能和 API {#deprecated-16544}

若要了解 AEM as a Cloud Service 中已過時或已移除的功能，請查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」。

### 內嵌技術 {#embedded-tech-16544}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
