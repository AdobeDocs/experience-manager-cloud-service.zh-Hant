---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 467e21aff1c2164be729598d03f30f6a9e90c8aa
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 15%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 21331 版 {#21331}

以下摘要說明維護版本21331數的持續改善，該版本於2025年6月24日公開發佈。 前一個維護版本為版本 21193。

啟用 2025.7.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-21331}

* CQ-4356522： `WorkflowResourceStatusProvider`最佳化。
* Forms-16458：用於選擇字型屬性（字型）的UI。
* Forms-17707： AEP聯結器無法用於AEP platform stage。
* Forms-19125：支援AF編輯器中的自動片段對應。
* Forms-19336：在AF編輯器的資料Source樹狀結構中新增搜尋。
* Forms-19417：支援「階層檢視」中的選項按鈕。
* Forms-19603：在規則編輯器中支援主版頁面和設計頁面。
* SITES-5358：內容片段Rest API：複製具有子系的CF。
* SITES-10575：「MSM Blueprint Bloomfilter Loader」嘗試載入超過100000列。
* SITES-14542：重新命名/移動即時副本來源頁面應觸發發佈重新命名/移動的即時副本頁面，以防該頁面先前已發佈。
* SITES-19754：使用通用編輯器的Edge Delivery：當整合發生問題時，新增人類看得懂的錯誤訊息。
* SITES-23499：使用通用編輯器的Edge Delivery：新增對用於區塊選項的多個欄位的支援。
* SITES-23518：使用Universal Editor的Edge Delivery：新增對Edge Delivery特定資產轉譯的支援。
* SITES-24436：內容片段Rest API：推出本機快取，以加速重複參考的擷取。
* SITES-25155：內容片段Rest API：移除模型清單上已棄用的「enabledForFolder」查詢引數。
* SITES-25913：內容片段Rest API：在開始發佈工作流程之前，進行資源的時限驗證。
* SITES-25976：MSM 推出後，Experience 片段內的連結無法調整。
* SITES-26271：內容片段Rest API：切換至GET變數端點的BFS周遊。
* SITES-27486：通用編輯器 — AEM整合。
* SITES-27775：發佈期間最佳化的參考搜尋（中繼資料延遲載入）。
* SITES-27782：使用通用編輯器的Edge Delivery：新增特定的發佈者 — 訂閱者實作，以將內容發佈到Edge Delivery （搶先存取）。
* SITES-27792：使用Universal Editor的Edge Delivery：新增專用的Edge Delivery服務設定範本。
* SITES-28557：內容片段Rest API：允許使用透過`references=direct`呼叫`/cf/fragments/{fragmentId}`擷取的ETags來修補內容片段。
* SITES-28683：允許MSM LiveRelationship搜尋跳過進階狀態。
* SITES-29601：內容片段Rest API：驗證長文字欄位的內容片段參考。
* SITES-29614：內容片段Rest API：使用`/cf/workflows/{workflowInstanceId}`端點擷取工作流程，其中workflowInstanceIda是發佈請求傳回的ID。
* SITES-29615：內容片段Rest API：列出使用`GET /cf/batch`透過POST `/cf/batch`建立的所有批次要求。
* SITES-29874：內容片段Rest API：現在可以擷取內容片段的長文字欄位參考並加以水合。
* SITES-29930：內容片段Rest API：為內容片段發佈工作流程新增量度。
* SITES-29986：內容片段Rest API：支援CF模型技術命名。
* SITES-30088：內容片段Rest API： CF發佈 — 當filterReferencesByStatus為空時，略過參照的擷取。
* SITES-30126：內容片段Rest API：CF發佈效能改善：以最低限度的檢查取代資源是否為片段的檢查。
* SITES-30328：使用通用編輯器的Edge Delivery：新增支援以從Sidekick預覽。
* SITES-30445：內容片段Rest API： CF模型UI結構描述：新增選項來控制可摺疊的初始狀態。
* SITES-30604：內容片段Rest API：支援新UI中採用模型中繼資料結構。
* SITES-30885：最佳化持續性查詢的 JSON 處理。
* SITES-30886：內容片段Rest API：根據工作流程中繼資料中儲存的片段uuid，內容片段端點的GET工作流程。
* SITES-31005：增強轉出工作UI以顯示進度。
* SITES-31020：增強建立即時副本工作UI以顯示進度。
* SITES-31111：內容片段Rest API：允許變異修補程式API接受內容片段啟動內的內容片段參考。
* SITES-31343：內容片段Rest API：依日期新增篩選和分頁至列出批次請求的端點。
* SITES-31472：刪除Launch會導致存放庫在Launch大量時暫停。
* SITES-31641：內容片段Rest API：將屬性新增至模型欄位，以儲存與擴充功能相關的動態地圖。
* SITES-31677：自訂工作區支援AEM內容片段匯出至Target。
* SITES-31770：內容片段Rest API：PATCH效能改善。
* SITES-31782：內容片段Rest API：新增本機資產的說明。
* SITES-32175：允許即時副本建立和MSM頁面轉出的中間認可。

