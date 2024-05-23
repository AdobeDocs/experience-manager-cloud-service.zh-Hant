---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d107f40c4bc43837db9d8fab3d06627d9e930620
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 9%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 16357 版本 {#release-16357}

以下摘要說明維護版本16357數的持續改善，該版本於2024年5月22日公開發佈。 上一個維護版本是版本 16145。

2024.5.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-16357}

* SITES-19579：將內容片段從一種模式移轉至另一種模式的Java API。
* SITES-19698： [開啟API] 建立讀取作業，以管理OpenAPI定義中每個模型的UI結構描述。
* SITES-19834：Adobe I/O事件遺失發佈/取消發佈的ID。
* SITES-20146：啟用已移動頁面的預覽版本/比較。
* SITES-19973： CFM Search API實作。
* SITES-20333：改善建立內容片段時的驗證。
* SITES-20334：改善編輯內容片段模型時的驗證。
* SITES-20585：增強內容片段搜尋API，以根據地區設定篩選。
* SITES-20594：傳回建立/修改/復寫資源的使用者全名。
* SITES-20601： [OpenAPI] 更新CF Search API以允許僅擷取直接子內容片段。
* SITES-20656： [BE] 提供取代字串時符合大小寫的選項。
* SITES-20405： [Xwalk] 支援欄位收合的mimeType。
* SITES-17854：支援CF與資產參考的UUID (Pfizer MVP)。
* SITES-19555：UI結構描述的簡單模型API。
* SITES-19611： [開啟API] 建立寫入/更新操作，以管理OpenAPI定義中每個模型的UI結構描述。
* SITES-19614： [Xwalk] 試算表分頁/無限捲動。
* SITES-20005：作者管道應該有可設定的事件延遲。
* SITES-20121：允許列舉欄位使用defaultValue。
* SITES-20342： [後端] 在資料夾層級發佈 — 將篩選器新增至僅發佈CF。
* SITES-20355：移除內容片段模型和許可權API servlet。
* SITES-20387：導覽tagadmin一律會計算標籤使用量。
* SITES-20495： [BE] 能夠取得在檔案夾層級發佈的許可權。
* SITES-20653： [Xwalk] 新增experiment-start-date和 — end-date。
* SITES-20666： [Xwalk] 根據編寫時的預設值，實驗應關閉。
* SITES-20752： [cq-wcm-core] 適用於CF的Apple啟動。
* SITES-20946：將etag新增為LIST模型端點中的屬性。
* SITES-20947： [persistence] 依內容片段id擷取子任務。
* SITES-21012：將模型中繼資料結構描述合併至產品。
* SITES-21769：使用/jcr：id/路徑前置詞進行逐一資源識別(resource-by-id)擷取。
* ASSETS-30379：DRM授權檢查會逐步顯示下載的整個資產樹狀結構。
* ASSETS-35535： [DataS介面卡錯誤] v1事件需要忽略空白資產下載。
* SITES-21550： [Xwalk] 自訂中繼資料：數字、日期、日期時間、時間欄位。
* SITES-20149： RTC： [cq-wcm-launches-core] 匯出新的API for Launches for CF。
* SITES-20150： RTC： [cq-command] 將新方法新增至現有API。
* SITES-20451：將Sidecar外掛程式新增至wcm-commons。
* SITES-20499： [MSM][Async] 將程式碼從AsyncOperationServlet解壓縮至公用程式類別。
* SITES-20763：更新網站整合中的傳送API端點。
* SITES-20583：將etag新增為中的屬性 `LIST`/search片段。
* CQ-4356445：事件產生器和結構描述實作。
* CQ-4356625：改善languagecopyrendercondition.jsp中的授權檢查。
* CQ-4356629：改善isWorkflowUser rendercondition中的授權檢查。
* CQ-4356934：使用ResponseEntities時簡化RequestProcessor API。
* CQ-4357214：請求處理器不得依賴於servlet邏輯。
* SITES-16392：失敗的啟動建立不應留下記憶體內容。
* SITES-20238： [RTC] Pfizer MVP — 新增CF API以解析CF路徑至ID，反之亦然。
* SITES-21043： [CF][launches] Cloud Service的側連線埠效能改善。
* SITES-21044： [CF][launches] 將側連線埠非同步編輯裝載實作至Cloud Service。
* Forms-7483： AEM Forms JSON結構描述剖析器現在支援JSON結構描述(2020-12)。
* Forms-13209：包含處理常式，可覆寫最適化Forms預設提交成功和提交失敗處理常式。 您可以透過最適化Forms規則編輯器設定這些處理常式。
* Forms-13612：熒幕助讀程式現在會閱讀錯誤訊息、簡短說明，以及核心元件型Adaptive Forms中欄位的完整說明。 此外，已新增支援，以在表單包含錯誤且無法提交時，使最適化表單輸入失效。
* Forms-12052：表單作者現在可以套用自訂函式，在提交之前預先處理資料。
* Forms-11295：新增對SHA256的支援，以及適用於AEM Forms數位簽名的ECDSA演演算法。
* Forms-9432：已將其他內容型別（REST端點）新增至資料來源雲端設定。 如此可讓索引鍵值配對中的資料提交至已驗證的端點。

### 已修正的問題 {#fixed-issues-16357}

