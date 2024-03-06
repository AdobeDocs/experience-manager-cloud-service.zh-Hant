---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b51ee1ebffc63b56a5b758395427f5587bd165da
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 11%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15262 版 {#release-15262}

以下摘要說明維護版本15262數的持續改善，該版本於2024年3月6日公開發佈。 之前的維護版本是版本 14697。

2024.3.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-15262}

* ASSETS-30632：在清單檢視中新增個別的Brand Portal發佈狀態列。
* ASSETS-30934：新增支援 `Iptc4xmpCore:AltTextAccessibility` 和 `Iptc4xmpCore:ExtDescrAccessibility` 屬性至資產中繼資料編輯器。
* ASSETS-31297：改善檢查以防止從Dynamic Media刪除複製的資產。
* ASSETS-33246：發行索引定義 `damAssetLucene-10`.
* ASSETS-33590：在處理設定檔中，新增對視訊的網頁轉譯支援。
* GRANITE-36205：將Oak版本更新為1.60-T20240131102219-0cde853。
* SITES-19326：更新資產UI中的連結以在新的CF編輯器中開啟CF。
* GUIDES-12945：AI支援的智慧型建議，可在編寫內容時新增內容參考
* GUIDES-12706：網頁編輯器中翻新的版本記錄功能
* GUIDES-14948：改善了翻譯面板的使用者體驗
* GUIDES-8782：改善「插入元素」對話方塊中的搜尋邏輯
* GUIDES-14681：可使用動態基準發佈多個輸出預設集
* 如需AEM Guides中增強功能的完整清單，請參閱： [AEM Guides的新增功能](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=en#release-info)

### 已修正的問題 {#fixed-issues-15262}

* ASSETS-15977：移除已棄用的v1搜尋事件和管道製作程式。
* ASSETS-18088：將Batik程式庫相依性升級至1.17。
* ASSETS-21965：中繼資料回寫工作流程必須僅在資產中繼資料變更時啟動。
* ASSETS-26368：如果工作設定不存在，則未移除已排程的大量匯入工作。
* ASSETS-26549：具有「jcr：lastModifiedBy」的資產/節點：「workflow-process-service」在清單檢視中顯示為「外部使用者」。
* ASSETS-26842：在處理設定檔中將「Firefly」文字更新為「App Builder」。
* ASSETS-28708：某些IMS權杖請求的回應非常慢。
* ASSETS-28767：如果資料夾包含大型編號，則資產的發佈狀態不一致。 個已發佈資產。
* ASSETS-29011：唯讀使用者可看見智慧型裁切。
* ASSETS-29348： AssetMoveEventHandler可能會佔用太多記憶體。
* ASSETS-29738：wff檔案的資產上傳限制因NullPointerException而失敗。
* ASSETS-30068：大量匯入Asset Essentials以包含「作業已完成，但發生錯誤」的狀態COMPLETED_WITH_ERROR。
* ASSETS-30261：針對資產事件傳送到管道的imsUserId不正確。
* ASSETS-30538：移動PDF檔案後遺失檢視頁面選項。
* ASSETS-30626：無法為具有空白assetId的資產建立已報告的傳送請求。
* ASSETS-30756：資料夾名稱結尾為「html」時，移動資產精靈動作失敗。
* ASSETS-30810：轉譯舊版YouTube設定之前會清理標籤。
* ASSETS-31015：無法上傳副檔名為.msg的資產。
* ASSETS-31038：未處理通知服務收到的任務事件。
* ASSETS-31097：停用WCM內容的非同步複製以避免周遊查詢警告。
* ASSETS-31256：具有「jcr：lastModifiedBy」的資產/節點：「workflow-process-service」在清單檢視中顯示為「外部使用者」。
* ASSETS-31260：當下拉式清單JSON中有大清單時，資產中繼資料表單下拉式欄位無法正常運作。
* ASSETS-31280：將資產新增至集合時，使其以平面化結構下載。
* ASSETS-31301： `dynamicmedia_sly.js` 無法使用Use API正確具現化。
* ASSETS-31330： ko_KR：字幕和音訊曲目中的未本地化字串。
* ASSETS-31405：大型InDesign配置會導致InDesign伺服器處理失敗。
* ASSETS-31570：Unified Shell — 需要按多次資產詳細資訊「儲存並關閉」、「取消」按鈕才能運作。
* ASSETS-31673：大型Dropbox檔案的大量匯入失敗。
* ASSETS-32108： AEM Assets未在檢視設定中儲存使用者定義的卡片大小。
* ASSETS-32230：升級com.adobe.aem.repoapi套件組合的最低執行階段版本。
* ASSETS-32544：中繼資料匯出作業間歇性失敗。
* ASSETS-32679：資產(PDF)預覽的快取問題。
* ASSETS-32754：無法將任務指派給之前未登入的使用者。
* ASSETS-32755：設定com/adobe/cq/dam/assetmove工作主題使用有序佇列。
* ASSETS-32899：在集合內搜尋速度非常慢。
* ASSETS-33098： AEM Assets搜尋Facet「標籤述詞」未如預期運作。
* ASSETS-33454：檢閱任務活動和未出現在時間軸中的註釋。
* ASSETS-34088：PDF預覽在AEM Assets上無法運作。
* ASSETS-34155： Dynamic Media — 更新AEM檢視器/ 2024.1.0。
* ASSETS-34684：在內容樹狀結構中處理多值dc：title。
* ASSETS-34789：修正檔案名稱衝突檢查中的正規化問題。
* DXML-13276： AEM Guides — 整合GraniteContent中的索引並將其從程式庫中移除。
* GRANITE-47995：刪除作業可能因與「cq：isDelivered」屬性衝突而失敗。
* GRANITE-48079：啟用OAuth線上權杖驗證的POST請求。
* GRANITE-48143：將org.apache.sling.resourcemerger升級至1.4.4 。
* GRANITE-49031：更新至Jackson 2.16.1。
* SCRNS-3961： Screens - Sequence channel：在淡化轉換中使用的Jquery動畫會產生黑色熒幕。
* SITES-15868：改善列出片段的效能。
* SITES-16079： `/fragments/{id}/references` 已開始傳回重複專案。
* SITES-16118：如果片段已修補，但模型中缺少片段欄位，則會擲回例外狀況。
* SITES-16121：擷取模型日期欄位時擲回例外狀況。
* SITES-16207：POST/adobe/sites/cf/models作業會傳回兩個不同的「確定」狀態代碼。
* SITES-17361：將Jsoup重新內嵌於sites-headless套裝中。
* SITES-17768：GraphQL可輸出內容片段中參考之資產的Dynamic Media URL。
* SKYOPS-66622：執行啟用buildTransform的管道後，製作部署當機回圈。
* SKYOPS-69977：最適化影像Servlet未在最新更新後載入影像。
* GUIDES-15045：編輯器中的拼字檢查不允許選擇建議。
* GUIDES-14968：全域導覽按鈕無法運作，且儀表板無法載入。
* GUIDES-14943：在原生PDF發佈中，條件預設集內的自訂屬性無法用於原生PDF發佈。
* GUIDES-15085：在原生PDF發佈中，無法針對2023年12月版的Adobe Experience Manager Guides解析關鍵參考資料。
* 指南 — 13486： **基線篩選** 檔案無法在網頁編輯器中使用檔案名稱。
* 如需AEM Guides中修正問題的完整清單，請參閱： [AEM Guides已修正問題](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=en#release-info)

### 已知問題 {#known-issues-15262}

無。

### 變更通知 {#change-notice-15262}

**需要動作**

即將進行的變更需要程式庫 [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) 用於自訂功能測試，以更新為最新版本 **1.2.1**

確定您的相依性在 `it.tests/pom.xml` 已更新。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

2024年4月6日之後需要此變更。

如果未更新相依性程式庫，將會在「自訂功能測試」步驟導致管道失敗。

### 內嵌技術 {#embedded-tech-15262}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
