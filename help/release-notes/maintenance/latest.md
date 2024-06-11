---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 8f7c2fc175a542df5725693cfc332802d54e1e88
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 88%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 16544 {#release-16544}

以下摘要說明 16544 維護版本的持續改善內容，該版本於 2024 年 6 月 4 日公開發佈。上一個維護版本是版本 16461。

2024.6.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/tw/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!CAUTION]
>
>請使用下方參考的SDK，因為先前的SDK已確認回歸：
>`AEM SDK v2024.06.16647.20240607T103723Z-240500`

### 增強功能 {#enhancements-16544}

* GRANITE-41133：支援 Jakarta Servlet API 5 和 OSGi Servlet Whiteboard API。
* GRANITE-51355：停止支援 org.slf4j.event。
* GRANITE-51565：從 AEM 發佈本機群組時，AEM 會遺失與外部群組的本機群組關係。
* GRANITE-51707：在 http 重新導向期間設定 cookie saml_request_path 以進行驗證。
* GRANITE-52010：將 Jackrabbit 版本更新至 2.20.16。
* GRANITE-52057：將 Filevault 更新至 3.7.3-T20240514105118-694f6aea，以修正 JCRVLT-745。
* SKYOPS-35998：更新「Sling RepoInit」相依性：Repoinit Parser 1.9.0、Repoinit JCR 1.1.46。

### 已修正的問題 {#fixed-issues-16544}

* GRANITE-51375：如果未指定中繼路徑，idp-sync 會擲回 NPE。
* GUIDES-17171：複製和貼上超過 15 KB 的主題的作業執行失敗，並顯示非預期錯誤。
* GUIDES-17088：從「**檔案屬性**」面板變更文件狀態的功能無法正常運作，且變更為「*草稿*」狀態。
* GUIDES-16931：建立版本後，主題中的連結影像無法出現在基準線中。
* GUIDES-16896：「**使用者偏好設定**」設定為依照「**檔案名稱**」檢視檔案時，可重複使用的內容面板不會列出元素。

如需更多有關 Experience Manager Guides 中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 版本藍圖](https://experienceleague.adobe.com/tw/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知問題 {#known-issues-16544}

無。

### 變更通知 {#change-notice-16544}

從2024年9月開始，AEMas a Cloud Service將透過Sling模型匯出工具架構停用資源解析器的序列化。 另請參閱 [說明檔案](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) 以取得更多詳細資料。

### 已過時的功能和 API {#deprecated-16544}

若要了解 AEM as a Cloud Service 中已過時或已移除的功能，請查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」。

### 內嵌技術 {#embedded-tech-16544}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
