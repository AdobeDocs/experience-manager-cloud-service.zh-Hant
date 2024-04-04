---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d07fc976fe9c8e7872468048f80e525fe8484339
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 8%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15787 版 {#release-15787}

以下摘要說明維護版本15787數的持續改善，該版本於2024年4月4日公開發佈。 之前的維護版本是版本 15575。

2024.3.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-15787}

* SITES-19059 — 內容片段 — OpenAPI — 允許列舉欄位的預設值
* SITES-20013 — 內容片段 — OpenAPI — 不存在ServletResolver時，WCMScriptHelper應中止轉譯
* SITES-19926 — 內容片段 — OpenAPI - OnOffTriggerProcessor的改良功能
* SITES-17945 — 內容片段 — OpenAPI — 取得每個版本的上次修改中繼資料
* SITES-17298 — 內容片段 — OpenAPI — 內容片段模型許可權
* SITES-14255 — 內容片段 — OpenAPI — 如果在片段模型中設定了唯一旗標，則驗證文字欄位的唯一性
* SITES-15557 — 內容片段 — OpenAPI — 允許列舉欄位的預設值
* SITES-1559 — 內容片段 — OpenAPI — 更新CF List API以允許僅擷取直接子內容片段(BE)
* SITES-16052 — 內容片段 — OpenAPI — 新增可能會使用資源的執行個體的URL
* SITES-17944 — 內容片段 — OpenAPI — 對應到CF許可權端點的適當JCR ACL
* SITES-17513 — 內容片段控制平面 — 取消發佈內容片段
* SITES-8831 — 內容片段控制平面 — PUT — 使用完整資訊更新片段
* SITES-8836 — 內容片段 — OpenAPI — 控制面 — GET參考 — 取得片段的父參考（依UUID）
* SITES-8986 — 內容片段 — OpenAPI — 發佈內容片段模型
* SITES-18073 — 內容片段 — OpenAPI - CFM的PreviewURL模式
* SITES-15242 — 內容片段 — OpenAPI — 擴充發佈事件以提供層級的相關資訊
* SITES-18702 — 內容片段 — OpenAPI - [後端] 可在資料夾層級發佈
* SITES-20020 — 內容片段 — OpenAPI — 移除 `X-Adobe-Accept-Unsupported-API` GA之前
* SITES-16066 — 內容片段 — 片段編輯器 — 變更資產選擇器JS URL
* SITES-19326 — 內容片段 — 片段編輯器 — 更新資產UI中的連結以在新的CF編輯器中開啟CF
* SITES-10515 — 內容片段 — GraphQL API - GraphQL — 載入參考的內容片段的AbstractFetcher效能問題
* SITES-17364 — 內容片段 — GraphQL API — 傳回「修改者」和「發佈者」屬性的完整名稱
* SITES-19165 — 內容片段 — GraphQL API — 允許在所有GraphQL端點中使用、參考及查詢全域模型
* SITES-17768 — 內容片段 — GraphQL API — 透過_dmS7Url公開影像的Dynamic Media URL
* SITES-11057 — 核心後端 — 開啟「時間軸>版本」時，避免載入所有版本
* SKYOPS-63033 - HTTPD — 修剪Dispatcher環境變數的空格
* SKYOPS-65518 - HTTPD — 如果Dispatcher資料夾中有不合法的檔案名稱，則讓驗證器失敗
* SITES-19626 — 啟動 — 將DAM-CFM lastUpdate欄位合併至主要
* SITES-19251 — 快速網站 — 建立精靈 — 當主題參考不等於網站名稱時，支援網站管理員UI側欄
* SITES-15430 — 通用編輯器 — AEM網域下的通用編輯器
* CQ-4344966 - WCM — 翻譯 — 建立網站結構更新的基本框架並更新資產的現有框架
* CQ-4347312 - WCM — 翻譯 — 建立工作流程以將「cq：translationsourcejcruuid」與現有來源和語言副本建立關聯
* CQ-4354509 - WCM — 翻譯 — 發佈翻譯工作事件 [OSGi EventAdmin]
* SITES-16318 — 行人穿越道 — 使用Edge Delivery Services以AEM為基礎的製作
* Forms-9889：使用者可在設定提交至REST端點的提交動作時新增POSTURL和雲端設定
* 在規則編輯器中，使用者可以：
   * Forms-12160：驗證When條件之Then區段中的欄位、面板或表單。
   * Forms-12570：重設When條件之Then區段中的欄位、面板或表單。
   * Forms-11541：透過自訂函式，在規則編輯器中使用欄位物件和全域物件。
   * Forms-11714：在自訂函式中將引數定義為選用引數。 依預設，自訂函式中宣告的引數是強制性的。
   * Forms-11756：對自訂函式使用快取，以改善在規則編輯器中擷取自訂函式清單時的回應時間。
   * Forms-12053：在「When」條件中新增「else」陳述式，以實作巢狀條件。
   * Forms-11269：在核心元件型表單的自訂函式中使用新式ES10 JavaScript功能，例如let和arrow函式。

