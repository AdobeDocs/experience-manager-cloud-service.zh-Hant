---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: fd0b8ca281f35a92876f3c31baa4e17884f23948
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 47%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 12441 版 {#release-12441}

下面是 12441 維護版本的持續改善內容，該版本於 2023 年 6 月 27 日公開發布。此維護版本是先前 12255 維護版的更新。

2023.7.0 Feature Activation將提供此維護版本的完整功能集。 請參閱 [Experience Manager發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) 以取得詳細資訊。

### 增強功能 {#enhancements-12441}

- SITES-8769：改善ResponsiveGrid中的StyleImpl呼叫

### 已修正的問題 {#fixed-issues-12441}

- 各種與協助工具相關的更新
- SITES-12688：頁面編輯器：邏輯運運算元或無法在資產尋找器搜尋中正常運作
- SITES-4951：頁面編輯器：頁面編輯器中的標籤搜尋找不到子標籤
- SITES-12465：體驗片段：體驗片段元件對話方塊中的箭頭鍵無法運作
- SITES-12893：體驗片段：套用體驗片段的循環參考驗證
- SITES-12715：體驗片段：套用至體驗片段資料夾的雲端服務設定未持續存在
- SITES-13097：體驗片段：無法新增體驗片段至翻譯專案
- SITES-13165： GraphQL：還原篩選null值的預設行為
- SITES-12577：連結檢查器：轉換器不會間歇性地重寫連結
- SITES-13559： MSM：轉出元件時擲回「不可修改」例外狀況
- SITES-11757： MSM：從父項繼承轉出設定不會為子頁面回覆
- SITES-14073：網站管理員：選取沒有要匯出的屬性時，CSV報表因500失敗

### 已知問題 {#known-issues-12441}

無。

### 內嵌技術 {#embedded-tech-12441}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.0 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
