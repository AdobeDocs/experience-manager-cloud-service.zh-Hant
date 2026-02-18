---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a58225edb8ca49db9743db6c9c5b08c786fa0144
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 25%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 24464 版 {#release-24464}

以下摘要說明維護版本24464數的持續改善，該版本於2026年2月17日公開發佈。 前一個維護版本是版本 24288。

2026.2.0 功能啟用會提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-24464}

* AEMARCH-264：新增支援以根據RequestEntity驗證條件式要求。
* AEMARCH-269：公開OpenAPI實作的JavaEE驗證API。
* AEMARCH-276：透過RequestEntity提供i18n支援。
* Assets-10995：設定下載zip中的資產數量限制。
* Assets-50788：更新搜尋API以使用資產中繼資料GET API。
* Assets-50946：使用中繼資料GET API將請求內文對應至JCR中繼資料。
* Assets-55866：在先前的處理完成前，請避擴音交相同資產的新請求。
* Assets-60300：提供API以擷取非同步工作內容和結果。
* Assets-60574：新增對最新版Sling API套裝的支援。
* Assets-61049：繼續中繼資料管理員套件組合開發。
* Assets-61692：依預設，在「搜尋開放API」中執行語意搜尋。
* Assets-61696：資產檢視上的BAM路由和MFE包裝函式。
* Assets-61854：在啟用/停用訊息中傳送GenStudio解決方案。
* Assets-61973：在AEM中建立API以管理提示。
* Assets-62182：c2pa-manifest轉譯的Asset Compute事件處理常式。
* Assets-62311：搜尋回歸問題。
* Assets-62413：在JSON的每個圖層中新增對customModifier欄位的支援。
* Assets-62432：合併資料夾刪除API PR。
* Assets-62540：增加quickstart中ui-touch-optimized版本。
* Assets-62622：在MatchQuery中處理搜尋模式。
* Assets-62671：修正MatchQuery startsWith運運算元。
* Assets-62780：為資料夾API新增切換功能。
* Assets-62988：隱藏c2pa資訊清單轉譯，使其不顯示在「轉譯」索引標籤中。
* Assets-63336：應該只會針對DAM名稱空間中繼資料執行從AEM同步至DM的範本。
* Assets-63375：將資產上傳實驗OpenAPI置於功能切換後面。
* Assets-63453：確保所有使用者都可讀取omnisearch設定。
* GRANITE-63744：允許將非同步作業連線至Sling作業。
* granite-64567：自動停用SKU搜尋的語意搜尋。
* GUIDES-41187：為Guides使用新增標題。
* SITES-30452：包含ASO的內容API — 標題和說明建議。
* SITES-33116：修正路徑驗證。
* SITES-34234：頁面編輯器：保留內容樹狀結構狀態。

### 已修正的問題 {#fixed-issues-24464}

* Assets-43198：資產到期通知電子郵件不遵循使用者語言偏好設定。
* Assets-51840：資產處理改善。
* Assets-52061：選取已儲存的搜尋後無法導覽回來。
* Assets-53155：改善資產內容。
* Assets-53745：Dynamic Media下載流程需要在選擇網頁預設集之前取消選取原始資產。
* Assets-54260：資產內容修正。
* Assets-54787：改善資產內容。
* Assets-57391：資產內容更新。
* Assets-59213： cq-dynamicmedia-core取決於已棄用的commons-lang資料庫。
* Assets-59214： cq-scene7-imaging取決於已棄用的commons-lang資料庫。
* Assets-59546： cq-remotedam-client-core取決於已棄用的commons-lang資料庫。
* Assets-59703： cq-dam-core取決於已棄用的commons-lang資料庫。
* Assets-59705： cq-dam-handler取決於已棄用的commons-lang資料庫。
* Assets-59707： cq-dam-indesign依賴已棄用的commons-lang資料庫。
* Assets-59709： cq-scene7-core取決於已棄用的commons-lang資料庫。
* Assets-59929：欄位含有新行字元時，中繼資料匯出的CSV會中斷。
* Assets-60241：重新命名資料夾時，非同步移動作業失敗。
* Assets-61134：從pom檔案中移除comparisonVersion標籤。
* Assets-61309：內容片段移動/複製不再更新內部參考。
* Assets-61730：重新導向至「直接二進位存取」時應遵守資產編碼。
* Assets-62358： Assets報表CSV會在內容路徑中顯示損毀的值。
* Assets-62610： Adobe Stock授權按鈕在Assets UI中停用。
* Assets-62613： `downloadasset`/`saveas`中的NPE。
* Assets-62656：非Assets搜尋時無法正確顯示OmnisearchAI 搜尋指標。
* GRANITE-55387：更正引號中的字會刪除整個字。
* GRANITE-61240：透過儲存在lazycontainer.js中的XSS執行RCE。
* GRANITE-64101：重新啟動時，轉換為ES的OOTB索引會恢復為Lucene。
* SITES-24530：搜尋模式中關閉/移除按鈕的觸控目標不夠大。
* SITES-31425：啟動工作流程中未本地化的錯誤訊息。

### 已知問題 {#known-issues-24464}

無。

### 已過時的功能和 API {#deprecated-24464}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-24464}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決 14 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-24464}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

