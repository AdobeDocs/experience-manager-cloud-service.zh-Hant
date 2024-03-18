---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d16d908d39df3c7d72dc48ac877c1543d2442416
workflow-type: ht
source-wordcount: '1240'
ht-degree: 100%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 15262 版 {#release-15262}

下面是 15262 維護版本的持續改善內容，該版本於 2024 年 3 月 6 日公開發行。之前的維護版本是版本 14697。

2024.3.0 功能啟用將為此維護版本提供完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-15262}

* ASSETS-30632：在清單檢視中新增單獨的 Brand Portal 發佈狀態欄。
* ASSETS-30934：新增對中繼資料編輯器的 `Iptc4xmpCore:AltTextAccessibility` 和 `Iptc4xmpCore:ExtDescrAccessibility` 屬性支援。
* ASSETS-31297：改善檢查行動以防止從動態媒體刪除複製資產。
* ASSETS-33246：發佈索引定義 `damAssetLucene-10`。
* ASSETS-33590：新增對處理設定檔影片的 webm 轉譯支援。
* GRANITE-36205：將 Oak 版本更新至 1.60-T20240131102219-0cde853。
* SITES-19326：更新 Assets UI 中的連結，以便在新的 CF 編輯器中開啟 CF。
* GUIDES-12945：AI 驅動智慧型建議，可在製作內容時加入內容參考
* GUIDES-12706：改善 Web 編輯器中的版本歷史記錄功能
* GUIDES-14948：改善翻譯面板中的使用者體驗
* GUIDES-8782：改善「插入元素」對話框中的搜尋邏輯
* GUIDES-14681：有能力發佈具備動態基準的多個輸出預設
* 有關 AEM Guides 增強功能的完整清單，請參閱：[AEM Guides 中的新增功能](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=zh-Hant#release-info)

### 已修正的問題 {#fixed-issues-15262}

* ASSETS-15977：刪除已過時 v1 搜尋事件和管道產生器。
* ASSETS-18088：將 batik 資料庫相依性升級至 1.17。
* ASSETS-21965：中繼資料回寫工作流程必須僅在資產中繼資料變更時啟動。
* ASSETS-26368：如果作業設定不存在，預計的批次匯入作業就不會移除。
* ASSETS-26549：具備「jcr:lastModifiedBy」的資產/節點：「workflow-process-service」在清單檢視中顯示為「外部使用者」。
* ASSETS-26842：更新「Firefly」文字，以便閱讀處理設定檔中的「應用程式建立工具」。
* ASSETS-28708：某些 IMS 權杖請求的回應非常慢。
* ASSETS-28767：如果是含有已發佈資產較大編號的資料夾，表示資產的發佈狀態不一致。
* ASSETS-29011：智慧型裁切可供唯讀使用者看見。
* ASSETS-29348：AssetMoveEventHandler 可能會佔用太多記憶體。
* ASSETS-29738：資產上傳限制失敗並出現 woff 檔案的 NullPointerException
* ASSETS-30068：批次匯入資產要素包括「狀態已完成，但有錯誤」的狀態 COMPLETED_WITH_ERROR。
* ASSETS-30261：傳送到資產事件管道的 imsUserId 不正確。
* ASSETS-30538：移動 PDF 檔案後，「檢視頁面」選項遺失。
* ASSETS-30626：無法為 assetId 為空的資產建立傳遞請求。
* ASSETS-30756：當資料夾名稱結尾是 &#39;html&#39; 時，移動資產精靈的操作失敗。
* ASSETS-30810：在呈現舊版 YouTube 設定之前清理標記。
* ASSETS-31015：無法上傳檔案副檔名為 .msg 的資產。
* ASSETS-31038：接收到通知服務的任務事件未經處理。
* ASSETS-31097：停用 WCM 內容的非同步複製，以避免出現周遊查詢警告。
* ASSETS-31256：具備「jcr:lastModifiedBy」的資產/節點：「workflow-process-service」在清單檢視中顯示為「外部使用者」。
* ASSETS-31260：當下拉式 JSON 具備較大筆清單時，資產中繼資料表單下拉式欄位無法正常運作。
* ASSETS-31280：將資產新增至集合時，以扁平結構下進行資產下載。
* ASSETS-31301：`dynamicmedia_sly.js` 無法透過 Use API 正確實例化。
* ASSETS-31330：ko_KR：字幕和音軌中未本地化的字串。
* ASSETS-31405：InDesign 伺服器處理大型 InDesign 版面配置時失敗。
* ASSETS-31570：Unified Shell - 「儲存並關閉」、「取消」按鈕的資產詳細資料需要按下多次才能運作。
* ASSETS-31673：大型 Dropbox 檔案的批次匯入失敗。
* ASSETS-32108：AEM Assets 未在檢視設定中儲存使用者定義的卡片大小。
* ASSETS-32230：升級最低執行時間版本的 com.adobe.aem.repoapi 套件組合。
* ASSETS-32544：中繼資料匯出作業發生間歇性失敗。
* ASSETS-32679：資產 (PDF) 預覽的快取問題。
* ASSETS-32754：無法將任務指派給先前未登入的使用者。
* ASSETS-32755：設定 com/adobe/cq/dam/assetmove 作業主題，以便使用排列有序的佇列。
* ASSETS-32899：在集合中搜尋非常慢。
* ASSETS-33098：AEM Assets 搜尋的「標記述詞」面向無法如預期運作。
* ASSETS-33454：查看未出現在時間軸中的任務活動和評論。
* ASSETS-34088：PDF 預覽不適用於 AEM Assets。
* ASSETS-34155：動態媒體 - 更新 AEM 檢視器 / 2024.1.0。
* ASSETS-34684：處理內容樹中的多值 dc:title。
* ASSETS-34789：修正檔案名稱衝突檢查中的標準化問題。
* DXML-13276：AEM Guides - 將索引整合到 GraniteContent 中並將其從資料庫中移除。
* GRANITE-47995：由於與「cq:isDelivered」屬性衝突，移除操作可能會失敗。
* GRANITE-48079：啟用 OAuth 線上權杖驗證的 POST 請求。
* GRANITE-48143：將 org.apache.sling.resourcemerger 升級至 1.4.4。
* GRANITE-49031：更新至 Jackson 2.16.1。
* SCRNS-3961：螢幕 - 序列管道：在淡化轉變中使用的 Jquery 動畫會造成螢幕變黑。
* SITES-15868：改善清單片段的效用。
* SITES-16079：`/fragments/{id}/references` 開始返回重複項目。
* SITES-16118：如果修補片段且模型中缺少片段欄位，則會引發異常。
* SITES-16121：檢索模型日期欄位會引發異常。
* SITES-16207：POST /adobe/sites/cf/models 操作傳回兩個不同的 OK 狀態碼。
* SITES-17361：將 Jsoup 重新嵌入 sites-headless 套件組合中。
* SITES-17768：GraphQL 以輸出內容片段中所引用資產的動態媒體 URL。
* SKYOPS-66622：在執行已啟用管道的 buildTransform 後，會發生作者部署崩潰循環。
* SKYOPS-69977：最適化影像 Servlet 在最新更新後不會載入影像。
* GUIDES-15045：編輯器中的拼字檢查不允許建議選擇。
* GUIDES-14968：全域導覽按鈕無法使用，儀表板無法載入。
* GUIDES-14943：在原生 PDF 發佈中，條件預設中的自訂屬性不適用於原生 PDF 發佈。
* GUIDES-15085：在原生 PDF 發佈中，2023 年 12 月版 Adobe Experience Manager Guides 的關鍵引用未獲得解決。
* GUIDES-13486：**基準線篩選器** 檔案無法與 Web 編輯器中的檔案名稱一起使用。
* 有關 AEM Guides 中已修正問題的完整清單，請參閱：[AEM Guides 已修正問題](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=zh-Hant#release-info)

### 已知問題 {#known-issues-15262}

* ASSETS-35923：將 `aem-sdk-api` 版本升級至 `2024.2.15262.20240224T002940Z-231200` 後，在 CM 管道建置步驟中發生 `UnsupportedClassVersionError`。**需要客戶採取行動將 CM Java 版本設定為 11**，請參閱[「組建環境/設定 Maven JDK 版本」](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=zh-Hant#alternate-maven-jdk-version)
* ASSETS-35860：AEM Assets 欄視圖中的時區轉換不正確。
* SCRNS-4171：Windows 升級到 15262 並發布頻道時，螢幕變成空白並停止運作。
* GRANITE-50774：GraniteContent 應在初始化時使用屬性值的確定性順序。

### 變更通知 {#change-notice-15262}

**必要採取的行動**

#### 將 CM Java 版本設定為 11 {#set-java-version-11}

新版本 aem-sdk-api 包含使用 Java 11 Target 編譯的類別，該應用程式與 Cloud Manager 組建環境預設 JDK 版本 1.8 不相容。此更新要求使用 JDK 11 執行 Maven。

建議客戶將 `.cloudmanager/java-version` 檔案加入其 git 存放庫的根目錄中，其內容為： `11`。[組建環境/設定 Maven JDK 版本](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=zh-Hant#alternate-maven-jdk-version)

#### 將 aem-cloud-testing-clients 更新至 1.2.1 {#update-aem-cloud-testing-clients}

未來變更將要求自訂功能測試中使用的 [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) 資料庫至少要更新到版本 **1.2.1**

確保 `it.tests/pom.xml` 中的相依性已更新。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

2024 年 4 月 6 日之後需要進行此變更。

無法更新相依性資料庫將造成「自訂功能測試」步驟中的管道失敗。

### 內嵌技術 {#embedded-tech-15262}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.4 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
