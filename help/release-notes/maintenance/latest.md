---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 39993d115d58d9dfe1f9328c5ceba0d30a78569d
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 19%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 23385 版 {#23385}

以下摘要說明維護版本23385數的持續改善，該版本於2025年11月13日公開發佈。 前一個維護版本是 22943 版。

啟用 2025.11.0 功能即可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行路徑圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>版本 23320 和 23122 已設為私人版本。

### 增強功能 {#enhancements-23385}

* CQ-4361363：最新的 AEM 和 Granite 翻譯。
* Forms-21594：為內容作者啟用互動式通訊範本內容與版面配置鎖定功能。
* Forms-20385：支援在互動式通訊編輯器中進行XDP編輯。
* Forms-10883：支援JSON搭配DoR產生中的XHTML名稱空間標籤，以確保準確轉譯透過API提交的RTF資料。
* Forms-21751：畫布功能 — 文字溢位，分頁的UI。
* Forms-22049：互動式通訊編輯器 — 移轉至Spectrum 2。
* Forms-22050：支援互動式通訊編輯器中的動態頁面編號。
* Forms-21606：互動式通訊的公用OSGi轉譯SPI。
* Forms-21613：轉譯器互動式通訊SPI的交易報表和效能記錄。
* GRANITE-62394：將joda-time更新為2.12.7。
* GRANITE-36205：將Oak版本更新至1.88.0。
* GRANITE-62020：改善`RepositoryServiceHttpClient`上的重試原則。
* GRANITE-62169：將commons-lang更新為3.19.0。
* SITES-35092：內容片段 — 語意搜尋的新mixin和升級程式。
* SITES-32319：傳送OpenAPI — 支援頁面參考。
* SITES-20123： GraphQL：支援JSON回應中的上標元素。
* SITES-34744：內容片段回應中新的「卡片」屬性，包含可用於呈現縮圖的資料。
* SITES-34571：允許列舉欄位為空。
* SITES-34812：新增使用值為「none」的「references」引數，擷取不含參考的內容片段的功能。
* SITES-35176：透過Touch UI簽出內容片段現在會防止其他使用者在新編輯器中編輯內容片段。
* SITES-30371：新增對uuid型參考欄位的支援。
* SITES-19309：開啟移動頁面精靈時，最多可擷取150個參考。
* SITES-32515：使用通用編輯器的Edge Delivery — 新增對多欄位和複合多欄位的支援（搶先存取）。
* SITES-33784：使用通用編輯器的Edge Delivery — 在頁面中繼資料中新增ld-json支援。
* SITES-34832：使用通用編輯器的Edge Delivery — 將頁面的公開路徑新增至頁面資訊servlet回應。
* SITES-25893：使用通用編輯器的Edge Delivery — 新增對強式字型的支援，並強調以區塊呈現文字。
* SITES-26158：使用通用編輯器的Edge Delivery — 新增對區塊和欄中表格標籤的支援（搶先存取）。
* SITES-27949：使用通用編輯器的Edge Delivery — 將路徑對應設為選用。
* SITES-35811：在內容片段查詢中使用新索引。
* SKYOPS-120857：將filevault更新至4.1.4。
* SKYOPS-118390：將JCR資源更新至3.3.6。
* SKYOPS-121082：更新`org.apache.sling.discovery.standalone`、`org.apache.sling.jcr.packageinit`和`org.apache.sling.commons.fsclassloader` Sling套裝的版本。

### 已修正的問題 {#fixed-issues-23385}

* Assets-58926：修正DM中的視訊變更縮圖功能。
* Assets-58623：設定存在時修正omnisearch中的npe。
* CQ-4361144：修正翻譯工作中略過內容片段的問題。
* CQ-4355446：修正取消翻譯工作對話方塊中翻譯專案未本地化的字串。
* CQ-4360747：修正可重複翻譯工作建立空負載並過於頻繁觸發的問題。
* GRANITE-61318：修正頁面建立精靈僅反白基本索引標籤中強制欄位的問題。
* GRANITE-60514：修正完整棧疊管道執行期間停止已排程發佈的問題。
* GRANITE-61019：修正AEM重新啟動後首次執行的GC問題。
* GRANITE-60456：修正管理員開啟任何使用者的屬性頁面時的問題。
* SITES-34555： GraphQL — 部署後出現QueryValidationError。
* SITES-35077：內容片段 — 由於錯誤的URL編碼，對帶有括弧的片段取消發佈失敗。
* SITES-35374：內容片段 — 已編輯的內容片段在導覽回到後面後會消失。
* SITES-36130： `EditorRestrictionsStatusImpl`中的NPE。
* SITES-35810： Launches中的NullPointerException區塊publishEdgeDeliverySubscriber佇列。
* SITES-34368： AEM CIF產生12個GraphQL別名，超過Magento 2.4.6-P12的10個限制。
* SITES-36193：CCS聯結器修正。
* SITES-35169：已解決當搜尋傳回無效的片段資源時，會導致錯誤分頁的問題。
* SITES-34574：修正內容片段搜尋API在某些情況下不會傳迴游標的問題。
* SITES-35520：修正嘗試發佈內容時，造成ClassCastException或逾時的問題。
* SITES-35210：修正嘗試使用空白參考篩選條件發佈中斷片段時會發生的NullPointerException。
* SITES-35933：修正會在內容片段發佈後觸發空白「啟用請求」工作流程的錯誤。
* SITES-35925：修正與修補內容片段模型相關的錯誤，這將從模型刪除「translatable」和「showThumbnail」屬性。
* SITES-35409：修正移動頁面時無法重新發佈已調整片段的錯誤。
* SITES-15757：修正無法在移動頁面時重新發佈已調整頁面的錯誤。
* SITES-34638：修正建立新版本時，不會納入祖父頁面屬性的錯誤。
* SITES-35226：修正導致頁面編輯器中的資產選擇器在某些情況下無法載入的回歸。
* SITES-35071：當Omnisearch使用引號中的短語時，CSV匯出會傳回未篩選的結果。
* SITES-32182：使用通用編輯器的Edge Delivery — 修正包含已編碼請求引數的URL的編碼問題。
* SITES-34324：使用通用編輯器的Edge Delivery — 修正使用tel：通訊協定轉譯連結的問題。
* SITES-35333：使用通用編輯器的Edge Delivery — 修正頁面中繼資料中影像的資產轉譯選擇。
* SITES-35549：使用通用編輯器的Edge Delivery — 修正頁面中繼資料中的雙重編碼html實體。

#### AEM Guides {#guides-23385}

* GUIDES-33597：如果將沒有屬性或值的空白`prop`元素新增到DITAVAL檔案，則無法新增其他`prop`元素。
* GUIDES-33693：當您透過Experience Manager Guides UI重新上傳已編輯的影像時，影像的原始轉譯會更新，但關聯的DITA內容會繼續顯示影像的先前版本。
* GUIDES-35607：透過Assets UI上傳資產或從編輯器介面建立新檔案時產生的錯誤記錄，在記錄訊息中錯誤使用字詞`predecessor`而非`successor`。
* GUIDES-37649：在AEM Sites上使用基準線（搭配舊版元件對應）發佈DITA map時，也會發佈屬性為`processing-role = resource-only`的map元素。

如需更多有關該版本中新增功能和增強功能以及已修復問題的資訊，請查看 [Experience Manager Guides 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。


### 已知問題 {#known-issues-23385}

* Forms-22633：使用依賴GuideBridge API （`getData`或`getDataXML`）的自訂程式碼時，表單提交可能會失敗。 如果您遇到此問題，請聯絡Adobe支援以尋求協助。

### 已過時的功能和 API {#deprecated-23385}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-23385}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護版本解決 31 個已確認的漏洞，強化我們提供健全系統保護的承諾。

### 嵌入技術 {#embedded-tech-23385}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.88.0 | [Oak 1.88.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| Apache HTTP 伺服器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心元件 | 2.30.2 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (預設) | [支援的 Node.js 版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