### 已修正的問題 {#fixed-issues-21331}

* CQ-4359756：翻譯規則現在包含元件層級的篩選屬性。
* CQ-4359826：解決內容片段參考面板中的不一致狀態。
* CQ-4359866： LanguageUtils類別現在支援單元測試，不新增其他相依性。
* Forms-13990： Forms服務API：檔案產生：資料欄位在選取後留空會產生200 （預期為400）。
* Forms-14309： Forms Service API ：擷取資料回應程式碼修正。
* Forms-18526：複製條件中有多個欄位的規則時，固定欄位不會變更。
* Forms-18977： DOR服務沒有傳遞檔案標題。
* Forms-19047：在SP22上發佈最適化表單後AEM Forms上缺少翻譯。
* Forms-19234：無法在AEM表單中使用PDF的時間軸功能。
* Forms-19628：在自動產生的DOR中，排除巢狀面板標題也會隱藏根面板標題。
* Forms-19651：當在二進位條件中使用按一下按鈕，並且在then陳述式中使用相同按鈕時，修正規則。
* Forms-19808：FormsPortal — 啟用延遲載入時，無法提取草稿。
* Forms-19887：Access屬性在HTML5預覽中無法運作。
* SITES-15452：啟動時不應根據其副本檢查唯一的 CF 元素。
* SITES-24492： ARIA表格沒有可存取的名稱。
* SITES-24623：內容片段Rest API：修正相同CF的端點之間的ETag不相符。
* SITES-24668：當縮放比例增加到400%時，參考邊欄功能會中斷。
* SITES-24678：熒幕助讀程式不會通知參考邊欄狀態訊息。
* SITES-24697：熒幕助讀程式不會宣告影像模型的載入狀態。
* SITES-24708：縮放比例增加至400%時，篩選器邊欄功能會失效。
* SITES-25235：熒幕助讀程式不會宣告篩選導軌內容載入訊息。
* SITES-25254：以320px檢視內容時，水準卷軸會出現在輪播模式中。
* SITES-25433：使用通用編輯器的Edge Delivery：修正多語言網站結構的頁面版本轉譯。
* SITES-26064：內容片段Rest API：修正建立片段並在後端取得`AccessDeniedException`時傳回的狀態碼。
* SITES-26890：使用鍵盤時，在管理出版物頁面中看不到「表格標題」鍵盤焦點範圍。
* SITES-29075：即時副本概觀不適用於高流量網站。
* SITES-29514：使用通用編輯器的Edge Delivery：建立新網站時強制使用GitHub/專案URL。
* SITES-29691：無法移動特定啟動相關案例中的頁面。
* SITES-29745：內容片段Rest API：在BFS周遊中實作參考變體的水合。
* SITES-29748：修正轉譯條件以顯示 CF 編輯器內部的管理發佈/快速發佈動作。
* SITES-29789：複製的根頁面上的元件連結變更問題。
* SITES-29987：內容片段Rest API：建立和編輯內容片段模型不支援`previewUrlPattern`。
* SITES-30140：建立內容片段參考時出現雙視窗問題。
* SITES-30327：內容片段Rest API：發佈沒有許可權的CF時，會為每個裝載資源建立個別的工作流程。
* SITES-30333：從 jcr 讀取資產中繼資料，以避免 xmp 剖析問題。
* SITES-30353：AEM 內容片段中「src」欄位發生 GraphQL DataFetchingExceptions。
* SITES-30377：使用通用編輯器的Edge Delivery：淨化組織和網站名稱。
* SITES-30386：使用通用編輯器的Edge Delivery：移除重複的舊版UE `cors.js`。
* SITES-30583：內容片段Rest API：尋找和取代工具將所有字元變更為小寫。
* SITES-30585：使用參考建立CFM時未設定內容片段Rest API： `previewUrlPattern`。
* SITES-30634： RTE影像Alt文字和對齊方式無法一致運作。
* SITES-30660：自訂AEM元件的ADA相容性問題。
* SITES-30695：使用通用編輯器的Edge Delivery：提高重寫程式管道的排名，以免干擾自訂程式碼。
* SITES-30727：無法在生產作者編輯器中拖放元件。
* SITES-30752：產生持續性查詢回應時，請勿使用 `If-modified-since`/`last-modified` 標題。
* SITES-30871：觸發afteredit接聽程式後DOM更新。
* SITES-30877：不正確的子頁面轉出狀態。
* SITES-30899：轉出「稍後」選項可讓您繼續而不選取任何日期。
* SITES-30947：由於轉出期間藍圖上缺少「行為」屬性，出現Null指標例外狀況。
* SITES-31157：內容片段Rest API：修補程式失敗為特定案例。
* SITES-31162：內容片段Rest API：修正`ModelFieldMapper`中`DateTimeField`欄位的轉型問題。
* SITES-31174：內容片段Rest API：標籤未與發佈請求一起發佈。
* SITES-31272：無法透過PageManager.copy建立Assets語言副本。
* SITES-31327：內容片段Rest API：移除GET片段請求中的ETag驗證。
* SITES-31387：重新啟用Ghost元件繼承時，JavaScript出現「ns.ui.alert不是函式」錯誤。
* SITES-31454：內容片段Rest API：放寬片段參考欄位的模式，使其也接受UUID。
* SITES-31455：內容片段Rest API：修正相同內容片段模式端點之間的ETag不相符。
* SITES-31459：內容片段Rest API：如果有內容參考欄位，就無法編輯CF即時副本。
* SITES-31467：頁面編輯器中contexthub.authoring-hook.js的js-errors。
* SITES-31487：內容片段Rest API：允許為根資料夾呼叫許可權端點。
* SITES-31621：使用通用編輯器的Edge Delivery：從即時副本試算表中移除空白列。
* SITES-31676：編寫或刪除元件會在頁面底部留下空格。
* SITES-31822：傳統UI核取方塊標籤遺失並編碼HTML。
* SITES-31857：在包含單引號的資料夾中建立CF失敗。
* SITES-31888：內容片段刪除無法傳播到預覽。
* SITES-31922：內容片段Rest API：referencedBy端點不會傳回頁面參考。
* SITES-31987：將內容片段發佈到預覽時不會顯示其預覽URL。
* SITES-32095：在Live Copy中的afterchilddelete事件接聽程式自動重新整理失敗。
* SITES-32237：使用通用編輯器的Edge Delivery：修正空白/格式錯誤的文字元件的轉譯。

### 已知問題 {#known-issues-21331}

無。

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
