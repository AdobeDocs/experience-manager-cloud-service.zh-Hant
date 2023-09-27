---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 0dab7428d8ae5ec4c11a88ff310fad649a365868
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 24%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 13665 版 {#release-13665}

以下摘要說明維護版本13665數的持續改善，該版本於2023年9月27日公開發佈。 此維護版本取代 13420 版。

2023.10.0 Feature Activation提供此維護版本的完整功能集。 如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-13665}

* 內容片段API中的多項改善。
* ASSETS-26713： Assets儀表板：新的Experience UI儀表板現在可從觸控式UI存取。
* SITES-11206：內容片段：搜尋內容片段的API。
* SITES-11262：內容片段：用於切換到新內容片段編輯器的按鈕。
* SITES-15447：核心元件：版本2.23.4。

### 已修正的問題 {#fixed-issues-13665}

* 各種翻譯相關更新。
* CQ-4354428：工作流程：無法完成收件匣中的任務。
* SITES-9733：內容片段：內容片段參考面板中的資產參考顯示0（零）參考。
* SITES-14561：內容片段：修正並改善標籤轉換的HTML。
* SITES-14882：內容片段：編輯內容片段並關閉索引標籤而不按一下儲存或關閉按鈕後，就會儲存值。
* SITES-15167：內容片段：使用無效承載修補變數不會傳回400而不是500。
* SITES-15514：內容片段： RTE內表格的格式錯誤的Markdown輸出。
* SITES-15661：內容片段：請勿在片段API的參考欄位中使用唯一限制和重新排序專案。
* SITES-15730：畫面：畫面頻道預覽功能在控制面板上無法運作。
* SITES-15995：內容片段：模式和片段長文字欄位的MIME型別均已硬式編碼。
* SITES-16074：內容片段：非字串的標籤欄位[] 無法從JCR中擷取。
* SITES-16084：內容片段：CFHomeCardModelImpl缺少目標導覽器。
* SITES-14773：體驗片段：連結參考未在體驗片段內更新。
* SITES-14899：體驗片段：已針對Target中的XF變數建立多個選件。
* SITES-8590： GraphQL：持續性查詢中的變數編碼問題。
* SITES-9224： GraphQL： GraphQLServlet中的「寫入器已關閉」例外狀況。
* SITES-14800： GraphQL：使用變數的持續GraphQL查詢出現例外狀況。
* SITES-15586： GraphQL：使用null值篩選的持續查詢問題。
* SITES-15622： GraphQL：數字和布林引數的持續查詢問題。
* SITES-15654： GraphQL：同名的聯合與屬性問題。
* SITES-15267：啟動：促銷活動不會擷取在修改啟動設定之前修改的啟動頁面。
* SITES-15406：啟動：無法新增啟動頁面。
* SITES-15427：啟動：「提升目前頁面和子頁面」範圍的行為不一致。
* SITES-15429：啟動：編寫頁面在提升啟動項時遭到刪除。
* SITES-15462：啟動：自動促銷活動程式發佈促銷活動範圍以外的頁面。
* SITES-15815：啟動：從啟動中刪除頁面導致啟動無法成功提升。
* SITES-15223：頁面編輯器：在平板電腦大小模擬器中無法調整元件大小。
* SITES-15463：頁面範本：無法發佈範本。

### 已知問題 {#known-issues-13665}

無

### 內嵌技術 {#embedded-tech-13665}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
