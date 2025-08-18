---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 280e02ba0ace1fe123fd5112a982c6434fd4d499
workflow-type: ht
source-wordcount: '1619'
ht-degree: 100%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 21772 {#21772}

以下是維護版本 21772 的持續改善內容，該版本於 2025 年 8 月 6 日公開發行。前一個維護版本是版本 21706。

啟用 2025.8.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行路徑圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新功能  {#new-features-21772}

* SITES-30049：加入新端點，以便使用其 UUID 來擷取內容片段的語言副本。

### 增強功能 {#enhancements-21772}

* CQ-4358722：已解決因為 Java 11 和 Java 17 之間地區設定代碼不同而造成的本地化問題。
* FORMS-19624：已啟用互動式通訊 (IC)。組織可以透過這項功能，將結構化範本與動態資料結合，並傳送個人化的隨選通訊 (例如報表明細、發票和來往信函)。IC 具有網頁型範本設計、可重複使用的內容片段、規則驅動的變化版本和資料無縫整合等功能，可實現跨頻道的一致且可擴充的客戶通訊內容。
* FORMS-19587、FORMS-17107、FORMS-19591、FORMS-19582、FORMS-20129、FORMS-20002、FORMS-19593、FORMS-20655、FORMS-19583、FORMS-18024、FORMS-19581：自適應表單規則編輯器增強以下功能：
   * 函數清單中的 `validate` 方法現在可以驗證面板、欄位和表單。
   * 改善用戶端自訂函數剖析功能，以支援 ES10+ 功能和靜態匯入。
   * 在規則編輯器中新增一個立即可用的 (OOTB)「下載記錄文件 (DoR)」按鈕。
   * 在規則中新增對動態變數的支援。
   * 啟用基於自訂事件建立規則的功能。
   * 現在可重複面板的規則可在正確的環境中執行，而不是僅在最後一個面板實例上執行。
   * 現在可以根據查詢參數、UTM 參數和瀏覽器參數觸發各個規則。
   * 在 EDS (體驗資料儲存區) 中新增對表單專用的自訂函數指令碼的支援。
   * 在規則編輯器的成功處理常式中，新增在「導航到」動作中使用 `EVENT_PAYLOAD` 的支援。
   * 在規則編輯器中支援在輸入參數中使用函數呼叫，並確保如果函數呼叫缺少任何必要的參數，便不會儲存規則。
   * 在規則編輯器 UI 中標示出有問題的規則。
* FORMS-18450：簡化在自適應表單中設定和使用 reCAPTCHA V2 (包括隱形 reCAPTCHA) 的流程。現在集中於一個地方管理設定，您可以更輕鬆地在表單中啟用垃圾郵件保護。
* FORMS-18385：新增在 AEM Forms 中透過 Output 服務使用 XDP 和資料來產生 AFP 的支援。
* FORMS-17789：在規則編輯器中新增一個立即可用的按鈕，可供下載記錄文件 (DoR)。
* FORMS-20313、FORMS-2896：新增對 `dorExclude` 屬性的支援，可以在核心元件型表單中停用特定功能。
* FORMS-20262：處理在用戶端的無效檔案附件 (0 位元組)。
* FORMS-18347：改善自適應表單編輯器記錄功能缺少表單容器代理元件的問題。
* FORMS-16205：在核心元件型表單中排除記錄文件 (DoR) 的停用元件。
* FORMS-10836：針對從右到左書寫的語言，變更記錄文件 (DoR) 主頁屬性的顯示方向。
* SITES-33025：透過 ID 而不是路徑開啟新的 CF 編輯器。
* SITES-32741：以非同步方式觸發內容片段頁面參考的更新。
* SITES-32087：GraphQL：在 StringArray 上新增對 `_ignoreCase` 的支援。
* SITES-12211：改善範本編輯器的效能
* SITES-32861：提高透過分塊處理建立 Live Copy 的效能。
* SITES-21383：刪除內容片段 Launch 的操作效能最佳化。
* SITES-31165：將轉出操作拆分為可管理的區塊來增強效能。
* SITES-21353：使用資料庫索引來改善內容片段 Launch 的查詢效能。
* SITES-30495：透過增強功能，支援在內容片段 Launch 中使用基於 UUID 的片段參考。
* SITES-32151：API 增強功能開放使用容器屬性功能。
* SITES-26849：在內容片段變化版本被移動或刪除時調整反向參考。
* SITES-31846：新增複製樹狀結構操作的選項，可將根片段和參考複製/貼上到同一個資料夾。
* SITES-30241：在移動、重新命名或刪除片段時，調整位於長文字欄位內的參考。
* SITES-32684：增強在 UI 結構描述中同步處理標籤變更的機制。
* SITES-33308：新增重試機制，以便在編輯模型時同步處理 UI 結構描述的變更。
* SITES-32247：「文字和個人化」元件中缺少對話框個人化設定以及 UI 無法正確對齊。
* SITES-32261：體驗片段國際化功能未套用至欄位。
* SITES-32666：範本述詞包含 `\n` 導致 HTML 查找失敗。
* SITES-32674：頁面建立精靈雖然已設定 `cq:showOnCreate`，但是特色影像欄位的影像選擇器無法正常運作。
* SITES-32014：搭配通用編輯器使用 Edge Delivery：針對 localhost、aem.page 和 aem.live 新增 CORS 原則自動設定
* SITES-26532：搭配通用編輯器使用 Edge Delivery：新增對本地化 URL 的支援 (搶先體驗)。
* SITES-30887：新增儲存在工作流程後設資料中的內容片段 UUID。

### 已修正的問題 {#fixed-issues-21772}

* CQ-4360190：已修正在嘗試對不支援該操作的 keySet 使用 add 時發生 `UnsupportedOperationException` 的問題。
* CQ-4360421：解決 Microsoft Translator 訂閱金鑰加密的問題，以提高安全性和相容性。
* FORMS-20980：修正自適應表單中具有自訂顯示格式的日期選擇器的鍵盤協助工具問題。
* FORMS-20498：在 OdataResponse 中新增對 Null 指標異常狀況的檢查，以防止執行階段錯誤。
* FORMS-20947：解決多個無障礙相關問題，包括螢幕閱讀器違規和文字截斷/重疊問題。
* FORMS-21030、FORMS-20630：解決自適應表單中下拉式欄位設定為多重選項的問題。所產生的 PDF 現在正確地包含所有選取的值。
* FORMS-19579：修正叫用服務規則在重新儲存時未自動修正的問題。
* FORMS-20734：已修正由 Output 服務為 XFAF 型輸入 PDF 範本所產生的 PDF 文件中，簽名欄位重複的問題。
* FORMS-20934：修正 AEM Forms 製作 UI 中自動填入屬性的下拉式選單，以移除重複的項目並包含所有標準 HTML 自動完成權杖。
* FORMS-20700：解決 AEM Forms 中初次載入時下拉式說明文字閃爍跳動的問題。
* FORMS-20307：修正網站頁面上嵌入的表單對於 4 個字元的地區設定均未進行翻譯的問題。
* FORMS-20493：解決提取資料時表單自動重新整理而造成使用者不便的問題。
* FORMS-18455：增強核心元件的自適應表單編輯器功能，針對資料來源樹中使用的資料物件顯示圓點。
* FORMS-19373：防止未設定任何複寫代理程式的發佈環境發生複寫錯誤。
* FORMS-20042：修正啟用 HTML 設定的 Apache Sling GET Servlet 設定導致屬性視圖無法顯示的問題。
* FORMS-20036、FORMS-19978：解決 PDF/A-1b 的合規性和驗證問題。
* FORMS-19166：將 pagedatasource.jsp 移至 servlet 以提高錯誤堆疊追蹤的清晰度，並新增更多護欄和記錄。
* FORMS-16466：修正 AEM Forms 中可重複面板並未正確填入的問題。
* FORMS-19629：解決客戶 JSON 結構描述剖析提供無效結果的問題。
* LC-3923083：解決 XDP 範本中有邊框項目的「路徑物件未標記」錯誤。
* SITES-33177：搭配通用編輯器使用 Edge Delivery：修正儲存為逗號分隔字串時區段樣式錯誤的問題。
* SITES-33262：搭配通用編輯器使用 Edge Delivery：修正未設定名稱屬性的區塊會中斷頁面轉譯與發佈的問題。
* SITES-33309：搭配通用編輯器使用 Edge Delivery：修正寫入到試算表時在欄中加入斜線而造成的 `IllegalArgumentException` 問題
* SITES-33408：搭配通用編輯器使用 Edge Delivery：修正試算表在進行變更後並未顯示為已修改的問題。
* SITES-31992：GraphQL：修正套件啟動期間模型掃描中偶爾出現的錯誤。
* SITES-29967：GraphiQL：長查詢名稱被截斷。
* SITES-26266：不是以 `/` 開頭的內容參考，後端回應便不會回傳 (Java API)。
* SITES-17874：GraphQL 持續性查詢：修正內容類型 application/graphql-response+json 的編碼。
* SITES-24506：螢幕閱讀器告知搜尋結果。
* SITES-25268：改善螢幕閱讀器的註解功能。
* SITES-32366：拼字檢查結果隱藏在 RTE 對話框後面。
* SITES-32829：改進 MediaQuery 模擬器功能，可以剖析 Media Query Level 3 和 4。
* SITES-32278：已修正標記欄位，可以正確使用欄位標籤。
* SITES-25244：影像的模態視窗中不再出現水平橫列。
* SITES-33395：修正內容片段 Live Copy 同步的轉出按鈕功能。
* SITES-33147：修正影響即時關係功能的服務繫結問題。
* SITES-33528：修正啟動促銷期間保存時間戳記的問題。
* SITES-33014：修正 LaunchesAdapterFactory 產生過多警告記錄的問題。
* SITES-32305：在版本變更後修正 Live Copy 的繼承中斷功能。
* SITES-32268：停用內容片段搜尋的 URL 編碼。
* SITES-32772：啟用 SITES-31455 的增強功能時，變化版本欄位中鎖定的屬性始終為 false - 與統一 etag 值有關。
* SITES-32696：修正繼承中斷的內容片段 Live Copy 欄位無法再進行編輯的問題。
* SITES-31712：針對生產環境作者進行全方位搜尋的查詢速度緩慢。
* SITES-33039：未正確觸發頁面事件。
* SITES-31192：體驗片段在移動後遺失版本歷史記錄。
* SITES-33529：將 ACS 行銷活動範本與 AEM 頁面連結時發生錯誤。
* SITES-33678：為 SITES-33529 新增切換功能。
* SITES-33468：AEMaaCS 無法連接到 ACS。

### 功能變動 {#altered-functionality-21772}

* SITES-26344：統一端點之間 `fragmentId`/`modelId` 的驗證 - 這些 ID 現在已完成驗證，若是無效則傳回 400 狀態代碼。
* SITES-29598：更新內容片段模型時，片段參考欄位中新增驗證內容片段的參考。

### 已知問題 {#known-issues-21772}

* SITES-31791：內容片段 GraphQL - 查詢失敗並顯示「超過最大欄位計數」。請參閱[知識庫文章](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-27231)。

### 已過時的功能和 API {#deprecated-21772}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21772}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決 35 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-21772}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
