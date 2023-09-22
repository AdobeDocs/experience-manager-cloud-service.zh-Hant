---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 44%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 13420 版 {#release-13420}

以下摘要說明維護版本13420數的持續改善，該版本於2023年9月12日公開發佈。 此維護版本取代 13323 版。

2023.9.0 Feature Activation提供此維護版本的完整功能集。 如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-13420}

- ASSETS-19544：屬性上次修改的資產現在已設定為請求處理的使用者。

### 已修正的問題 {#fixed-issues-13420}

- ASSETS-27628：自訂「資產」搜尋面板時，建立了錯誤的「管道」節點
- ASSETS-27539：上傳限制規則運算式比對。
- ASSETS-26530： Unified Shell不會將使用者帶回原始頁面。
- ASSETS-22719：智慧型裁切中斷點命名中的方括弧會中斷智慧型裁切編輯功能。
- ASSETS-27726： linkshare.html不應由Google編制索引。
- ASSETS-27791：中繼資料結構驗證只會針對第一個欄位進行。
- ASSETS-25544：修正停用的CDN快取失效按鈕。
- ASSETS-26575：建立影像集時修正名稱截斷。
- ASSETS-26705：修正非DM資料夾資產和內容片段不必要的處理。
- ASSETS-25740：修正熒幕助讀程式無法使用向下方向鍵，針對「編輯智慧型裁切」頁面上的編輯/裁切控制項，提供名稱和角色的旁白。
- CQ-4354266：無法打開收件匣項目。
- CQ-4354347：更新AEM翻譯。
- DISP-1009：User-Agent作為非第一個標頭會裁切X-Forwarded-Host。
- 各種協助工具及安全性相關修正。

### 已知問題 {#known-issues-13420}

無。

### 內嵌技術 {#embedded-tech-13420}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
