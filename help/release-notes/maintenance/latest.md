---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9a653fbe13b29fa60af7410fff178cbac6ca554d
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 23%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 18598 {#18598}

以下摘要說明維護版本18598數的持續改善，該版本於2024年11月13日公開發佈。 之前的維護版本是版本 18311。由於問題，版本 18459 已設為私人版本。

2024.11.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-18598}

* CQ-4357471：在AEMaaCS中新增對i18n字典翻譯的支援。
* Forms-11646：為AEM Forms相關頁面設定globalContext變數。
* Forms-14833： AEM Forms現在能在最終記錄檔案(DoR)中包含最適化表單片段。
* Forms-14255：使用者現在可以受益於自動儲存功能，該功能會自動將部分完成的表單儲存為草稿。 他們可以稍後再回來，在相同或其他裝置上完成填寫。
* SITES-23591：內容片段：UUID支援的內容片段升級。
* SITES-25440：內容片段：CFM搜尋API以顯示復寫狀態。
* SITES-24369：內容片段：OpenAPI檔案改善。
* SITES-25478：內容片段：新增外部資產參考的後端支援。
* SITES-26119：內容片段：新增對參考型別中外部資產參考的支援。
* SITES-21199：使用通用編輯器的Edge Delivery：新增對從頁面建立的範本的支援。
* SITES-20311：使用通用編輯器的Edge Delivery：新增將CSV匯入試算表的支援。
* SITES-24821：使用通用編輯器的Edge Delivery：將aem.page / aem.live設為與Edge Delivery整合的預設值。

### 已修正的問題 {#fixed-issues-18598}

* CQ-4358730：超過10個要轉譯的索引鍵時，CQPagePreviewGenerator會失敗。
* CQ-4358028：當只有專案管理員群組的使用者在專案建立頁面上上傳新縮圖時，AEM專案建立失敗。
* Forms-14978：為主題編輯器的核心元件式表單啟用頁面載入。
* Forms-15682：問題與AEM Forms和Dynamics FDM整合有關。 當使用者提交表單時，記錄檔案(DOR)未作為PDF附件傳送到指定實體欄位。
* Forms-15799： Adobe Sign GovCloud簽名頁面不會在iframe中轉譯。
* Forms-16113：當身為Adobe Sign帳戶管理員的使用者嘗試存取由另一個使用者（也是管理員）傳送的檔案時，取得合約API可能會傳回與最初建立合約時產生的合約ID不同的合約ID。
* Forms-16596：協助工具問題：熒幕Reader無法辨識已停用的按鈕。
* GRANITE-53907：無法將服務使用者識別為工作流程超級使用者。
* SKYOPS-90560：最新Sling模型版本影響Sling模型匯出的效能。
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
* SITES-25938：啟動：翻譯後專案發生未預期的刪除。
* SITES-25393：使用通用編輯器的Edge Delivery：呈現具有單一段落的格式化RTF文字時，文位元組點遺失。
* SITES-24643：使用通用編輯器的Edge Delivery：OpenGraph和twitter中繼資料屬性在頁面中繼資料模型中無法運作。
* SITES-25401：體驗片段：XF參考更新緩慢。

### 已知問題 {#known-issues-18598}

無。

### 已過時的功能和 API {#deprecated-18598}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-18598}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 21 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-18598}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
