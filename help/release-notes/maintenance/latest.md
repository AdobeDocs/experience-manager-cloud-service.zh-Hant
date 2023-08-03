---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: acaed9eed20e8134574fd326e23ac68130ac019b
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 14%

---

# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 12874 版 {#release-12874}

以下摘要說明維護版本12874數的持續改善，該版本於2023年8月2日公開發佈。 此維護版本是先前 12790 維護版本的更新。

2023.8.0 功能啟用將提供此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增強功能 {#enhancements-12874}

- 新版本的索引定義： `/oak:index/damAssetLucene-9`
- ASSETS-18351：切換至不安全的Facet — 提升搜尋效能
- ASSETS-17896：從索引中移除特徵向量 — 根據智慧標籤的相似性搜尋
- ASSETS-8715：為屬性&quot;jcr：content/metadata/dam：status&quot;新增null檢查/非null檢查
- GRANITE-45138：從預測的標籤動態提升屬性中移除屬性索引
- ASSETS-17614：新增Scene7 ID作為索引屬性（啟用Null檢查而非Null檢查）
- ASSETS-14516：將「新UI」垃圾桶功能的屬性新增到索引
- ASSETS-16270：將聯合標題屬性新增到索引（用於排序）
- ASSETS-24478：從索引中移除5個潛在的大型屬性（根據客戶索引資料的分析）
- ASSETS-3383：新增額外標籤「assetsOmnisearch」

AEM版本12874和更新版本包含新版本的damAssetLucene索引(damAssetLucene-9)。 為了提供回應最迅速的搜尋體驗，damAssetLucene-9變更了Oak查詢結果Facet的行為，不再評估基礎搜尋索引傳回之Facet計數的存取控制（稱為「不安全」模式）。

因此，使用者可能會看到面向計數值，其中包含目前使用者無權存取的資產。 這不允許使用者存取、下載或讀取這些資產，也不允許使用者取得有關資產存在的任何進一步資訊。

如果需要先前的行為，客戶應遵循中所述的步驟 [內容搜尋與索引](/help/operations/indexing.md) 使用先前的「統計」Facet模式建立damAssetLucene-9索引的自訂版本。

### 已修正的問題 {#fixed-issues-12874}

- ASSETS-24379：改善ReplicateOnModifyListener。
- ASSETS-25794：解決S7ConfigResolverImpl導致其在啟動時執行昂貴查詢的問題。
- ASSETS-25473：修正沒有復寫許可權的使用者看見「快速發佈選項」的錯誤。
- ASSETS-24803：解決Viewers功能中的XSS弱點。
- ASSETS-25489：修正下載含有錯誤尾碼的智慧型裁切的問題。
- ASSETS-25435：修正動態轉譯的下載中缺少WidthxHeight欄位的錯誤
- ASSETS-25741：修正缺少視覺星號(`*`)符號，代表「基本」索引標籤區段中的必要「寬度」編輯欄位。
- ASSETS-25759：改善高對比黑白模式中下拉式清單元素的可見度。
- ASSETS-25749：修正使用鍵盤標籤導覽時，焦點未移至視訊下方的多個控制項，導致無法存取的問題。
- ASSETS-26074：恢復非視訊資產名稱127個字元的限制。
- ASSETS-21428：修正中繼資料結構編輯器中的多行欄位與下列欄位重疊的問題
- ASSETS-21989：修正302和401回應時可能覆寫CORS標題，導致遠端DAM無法登入的問題
- ASSETS-22603：修正檢視「資產下載報表」時，影響欄名稱和值的問題
- ASSETS-23120：修正AssetSetLastModifiedProcess中有關洩漏資源解析器的問題
- ASSETS-24938：修正導致「資產資料夾屬性」對話方塊的「儲存」按鈕行為類似於「儲存+關閉」的問題
- ASSETS-25456：修正長名稱的資產無法在Asset Properties編輯器中點選動作的問題
- ASSETS-25832：修正將完整存取資料夾中的資產關聯至唯讀存取資料夾的問題。
- ASSETS-25397：修正搜尋結果無法反映在新UI中重新命名之資產新名稱的問題
- ASSETS-26102：修正無法從CI中樞聯結器上傳的問題
- ASSETS-26172：減少永久性Sling作業節點中儲存的「大量匯入」進度記錄檔內容大小
- ASSETS-26292：在Java API中棄用的AssetManager createOrUpdateAsset()和createOrReplaceAsset()方法
- ASSETS-26399：修正無法將集合發佈至Brand Portal的問題
- ASSETS-26533：修正Indesign伺服器整合中，可能導致長時間處理請求逾時的問題
- ASSETS-26549：修正「資產清單」檢視中，造成「外部使用者」顯示為所有已上傳資產的最後修改使用者的問題
- ASSETS-26551：解決在作者中刪除的資產未取消發佈的問題
- ASSETS-26571：修正「Assets報表」頁面在清單中出現多個失敗報表作業時無法載入頁面的問題
- ASSETS-26147：修正設定window.top.opener但未設定window.opener時，Unified Shell會嘗試將iframe重新導向至/ui的問題
- ASSETS-26576：修正「Dropbox匯入」中建立錯誤資料夾階層的問題
- ASSETS-26671：修正大量匯入無法包含位於DCIM資料夾中檔案的問題
- ASSETS-26700：修正儲存公用資料夾的屬性頁面而不做變更時，會建立3個不必要群組的問題
- CQ-4353449：修正具有唯讀標籤許可權的使用者可使用標籤UI建立標籤的問題
- GRANITE-46601：修正快速入門SDK無法在JDK 11.0.20上啟動的問題
- SKYOPS-33168：修正CM開發人員控制檯中，無法載入無副檔名之資產名稱的/content/dam的問題
- SKYOPS-61484：修正RDEProvider服務允許未取代的${sling.home} Token保留在合併OSGi設定中的問題
- 各種安全性、協助工具和本地化修正

### 已知問題 {#known-issues-12874}

- GRANITE-46851：內容發佈中的測試連線無法運作

### 內嵌技術 {#embedded-tech-12874}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.23.0 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
