---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 0f16c31a5fea1fc538fbeabe6db182ad3a30560d
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 12%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 21772 {#21772}

以下摘要說明維護版本21772的持續改善，該版本於2025年8月6日公開發佈。 前一個維護版本為版本 21706。

啟用 2025.8.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新功能  {#new-features-21772}

* SITES-30049：新增端點，以依據其UUID擷取內容片段的語言副本。

### 增強功能 {#enhancements-21772}

* CQ-4358722 ：解決Java 11和Java 17之間地區設定代碼不同所導致的本地化問題。
* Forms-19624：啟用互動式通訊(IC)。 它可讓組織結合結構化範本與動態資料，以提供個人化的隨選通訊，例如報表、發票和信件。 IC具備網路型範本設計、可重複使用的內容片段、規則驅動的變化以及順暢的資料整合等功能，可跨管道實現一致且可擴充的客戶通訊。
* Forms-19587、FORMS-17107、FORMS-19591、FORMS-19582、FORMS-20129、FORMS-20002、FORMS-19593、FORMS-20655、FORMS-19583、FORMS-18024、FORMS-19581：已對最適化Forms規則編輯器進行下列增強功能：
   * 函式清單中的`validate`方法現在可以驗證面板、欄位和表單。
   * 改善使用者端自訂函式剖析，以支援ES10+功能和靜態匯入。
   * 在規則編輯器中新增現成可用的(OOTB) 「下載記錄檔案(DoR)」按鈕。
   * 新增對規則中動態變數的支援。
   * 啟用根據自訂事件建立規則的功能。
   * 可重複面板的規則現在會在正確上下文中執行，而非僅在最後一個面板例項上執行。
   * 現在可以根據查詢引數、UTM引數和瀏覽器引數觸發規則。
   * 新增對EDS (Experience Data Store)中表單特定自訂函式指令碼的支援。
   * 新增在規則編輯器的成功處理常式中，在「瀏覽至」動作中使用`EVENT_PAYLOAD`的支援。
   * 在規則編輯器的輸入引數中支援的函式呼叫，而且如果函式呼叫中遺漏任何必要的引數，確保不會儲存規則。
   * 在規則編輯器UI中醒目提示失效的規則。
* Forms-18450： reCAPTCHA V2 （包括隱藏的reCAPTCHA）現在更容易在調適型Forms中設定和使用。 設定現在可在單一位置管理，讓您更輕鬆地在表單中啟用垃圾郵件保護。
* Forms-18385：新增支援透過Output服務從XDP產生AFP，以及在AEM Forms中產生資料。
* Forms-17789：在規則編輯器中新增立即可用按鈕以下載記錄檔案(DoR)。
* Forms-20313、FORMS-2896：新增對`dorExclude`屬性的支援，以停用核心元件型表單中的特定功能。
* Forms-20262：在使用者端處理無效的檔案附件（0位元組）。
* Forms-18347：改善遺失表單容器Proxy元件的最適化Forms編輯器記錄。
* Forms-16205：從核心元件型表單的記錄檔案(DoR)中排除停用的元件。
* Forms-10836：將記錄檔案(DoR)中主版頁面屬性的方向從右至左語言變更。
* SITES-33025：透過ID而非路徑開啟新的CF編輯器。
* SITES-32741：非同步觸發內容片段頁面參考的更新。
* SITES-32087： GraphQL：在StringArray上新增對`_ignoreCase`的支援。
* SITES-12211：改善範本編輯器中的效能
* SITES-32861：透過區塊處理來改善即時副本建立的效能。
* SITES-21383：內容片段啟動刪除操作的效能最佳化。
* SITES-31165：將轉出作業分割為易於管理的區塊，以提升效能。
* SITES-21353：使用資料庫索引改善內容片段啟動項的查詢效能。
* SITES-30495：增強功能支援內容片段啟動中以UUID為基礎的片段參考。
* SITES-32151： API增強功能公開容器屬性功能。
* SITES-26849：移動或刪除內容片段變數時調整反向參照。
* SITES-31846：新增選項，以便在相同的資料夾中複製/貼上根片段和參照，以進行複製樹狀結構操作。
* SITES-30241：移動、重新命名或刪除片段時，調整位於長文字欄位中的參照。
* SITES-32684：增強同步UI結構描述中索引標籤變更的機制。
* SITES-33308：新增在編輯模型時重試機制，以將變更同步到UI結構描述。
* SITES-32247：「文字和Personalization」元件中缺少對話方塊Personalization和UI不對齊。
* SITES-32261：體驗片段i18n未套用至欄位。
* SITES-32666：範本述詞包含`\n`而導致HTML查詢失敗。
* SITES-32674：精選影像欄位影像選擇器不適用於「頁面建立精靈」，儘管`cq:showOnCreate`。
* SITES-32014：使用通用編輯器的Edge Delivery：為localhost、aem.page和aem.live新增自動設定CORS原則
* SITES-26532：使用通用編輯器的Edge Delivery：新增對本地化URL的支援（搶先存取）。
* SITES-30887：新增儲存在工作流程中繼資料中的內容片段uuid。

### 已修正的問題 {#fixed-issues-21772}

* CQ-4360190：修正嘗試在不支援作業的keySet上使用add時發生的`UnsupportedOperationException`。
* CQ-4360421：解決Microsoft Translator訂閱金鑰加密的問題，以改善安全性和相容性。
* Forms-20980：修正最適化Forms中自訂顯示格式之日期選擇器的鍵盤協助工具問題。
* Forms-20498：在OdataResponse中新增檢查Null指標例外狀況，以防止執行階段錯誤。
* Forms-20947：解決多項協助工具問題，包括熒幕助讀程式違規和文字截斷/重疊問題。
* Forms-21030、FORMS-20630：解決在調適型表單中，針對多個選取專案設定的下拉式欄位問題。 產生的PDF現在正確包含所有選取的值。
* Forms-19579：修正重新儲存時「叫用」服務規則無法自動修正的問題。
* Forms-20734：修正輸出服務針對XFAF型輸入PDF範本所產生PDF檔案中的簽名欄位重複。
* Forms-20934：修正AEM Forms編寫UI中的「自動填寫屬性」下拉式清單，移除重複專案並納入所有標準HTML自動完成Token。
* Forms-20700：解決AEM Forms中初次載入時，下拉式說明文字忽隱忽現的問題。
* Forms-20307：修正內嵌在網站頁面上的表單未透過4字元地區設定翻譯的問題。
* Forms-20493：解決擷取資料時自動重新整理表單，造成使用者不便的問題。
* Forms-18455：增強核心元件的最適化Forms編輯器，以顯示資料來源樹狀結構中已使用資料物件的點。
* Forms-19373：防止未設定任何復寫代理的發佈環境發生復寫錯誤。
* Forms-20042：修正啟用HTML設定的Apache Sling GET Servlet設定所導致的屬性檢視中斷。
* Forms-20036、FORMS-19978：解決PDF/A-1b的法規遵循和驗證問題。
* Forms-19166：將pagedatasource.jsp移動到servlet以提高錯誤棧疊追蹤的清晰度，並新增更多護欄和記錄。
* Forms-16466：修正AEM Forms中無法正確填入可重複面板的問題。
* Forms-19629：解決客戶JSON結構描述剖析的問題，提供無效結果。
* LC-3923083：解決XDP範本中邊界專案的「路徑物件未標籤」錯誤。
* SITES-33177：使用通用編輯器的Edge Delivery：當儲存為逗號分隔字串時，請修正損壞的區段樣式。
* SITES-33262：使用通用編輯器的Edge Delivery：修正沒有名稱的區塊屬性會中斷頁面的轉譯和發佈。
* SITES-33309：使用通用編輯器的Edge Delivery：在寫入試算表時修正`IllegalArgumentException`。
* SITES-33408：使用通用編輯器的Edge Delivery：修正試算表在變更後未顯示為已修改。
* SITES-31992： GraphQL：修正套件組合啟動期間模型掃描偶爾發生的錯誤。
* SITES-29967： GraphiQL：長查詢名稱被切斷。
* SITES-26266：不以`/`開頭的內容參考不會從BE回應(Java API)傳回。
* SITES-17874： GraphQL持續查詢：修正內容型別應用程式/graphql-response+json的編碼。
* SITES-24506：通知搜尋結果的熒幕閱讀器。
* SITES-25268：改善註解的熒幕助讀程式。
* SITES-32366：隱藏在RTE對話方塊後的拼字檢查結果。
* SITES-32829：改進MediaQuery模擬器以剖析媒體查詢層級3和層級4。
* SITES-32278：已修正標籤欄位，以正確使用欄位標籤。
* SITES-25244：水準列不再出現在影像強制回應視窗中。
* SITES-33395：修正內容片段Live Copy同步化的轉出按鈕功能。
* SITES-33147：修正影響即時關係功能的服務繫結問題。
* SITES-33528：修正啟動促銷活動期間的時間戳記保留問題。
* SITES-33014：修正從LaunchesAdapterFactory產生過多警告記錄的問題。
* SITES-32305：修正版面變更後的即時副本繼承中斷功能。
* SITES-32268：停用內容片段搜尋的URL編碼。
* SITES-32772：啟用SITES-31455的增強功能時，變數欄位中鎖定的屬性一律為false — 這和統一etag值有關。
* SITES-32696：修正具有中斷繼承的內容片段即時副本欄位無法再編輯的問題。
* SITES-31712：來自Prod Author上的Omni-search的緩慢查詢。
* SITES-33039：頁面事件未正確觸發。
* SITES-31192：體驗片段在移動後遺失版本歷史記錄。
* SITES-33529：將ACS行銷活動範本與AEM頁面連結時發生錯誤。
* SITES-33678：為SITES-33529新增切換按鈕。
* SITES-33468： AEMaaCS無法連線到ACS。

### 功能變更 {#altered-functionality-21772}

* SITES-26344：在端點之間統一驗證`fragmentId`/`modelId` — 這些ID現在已驗證，若無效，將傳回400狀態代碼。
* SITES-29598：更新內容片段模型時，驗證新增到片段參考欄位中的內容片段參考。

### 已知問題 {#known-issues-21772}

* SITES-31791：內容片段GraphQL — 查詢失敗，顯示「超出最大欄位計數」。 請參閱[知識庫文章](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27231)。

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
| Node.js | 14 （預設） | [支援的Node.js版本](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

