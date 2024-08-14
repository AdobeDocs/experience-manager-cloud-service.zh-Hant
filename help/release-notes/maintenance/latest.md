---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 80edd0255b38beee93b3f9c779ae0f364500b4a5
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 15%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17465 {#release-17465}

以下摘要說明維護版本17465數的持續改善，該版本於2024年8月14日公開發佈。 上一個維護版本是版本 17258。

2024.8.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17465}

* Forms-15436 — 在Adobe Sign狀態排程器中正常處理例外狀況。
* Forms-15362 — 在AEMDS中新增Forms-foundation的設定以啟用登入。
* Forms-15261 - SPA不會在Forms編輯器中轉譯。
* Forms-15138 — 處理由於Sling Commons json升級造成的雙重資料回溯相容性。
* Forms-15113 — 將金鑰名稱從vistorId變更為sid，以進行RUM追蹤。
* Forms-15103 — 表單中附加的Assets未在Edge傳送中發佈。
* Forms-15082 — 要對應至自訂最適化表單元件的JSON結構描述。
* Forms-15002 - v1片段的範本型別註冊。
* Forms-14845 — 透過Forms Manager支援核心元件基礎表單中的xdpRef。
* Forms-14840 - Forms預填服務錯誤。
* Forms-14836 — 改善表單管理員UI，以列出AF1片段範本。
* Forms-14834 - AF1中片段的範本支援。
* Forms-14275 — 在內嵌容器中覆寫感謝頁面和感謝訊息。
* Forms-13623 — 為V2啟用自動節省時間功能。
* Forms-8651 — 有關變更表單屬性頁面上資料模型設定的警告對話方塊。
* SITES-23310 — 內容片段REST API：防止內容片段的巢狀參考中出現循環相依性。
* SITES-23285 — 內容片段REST API：建立端點以列出所有可用語言。
* SITES-22857 — 內容片段REST API：核取方塊列舉欄位不應允許將多個屬性設定為false。
* SITES-22813 — 內容片段REST API：定義列舉欄位的最小值/最大值屬性。
* SITES-22031 — 內容片段REST API：取得片段資料夾的允許內容片段模型。
* SITES-17640 — 內容片段REST API：內容片段Publish操作驗證。
* SITES-22677 — 內容片段REST API：擷取下級參考的平面清單。
* SITES-22207 — 建立內容片段時複製的模型。
* SITES-23093 — 事件：將標籤新增至內容片段模型事件的裝載。
* SITES-23092 — 事件：將標籤新增至內容片段事件的裝載。
* SITES-22447 — 將體驗片段屬性繼承支援新增到基本屬性索引標籤。
* SITES-12209 — 將cq：policy新增到索引以改善原則編輯器效能。

### 已修正的問題 {#fixed-issues-17465}

