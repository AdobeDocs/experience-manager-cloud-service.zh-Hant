---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: a1686d7796bb1e310b776195bd19df98f6f10650
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 41%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 13323 版 {#release-13323}

以下摘要說明維護版本13323數的持續改善，該版本於2023年9月1日公開發佈。 此維護版本取代發行說13239。

2023.9.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-13323}

- GRANITE-46784：新增選項以停用BearerAuthenticationHandler
- GRANITE-36205：將內部Oak發行版本更新至最新版本
- ASSETS-26713：觸控式UI新版Experience UI儀表板的外部連結 — 統一介面整合和UI觸控最佳化升級
- SKYOPS-63302：將com.adobe.granite：com.adobe.granite.auth.saml升級至v1.0.54
- GRANITE-46634：升級至事件使用者端1.4.0
- GRANITE-46788：將程式庫更新為Apache Commons IO 2.13.0、Commons Lang 3.13.0、Commons Code 1.16.0和Commons Compress 1.23.0
- GRANITE-46705：Apache Felix Http Jetty 4.1.14的更新
- GRANITE-46631：將Jackrabbit版本更新至2.20.11
- SKYOPS-61895：Jackrabbit Filevault 3.7.0更新

### 已修正的問題 {#fixed-issues-13323}

- SKYOPS-63290：修正貯體的不正確演化
- SKYOPS-54607：速率限制器serverload計算對失敗的請求而言不正確
- ASSETS-27648： ContentModelIT無法從其他套件組合讀取排除檔案
- GRANITE-43744：如果驗證需求和虛名路徑配置錯誤，Sling Authenticator就無法正常運作
- GRANITE-46419：AEM與Auth0 Idp的整合問題
- GRANITE-46292： AEM Cloud更新後Okta SAML設定無法運作
- GRANITE-47059：移除Granite Jetty SSL套件

### 已知問題 {#known-issues-13323}

- SITES-15622： GraphQL — 使用數字和布林引數的持續查詢問題。
- SITES-15654： GraphQL — 同名的聯合和屬性發生問題。

### 內嵌技術 {#embedded-tech-13323}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
