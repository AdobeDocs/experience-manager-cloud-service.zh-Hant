---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3fbdb150a9a1c133b4910603682e37f1c5d885d2
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 33%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 13804 版 {#release-13804}

以下摘要說明維護版本13804數的持續改善，該版本於2023年10月10日公開發佈。 此維護版本是先前 13665 維護版本的更新。

2023.10.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-13804}

* GRANITE-47238：稽核記錄維護 — 永久刪除cronjobs以使用客戶組態。
* GRANITE-47123：發佈(Sling) — 透過預設非同步初始化虛名路徑快取，改善啟動時間。
* GRANITE-46618：發佈（復寫） — 透過復寫狀態訊息批次處理程式，改善發佈啟動速度。
* GRANITE-47136：建立索引（下載） — 改善新平行索引下載程式的下載速度（透過停用總和檢查碼驗證）。
* GRANITE-47211：發佈(Infra) — 改善發佈層部署的分離（透過儲存和擷取區段存放區修訂名稱）。
* GRANITE-47267：更新至Apache Felix Http Jetty 4.2.18 （包含請求引數處理的錯誤修正）[FELIX-6625](https://issues.apache.org/jira/browse/FELIX-6625))，並改善本機和RDE開發的效能)。
* GRANITE-47247：更新至Sling Servlet Resolver 2.9.14，改善servlet解析度的效能。

### 已修正的問題 {#fixed-issues-13804}

* GRANITE-47376：作者(Infra) — 在滾動式重新啟動後，修正DiscoveryTopologyUndefined錯誤。
* CQ-4353436： AEM Web Console (Sling) - ServiceUserMapperImpl Validators （主體/使用者）中的空設定中斷AEM執行個體([SLING-11912](https://issues.apache.org/jira/browse/SLING-11912))。
* SKYOPS-63925：轉換作業 — 避免出現JDK 11的TransformJob失敗 — ZipException：無效的CEN標頭錯誤（具有disableZip64ExtraFieldValidation JVM標幟）。
* SKYOPS-63361：轉換工作（記錄）透過轉換工作（CUSTOMER_EXTRACT子步驟）改善記錄。
* SKYOPS-64103： FACT工具（記錄） — 減少或截斷Clientlib編譯錯誤和警告訊息。
* SKYOPS-65109： FACT工具（錯誤處理） — 相依性未解析的內容套件會導致正確報告的錯誤。
* SKYOPS-65368： FACT工具（錯誤處理） — 工具陷入無休止的包含循環，並且最終在Clientlibs的循環嵌入時逾時。
* SKYOPS-64031： RDE — 由於ResourceResolverFactory註冊重複([SLING-12019](https://issues.apache.org/jira/browse/SLING-12019))。
* ASSETS-29105： RDE - RDE功能模型中SecurityProviderRegistration requiredServicePids缺少限制提供者。
* GRANITE-44674： CoralUI - Datepicker必填欄位功能不正確。

### 已知問題 {#known-issues-13804}

無。

### 內嵌技術 {#embedded-tech-13804}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
