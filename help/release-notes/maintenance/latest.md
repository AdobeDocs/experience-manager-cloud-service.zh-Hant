---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 26c42152bdebc069dd60cc4f5f070276eb1a1f46
workflow-type: tm+mt
source-wordcount: '1780'
ht-degree: 99%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 21331 版 {#21331}

以下摘要說明 21331 維護版本的持續改善內容，該版本於 2025 年 6 月 24 日公開發佈。前一個維護版本為 21193 版。

啟用 2025.7.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-21331}

* CQ-4356522：`WorkflowResourceStatusProvider`最佳化。
* FORMS-16458：用於選擇字體屬性 (字體) 的 UI。
* FORMS-17707：AEP 連接器不適用於 AEP 平台階段。
* FORMS-19125：支援 AF 編輯器的自動片段對應。
* FORMS-19336：在 AF 編輯器的資料來源樹新增搜尋。
* FORMS-19417：支援階層檢視中的選項按鈕。
* FORMS-19603：在規則編輯器中同時支援主版頁面和設計頁面。
* SITES-5358：內容片段 Rest API：複製具有子系的內容片段。
* SITES-10575：「MSM Blueprint Bloomfilter 載入程式」嘗試載入超過 100,000 行。
* SITES-14542：重新命名或移動 Live Copy 的來源頁面時，若先前已發佈該頁面，則應觸發發佈已重新命名或移動的 Live Copy 頁面。
* SITES-19754：使用通用編輯器的 Edge Delivery：在整合出現問題時，新增人類可讀的錯誤訊息。
* SITES-23499：Edge Delivery 搭配通用編輯器：新增區塊選項可以使用多個欄位的支援。
* SITES-23518：Edge Delivery 搭配通用編輯器：新增 Edge Delivery 特定資產轉譯的支援。
* SITES-24436：內容片段 Rest API：導入本機快取以加速重複參考資料的擷取速度。
* SITES-25155：內容片段 Rest API：移除模型清單中已棄用的「enabledForFolder」查詢參數。
* SITES-25913：內容片段 Rest API：在開始發佈工作流程之前需於限定時間內完成資源的驗證。
* SITES-25976：MSM 推出後，Experience 片段內的連結無法調整。
* SITES-26271：內容片段 Rest API：切換到 GET 變化端點的 BFS 周遊。
* SITES-27486：通用編輯器 - AEM 整合。
* SITES-27775：在發佈期間的最佳化參考資料搜尋 (後設資料延遲載入)。
* SITES-27782：搭配通用編輯器的 Edge Delivery：新增特定的發佈者 - 訂閱者實施以將內容發佈到 Edge Delivery (搶先體驗)。
* SITES-27792：Edge Delivery 搭配通用編輯器：新增專用 Edge Delivery Service 設定範本。
* SITES-28557：內容片段 Rest API：允許透過呼叫具有 `references=direct` 的 `/cf/fragments/{fragmentId}` 使用已擷取的 ETag 來修補內容片段。
* SITES-28683：允許 MSM LiveRelationship 搜尋略過進階狀態。
* SITES-29601：內容片段 Rest API：驗證長文字欄位的內容片段參考資料。
* SITES-29614：內容片段 Rest API：使用 `/cf/workflows/{workflowInstanceId}` 端點 (workflowInstanceIda 是發佈請求傳回的 ID) 來擷取工作流程。
* SITES-29615：內容片段 Rest API：列出透過 POST `/cf/batch` 使用 `GET /cf/batch` 建立的所有批次請求。
* SITES-29874：內容片段 Rest API：內容片段長文字欄位的參考資料現已擷取並序列化。
* SITES-29930：內容片段 Rest API：為內容片段發佈工作流程新增量度。
* SITES-29986：內容片段 Rest API：支援 CF 模型技術命名。
* SITES-30088：內容片段 Rest API：CF 發佈 - 在 filterReferencesByStatus 為空時略過參考資料擷取。
* SITES-30126：內容片段 Rest API：CF 發佈效能改善：以最精簡的檢查取代檢查資源是否為片段。
* SITES-30328：Edge Delivery 搭配通用編輯器：新增從 Sidekick 預覽的支援。
* SITES-30445：內容片段 Rest API：CF 模型 UI 綱要：新增一個選項來控制可摺疊的初始狀態。
* SITES-30604：內容片段 Rest API：支援在新 UI 中採用模型後設資料結構。
* SITES-30885：最佳化持續性查詢的 JSON 處理。
* SITES-30886：內容片段 Rest API：根據儲存在工作流程後設資料中的片段 uuid 取得內容片段端點的工作流程。
* SITES-31005：增強「推出作業」UI，以顯示進度。
* SITES-31020：增強「建立 Live Copy 作業」UI，以顯示進度。
* SITES-31111：內容片段 Rest API：允許變體修補程式 API 接受內容片段啟動中的內容片段參考。
* SITES-31343：內容片段 Rest API：新增依日期篩選和分頁功能至列出批次請求的端點。
* SITES-31472：如果是大規模啟動，則刪除啟動可能會造成存放庫暫停。
* SITES-31641：內容片段 Rest API：新增屬性至模型欄位，以儲存擴充功能相關的動態地圖。
* SITES-31677：自訂工作區支援 AEM 內容片段匯出至 Target。
* SITES-31770：內容片段 Rest API：PATCH 效能改善。
* SITES-31782：內容片段 Rest API：新增本機資產的說明。
* SITES-32175：允許對 Live Copy 建立和 MSM 頁面推出進行中介認可。

