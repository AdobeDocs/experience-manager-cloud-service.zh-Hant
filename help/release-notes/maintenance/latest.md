---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c638039ea957f5f7ae0dc64f49c3ace4381cb040
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 26%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 18459 {#18459}

以下摘要說明維護版本18459數的持續改善，該版本於2024年11月5日公開發佈。 前一個維護版本是版本 18311。

2024.11.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-18459}

* CQ-4357471：在AEMaaCS中新增對i18n字典翻譯的支援。
* SITES-23591：內容片段：UUID支援的內容片段升級。
* SITES-25440：內容片段：CFM搜尋API以顯示復寫狀態。
* SITES-24369：內容片段：OpenAPI檔案改善。
* SITES-25478：內容片段：新增外部資產參考的後端支援。
* SITES-26119：內容片段：新增對參考型別中外部資產參考的支援。
* SITES-21199：使用通用編輯器的Edge Delivery：新增對從頁面建立的範本的支援。
* SITES-20311：使用通用編輯器的Edge Delivery：新增將CSV匯入試算表的支援。
* SITES-24821：使用通用編輯器的Edge Delivery：將aem.page / aem.live設為與Edge Delivery整合的預設值。

### 已修正的問題 {#fixed-issues-18459}

* CQ-4358730：超過10個要轉譯的索引鍵時，CQPagePreviewGenerator會失敗。
* Forms-14978：為主題編輯器的核心元件式表單啟用頁面載入。
* Forms-16596：協助工具問題：熒幕Reader無法辨識已停用的按鈕。
* SITES-10575： MSM：Blueprint Bloomfilter載入器嘗試載入>100,000列。
* SITES-20755：內容片段：具有UUID重新整理的資產參考未顯示縮圖。
* SITES-26253：內容片段： UUID移轉：將Sling作業主題變更為通用。
* SITES-21338：內容片段：referencedBy端點未傳回正確的頁面參考。
* SITES-24421：內容片段：編輯CF端點不適用於透過GETCF擷取的CF。
* SITES-25461：內容片段：在搜尋CF時依模型篩選應該不區分大小寫。
* SITES-25471：內容片段：修正ModelValidatorServlet中全域模型的驗證。
* SITES-25795：內容片段：沒有cq日期集時，CF模型API會失敗。
* SITES-25817：內容片段：增強promoteLaunch： CF啟動項的更新上次促銷活動。
* SITES-26030：內容片段：端點/referencesTree未傳回所需的標頭。
* SITES-26031：內容片段：CFM搜尋端點未傳回覆寫狀態。
* SITES-26213：內容片段：取消發佈內容片段應該僅驗證已發佈的引用。
* SITES-26226：內容片段：指定路徑皆無效時，出現開始工作流程問題。
* SITES-26238：內容片段： API傳回的資產參考與JCR的順序不同。
* SITES-25456：事件：移動頁面時，除了頁面移動事件外，也會產生頁面刪除事件。
* SITES-25658：事件：頁面內容狀態事件中未填入tier和sourceUrl。
* SITES-6497：啟動：在啟動中建立頁面無法運作。
* SITES-25393：使用通用編輯器的Edge Delivery：呈現具有單一段落的格式化RTF文字時，文位元組點遺失。
* SITES-24643：使用通用編輯器的Edge Delivery：OpenGraph和twitter中繼資料屬性在頁面中繼資料模型中無法運作。

### 已知問題 {#known-issues-18459}

無。

### 已過時的功能和 API {#deprecated-18459}

 [已過時和移除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文件中詳細介紹了 AEM as a Cloud Service 已過時和移除的功能和 API。

### 內嵌技術 {#embedded-tech-18459}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
