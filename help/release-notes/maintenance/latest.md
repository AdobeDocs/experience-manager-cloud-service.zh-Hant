---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 42%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17098 {#release-17098}

以下摘要說明維護版本17098數的持續改善，該版本於2024年7月16日公開發佈。 上一個維護版本是版本 16971。

2024.7.0功能啟動將提供此維護版本的完整功能集。 如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17098}

- SKYOPS-79817：為服務使用者對應啟用Sling功能分析器工作

### 已修正的問題 {#fixed-issues-17098}

- Assets-39665：從6.5移轉至AEMCS後，智慧型裁切同步無法運作
- Forms-14993：Forms API傳回先前有效宣傳品500美元
- GRANITE-52120：CRXDE在顯示存取控制資料時傳回500
- GRANITE-52573：在重新寫入的URL中使用//時傳回400的請求
- GRANITE-52746：所有節點型別未載入建立節點對話方塊
- GRANITE-52777：要求包裝時對404的處理中斷
- GRANITE-52871：確保publish-worker與golden-publish同步，並在壓縮前完成
- SKYOPS-79173：復寫器沒有復寫到符合指定AgentIdFilter的多個代理程式
- SKYOPS-80075：資產名稱中出現變音的問題，導致發佈佇列阻塞(Mac)
- SKYOPS-81032：篩選掉請求產生的記錄，以便在使用增強式記錄時取得記錄

### 已知問題 {#known-issues-17098}

無

### 變更通知 {#change-notice-17098}

- 從 2024 年 9 月開始，AEM as a Cloud Service 將透過 Sling 模型匯出工具框架，停用 Resource Resolver 的序列化。如需詳細資訊，請參閱[文件](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)。

### 已過時的功能和 API {#deprecated-17098}

在AEM as a Cloud Service中已過時和已移除的功能和API的詳細資訊，請參閱[已過時和已移除的功能和API](/help/release-notes/deprecated-removed-features.md)檔案。

### 內嵌技術 {#embedded-tech-17098}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