* Forms-9014：塗鴉簽名元件的各種協助工具相關改良


### 已修正的問題 {#fixed-issues-15787}

* 已修正各種協助工具和國際化問題
* SITES-16966 - AEM：未當地語系化「未建立版本！」 「網站>還原>還原樹狀結構」中的字串
* SITES-16208 - ContentFragmentModelIdentifier公開誤導性的標題屬性
* SITES-18024 — 缺少If-Match標頭時，回應必須為428
* SITES-18003 — 無法正確傳回建立版本的使用者
* SITES-17937 — 在同步作者Pod之前會發出「內容片段建立」事件
* SITES-18029 — 當JCR觀察同時通知時，事件處理管道掛起
* SITES-17882 — 從結構描述中移除片段文字欄位長度上限
* SITES-19252 — 修正與HTTP狀態代碼406和415相關的不一致問題
* SITES-16964 - [後端] 依「修改者」排序的功能無法正常運作
* SITES-17519 - Sites頁面屬性編輯器 — 長頁面名稱使得按鈕無法點按
* SITES-16852 — 發佈API正在發佈具有新狀態的參考
* SITES-18833 - OpenAPI端點中看不到中的唯一性限制
* SITES-15553 — 如果XF的URL包含選擇器，則XF的側面板無法載入
* SITES-14340 - VersioningTimelineEventProvider.accepts中的NPE
* SITES-1605 - [網站] DeletePageCommand會在Null來源路徑的情況下擲回NPE
* SITES-16308 - [GB18030]：建立以GB18030字元命名的新網站資料夾時出現警告訊息
* SITES-16304 - [GB18030]：建立以GB18030字元命名的新體驗片段資料夾時顯示警告訊息
* SITES-8769 — 改善StyleImpl效能
* CQ-4343815 — 行銷活動 — 目標定位 — Teaser的預設變體具有空白URL
* CQ-4355889 - Campaign — 目標定位 — 建立對象請求因IMS設定而失敗。
* SITES-12460 - Campaign整合 — Campaign / AEM Cloud Service整合中斷
* SITES-11571 — 內容片段 — GraphQL API - PersistedQueryServlet應在格式錯誤的URL上傳送400
* SITES-19946 — 內容片段 — GraphQL API — 啟動時不再掃描模型
* SITES-1605 — 核心後端 — DeletePageCommand在來源路徑為null時擲回NPE
* SITES-5429 — 核心後端 — ChildrenListServlet itemResourceType允許直接執行程式碼
* SITES-15553 — 體驗片段 — 如果XF的URL包含選取器，則XF的側面板無法載入
* SITES-13666 - Headless — 管理員 — 錯誤記錄誤判「com.adobe.cq.dam.cfm.headless.ui.impl.models.CFHomeCardModelImpl設定ID不得為空」
* SITES-17164 — 頁面編輯器 —  [雲端， 6.5 Forms] AF主題編輯器預覽已中斷
* SITES-14340 — 網站管理員UI - VersioningTimelineEventProvider.accepts中的NPE
* SKYOPS-68611 - Sling - repoinit - Port sling repoinit在維護分支中建立路徑修正
* CQ-4354678 - WCM — 翻譯 — 翻譯工作正在匯出翻譯的內容
* CQ-4355167 - WCM — 翻譯 — 將翻譯工作標籤為完成或封存時未出現快顯視窗
* CQ-4355913 - WCM — 翻譯 — 翻譯專案語言卡片出錯
* GRANITE-47694 — 工作流程 — 無法在雲端工作流程中為非管理員使用者取得子任務
* ASSETS-31097 - Assets Cloud — 包含索引的記錄已遍歷/bin/numberofentitiesinfolders.json的警告
* ASSETS-35860 - Assets Cloud - AEM Assets欄檢視中的時區轉換不正確
* SITES-15260 — 傳統UI （舊版） — 如果使用工作表匯入，Bulkedit會在頁面上新增EMPTY屬性
* SITES-16834 — 傳統UI （舊版） — 文字內有逗號時，使用大量編輯器編輯文字後遺失文字
* SITES-17767 — 內容片段 — 管理員 — 對沒有jcr：content節點的資料夾也支援允許的cf-model
* SITES-17683 — 內容片段 — 核心後端 — 內容片段無法透過Jackson匯出工具序列化
* SITES-18797 — 內容片段 — 核心後端 — 自訂索引後重複GraphQL結果
* SITES-18076 — 內容片段 — 核心後端 — 多值文字的@TypeHint稱不正確
* SITES-17856 — 內容片段 — 模型與模型編輯器 — 如果config不是資料夾，則不會顯示CF模型
* SITES-17071 — 核心後端 — 特定頁面不會在時間軸中顯示版本
* SITES-17285 — 核心元件 — 內嵌影像裁切在AEMaCS中的作者和發佈上不同
* SITES-19187 — 核心元件 — 在影像元件中放置資產的兩種方法在對話方塊上會產生不同的結果
* SITES-20077 — 核心元件 — 內嵌影像裁切 — 裁切錯誤，影像模糊
* SITES-17211 — 體驗片段 — 體驗片段元件路徑選擇器對話方塊，其中顯示已刪除的體驗片段
* SITES-17894 — 啟動 — 提升巢狀啟動會將啟動內容恢復到其上階的版本
* SITES-16042 - MSM — 即時副本 — 轉出後，註解在LiveCopy中顯示不正確
* SITES-16691 - MSM — 即時副本 — 當客戶從元件上的「轉出」圖示選取「轉出」或「轉出為」時，「繼續」按鈕會呈現灰色。
* SITES-16733 - MSM — 即時副本 — Blueprint索引頁面在rep：policy套用至節點時無法轉出
* SITES-17155 - MSM — 即時副本 — 重新命名LiveCopy時，頁首與頁尾會翻譯回英文
* SITES-17492 - MSM — 即時副本 — AEM頁面即時副本版面配置不一致
* SITES-19316 - MSM — 即時副本 — 體驗片段的參考連結未在語言副本中更新
* SITES-19347 - MSM — 即時副本 — Prod作者速度緩慢和服務中斷訊息 — pod經常重新啟動 — 健全狀況警報
* SITES-19790 - MSM — 即時副本 — 建立即時副本後的預覽資訊不正確
* SITES-20086 - MSM — 即時副本 — 在Assets中轉出CF的MSM將轉出所有即時副本，即使已選取轉出一個即時副本
* SITES-20088 - MSM — 即時副本 — 屬性中XF轉出後的空白頁面問題 — AEMas a Cloud Service
* SITES-16854 — 頁面編輯器 — 置放目標覆蓋覆蓋元件中具有「選取面板」功能的parsys
* CQ-4355563 — 專案 — 路徑引數錯誤。 正在填入專案收件匣搜尋指令碼的「？appId=aemshell」
* SITES-16876 — 快速網站 — 主題部署 — 預覽頁面2上缺少CSS和JS
* SITES-18418 — 網站管理員UI — 需要欄位時，路徑欄位Widget的顯示/隱藏功能無法正常運作
* SITES-19534 — 網站管理員UI — 在AEM 6.5.19升級後無法開啟有效許可權對話方塊
* SITES-19203 — 範本編輯器 — 可編輯的範本原則文字未對齊和樣式重疊刪除按鈕
* CQ-4354881 - WCM — 翻譯 — 將內容片段翻譯為頁面的一部分時，內容片段路徑會設為source (en-us)
* CQ-4355289 - WCM — 翻譯 — 翻譯Cloud Service中只顯示前40個元素
* CQ-4355866 - WCM — 翻譯 — 翻譯工作流程擲回現有頁面的錯誤
* CQ-4355797 — 工作流程 — 無法使用OOTB工作流程步驟
* GRANITE-48938 — 工作流程 — 作者顯示資產在「待發佈」狀態中停止。 新持續性裝載對應快取中的問題。
* GRANITE-49036 — 工作流程 — 功能要求 | 能夠排程並設定工作流程封裝的清除
* SITES-17393 — 工作流程擴充功能 — 針對cq：Tag使用工作流程啟動器時，發佈內容樹狀結構失敗
* SITES-17759 — 工作流程延伸模組 — 樹狀結構啟動在AEMaaCS中無法運作之標籤的工作流程
* Forms-12411：在Android裝置上， `Maximum Number of Characters Validation` 選項無法用於最適化表單文字方塊元件。
* Forms-13377：當使用者嘗試新增自訂字型並執行管道以進行設定時，它會失敗並出現「ContainersNotReady」錯誤
* Forms-13267：使用者新增最適化表單下拉式清單元件時，下拉式清單的ID無法產生
* Forms-13544：使用者使用精靈版面配置新增最適化表單容器元件時，無法在表單製作期間正常運作
* Forms-13091、FORMS-13414：如果使用者嘗試在Azure Blob儲存空間中設定自訂網域URL，則會失敗
* Forms-13595：當使用者嘗試將表單儲存在其他位置時，如果瀏覽器解析度設定為100%，使用者無法看到「選取資料夾」和「取消」按鈕。 但是，當解析度設定為75%時，選項是可見的
* Forms-10952：當使用者將調適型表單下拉式清單元件新增到調適型表單中，並根據各種自訂規則使用「設定選項」屬性時，「設定選項」屬性只對最後一個規則起作用
* Forms-11471：當「emitter.json」呼叫因網路中斷而失敗時，片段的延遲載入會失敗。
* Forms-11786：當使用者在行事曆Widget中的月份之間切換時，日期選擇器元件會顯示額外的列。
* Forms-12093、FORMS-12093：使用者勾選最適化表單核取方塊以提交表單時，系統會使用不正確的值加上一個額外的  `\` 儲存在文字方塊中
* Forms-11993：當使用者在iOS裝置上的附件元件中使用「拍攝影片」按一下影像時，所有影像都會新增到具有相同名稱的資料夾中
* Forms-12555：當使用者嘗試將AEM Forms整合到具有AEM已發佈URL的郵寄平台時，AEM Forms在轉譯頁面時不會新增method=post。 即使在具有URL的提交動作中設定POST，也會發生此問題。 這會導致郵寄平台無法將此識別為表單
* Forms-12938：HTML5表單在具有IE相容模式的Microsoft Edge瀏覽器中無法運作或正確載入
* Forms-12032：使用者提交表單時，提交動作路徑的路徑未正確指向
* Forms-12445：變更選項按鈕選項的順序並發佈表單後，會在表單資料模型中擷取錯誤值。
* Forms-12947：使用者向現有字典新增語言時，無法合併或新增
* Forms-11363：使用者透過工作區提交表單時，在呈現表單期間表格中會發生顯示問題
* Forms-11756：使用者新增ES6 JavaScript功能時，例如 `let` 和 `const` 在自訂函式中，無法開啟規則編輯器。 此維護發行版本提供ES10的支援
* Forms-13164：如果使用者產生PDF，提交後會在其中新增非預期的空白行
* Forms-13789：使用者嘗試產生多個PDF時，輸出批次API會失敗
* Forms-11483：當使用者將PDF轉換為PDF/A-2B或PDF/A-3B時，轉換失敗並顯示驗證錯誤
* Forms-10501：當使用者叫用HSM時，檔案會經過認證，但不會啟用LTV
* Forms-11546：當表單作者在最適化表單中使用重複的面板時，HTML標籤中缺少ARIA屬性。 這可改善最適化表單重複面板的協助工具功能
* Forms-11826：由於相符的標籤Arial® labelledby和Arial® label，熒幕助讀程式無法區分這兩者。 為了解決問題 — 表單欄位的「aria-labelledby」標籤已取代為「aria-describedby」。 (F)。 這可改善最適化Forms的協助工具
* Forms-12626、FORMS-13094：使用者無法使用鍵盤存取工具列，無法在表單編輯器頁面上儲存或編輯內容。 已修正此協助工具問題
* Forms-13102：在表單撰寫程式中，Forms和檔案頁面上可用的圖示缺乏適用於不同能力個體的描述性功能。 已修正此協助工具問題

### 已知問題 {#known-issues-15787}

* SITES-17934 — 內容片段 — 由於DoS保護大型片段樹狀結構，預覽失敗。 另請參閱 [KB](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945)

### 已棄用的功能和API {#deprecated-15787}

* [Adobe Developer Console 中的 JWT 憑證已被取代](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

請檢視 [過時和移除的功能和API](/help/release-notes/deprecated-removed-features.md) 以瞭解AEMas a Cloud Service中已過時或移除的內容。

### 變更通知 {#change-notice-15787}

**必要採取的行動**

#### 將 CM Java 版本設定為 11 {#set-java-version-11}

新版本 aem-sdk-api 包含使用 Java 11 Target 編譯的類別，該應用程式與 Cloud Manager 組建環境預設 JDK 版本 1.8 不相容。此更新要求使用 JDK 11 執行 Maven。

建議客戶將 `.cloudmanager/java-version` 檔案加入其 git 存放庫的根目錄中，其內容為： `11`。請參閱「[組建環境/設定 Maven JDK 版本](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version)」。


### 內嵌技術 {#embedded-tech-15787}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.24.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