* SITES-20608：包含到範本中時已啟用個人化的體驗片段會導致無限回圈。
* SITES-19554： [Xwalk] 試算表編輯器：無法清空儲存格。
* SITES-19971：修補包含索引標籤的CFM會變更欄位順序。
* SITES-20168：內容片段模型 `locked` 欄位未正確更新。
* SITES-20522：損毀的內容片段中斷/adobe/sites/cf/fragments端點。
* SITES-20816： CF OpenAPI — 輸出與參考片段的缺少模型不一致。
* SITES-21239：移除ContentFragmentSearchService循環相依性。
* SITES-20582：搜尋和列出內容片段應允許深度0。
* SITES-20559： [MSM][XF][Lufthansa] 從主版/語言轉出體驗片段至國家/語言時，不會更新引用。
* SITES-17772： AEM：具有管理員群組的使用者無法解鎖另一個使用者鎖定的頁面。
* SITES-20401： [Xwalk] 章節中繼資料不支援多值屬性。
* SITES-21391： [OpenAPI事件] 修改內容片段模型的標題或標籤（屬性）時不會觸發任何事件。
* SKYOPS-73234：AEM Assets全域DAM計畫升級至AEM版本15553和PR ID 35362時，錯誤記錄失敗增加。
* SKYOPS-75341：分佈交叉通路套件組合中的NoSuchMethodError。
* SCRNS-3945： Skyline：畫面中未本地化的「已排程」字串。
* SITES-20586：範本「已發佈」時間戳記未更新。
* SITES-16674：繼承轉出設定核取方塊不適用於即時副本屬性。
* SITES-18680：無法提取graphql查詢(Apple)中的參考變數。
* SITES-21233： [CoreCmp] 升級至15860後，GS1美國的收合式選單已損毀。
* SITES-20367：刪除AEM中的啟動的問題。
* CQ-4357161：AEM 收件匣承載畫面傳回 404。
* SITES-20214：儲存時出現AEM轉出設定順序問題。
* SITES-20364： 302重新導向無法搭配URL中的選取器運作。
* SITES-20547：AEMas a Cloud Service即時副本排除路徑清單中的截斷路徑。
* SITES-20691：體驗片段範本限制不遵守cq：allowedTemplates。
* SITES-21122：AEM CS Live Copy具有內容片段瑕疵。
* ASSETS-38723：在初始化this.readRules之前呼叫getReadRulesForMetadataChildNodes()時，MetadataRulesProviderImpl擲回NPE。
* SITES-11727： [GQL] 內容片段參考的完整水合缺少資料。
* SITES-19462：資產搜尋在AEM Cloud中無法正常運作。
* SITES-19994：當使用者嘗試關閉內容片段時，關閉按鈕會計時。
* SITES-20029：內容片段版本是在關閉後立即建立，不會變更內容。
* SITES-21316：片段預覽：由於從SITES-11727變更程式碼，預覽失敗。
* SITES-20023：檔案上傳無法用於多欄位中的遠端（新一代資產）資產。
* ASSETS-37611：會針對未發佈的資產觸發「要求完成移動作業」工作流程。
* CQ-4357278：如果getRequestBodyType傳回null，DispatcherServlet會擲回NPE。
* CQ-4357279：當請求沒有pathInfo時，請求處理失敗。
* SITES-20496： [Xwalk] 在網站管理員中選取試算表時，沒有屬性選項。
* Forms-13827：在最適化Forms規則編輯器中，WHEN操作目前不支援具有日期選擇器的不同型別欄位。
* Forms-13786：在最適化Forms規則編輯器中，拖放功能無法用於自訂函式。
* Forms-13587：在調適型Forms編輯器中，基於核心元件的調適型Forms的「裝置模擬器」功能無法正常運作。
* Forms-14376使用者按下「重設」按鈕時，如果靜態文字標示為未繫結，則會導致主控台錯誤。
* Forms-13801：即使條款與條件元件已停用，對應的核取方塊仍會保持啟用狀態。
* Forms-11952：提交表單時，表單產生的提交URL會以/content/開頭，而非/portale/，導致請求路由錯誤。 這可防止請求到達預期的伺服器。
* Forms-13616：日期選擇器將目前日期顯示為晚一天，可能是因為時區問題，而且由於這種不一致性和額外的顯示模式問題，很難設定正確的日期格式。
* Forms-13829：在清除並重新選取某個選取專案後，下拉式清單（由規則控制以模擬選項按鈕功能）無法正確填入。 需要的行為是讓個別核取方塊做為選項按鈕，一次只允許一個選項，並允許取消選取所有選項。
* Forms-14244：在以XDP為基礎的最適化表單中，核取方塊上具有內嵌指令碼，此類核取方塊之後的元素不會執行指令碼。
* Forms-14267：使用者在開發、中繼和生產環境中傳送API請求時，會遇到一致的逾時錯誤。 這些請求與產生PDF有關，有時是使用資料繫結預先填入的資料。 此問題會導致擱置程式，該程式最終會逾時，但在發生錯誤後重試時會成功。
* Forms-11589：對於只有AEM Forms解決方案（沒有任何其他解決方案）的使用者，前端管道無法運作。
* Forms-13896：在DoR （記錄檔案）輸出中，無論是否使用西曆數字合併輸入資料，日期和數字都會以阿拉伯文顯示。

### 已知問題 {#known-issues-16357}

無。

### 已過時的功能和 API {#deprecated-16357}

若要了解 AEM as a Cloud Service 中已過時或已移除的功能，請查看「[已過時和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)」。

### 內嵌技術 {#embedded-tech-16357}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.25.4 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