### 已修正的問題 {#fixed-issues-21331}

* CQ-4359756：翻譯規則現在納入了元件層級的篩選器屬性。
* CQ-4359826：解決內容片段參考資料面板的不一致狀態。
* CQ-4359866：LanguageUtils 類別現在支援單元測試，無需新增額外的相依性。
* FORMS-13990：Forms 服務 API：產生文件：如果資料欄位在選取後保留空白，則給予 200，而預期為 400。
* FORMS-14309：Forms 服務 API：擷取資料回應代碼修正。
* FORMS-18526：在複製包含多個條件欄位的規則時，固定的欄位不會變更。
* FORMS-18977：DOR 服務未傳遞文件標題。
* FORMS-19047：在 SP22 的 AEM Forms 上發布自適應表單之後缺少翻譯。
* FORMS-19234：無法在 AEM Forms 中使用 PDF 的時間軸功能。
* FORMS-19628：在自動產生的 DOR 中，若排除巢狀面板標題，也會一併隱藏根面板標題。
* FORMS-19651：修正在二進位條件中使用點選的按鈕並在 then 陳述式中使用同一個按鈕時的規則。
* FORMS-19808：FormsPortal - 啟用延遲載入時無法提取草稿。
* FORMS-19887：存取權屬性在 HTML5 預覽中無法運作。
* SITES-15452：啟動時不應根據其副本檢查唯一的 CF 元素。
* SITES-24492：ARIA 索引標籤清單沒有可存取的名稱。
* SITES-24623：內容片段 Rest API：修正相同 CF 端點之間的 ETag 不相符問題。
* SITES-24668：當縮放比例增加到 400% 時，參考資料邊欄功能會失效。
* SITES-24678：螢幕閱讀器未讀出參考資料邊欄狀態訊息。
* SITES-24697：螢幕閱讀器未宣佈影像模型的載入狀態。
* SITES-24708：當縮放比例增加到 400% 時，篩選器邊欄功能會失效。
* SITES-25235：螢幕閱讀器未宣佈篩選器邊欄內容載入訊息。
* SITES-25254：在以 320px 的解析度檢視內容時，輪播模式中會出現水平捲軸。
* SITES-25433：搭配通用編輯器的 Edge Delivery：修正多語言網站結構的頁面版本轉譯。
* SITES-26064：內容片段 Rest API：修正在後端建立片段和取得 `AccessDeniedException` 時傳回的狀態代碼。
* SITES-26890：在使用鍵盤操作時，「表格標題」範圍的鍵盤焦點在「管理發佈」頁面中無法顯示。
* SITES-29075：Live Copy 概覽不適用於高流量網站。
* SITES-29514：搭配通用編輯器的 Edge Delivery：建立新網站時，強制填入 GitHub/專案 URL。
* SITES-29691：無法在特定的相關啟動情況下移動頁面。
* SITES-29745：內容片段 Rest API：在 BFS 周遊中實施參考資料變化的水合。
* SITES-29748：修正轉譯條件以顯示 CF 編輯器內部的管理發佈/快速發佈動作。
* SITES-29789：在複製根頁面上的元件連結變更問題。
* SITES-29987：內容片段 Rest API：不支援建立和編輯內容片段模型`previewUrlPattern`。
* SITES-30140：建立內容片段參考時出現雙視窗問題。
* SITES-30327：內容片段 Rest API：在沒有權限之下發佈內容片段，會為每個承載資源建立個別的工作流程。
* SITES-30333：從 jcr 讀取資產中繼資料，避免 xmp 剖析問題。
* SITES-30353：AEM 內容片段中「src」欄位發生 GraphQL DataFetchingExceptions。
* SITES-30377：搭配通用編輯器的 Edge Delivery：清理組織名稱和網站名稱。
* SITES-30386：搭配通用編輯器的 Edge Delivery：刪除重複的舊版 UE `cors.js`。
* SITES-30583：內容片段 Rest API：尋找和取代工具將所有字元變更為小寫。
* SITES-30585：內容片段 Rest API：`previewUrlPattern` 未在建立隨附參考資料的 CFM 時設定。
* SITES-30634：RTE 影像替代文字和對齊方式的作用不一致。
* SITES-30660：自訂 AEM 元件的 ADA 法規遵循問題。
* SITES-30695：搭配通用編輯器的 Edge Delivery：提高重寫程式管道的排名，避免干擾自訂程式碼。
* SITES-30727：無法在生產作者編輯器上拖放元件。
* SITES-30752：產生持續性查詢回應時，請勿使用 `If-modified-since`/`last-modified` 標題。
* SITES-30871：在觸發 afteredit 監聽程式之後的 DOM 更新。
* SITES-30877：不正確的下層頁面轉出狀態。
* SITES-30899：轉出「稍後」選項允許在未選取日期的情況下繼續。
* SITES-30947：在轉出過程中，因藍圖缺少「behavior」屬性而導致 Null 指標例外狀況。
* SITES-31157：內容片段 Rest API：修補失敗是特定情況。
* SITES-31162：內容片段 Rest API：修正 `ModelFieldMapper` 中 `DateTimeField` 欄位的轉換問題。
* SITES-31174：內容片段 Rest API：標記未和發佈請求一起發布。
* SITES-31272：無法透過 PageManager.copy 建立資產語言副本。
* SITES-31327：內容片段 Rest API：移除 GET 片段要求的 ETag 驗證。
* SITES-31387：重新啟用 ghost 元件繼承時出現 JavaScript 錯誤「ns.ui.alert 不是函數」。
* SITES-31454：內容片段 Rest API：放寬片段參考欄位模式，使其也接受 UUID。
* SITES-31455：內容片段 Rest API：針對相同內容片段模型修正端點之間的 ETag 不相符問題。
* SITES-31459：內容片段 Rest API：在有內容參考欄位時，無法編輯 CF Live Copy。
* SITES-31467：頁面編輯器中 contexthub.authoring-hook.js 的 js 錯誤。
* SITES-31487：內容片段 Rest API：允許針對權限端點呼叫根資料夾。
* SITES-31621：搭配通用編輯器的 Edge Delivery：從 Live Copy 的試算表移除空白行。
* SITES-31676：製作或刪除元件會在頁面底部留下空白空間。
* SITES-31822：ClassicUI 取方塊標籤遺失且包含已編碼的 HTML。
* SITES-31857：在包含單引號的資料夾中建立內容片段失敗。
* SITES-31888：內容片段刪除無法傳播到預覽。
* SITES-31922：內容片段 Rest API：referencedBy 端點未傳回頁面參考。
* SITES-31987：將內容片段發佈到預覽時並未顯示其預覽 URL。
* SITES-32095：Live Copy 中的 afterchilddelete 事件監聽程式自動重新整理失敗。
* SITES-32237：搭配通用編輯器的 Edge Delivery：修正空/格式錯誤的文字元件轉譯。

### 已知問題 {#known-issues-21331}

* SITES-33177：儲存為逗號分隔字串的區段樣式已損壞。
* SITES-33262：沒有名稱的區塊會導致頁面轉譯和發佈失敗。

### 已過時的功能和 API {#deprecated-21331}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-21331}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決了 21 個已確認的漏洞，從而強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-21331}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.29.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
