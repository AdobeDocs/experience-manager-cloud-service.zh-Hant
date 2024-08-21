---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 80edd0255b38beee93b3f9c779ae0f364500b4a5
workflow-type: ht
source-wordcount: '1176'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17465 {#release-17465}

下面是 17465 維護版本的持續改善內容，該版本於 2024 年 8 月 14 日公開發行。上一個維護版本是版本 17258。

2024.8.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17465}

* FORMS-15436 - 妥善處理 Adobe Sign 狀態排程器中的異常。
* FORMS-15362 - 在 aemds 中新增 forms-foundation 設定，以啟用登入。
* FORMS-15261 - SPA 不會在表單編輯器中呈現。
* FORMS-15138 - 由於 sling commons json 升級而處理雙資料回溯相容性。
* FORMS-15113 - 將金鑰名稱從 vistorId 變更為 sid，以進行 RUM 追蹤。
* FORMS-15103 - 表單中附加的資產未在 Edge Delivery 中發佈。
* FORMS-15082 - 用於對應到自訂最適化表單元件的 JSON 架構描述。
* FORMS-15002 - v1 片段的範本類型註冊。
* FORMS-14845 - 透過表單管理器，支援核心元件基礎表單中的 xdpRef。
* FORMS-14840 - 表單預填服務錯誤。
* FORMS-14836 - 改善表單管理器 UI，以列出 AF1 片段範本。
* FORMS-14834 - AF1 中的片段範本支援。
* FORMS-14275 - 覆寫嵌入容器中的感謝頁面和感謝訊息。
* FORMS-13623 - 為 V2 啟用自動儲存時間功能。
* FORMS-8651 - 在屬性頁面上變更資料模型設定的警告對話框。
* SITES-23310 - 內容片段 REST API：防止內容片段的巢狀參考資料中出現循環相依性關係。
* SITES-23285 - 內容片段 REST API：建立端點以列出所有可用語言。
* SITES-22857 - 內容片段 REST API：核取方塊分項清單欄位不應允許將多個屬性設為 false。
* SITES-22813 - 內容片段 REST API：定義分項清單欄位的最小/最大屬性。
* SITES-22031 - 內容片段 REST API：取得片段資料夾的允許內容片段模型。
* SITES-17640 - 內容片段 REST API：內容片段發佈作業驗證。
* SITES-22677 - 內容片段 REST API：獲取下階參考資料的平面清單。
* SITES-22207 - 建立內容片段時的重複模型。
* SITES-23093 - 事件：為內容片段模型事件的承載新增標籤。
* SITES-23092 - 事件：為內容片段事件的承載新增標籤。
* SITES-22447 - 將體驗片段屬性繼承支援新增至「基本屬性」索引標籤。
* SITES-12209 - 將 cq:policy 新增至索引標籤，提高策略編輯器效能。

### 已修正的問題 {#fixed-issues-17465}

