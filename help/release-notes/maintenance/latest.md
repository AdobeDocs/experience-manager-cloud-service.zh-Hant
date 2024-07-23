---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: ht
source-wordcount: '332'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17098 {#release-17098}

以下摘要說明 17098 維護版本的持續改善內容，該版本於 2024 年 7 月 16 日公開發佈。上一個維護版本是版本 16971。

2024.7.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17098}

- SKYOPS-79817：為服務使用者對應啟用 Sling 功能分析器任務

### 已修正的問題 {#fixed-issues-17098}

- ASSETS-39665：從 6.5 遷移到 AEMCS 後，Smart Crops Sync 無法運作
- FORMS-14993：為先前工作附屬物，表單 API 傳回 500
- GRANITE-52120：顯示「存取控制」資料時，CRXDE 傳回 500
- GRANITE-52573：在重寫的 URL 中使用 // 時請求傳回 400
- GRANITE-52746：「建立節點」對話方塊中未載入所有節點類型
- GRANITE-52777：包裝請求時 404 的處理中斷
- GRANITE-52871：確保 publish-worker 與 golden-publish 同步，並在壓縮之前完成
- SKYOPS-79173：複製器未複製到與給定 AgentIdFilter 相符的多個代理程式
- SKYOPS-80075：資產名稱中的 Umlaut 問題導致發佈佇列阻塞 (Mac)
- SKYOPS-81032：使用增強記錄功能時，篩除取得記錄之請求所產生的記錄

### 已知問題 {#known-issues-17098}

無

### 變更通知 {#change-notice-17098}

- 從 2024 年 9 月開始，AEM as a Cloud Service 將透過 Sling 模型匯出工具框架，停用 Resource Resolver 的序列化。如需詳細資訊，請參閱[文件](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)。

### 已過時的功能和 API {#deprecated-17098}

 [已過時和移除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文件中詳細介紹了 AEM as a Cloud Service 已過時和移除的功能和 API。

### 內嵌技術 {#embedded-tech-17098}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
