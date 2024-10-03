---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fa2da21ef6424bce0830d503eba650e1c1bf3dc2
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 98%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17964 {#release-17964}

以下是 17964 維護版本的持續改善內容，該版本於 2024 年 9 月 25 日公開發佈。先前的維護發行版本為發行說17689。 由於發生問題，發行說17882已設為私人。

2024.10.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17964}

* ASSETS - 37750：[優先順序 4][GraphQL] 支援 DM scene7 URL：影像智慧裁切。
* CQ - 4354583：[AEMaaCS] 透過 Adobe Pipeline 傳送翻譯流程事件。
* CQ - 4357642：更新 OOTB 連接器中的 MSFT 認證。
* CQ - 4358217：從請求實體還原序列化請求內文。
* CQ - 4358342：僅使用一種 HTTP 方法註冊 RequestProcessors。
* FORMS - 10781：增強規則編輯器，為面板中的下一個/上一個項目建立規則。
* FORMS - 14595：[無瀏覽器功能] 在使用預填資料計算無瀏覽器轉譯的記錄文件時，記錄文件中缺少值。
* FORMS - 15619：AEM Forms 已更新翻譯套件。
* 表格 - 16113：[Adobe Sign] 無法由不同的使用者更新合約狀態。
* FORMS - 16155：[規則編輯器] 實施非同步功能。
* GRANITE - 53872：為 IMS 用戶端 ID 新增新的環境變數。
* SITES - 23738：核心元件 2.27.0 版。
* SITES - 16610：內容片段：取得 Launch 詳細資訊端點。
* SITES - 16614：內容片段：重新設定 Launch 端點基底。
* SITES - 16615：內容片段：提升 Launch 端點。
* SITES - 24215：內容片段：實施取得 Launch 來源端點。
* SITES - 20336：內容片段：改善刪除內容片段模型時的驗證。
* SITES - 21090：內容片段：新增對數字欄位的分數最小/最大值的支援
* SITES - 21658：內容片段：升級以使用 UUID 參考。
* SITES - 23054：內容片段 - 複製內容片段模型。
* SITES - 23264：內容片段：建立模型的靜態結構。
* SITES - 23265：內容片段：透過 UI 結構 GET 端點公開模型的靜態結構。
* SITES - 23266：內容片段：為內容片段模型新增限制的能力。
* SITES - 23778：內容片段：搜尋內容片段模型應允許搜尋從未發佈的模型。
* SITES - 23335：內容片段：新增對外部資產參考的支援。
* 網站 - 24626：內容片段：RTC：UUID 移轉的權限：2。
* SITES - 24786：內容片段：`referencesTree` 端點的增強功能。
* SITES - 24833：內容片段：移除依照許可的 HTML 標記清單進行 HTML 輸入驗證。
* 網站 - 23380：GraphQL：使用適當的 API 讀取資產中繼資料。
* SITES - 22864：[Edge Delivery] 通用編輯器在 2024 年下半年有新的 AEM 內容結構整合。
* SITES - 23584：Java 17 的 Foundation 元件測試失敗。
* SITES - 23662：事件：無法從伺服器記錄的 JCR 記錄陳述式擷取觸發發佈請求的使用者。
* SITES - 23301：新增支援，在建立內容片段翻譯時可啟動新工作流程以建立檔案夾結構。
* SITES - 23336：內容片段：新增對外部資產參考的支援
* SITES - 24091：MSM 內容套件分割：master。
* SITES - 24114：isSourceRenderCondition：將錯誤日誌訊息縮減為 DEBUG。
* SITES - 24166：觸控 UI 編輯器的遠端資產緩解。
* SITES - 24409：僅在一種 HTTP 方法上註冊所有請求處理器。
* SITES - 25008：改善對 PersistenceExceptions 和權限問題的處理。
* SITES - 24821：[Xwalk] 將 aem.page / aem.live 設定為預設值。

### 已修正的問題 {#fixed-issues-17964}