* CQ-4358028 — 如果已上傳縮圖，則無法建立專案。
* CQ-4357891 — 匯出的XLIFF出現順序問題。
* CQ-4357059 — 翻譯工作需要數小時才能完成，導致AEMaaCS中出現503逾時。
* Forms-15320 — 電子郵件提交在核心元件型表單中無法運作。
* Forms-15272 - AEM Forms — 核取方塊群組僅傳送1個值。
* Forms-15269 — 在維護發行16461定後面臨產品相關問題。
* Forms-15174 - JsonSchemaParser isValid問題。
* Forms-15095 — 多行文字方塊可以延伸到AEM Forms中可包含的面板之外。
* Forms-15057 — 針對提交> 999擲回附件錯誤的FDM Sharepoint清單。
* Forms-15011 — 在編輯器中開啟表單時，核心編輯器造成主控台錯誤。
* Forms-14809 — 未在共用的臨時目錄中自動建立SDK資料夾。
* Forms-14327 - Forms Service API ：擷取資料： — 當輸入中提供非互動式pdf時，會提供500個回應代碼。
* Forms-7475 — 排序功能無法用於最適化表單建立頁面。
* Forms-3309 — 如果在提交表單時選取了多個選項，則在產生的DoR中只會顯示一個選項。
* SITES-23646 — 如果欄位包含唯一，則使用OpenAPI建立的模型的GraphQL模型端點會失敗。
* SITES-23637 — 內容片段REST API： OpenAPI沒有使用正確的列舉值型別。
* SITES-23573 — 內容片段REST API：未依照uuid在GET內容片段上遵循即時關係。
* SITES-23535 — 內容片段REST API：內容片段模型列舉多個欄位有空白值。
* SITES-23534 — 內容片段REST API：內容片段驗證ClassCastException。
* SITES-23524 — 調整GraphQL BFF模型端點以支援多欄位列舉欄位。
* SITES-23467 — 內容片段REST API：搜尋模型因游標問題而失敗。
* SITES-23327 — 在時間表事件處理說明期間，AuditLogTimelineEventProvider中的ArrayIndexOutOfBoundsException。
* SITES-23277 — 內容片段REST API：應僅對即時副本執行內容片段欄位即時關係檢查。
* SITES-23232 — 自訂驗證在新的CF編輯器UI中無法運作。
* SITES-23090 — 內容片段REST API：無法更新鎖定的內容片段的標題。
* SITES-22981 — 提升非深層的巢狀啟動不會發佈。
* SITES-22870 - PathAttributesHandler.processSrcAttr ArrayIndexOutOfBoundsException。
* SITES-22814 — 內容片段REST API：核取方塊列舉片段欄位值應該按照模型中定義的索引鍵排序。
* SITES-22716 - OOTB元件即時使用清單問題。
* SITES-22457 — 提升非深層啟動不會更新來源內容。
* SITES-22449 — 在AEM P20升級後無法儲存內容片段中的變更。
* SITES-22279 — 內容片段REST API：內容片段缺少列舉型別的唯一屬性。
* SITES-22203 — 內容片段REST API：協調管理API以針對相同情形做出相同回應。
* SITES-21973 — 內容片段REST API：模型遺失列舉型別的唯一屬性。
* SITES-20364 - 302重新導向無法使用URL中的選取器。
* SITES-21198 - VersionPreviewServlet：清除會在所有叢集節點上同時執行，造成合併衝突與區塊認可。

### 已知問題 {#known-issues-17465}

* Assets-40875 - AssetDeleteHandler類別會監聽資產刪除事件，並根據刪除DELETE型別(PRE_event或POST_event)執行特定動作。DELETE 在某些情況下，事件的POST_DELETE型別會造成NullPointerException。
* Forms-14340 — 具現化FormsAndDocumentOmniSearchHandler和CloudStorageSubmitActionInserter時發生錯誤。 這些是無害的log陳述式。
* Forms-15818 — 元件描述項專案「OSGI-INF/com.adobe.aemfd.docmanager.impl」。在伺服器記錄檔中找不到*.xml&#39;陳述式。 這些是無害的log陳述式。
* 
   * SITES-23662 — 無法從伺服器記錄檔中的JCR記錄陳述式中擷取觸發發佈的使用者。 這是針對正在開發中的功能，可能會在記錄中造成間歇性和無害的「在批次OSGI事件中找不到有效的使用者ID」錯誤。

### 變更通知 {#change-notice-17465}

* 從 2024 年 9 月開始，AEM as a Cloud Service 將透過 Sling 模型匯出工具框架，停用 Resource Resolver 的序列化。如需詳細資訊，請參閱[文件](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)。

### 已過時的功能和 API {#deprecated-17465}

請注意，我們正在更新`com.day.cq.wcm.api`，而目前版本中，我們已將其一些方法和類別標示為`@Deprecated`。 這些功能將在未來版本中移除，因此，如果您使用任何這些功能，請考慮改用其建議的替代功能。

 [已過時和移除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文件中詳細介紹了 AEM as a Cloud Service 已過時和移除的功能和 API。

### 安全性修正 {#security-17465}

AEM as a Cloud Service致力於將平台的安全性和效能最佳化。 此維護發行版本解決了7個已識別的漏洞，強化我們對強大系統保護的承諾。

### 內嵌技術 {#embedded-tech-17465}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