* CQ-4358028 - 如果上傳影片縮圖，則無法建立專案。
* CQ-4357891 - 匯出的 XLIFF 的序列問題。
* CQ-4357059 - 翻譯工作需要數小時才能完成，導致 AEMaaCS 出現 503 逾時。
* FORMS-15320 - 電子郵件提交無法在核心元件表單中運作。
* FORMS-15272 - AEM Forms - 核取方塊群組僅傳送 1 個值。
* FORMS-15269 - 面臨維護版本 16461 後的產品相關問題。
* FORMS-15174 - JsonSchemaParser isValid 問題。
* FORMS-15095 - 多行文字方塊可以延伸到 AEM Forms 中包含的面板外。
* FORMS-15057 - FDM Sharepoint 列出提交 > 999 時的擲回附件錯誤。
* FORMS-15011 - 在編輯器中開啟表單時，核心編輯器導致控制台錯誤。
* FORMS-14809 - SDK 資料夾未在共用臨時目錄中自動建立。
* FORMS-14327 - 表單服務 API：擷取資料：- 在輸入中提供非互動式 pdf 時，給予 500 個回應代碼。
* FORMS-7475 - 排序無法在最適化表單建立頁面上運作。
* FORMS-3309 - 如果在提交表單時選取多個選項，則產生的記錄文件中僅會顯示一個選項。
* SITES-23646 - 如果欄位包含唯一值，則 GraphQL 模型端點對於使用 OpenAPI 建立的模型會失敗。
* SITES-23637 - 內容片段 REST API：OpenAPI 未使用正確的列舉值類型。
* SITES-23573 - 內容片段 REST API：透過 uuid 取得內容片段時，未遵循即時關係。
* SITES-23535 - 內容片段 REST API：內容片段模型分項清單多重欄位具有空值。
* SITES-23534 - 內容片段 REST API：內容片段驗證 ClassCastException。
* SITES-23524 - 調整 GraphQL BFF 模型端點，以支援多重欄位分項清單欄位。
* SITES-23467 - 內容片段 REST API：游標發生問題導致無法搜尋模型。
* SITES-23327 - 時間軸事件處理描述期間，AuditLogTimelineEventProvider 中出現 ArrayIndexOutOfBoundsException。
* SITES-23277 - 內容片段 REST API：內容片段欄位即時關係檢查應僅針對即時副本進行。
* SITES-23232 - 自訂驗證無法在新的 CF 編輯器 UI 中運作。
* SITES-23090 - 內容片段 REST API：無法更新鎖定內容片段的標題。
* SITES-22981 - 提升不深且未發佈的巢狀啟動。
* SITES-22870 - PathAttributesHandler.processSrcAttr ArrayIndexOutOfBoundsException。
* SITES-22814 - 內容片段 REST API：核取方塊分項清單片段值應按模型中定義的金鑰排序。
* SITES-22716 - OOTB 元件即時使用清單有問題。
* SITES-22457 - 提升非深層的啟動不會更新來源內容。
* SITES-22449 - AEM P20 升級後，無法儲存內容片段中的變更。
* SITES-22279 - 內容片段 REST API：內容片段缺少分項清單類型的唯一屬性。
* SITES-22203 - 內容片段 REST API：統一管理 API，以對相同情況做出相同回應。
* SITES-21973 - 內容片段 REST API：模型缺少分項清單類型的唯一屬性。
* SITES-20364 - 302 重新導向無法用於 URL 中的選擇器。
* SITES-21198 - VersionPreviewServlet：在所有叢集節點上同時執行清理造成合併衝突且無法認可。

### 已知問題 {#known-issues-17465}

* ASSETS-40875 - AssetDeleteHandler 類別偵聽資產刪除事件，並根據刪除事件的類型 (PRE_DELETE 或 POST_DELETE) 執行特定動作。在某些情況下，POST_DELETE 類型的事件會導致 NullPointerException。
* FORMS-14340 - FormsAndDocumentOmniSearchHandler 和 CloudStorageSubmitActionInserter 實例化時發生錯誤。這些是無害的記錄陳述式。
* FORMS-15818 - 元件描述項的項目「OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml」在伺服器記錄中找不到陳述式。這些是無害的記錄陳述式。
* &#x200B;
   * SITES-23662 - 無法從伺服器記錄的 JCR 記錄陳述式內提取觸發發佈的使用者。這是針對一項正在開發的功能，可能會導致記錄中出現間歇性且無害的「無法在 OSGI 事件的批次中找到有效的使用者 ID」錯誤。

### 變更通知 {#change-notice-17465}

* 從 2024 年 9 月開始，AEM as a Cloud Service 將透過 Sling 模型匯出工具框架，停用 Resource Resolver 的序列化。如需詳細資訊，請參閱[文件](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)。

### 已過時的功能和 API {#deprecated-17465}

請注意，我們正在更新 `com.day.cq.wcm.api`，並且在目前版本中，我們已將其中某些方法和類別標記為 `@Deprecated`。這些將於未來的版本中刪除，因此若您正在使用其中的任何一個，請考慮改用所建議的替代方案。

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-17465}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 7 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-17465}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
