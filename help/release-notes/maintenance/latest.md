---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9a653fbe13b29fa60af7410fff178cbac6ca554d
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 73%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 18598 {#18598}

以下摘要說明維護版本18598數的持續改善，該版本於2024年11月13日公開發佈。 之前的維護版本是版本 18311。由於問題，版本 18459 已設為私人版本。

2024.11.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-18598}

* CQ-4357471：在 AEMaaCS 中新增對 i18n 字典翻譯的支援。
* Forms-11646：為AEM Forms相關頁面設定globalContext變數。
* Forms-14833： AEM Forms現在能在最終記錄檔案(DoR)中包含最適化表單片段。
* Forms-14255：使用者現在可以受益於自動儲存功能，該功能會自動將部分完成的表單儲存為草稿。 他們可以稍後再回來，在相同或其他裝置上完成填寫。
* SITES-23591：內容片段：UUID 支援的內容片段升級。
* SITES-25440：內容片段：CFM 搜尋 API 可顯示複寫狀態。
* SITES-24369：內容片段：OpenAPI 文件改善。
* SITES-25478：內容片段：新增對外部資產參考的後端支援。
* SITES-26119：內容片段：在參考類型中新增對外部資產參考的支援。
* SITES-21199：Edge Delivery 搭配通用編輯器：新增支援從頁面建立的範本。
* SITES-20311：Edge Delivery 搭配通用編輯器：新增將 CSV 匯入試算表的支援。
* SITES-24821：Edge Delivery 搭配通用編輯器：將 aem.page / aem.live 設定為與 Edge Delivery 整合的預設值。

### 已修正的問題 {#fixed-issues-18598}

* CQ-4358730：有超過 10 個索引鍵需要翻譯時，CQPagePreviewGenerator 會失敗。
* CQ-4358028：當只有專案管理員群組的使用者在專案建立頁面上上傳新縮圖時，AEM專案建立失敗。
* FORMS-14978：為主題編輯器的核心元件式表單啟用頁面載入。
* Forms-15682：問題與AEM Forms和Dynamics FDM整合有關。 當使用者提交表單時，記錄檔案(DOR)未作為PDF附件傳送到指定實體欄位。
* Forms-15799： Adobe Sign GovCloud簽名頁面不會在iframe中轉譯。
* Forms-16113：當身為Adobe Sign帳戶管理員的使用者嘗試存取由另一個使用者（也是管理員）傳送的檔案時，取得合約API可能會傳回與最初建立合約時產生的合約ID不同的合約ID。
* FORMS-16596：協助工具問題：螢幕閱讀器無法識別停用按鈕。
* GRANITE-53907：無法將服務使用者識別為工作流程超級使用者。
* SKYOPS-90560：最新Sling模型版本影響Sling模型匯出的效能。
* SITES-10575：MSM：Blueprint Bloomfilter 載入程式嘗試載入 > 100,000 行。
* SITES-20755：內容片段：具有 UUID 重新整理的資產參考無法顯示縮圖。
* SITES-26253：內容片段：UUID 移轉：將 Sling 工作主題變更為一般。
* SITES-21338：內容片段：referencedBy 端點未傳回正確的頁面參考。
* SITES-24421：內容片段：編輯 CF 端點無法用於透過 GET CF 擷取的 CF。
* SITES-25461：內容片段：依照模型篩選來搜尋 CF 時，應不區分大小寫。
* SITES-25471：內容片段：修正 ModelValidatorServlet 中全域模型的驗證。
* SITES-25795：內容片段：未設定 cq 日期時，CF 模型 API 會失敗。
* SITES-25817：內容片段：增強 promotionLaunch：更新 CF 啟動的最後促銷活動。
* SITES-26030：內容片段：端點 /referencesTree 未傳回所需的標頭。
* SITES-26031：內容片段：CFM 搜尋端點未傳回複寫狀態。
* SITES-26213：內容片段：取消發佈內容片段應僅驗證已發佈的參考。
* SITES-26226：內容片段：在指定的路徑都無法使用時開始工作流程的問題。
* SITES-26238：內容片段：API 傳回的資產參考的順序與 JCR 的順序不同。
* SITES-25456：事件：移動頁面時，除了頁面移動事件之外，還會產生頁面刪除事件。
* SITES-25658：事件：頁面內容狀態事件中未填入層級和 sourceUrl。
* SITES-6497：啟動：無法在啟動中建立頁面。
* SITES-25938：啟動：在翻譯專案後意外刪除。
* SITES-25393：Edge Delivery 搭配通用編輯器：使用單一段落轉譯格式化的 RTF 時，文字節點遺失。
* SITES-24643：Edge Delivery 搭配通用編輯器：OpenGraph 和 Twitter 中繼資料屬性無法在頁面中繼資料模型中運作。
* SITES-25401：體驗片段：XF參考更新緩慢。

### 已知問題 {#known-issues-18598}

無。

### 已過時的功能和 API {#deprecated-18598}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-18598}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 21 個已確認的漏洞，從而強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-18598}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