* CQ - 4356887：Akamai Technologies Inc. 翻譯專案狀態不一致
* CQ - 4357878：翻譯框架不會在供應商翻譯失敗時設定錯誤狀態。
* CQ - 4358028：如果上傳影片縮圖，則無法建立專案。
* CQ - 4358290：在已發佈的頁面上 Target 設定無法運作。
* FORMS - 13173：最適化表單 > 規則編輯器 > 放置物件欄位中的下拉清單未能對齊。
* FORMS - 13873：AFv2：元件名稱中有 (“-”) 會導致規則失敗。
* FORMS - 14340：FormsAndDocumentOmniSearchHandler 和 CloudStorageSubmitActionInserter 具現化時發生錯誤。
* FORMS - 15363：規則編輯器中顯示的名稱。
* FORMS - 15381：授權範圍訊息的 UI 增強功能。
* FORMS - 15595：AEM Form TnC 元件同意文字換行問題。
* FORMS - 15623：AEMaaCS 表單 - 使用一個 POST 更新 Dynamics 中多個表格的替代方法。
* FORMS - 15682：AEM Forms - 無法將 DOR 綁定到 Dynamics FDM。
* FORMS - 15799：Adobe Sign GovCloud 簽章頁面不會在 iframe 中轉譯。
* FORMS - 15835：提交後表單 URL 重寫問題。
* FORMS - 16091：使用重組的 Binary.java。
* FORMS - 16096：Forms 使用者無權存取 restendpoint 對話框。
* FORMS - 16139：以核心元件形式新增記錄文件的必要記錄。
* FORMS - 6935：使用中元件的狀態缺乏 3 比 1 的對比率。
* FORMS - 7018：空白元素取得焦點。
* GRANITE - 53028：ExternalProcessPollingHandler 中的 NPE。
* GRANITE - 53907：無法將服務使用者識別為工作流程超級使用者。
* SITES - 24405：內容片段：列舉的擴充資訊應該更具彈性
* 網站 - 23024：內容片段：列舉不會在 GET 片段中傳回 locked: true。
* SITES - 23269：內容片段：建立內容片段允許設定鎖定欄位。
* SITES - 23337：內容片段：擁有 `body` 的批次端點執行失敗並顯示轉換例外情況。
* SITES - 23474：內容片段：分頁應該排除搜尋內容片段中損壞的資源。
* SITES - 23615：內容片段：內容片段副本 AuthoringInfo 未更新
* SITES - 23668：內容片段：擁有多欄位的修補程式 Live Copy 失敗，顯示 400
* SITES - 23695：內容片段：UiSchema 中無法使用索引標籤描述
* SITES - 23704：內容片段：_extendedInfo 不支援多值列舉
* SITES - 23781：內容片段：列舉欄位中不允許出現重複值
* SITES - 24150：內容片段：內容片段版本有關建立的撰寫資料遺失
* SITES - 24230：內容片段：修復在搜尋內容片段模型中出現 `modified` 複寫狀態之後的篩選
* 網站 - 24233：內容片段：按 `publishedBy` 篩選可以在搜尋內容片段模型中包含未發佈的資源
* SITES - 24355：內容片段：建立內容片段的資料夾未遵循即時關係
* SITES - 24816：內容片段：ValidationStatus 訊息順序不一致。
* SITES - 23896：事件：更多事件與頁面移動事件一起出現
* SITES - 23899：事件：頁面事件延遲或完全不生成
* SITES - 23961：事件：設定資料夾存在時，無法使用參考來建立內容片段模型
* SITES - 23963：事件：頁面刪除事件有時不會出現
* SITES - 23443：GraphQL：GraphQL 游標查詢行為不一致。
* SITES - 10994：鍵盤焦點順序不合邏輯。
* SITES - 16357：AEM：Sites 選單的「設定分析」索引標籤中的按鈕被截斷。
* SITES - 19836：容器中的 Ghost 元件顯示在發佈和預覽實例上。
* Sites - 22348：如果專案的 Live Copy 數量超過 100 個，則無法載入 Live Copy 概觀頁面。
* SITES - 22960：ContentFragmentModelOmniSearchHandler 中未關閉的資源解析器。
* SITES - 23284：URL 編碼造成空白路徑瀏覽器對話框。
* SITES - 23505：當頁面移動到另一個位置時，元件顯示不正確的 URL。
* SITES - 23574：無法預覽/比較許多頁面的目前版本
* SITES - 23585：為具有 cq:responsive 節點的元件還原繼承時發生問題
* SITES - 23650：AEM 撰寫環境中傳入連結計數出現差異
* SITES - 23659：切換 FT_* SITES - 9757 造成內容語言 Servlet 迴歸
* SITES - 23759：在體驗片段新增的資產不會隨 Launch 一起發佈
* SITES - 24025：AEM 返回位置標頭的 302 重新導向使用內部 DNS 而非公共 DNS
* SITES - 24036：需要對 ASCII 格式的 AEM RTE 持續性字元進行調查
* SITES - 24317：代理程式設定不適用於基本驗證
* SITES - 24918：[Xwalk] 修正在使用專用出口 IP 時偶爾傳回的 504 錯誤。

### 已知問題 {#known-issues-17964}

* FORMS - 15818：元件描述項條目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在伺服器記錄中找不到陳述式。這些是無害的記錄陳述式。

### 已過時的功能和 API {#deprecated-17964}

請注意，我們正在更新 `com.day.cq.wcm.api`，並且在目前版本中，我們已將其中某些方法和類別標記為 `@Deprecated`。這些將於未來的版本中刪除，因此若您正在使用其中的任何一個，請考慮改用所建議的替代方案。

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-17964}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 16 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 內嵌技術 {#embedded-tech-17964}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
