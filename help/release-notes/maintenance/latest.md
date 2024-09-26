---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fa2da21ef6424bce0830d503eba650e1c1bf3dc2
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 16%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本 17964 {#release-17964}

以下摘要說明維護版本17964數的持續改善，該版本於2024年9月25日公開發佈。 先前的維護發行版本為發行說17689。 由於發生問題，發行說17882已設為私人。

2024.10.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-17964}

* Assets - 37750： [優先順序4] [GraphQL]對DM scene7 URL的支援：影像智慧型裁切。
* CQ - 4354583： [AEMaaCS]透過Adobe管道傳送翻譯程式事件。
* CQ - 4357642：更新OOTB Connector中的MSFT認證。
* CQ - 4358217：從請求實體還原序列化請求內文。
* CQ - 4358342：僅在一個HTTP方法上註冊RequestProcessors。
* Forms - 10781：增強規則編輯器，以為面板中的下一個/上一個專案建立規則。
* Forms - 14595：使用預填資料計算無瀏覽器轉譯的DoR時，DoR中缺少[無瀏覽器功能]值。
* Forms - 15619： AEM Forms更新翻譯套件。
* Forms - 16113： [Adobe Sign]無法由其他使用者更新合約狀態。
* Forms - 16155： [規則編輯器]實作Async函式。
* GRANITE - 53872：為IMS使用者端ID新增環境變數。
* SITES - 23738：發行核心元件2.27.0。
* SITES - 16610：內容片段：取得啟動詳細資訊端點。
* SITES - 16614：內容片段：重新基底啟動端點。
* SITES - 16615：內容片段：提升啟動端點。
* SITES - 24215：內容片段：實作取得啟動來源端點。
* SITES - 20336：內容片段：改善刪除內容片段模型時的驗證。
* SITES - 21090：內容片段：新增數字欄位分數最小/最大值支援
* SITES - 21658：內容片段：升級以使用UUID參考。
* 網站 — 23054：內容片段：複製內容片段模型。
* SITES - 23264：內容片段：建立模型的靜態結構。
* SITES - 23265：內容片段：透過UI結構GET端點公開模型的靜態結構。
* SITES - 23266：內容片段：為內容片段模型新增限制的功能。
* SITES - 23778：內容片段：搜尋內容片段模型應允許搜尋從未發佈的模型。
* SITES - 23335：內容片段：新增對外部資產參考的支援。
* 網站 — 24626：內容片段： RTC：UUID移轉的許可權： 2。
* 網站 — 24786：內容片段： `referencesTree`端點的增強功能。
* SITES - 24833：內容片段：針對允許的HTML標籤清單移除HTML輸入驗證。
* 網站 — 23380： GraphQL：使用適當的API讀取資產中繼資料。
* SITES - 22864： [Edge Delivery]具有新AEM內容結構整合H2 2024的通用編輯器。
* SITES - 23584：基礎元件測試在Java 17上失敗。
* SITES - 23662：事件：無法從伺服器記錄檔中的JCR記錄陳述式擷取觸發發佈要求的使用者。
* SITES - 23301：新增在建立內容片段翻譯時啟動新工作流程以建立資料夾結構的支援。
* SITES - 23336：內容片段：新增對外部資產參考的支援
* SITES - 24091： MSM內容封裝分割：主版。
* SITES - 24114： isSourceRenderCondition：將錯誤記錄訊息減少為DEBUG。
* SITES - 24166：觸控式UI編輯器的遠端資產緩解功能。
* SITES - 24409：僅在一個HTTP方法上註冊所有要求處理器。
* SITES - 25008：改善PersistenceExceptions和許可權問題的處理。
* SITES - 24821： [Xwalk]將aem.page / aem.live設為預設值。

### 已修正的問題 {#fixed-issues-17964}

* CQ - 4356887：Akamai Technologies Inc.翻譯專案狀態不一致
* CQ - 4357878：在供應商翻譯失敗時，翻譯框架未設定錯誤狀態。
* CQ - 4358028：如果上傳縮圖，則無法建立專案。
* CQ - 4358290：已發佈頁面上的目標設定無法運作。
* Forms - 13173：最適化表單>規則編輯器>放置物件欄位中的下拉式清單未對齊。
* Forms - 13873：元件名稱中的AFv2： (「 — 」)導致規則失敗。
* Forms - 14340：具現化FormsAndDocumentOmniSearchHandler和CloudStorageSubmitActionInserter時發生錯誤。
* Forms - 15363：在規則編輯器中顯示的名稱。
* Forms - 15381：增強授權範圍訊息的UI。
* Forms - 15595： AEM表單TnC元件同意文字換行問題。
* Forms - 15623： AEMaaCS Forms — 使用一個POST更新Dynamics中多個表格的替代方案。
* Forms - 15682： AEM Forms — 無法將DOR繫結至Dynamics FDM。
* Forms - 15799： Adobe Sign GovCloud簽名頁面不會在iframe中轉譯。
* Forms - 15835：提交後表單URL重寫問題。
* Forms - 16091：使用重新建構的Binary.java。
* Forms - 16096： Forms使用者無權存取restendpoint對話方塊。
* Forms - 16139：在核心元件表單中新增DoR的必要記錄。
* Forms - 6935：作用中元件的狀態缺少3對1的對比率。
* Forms - 7018：空白元素接收焦點。
* GRANITE - 53028： ExternalProcessPollingHandler中的NPE。
* GRANITE - 53907：無法將服務使用者識別為工作流程超級使用者。
* SITES - 24405：內容片段：列舉的延伸資訊應更具彈性
* SITES - 23024：內容片段：列舉未傳回locked： true inGET片段。
* 網站 — 23269：內容片段：建立內容片段可設定鎖定的欄位。
* SITES - 23337：內容片段：具有`body`的批次端點因轉型例外而失敗。
* SITES - 23474：內容片段：分頁應在搜尋內容片段中排除損壞的資源。
* SITES - 23615：內容片段：內容片段副本AuthoringInfo未更新
* SITES - 23668：內容片段：修補多欄位即時副本失敗，出現400錯誤
* SITES - 23695：內容片段：索引標籤說明在UiSchema中無法使用
* SITES - 23704：內容片段： _extendedInfo不支援多值列舉
* SITES - 23781：內容片段：列舉欄位中不允許重複值
* SITES - 24150：缺少內容片段：關於建立的內容片段版本編寫資料
* SITES - 24230：內容片段：修正搜尋內容片段模型中`modified`復寫狀態的篩選
* SITES - 24233：內容片段：依`publishedBy`篩選可在搜尋內容片段模型中包含未發佈的資源
* SITES - 24355：內容片段：未對建立的內容片段遵循即時關係
* SITES - 24816：內容片段：ValidationStatus訊息順序不一致。
* SITES - 23896：事件：更多事件會與「頁面移動」事件一起出現
* SITES - 23899：事件：頁面事件延遲或完全未產生
* SITES - 23961：事件：出現設定資料夾時，使用參照建立內容片段模型失敗
* SITES - 23963：事件：已刪除頁面的事件有時不會來
* SITES - 23443： GraphQL： GraphQL資料指標查詢不一致行為。
* SITES - 10994：鍵盤焦點順序不符合邏輯。
* SITES - 16357：AEM：在「網站」功能表的「設定Analytics」標籤中，按鈕被截斷。
* SITES - 19836：容器中的Ghost元件會顯示在發佈和預覽執行個體上。
* SITES - 22348：如果專案的即時副本超過100個，則無法載入即時副本概觀頁面。
* SITES - 22960： ContentFragmentModelOmniSearchHandler中的資源解析程式未關閉。
* SITES - 23284：URL編碼導致空白路徑瀏覽器對話方塊。
* SITES - 23505：頁面移至其他位置時，元件會顯示不正確的URL。
* SITES - 23574：許多頁面無法預覽/與目前版本比較
* SITES - 23585：還原具有cq：responsive節點的元件繼承的問題
* SITES - 23650：AEM作者環境中傳入連結計數的差異
* SITES - 23659：由切換FT_* SITES - 9757引起的內容語言Servlet回歸
* SITES - 23759：在體驗片段上新增的Assets不會隨啟動發佈
* SITES - 24025： 302在AEM中的重新導向使用內部DNS而不是公用DNS傳回位置標頭
* SITES - 24036：ASCII格式的AEM RTE持續字元所需調查
* SITES - 24317：Proxy設定不適用於基本驗證
* SITES - 24918：使用專用IP輸出時，偶爾會傳回[Xwalk]修正504錯誤。

### 已知問題 {#known-issues-17964}

* Forms - 15818：在伺服器記錄檔中找不到元件描述項專案`OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml`的陳述式。 這些是無害的記錄陳述式。

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
